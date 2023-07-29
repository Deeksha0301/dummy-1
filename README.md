# dummy-1

![pppp](https://github.com/Deeksha0301/dummy-1/assets/92042650/dfcafb1f-7799-4ed7-94c0-30a404dc982c)

## uploadImage API:

- Endpoint: /api/uploadImage
- HTTP Method: POST
- Description: This API allows users to upload images to the server. The image data is provided as a base64-encoded string in the - -request body. The API then processes the image data, saves it to an AWS S3 bucket, and returns the URL of the uploaded image in the response. The uploaded image is publicly accessible due to the ACL: "public-read" setting.

## removeImage API:

- Endpoint: /api/removeImage
- HTTP Method: POST
- Description: This API is used to remove an image from the AWS S3 bucket. The API expects the Key and Bucket parameters in the - -request body, which specify the location of the image in the S3 bucket. If the image is successfully removed, the API returns { ok: true }.

## create API:

- Endpoint: /api/create
- HTTP Method: POST
- Description: This API is used to create a new ad entry in the database. It expects various parameters, such as photos, description, title, address, price, type, and landsize, in the request body. The API creates a new Ad document using the Mongoose model, populates some fields, such as postedBy, and generates a unique slug for the ad. It also updates the user's role to "Seller" and returns the created ad and updated user data in the response.

## ads API:

- Endpoint: /api/ads
- HTTP Method: GET
- Description: This API is used to fetch a list of ads for both "Sell" and "Rent" actions. It retrieves 12 ads for each action and returns them as separate arrays in the response.

### Response:

- Status: 200 OK
- Description: Returns a JSON response with two arrays: adsforRent (containing 12 ads with action "Rent") and adsforSell (containing 12 ads with action "Sell"). Each ad object in the arrays excludes the Key, key, and ETag properties of the photos field.

### read API:
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
