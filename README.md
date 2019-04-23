# Clio Organization API

App URL: https://clio-1532190191611.appspot.com

## Authentication
Many API requests require authentication with a JWT. To authenticate a request, this must be included in the request’s header:

```json
"Authorization": "Bearer <YOUR_TOKEN_HERE>"

```

### Getting a Valid Token

```json
POST /organizationLogin
Body
  name
    - Required
    - String
  key
    - Required
    - String

```

If a valid name and key combination is providide, this will return:

```json
{
  "token": "<TOKEN>"
}

```

This token will be valid for 60 days.

## API Routes

### Create an Entry
```json
POST /api/v1/org/createEntry
Headers
  Authorization: "Bearer <TOKEN>"
Body
  title
    - Required
    - String
  latitude
    - Required
    - Number
  longitude
    - Required
    - Number
  shortDescription
    - Optional
    - String
  description
    - Optional
    - String
    - Gets sanitized, displayed as raw HTML
  sources
    - Optional
    - String
    - Gets sanitized, displayed as raw HTML
  phone
    - Optional
    - String
  hours
    - Optional
    - String
  isLocked
    - Optional
    - Boolean
  improvement
    - Optional
    - String
  signature
    - Optional
    - String
  streetViewEnabled
    - Optional
    - Boolean
  streetViewPitch
    - Optional
    - Number
  streetViewHeading
    - Optional
    - Number
  street
    - Optional
    - String
  state
    - Optional
    - String
  country
    - Optional
    - String
  city
    - Optional
    - String
  zip
    - Optional
    - String
  thumbnailIndex
    - Optional
    - Number
  images
    - Optional
    - Array
    - Replaces All Images
    - see 'Image' data type
  links
    - Optional
    - Array
    - Replaces All Links
    - see 'Link' data type

```

Return the newly created entry:
```js
{
  id: <ENTRY_ID>,
  ...other attributes
}

```

### Edit an Entry

Your organization must have permissions to edit an entry. When you create an entry, you are autmatically given permissions to edit it. If you need to edit a pre-existing entry, those permissions need to be added manually.

```json
POST /api/v1/org/editEntry/:id
Headers
  Authentication: "Bearer <TOKEN>"
Body
  Same as /createEntry

```

Returns successful

### Upload a new Image
```json
POST /api/v1/org/uploadImage
Headers
  Authentication: "Bearer <TOKEN>"
Body
  file
    - Required
    - an image file

```

Uploads the image to the cloud storage and returns the new image path
```js
{
  path: <IMAGE_PATH_HERE>
}

```

Only updates the fields included in the request

## Other DataTypes

### Image

```json
  path
    - Required
    - String
  description
    - Optional
    - String
  source
    - Optional
    - String

```

### Link

```json
  linkTypeId
    - Required
    - Number
  description
    - Optional
    - String
  url
    - Required
    - String

```

# Using iBeacons with Clio

The Clio mobile app can detect iBeacons and prompt the user with the option to navigate to the entry associated the the detected beacons. For this to happen, several configuration options need to be set on the iBeacon

## Configuration

### Tags
