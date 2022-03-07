# This is an OpenAPI template for a POST operation.
# To use this file:
#  1. Make a copy of it.
#  2. Delete these comments.
#  3. Fill in empty fields and choose between elements separated by a "/".
#  4. Rename the file extension to *.yaml.
post:
  description: Add a description for the operation.
  operationId: Set a unique operationId in camel case.
  parameters:
    - name: Specify the name.
      description: | 
        Describe the parameter on multiple lines.
      in: path/query
      required: true/false
      schema:
        type: Specify the type.
  requestBody:
    description: "If necessary, add a description of the request body."
    required: true/false
    content:
      application/json:
        schema:
          type: object
          properties:
            example_property:
              description: Describe the property.
              type: Specify the type.
              format: Specify the format, if relevant.
          required: [List which parameters are required in alphabetical order, separated by commas]
  responses:
    '200':
      description: Request successful
      content:
        application/json:
          example:
            $ref: '../link-to-your-example-response-if-applicable.json'
          schema:
            type: object
            properties:
              success:
                $ref: '../components/schemas/Success.yaml'
              data: 
                description: Add a description.
                type: object
                properties:
                  example_property:
                    $ref: '../link-to-example_property-schema.yaml'
                  example_with_array:
                    type: array
                    items:
                      $ref: '../link-to-example_with_array-items-schema.yaml'
    '404':
      description: Describe the error.
      content:
        application/json:
          schema:
            $ref: '../components/errors/404Error.yaml'
  summary: Add a summary (appears in the side menu).
  tags:
    - Add relevant tags (used to group requests in the side menu).