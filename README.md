# dummy-1

![pppp](https://github.com/Deeksha0301/dummy-1/assets/92042650/dfcafb1f-7799-4ed7-94c0-30a404dc982c)
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
