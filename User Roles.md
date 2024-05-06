
To implement roles and permissions with a database-driven approach, you can create two tables: `roles` and `permissions`. Then, establish a many-to-many relationship between them to allow each role to have multiple permissions. Here's a general outline:

### Database Schema:

1. **Roles Table:**

    - `id` (Primary Key)
    - `name` (Unique)
2. **Permissions Table:**
    
    - `id` (Primary Key)
    - `name` (Unique)
3. **Role_Permissions Table (Many-to-Many Relationship):**
    
    - `id` (Primary Key)
    - `roleId` (Foreign Key referencing `roles.id`)
    - `permissionId` (Foreign Key referencing `permissions.id`)

### Database Model:

```
CREATE TABLE roles (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255) UNIQUE NOT NULL
);

CREATE TABLE permissions (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255) UNIQUE NOT NULL
);

CREATE TABLE role_permissions (
  id INT PRIMARY KEY AUTO_INCREMENT,
  roleId INT,
  permissionId INT,
  FOREIGN KEY (roleId) REFERENCES roles(id),
  FOREIGN KEY (permissionId) REFERENCES permissions(id)
);

```
### Data:
Populate the `roles` and `permissions` tables with the necessary data.

### JWT Payload:
When issuing a JWT during user authentication, include only the user's role in the JWT payload, not the permissions.

### Middleware:
Modify the middleware to fetch the user's permissions from the database based on their role and then check if they have the required permission for a specific action.

Example middleware:

```
const jwt = require('jsonwebtoken');
const db = require('./your-database-connection'); // Replace with your actual database connection

async function authorizePermissions(requiredPermissions) {
  return async (req, res, next) => {
    const token = req.header('Authorization');

    if (!token) {
      return res.status(401).json({ message: 'Unauthorized - Missing token' });
    }

    try {
      const decoded = jwt.verify(token, 'your_secret_key');
      const userRole = decoded.role;

      // Fetch user's permissions from the database based on their role
      const userPermissions = await getUserPermissions(userRole);

      // Check if the user has at least one of the required permissions
      const authorized = requiredPermissions.some(permission =>
        userPermissions.includes(permission)
      );

      if (!authorized) {
        return res.status(403).json({ message: 'Forbidden - Insufficient permissions' });
      }

      req.user = decoded; // Attach user information to the request
      next();
    } catch (error) {
      return res.status(401).json({ message: 'Unauthorized - Invalid token' });
    }
  };
}

async function getUserPermissions(role) {
  // Fetch user's permissions from the database based on their role
  const result = await db.query(
    'SELECT permissions.name FROM permissions ' +
    'JOIN role_permissions ON permissions.id = role_permissions.permissionId ' +
    'JOIN roles ON role_permissions.roleId = roles.id ' +
    'WHERE roles.name = ?',
    [role]
  );

  // Extract and return an array of permission names
  return result.map(row => row.name);
}

module.exports = authorizePermissions;

```

### Usage:

Protect a route with the middleware and specify the required permissions:

```
app.get('/delete-user', authorizePermissions(['delete_user']), (req, res) => {
  // Your route logic here
});

```

In this example, the middleware fetches the user's permissions from the database based on their role and then checks if they have the required permission for a specific action. This ensures that you can dynamically manage roles and permissions in your application.