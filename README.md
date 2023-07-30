# dummy-1

![p9](https://github.com/Deeksha0301/dummy-1/assets/92042650/8deac337-36fe-4df4-b9b1-655e232dd405)


![pppp](https://github.com/Deeksha0301/dummy-1/assets/92042650/dfcafb1f-7799-4ed7-94c0-30a404dc982c)

# Backend Server Documentation
This documentation provides an overview of the backend server code and its functionalities.

### Setup and Configuration
- The backend server is built using Express.js, a Node.js web application framework.
- MongoDB is used as the database, and the connection URL is specified in the .env file using the DB_URL environment variable.
- Cross-Origin Resource Sharing (CORS) is enabled to allow cross-origin requests.

### API Endpoints
This documentation provides information about the User API endpoints and their usage.

# ad.js

## uploadImage API:

- Endpoint: /api/uploadImage
- HTTP Method: POST
- Description: This API is used to upload an image to an AWS S3 bucket. The image is provided in the request body as a base64-encoded string. The API extracts the image data, generates a unique key using nanoid, and then uploads the image to the specified S3 bucket.

### Request:
- image (Request body): Base64-encoded image data.
### Response:
- Status: 200 OK (on successful upload)
- Description: Returns the S3 bucket upload response data as a JSON object. If there is an error during the upload process, the API logs the error and sends a status of 400 Bad Request.

## removeImage API:

- Endpoint: /api/removeImage
- HTTP Method: POST
- Description: This API is used to remove an image from an AWS S3 bucket. It expects the Key and Bucket of the image to be deleted in the request body.
### Request:
- Key (Request body): The key of the image in the S3 bucket.
- Bucket (Request body): The name of the S3 bucket.
### Response:
- Status: 200 OK (on successful removal)
- Description: Returns { ok: true } as a JSON response if the image is successfully deleted from the S3 bucket. If there is an error during the removal process, the API logs the error and sends a status of 403 Forbidden.

## create API:
- Endpoint: /api/create
- HTTP Method: POST
- Description: This API is used to create a new ad. It expects various properties related to the ad, such as photos, description, title, address, price, type, and landsize. Before creating the ad, the API performs validations to check if all the required properties are provided.
### Request:
- Various properties (Request body): The properties required to create a new ad.
### Response:
- Status: 200 OK (on successful ad creation)
- Description: Returns a JSON response with the newly created ad and the user who posted the ad. The password and resetCode fields of the user are removed from the response.

## ads API:

- Endpoint: /api/ads
- HTTP Method: GET
- Description: This API is used to fetch a list of ads for both "Sell" and "Rent" actions. It retrieves 12 ads for each action and returns them as separate arrays in the response.

### Response:

- Status: 200 OK
- Description: Returns a JSON response with two arrays: adsforRent (containing 12 ads with action "Rent") and adsforSell (containing 12 ads with action "Sell"). Each ad object in the arrays excludes the Key, key, and ETag properties of the photos field.

## read API:
- Endpoint: /api/read/:slug
- HTTP Method: GET
- Description: This API fetches the details of a single ad based on its slug value and populates the postedBy field with specific user data (name, username, email, phone, company, and photo.Location).
### Request:
- slug (URL parameter): The unique identifier of the ad.
#### Response:
- Status: 200 OK
- Description: Returns a JSON response with the detailed information of the requested ad, including the related ads that have similar action, type, and address (up to 3 related ads). The photo-related properties are excluded from the response.

## addToWishlist API:

- Endpoint: /api/addToWishlist
- HTTP Method: POST
- Description: This API is used to add an ad to the wishlist of a user. It expects the adId of the ad to be added in the request body.

### Request:
- adId (Request body): The unique identifier of the ad to be added to the wishlist.
Response:
- Status: 200 OK
- Description: Returns the updated user object after adding the adId to the user's wishlist. The password and resetCode fields are removed from the response.
  
## removeFromWishlist API:

- Endpoint: /api/removeFromWishlist/:adId
- HTTP Method: POST
- Description: This API is used to remove an ad from the wishlist of a user. It expects the adId of the ad to be removed as a URL parameter.
### Request:
- adId (URL parameter): The unique identifier of the ad to be removed from the wishlist.
Response:
- Status: 200 OK
- Description: Returns the updated user object after removing the adId from the user's wishlist. The password and resetCode fields are removed from the response.
  
## contactSeller API:

- Endpoint: /api/contactSeller
- HTTP Method: POST
- Description: This API is used to send a customer enquiry email to the seller of an ad. It expects the name, email, message, phone, and adId of the ad in the request body.

### Request:
- name (Request body): Name of the customer.
- email (Request body): Email of the customer.
- message (Request body): The message from the customer to the seller.
- phone (Request body): Phone number of the customer.
- adId (Request body): The unique identifier of the ad for which the enquiry is being made.
### Response:
- Status: 200 OK
- Description: Returns { ok: true } if the email is successfully sent to the seller, or { ok: false } if there's an error.

## userAds API:

- Endpoint: /api/userAds/:page
- HTTP Method: GET
- Description: This API fetches a paginated list of ads created by the logged-in user. The number of ads per page is specified by the perPage constant in the code.

### Request:
- page (URL parameter, optional): The page number of the ads to fetch (default is 1).
### Response:
- Status: 200 OK
- Description: Returns a JSON response with an array of ads created by the user and the total number of ads owned by the user.

# auth.js

## welcome API:
- Endpoint: /api/welcome
- HTTP Method: GET
- Description: This API is used to send a welcome message from the server controller. It returns a JSON object with the message "hi from server controller".
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the message "hi from server controller".

## preRegister API:
- Endpoint: /api/preRegister
- HTTP Method: POST
- Description: This API is used for pre-registration. It expects an email and password in the request body. The API performs various validations on the email and password and then sends an email with an activation link to the provided email.
### Request:
- email (Request body): The email of the user for pre-registration.
- password (Request body): The password of the user for pre-registration.
### Response:
- Status: 200 OK
- Description: Returns { ok: true } as a JSON response if the pre-registration email is successfully sent. If there is an error - - during the email sending process, the API logs the error and returns { ok: false }.

## register API:
- Endpoint: /api/register
- HTTP Method: POST
- Description: This API is used for registration. It expects a token (received via email during pre-registration) in the request body. The API verifies the token, extracts the email and password, and then creates a new user with the provided email and password.
### Request:
- token (Request body): The token received during pre-registration.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with a newly created user and JWT tokens (token and refreshToken) for authentication - purposes.

## login API:
- Endpoint: /api/login

- HTTP Method: POST

- Description: This API is used for user login. It expects an email and password in the request body. The API finds the user based on the provided email, verifies the password, and then creates JWT tokens (token and refreshToken) for authentication.
### Request:
- email (Request body): The email of the user for login.
- password (Request body): The password of the user for login.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the user and JWT tokens (token and refreshToken) on successful login. If the user is not found or the password is incorrect, appropriate error messages are returned.

## forgotPassword API:
- Endpoint: /api/forgotPassword
- HTTP Method: POST
- Description: This API is used when a user forgets their password. It expects the user's email in the request body. The API finds the user based on the provided email, generates a resetCode (used for resetting the password), and sends an email to the user with a link for password reset.
### Request:
- email (Request body): The email of the user for password reset.
### Response:
- Status: 200 OK
- Description: Returns { ok: true } as a JSON response if the password reset email is successfully sent. If there is an error during the email sending process or the user is not found, appropriate error messages are returned.

## accessAccount API:
- Endpoint: /api/accessAccount
- HTTP Method: POST
- Description: This API is used to access a user account after resetting the password. It expects a resetCode (received via email during the password reset process) in the request body. The API verifies the resetCode, finds the user based on the resetCode, and then creates JWT tokens (token and refreshToken) for authentication.
### Request:
- resetCode (Request body): The resetCode received during the password reset process.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the user and JWT tokens (token and refreshToken) on successful access to the account after resetting the password.

## refreshToken API:
- Endpoint: /api/refreshToken
- HTTP Method: GET
- Description: This API is used to refresh the access token. It expects the refreshToken in the request header. The API verifies the refreshToken, finds the user based on the decoded _id from the refreshToken, and then creates a new JWT token (token) for authentication.
### Request:
- refreshToken (Request header): The refreshToken received during login or registration.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the new token on successful token refresh. If the refreshToken is invalid or expired, appropriate error messages are returned with a status of 403 Forbidden.

## currentUser API:
- Endpoint: /api/currentUser
- HTTP Method: GET
- Description: This API is used to get the current user's profile. It expects the user's JWT token in the request header for authentication. The API finds the user based on the decoded _id from the token and returns the user's profile data.
### Request:
- Authorization (Request header): The JWT token for authentication.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the current user's profile data. The user's password and resetCode are removed from the response.

## publicProfile API:
- Endpoint: /api/publicProfile/:username
- HTTP Method: GET
- Description: This API is used to get the public profile of a user based on their username. It expects the username as a URL parameter. The API finds the user based on the provided username and returns their public profile data.
### Request:
- username (URL parameter): The username of the user whose public profile is requested.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the user's public profile data. The user's password and resetCode are removed from the response.

## updatePassword API:
- Endpoint: /api/updatePassword
- HTTP Method: POST
- Description: This API is used to update the current user's password. It expects the new password in the request body. The API finds the user based on the authenticated JWT token and updates their password.
### Request:
- password (Request body): The new password to be updated.
### Response:
- Status: 200 OK
- Description: Returns { ok: true } as a JSON response on successful password update. If the password is not provided or does not meet the required criteria, appropriate error messages are returned with a status of 403 Forbidden.

## updateProfile API:
- Endpoint: /api/updateProfile
- HTTP Method: POST
- Description: This API is used to update the current user's profile. It expects various user profile data in the request body. The API finds the user based on the authenticated JWT token and updates their profile data.
### Request:
- Various profile data (Request body): The updated user profile data.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the updated user profile data. The user's password and resetCode are removed from the response. If there is an error during the update, such as a duplicate username or email, appropriate error messages are returned.

## agents API:
- Endpoint: /api/agents
- HTTP Method: GET
- Description: This API is used to get a list of all agents. It finds all users with the role "Seller" and returns their profile data.
### Response:
- Status: 200 OK
- Description: Returns a JSON response with the list of agent profiles. The users' passwords and other sensitive data are removed from the response.

## agentAdCount API:
- Endpoint: /api/agentAdCount/:_id
- HTTP Method: GET
- Description: This API is used to get the count of ads posted by a specific agent. It expects the agent's _id as a URL parameter. The API finds all ads posted by the agent and returns the count.
### Request:
- _id (URL parameter): The _id of the agent whose ad count is requested.
### Response:
-Status: 200 OK
-Description: Returns a JSON response with the count of ads posted by the agent.

## agent API:
- Endpoint: /api/agent/:username
- HTTP Method: GET
- Description: This API is used to get the public profile and ads posted by a specific agent. It expects the agent's username as a URL parameter. The API finds the agent based on the provided username, returns their public profile data, and also returns all ads posted by the agent.

### Request:
-username (URL parameter): The username of the agent whose public profile and ads are requested.
### Response:
-Status: 200 OK
-Description: Returns a JSON response with the agent's public profile data and a list of ads posted by the agent. The users' -passwords and other sensitive data are removed from the response.
