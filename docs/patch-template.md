# This is an OpenAPI template for a PATCH operation.
# To use this file:
#  1. Make a copy of it.
#  2. Delete these comments.
#  3. Fill in empty fields and choose between elements separated by a "/".
#  4. Rename the file extension to *.yaml.
patch:
  description: "Add a description for the operation."
  operationId: Set a unique operationId in camel case.
  parameters:
    - description: | 
        Describe the parameter on multiple lines.
      in: path/query
      name: Specify the name.
      required: true/false
      schema:
        type: Specify the type.
  requestBody:
    content:
      application/json:
        schema:
          properties:
            example_property:
              type: Specify the type.
              format: Specify the format, if relevant.
          required:
            - List which parameters are required.
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
                description: "Add a description."
                type: object
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
  summary: Add a summary (appears in the side menu).
  tags:
    - Add relevant tags (used to group requests in the side menu).