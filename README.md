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
