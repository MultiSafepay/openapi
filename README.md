# MultiSafepay API OpenAPI definition

## Working on the OpenAPI definition

## Installation

1. Install [Node JS](https://nodejs.org/).
2. Clone this repo, and then in the repo root, run `npm install`.

### Use

#### `npm start`
Starts the reference docs preview server.

#### `npm run build`
Bundles the definition in the dist folder.

#### `npm test`
Validates the definition.

## Contribution guide

If you adjust the file/folder organization, update this contribution guide.

The `.redocly.yaml` controls the settings for various
tools, including the lint tool and the reference
docs engine. For examples, open the file. For more information,
[read the docs](https://redoc.ly/docs/cli/configuration/).

### Schemas

#### Adding schemas

1. Go to the `openapi/components/schemas` folder.
2. To name the schema, add a file with an appropriate filename.
3. Define the schema.
4. Refer to the schema using the `$ref`. See the example below.

##### Example schema
A very simple example:
```yaml
type: string
description: The resource ID. Default: UUID v4
maxLength: 50
example: 4f6cf35x-2c4y-483z-a0a9-158621f77a21
```
A more complex example:
```yaml
type: object
properties:
  id:
    description: The customer identifier string
    readOnly: true
    allOf:
      - $ref: ./ResourceId.yaml
  websiteId:
    description: The website's ID
    allOf:
      - $ref: ./ResourceId.yaml
  paymentToken:
    type: string
    writeOnly: true
    description: |
      A write-only payment token. If supplied, it is converted into a
      payment instrument and set as the `defaultPaymentInstrument`. If both are supplied, the
      value of this property overrides the `defaultPaymentInstrument. The token can only be used once
      before it expires.
  defaultPaymentInstrument:
    $ref: ./PaymentInstrument.yaml
  createdTime:
    description: The customer created time
    allOf:
      - $ref: ./ServerTimestamp.yaml
  updatedTime:
    description: The customer updated time
    allOf:
      - $ref: ./ServerTimestamp.yaml
  tags:
    description: A list of customer's tags
    readOnly: true
    type: array
    items:
      $ref: ./Tags/Tag.yaml
  revision:
    description: >
      The number of times the customer data has been modified.

      The revision is useful when analyzing webhook data to determine if the
      change takes precedence over the current representation.
    type: integer
    readOnly: true
  _links:
    type: array
    description: The links related to resource
    readOnly: true
    minItems: 3
    items:
      anyOf:
        - $ref: ./Links/SelfLink.yaml
        - $ref: ./Links/NotesLink.yaml
        - $ref: ./Links/DefaultPaymentInstrumentLink.yaml
        - $ref: ./Links/LeadSourceLink.yaml
        - $ref: ./Links/WebsiteLink.yaml
  _embedded:
    type: array
    description: >-
      Any embedded objects available that are requested by the `expand`
      querystring parameter.
    readOnly: true
    minItems: 1
    items:
      anyOf:
        - $ref: ./Embeds/LeadSourceEmbed.yaml

```

##### Using the `$ref`

In the complex example above, the schema definition contains `$ref` links to other schema definitions.

Example:

```yaml
defaultPaymentInstrument:
  $ref: ./PaymentInstrument.yaml
```

The value of the `$ref` is the path to another schema definition.

You can use `$ref`s to build schemas using other existing schemas to avoid duplication.

Use `$ref`s to reference schemas from your path definitions.

#### Editing schemas

1. Go to the `openapi/components/schemas` folder.
2. Open the file you want to edit.
3. Edit as required.

### Paths

#### Adding a path

1. Go to the `openapi/paths` folder.
2. Add a new YAML file named with your URL endpoint, but replace `/` with `@` and put path parameters between curly braces like `{example}`.
3. Add the path and a ref to it in your `openapi.yaml` file in the `openapi` folder.

Example addition to the `openapi.yaml` file:
```yaml
'/customers/{id}':
  $ref: './paths/customers@{id}.yaml'
```

Example of a YAML file named `customers@{id}.yaml` in the `paths` folder:

```yaml
get:
  tags:
    - Customers
  summary: Retrieve a list of customers
  operationId: GetCustomerCollection
  description: |
    You can include a markdown description here.
  parameters:
    - $ref: ../components/parameters/collectionLimit.yaml
    - $ref: ../components/parameters/collectionOffset.yaml
    - $ref: ../components/parameters/collectionFilter.yaml
    - $ref: ../components/parameters/collectionQuery.yaml
    - $ref: ../components/parameters/collectionExpand.yaml
    - $ref: ../components/parameters/collectionFields.yaml
  responses:
    '200':
      description: A list of customers was successfully retrieved
      headers:
        Rate-Limit-Limit:
          $ref: ../components/headers/Rate-Limit-Limit.yaml
        Rate-Limit-Remaining:
          $ref: ../components/headers/Rate-Limit-Remaining.yaml
        Rate-Limit-Reset:
          $ref: ../components/headers/Rate-Limit-Reset.yaml
        Pagination-Total:
          $ref: ../components/headers/Pagination-Total.yaml
        Pagination-Limit:
          $ref: ../components/headers/Pagination-Limit.yaml
        Pagination-Offset:
          $ref: ../components/headers/Pagination-Offset.yaml
      content:
        application/json:
          schema:
            type: array
            items:
              $ref: ../components/schemas/Customer.yaml
        text/csv:
          schema:
            type: array
            items:
              $ref: ../components/schemas/Customer.yaml
    '401':
      $ref: ../components/responses/AccessForbidden.yaml
  x-code-samples:
    - lang: PHP
      source:
        $ref: ../code_samples/PHP/customers/get.php
post:
  tags:
    - Customers
  summary: Create a customer (without an ID)
  operationId: PostCustomer
  description: Another markdown description here.
  requestBody:
    $ref: ../components/requestBodies/Customer.yaml
  responses:
    '201':
      $ref: ../components/responses/Customer.yaml
    '401':
      $ref: ../components/responses/AccessForbidden.yaml
    '409':
      $ref: ../components/responses/Conflict.yaml
    '422':
      $ref: ../components/responses/InvalidDataError.yaml
  x-code-samples:
    - lang: PHP
      source:
        $ref: ../code_samples/PHP/customers/post.php
```

This example contains a lot of `$ref`s to different types of components, including schemas, as well as `$ref`s to code samples.

### Adding code samples

1. Go to the `openapi/code_samples` folder.
2. Then go to the `<language>` (e.g. PHP) sub-folder.
3. Go to the `path` folder, and add the ref to the code sample.

To add other languages, add new folders at the appropriate path level.

For more information, see the `code_samples` README.
