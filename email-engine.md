

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

#### Profile Selection and Email Fetching

1. **User Action**: User selects an email profile from a dropdown.
2. **Frontend**: Retrieves the corresponding access token from cookies.
3. **Backend**:
    1. **Access Token Check**: Checks if the access token is expired by comparing the current time with the stored expiration time.
    2. **Token Expired?**:
        - **Yes**: Attempts to retrieve the refresh token from Redis.
            1. **Redis Check**: If not found, retrieves from the database.
            2. **Database Check**: Retrieves and updates Redis cache.
            3. **Token Revalidation**: Uses the refresh token to obtain a new access token and expiration time.
            4. **Access Token Update**: Updates the cookies and Redis cache with the new access token and expiration time.
        - **No**: Proceeds with the current access token.
    3. **Email Fetching**: Fetches emails using the valid access token.
4. **Frontend**: Displays the fetched emails to the user.

#### Token Refresh and Error Handling

1. **Backend**:
    1. **Periodic Token Check**: Optionally, checks token expiration and proactively refreshes if necessary.
    2. **Error Handling**: Implements retry mechanisms for network issues and logs errors.
2. **User Notification**: If revalidation fails, notifies the user to re-authenticate.
