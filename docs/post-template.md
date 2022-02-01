# This is a template for defining a POST API operation that is OpenAPI compliant.
# To use this file:
#  1. Make a copy of it.
#  2. Delete these comments.
#  3. Fill in empty fields and choose between elements separated by a "/".
#  4. Rename the file extension to *.yaml.
post:
  description: "Add a description for the operation."
  operationId: Set a unique operationId in camel case.
  parameters:
    - description: | 
        Describe the parameter on multiple lines.
      in: path/query
      name: Choose a name
      required: true/false
      schema:
        type: Choose a type
  requestBody:
    content:
      application/json:
        schema:
          properties:
            example_property:
              format: Choose a format
              type: Choose a type
          required:
            - List which parameters are required
          type: object
    description: "If necessary, add a description of the request body."
    required: true/false
  responses:
    '200':
      content:
        application/json:
          example:
            $ref: '../link-to-your-example-response-if-applicable.json'
          schema:
            properties:
              success:
                type: boolean
              data: 
                type: object
                description: "Add a description."
                properties:
                  example_property:
                    $ref: '../link-to-example_property-schema.yaml'
                  example_with_array:
                    type: array
                    items:
                      $ref: '../link-to-example_with_array-items-schema.yaml'
            type: object
      description: ""
    '404':
      content:
        application/json:
          schema:
            $ref: '../components/schemas/GenericErrorResponse.yaml'
      description: Error
  summary: Add a summary - this is used as a title
  tags:
    - Add relevant tags