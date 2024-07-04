

### Data Flow Diagram

#### User Profile Creation and Sign-In

1. **User Action**: User creates a profile on your application.
2. **Frontend**: Sends profile creation request to the backend.
3. **Backend**: Creates a user profile in the database.
4. **Database**: Stores user profile details.

#### OAuth Authentication for Email Providers

1. **User Action**: User initiates sign-in to an email provider (e.g., Gmail, Outlook) from the settings tab.
2. **Frontend**: Redirects user to the email provider's OAuth consent screen.
3. **Email Provider**: User grants permissions; provider redirects back with authorization code.
4. **Backend**: Exchanges authorization code for access and refresh tokens.
5. **Database**: Stores encrypted refresh token, access token, and expiration time.
6. **Redis**: Caches the refresh token and expiration time for quick access.
7. **Frontend**: Stores the encrypted access token in secure, HTTP-only cookies.
