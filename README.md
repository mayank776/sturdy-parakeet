# sturdy-parakeet

## pantry-cloud-backend

### instructions

### Models

- first of all i have created the 3 models required to store the data, they are user Model, pantry Model, and basket model.

- User Model

```yaml
{
  email:
    {
      type: String,
      required: true,
      unique: true,
      trim: true,
      validate:
        {
          validator: validator.validateEmail,
          message: "Please enter a valid email address",
          isAsync: false,
        },
      match: [validator.emailRegex, "Please enter a valid email address"],
    },
}
```

- pantry Model

```yaml
{
  name: { type: String, required: true, trim: true },
  user: { type: mongoose.Types.ObjectId },
  basket: [{ type: mongoose.Types.ObjectId }],
}
```

- basket model

```yaml
{
    name: { type: String, trim: true },
    key: { type: String, default: "value" },
    createdAt: {
      type: Date,
      expires: 3600,
      default: Date.now,
    },
}
```

## controllers

## user api's

- Users should be able to register using email.

### POST /signup

- Created a user document from request body email.
- Return HTTP status 201 on a succesful user creation. Also return the user document. The response should be a JSON object like [this](#successful-response-structure)
- Return HTTP status 400 if no params or invalid params received in request body. The response should be a JSON object like [this](#error-response-structure)

## pantry api's

- Users should be able to create and get pantries to contain the basket.

### POST /:userId/createPantry

- Created a pantry for a user that contains all the user's basket.
- Return HTTP status 201 on a succesful user creation. Also return the user document. The response should be a JSON object like [this](#successful-response-structure)
- Return HTTP status 400 if no params or invalid params received in request body. The response should be a JSON object like [this](#error-response-structure)

### GET /:userId/pantry/:pantryId

- get the pantry of a user using the pantry id.
- Return HTTP status 201 on a succesful user creation. Also return the user document. The response should be a JSON object like [this](#successful-response-structure)
- Return HTTP status 400 if no params or invalid params received in request body. The response should be a JSON object like [this](#error-response-structure)

## basket api's

- pantry will contain the baskets for the user.

### CRUD /:userId/pantry/:pantryId/basket/:basketname

- i have done all the CRUD opeartion on the basket
- Return HTTP status 201 on a succesful user creation. Also return the user document. The response should be a JSON object like [this](#successful-response-structure)
- Return HTTP status 400 if no params or invalid params received in request body. The response should be a JSON object like [this](#error-response-structure)


## Response

### Successful Response structure

```yaml
{ status: "Success", data: {} }
```

### Error Response structure

```yaml
{ status: "Failure", message: "" }
```