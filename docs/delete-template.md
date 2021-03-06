# This is an OpenAPI template for a DELETE operation.
# To use this file:
#  1. Make a copy of it.
#  2. Delete these comments.
#  3. Fill in empty fields and choose between elements separated by a "/".
#  4. Rename the file extension to *.yaml.
delete:
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
                $ref: '../components/schemas/Success.yaml
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
    '404':
      description: Error
      content:
        application/json:
          schema:
            $ref: '../components/errors/404Error.yaml'
  summary: Add a summary (appears in the side menu).
  tags:
    - Add relevant tags (used to group requests in the side menu).