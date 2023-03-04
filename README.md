# API-Auth-Authorization-Library-L0k1
This library provides secure authentication and authorization mechanisms for APIs based on the OWASP Top 10 API 2023. The library is written in Python and uses the Flask framework for API development.
    Install the required packages: The library requires the Flask, bcrypt, and Flask-Limiter packages. You can install these packages using pip by running the following command: pip install Flask Flask-Limiter bcrypt.

    Import the library: In your Flask application, import the library by running from api_auth import ApiAuth.

    Create a dictionary of users and hashed passwords: The library requires a dictionary of users and hashed passwords for authentication. You can create this dictionary as follows:

bash

users = {
    'user1': '$2b$12$QzJ./cVXrlXo8pI/ObOpvOg1eJ0dLVrRy8.IvMZJncdM9TtTjvhEy',  # hashed password: password1
    'user2': '$2b$12$2u1aVJ./XcbK/Z7LpJvD.Ol7lIYrKpmrWC0MvtKjzB4E1mr4lb4ra',  # hashed password: password2
}

    Create a dictionary of endpoint permissions: The library requires a dictionary of API endpoints and the required permissions to access them. You can create this dictionary as follows:

python

endpoint_permissions = {
    '/public_endpoint': ['public'],  # accessible by all users
    '/private_endpoint': ['admin'],  # accessible only by users with admin permission
}

    Initialize the library: Initialize the library by creating an instance of the ApiAuth class and passing in the users and endpoint_permissions dictionaries:

scss

api_auth = ApiAuth(users, endpoint_permissions)

    Add the authentication and authorization decorators to your API endpoints: To secure your API endpoints, add the auth_required and auth_required_roles decorators to your endpoint functions. The auth_required decorator checks if an authentication token is present in the request headers and validates it. The auth_required_roles decorator checks if the user making the request has the required permissions to access the endpoint. Here's an example:

less

@app.route('/private_endpoint')
@api_auth.auth_required
@api_auth.auth_required_roles(['admin'])
def private_endpoint():
    return 'You have access to the private endpoint!'

    Set rate limiting parameters (optional): You can set rate limiting parameters for the library by adding the following configuration to your Flask application:

python

app.config['RATELIMIT_STORAGE_URL'] = 'redis://localhost:6379/0'  # Redis server URL
app.config['RATELIMIT_HEADERS_ENABLED'] = True  # enable rate limit headers in API response
limiter = Limiter(app, key_func=get_remote_address)  # create Limiter instance
