# docker-compose
```yaml
version: '3.9'

services: 
  # See: https://hub.docker.com/r/swaggerapi/swagger-editor
  # Swagger Editerは Swagger ファイルの生成や編集を行うためのツールです。ブラウザ上で動きます。
  # 左側にYAMLまたはJSONで記述します。右側には左の記述をもとに生成されたドキュメントです。
  # リアルタイムにドキュメントが更新されるので構文チェックを行うこともできます。またこの画面からAPIの実行も可能です。
  swagger-editor:
    image: swaggerapi/swagger-editor
    container_name: swagger-editor
    ports:
      - 8081:8080
  # See: https://hub.docker.com/r/swaggerapi/swagger-ui
  # Swagger UIは Swagger-Specを読み込んで、HTML形式でドキュメントを生成するためのツールです。
  swagger-ui:
    image: swaggerapi/swagger-ui
    container_name: swagger-ui
    ports:
      - 8082:8080
    volumes: 
      # - ./swagger.yaml:/usr/share/nginx/html/swagger.yaml
      - ./swagger.yaml:/app/swagger.yaml
    environment: 
      SWAGGER_JSON: /app/swagger.yaml
  # See: https://hub.docker.com/r/stoplight/prism
  # Prismは、OpenAPI v2（旧称Swagger）およびOpenAPIv3.xを使用したAPIモックおよびコントラクトテスト用のパッケージのセットです。
  swagger-api:
    image: stoplight/prism
    container_name: swagger-api
    ports:
      - 8083:4010
    volumes:
      - ./swagger.yaml:/app/swagger.yaml
    command: mock -h 0.0.0.0 /app/swagger.yaml
```

# Swagger API設定
```yaml:/app/swagger.yaml
openapi: 3.0.0
info:
  version: 1.0.0
  title: Sample API
  description: >-
    A sample API that uses a sample-site as an example to demonstrate features in
    the OpenAPI 3.0 specification
servers:
  - url: 'http://localhost:8003'
paths:
  /users:
    get:
      description: >
        Returns all users
      operationId: findUsers
      parameters:
        - name: tags
          in: query
          description: tags to filter by
          required: false
          style: form
          schema:
            type: array
            items:
              type: string
        - name: limit
          in: query
          description: maximum number of results to return
          required: false
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: user response
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
        default:
          description: unexpected error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
components:
  schemas:
    User:
      type: "object"
      required:
        - "name"
      properties:
        id:
          type: "integer"
          format: "int64"
          example: 100
        name:
          type: "string"
          example: "Taro"
        status:
          type: "string"
          description: "user status"
          enum:
            - "pending"
            - "active"
            - "inactive"
    Error:
      type: "object"
      properties:
        code:
          type: "integer"
          format: "int32"
        type:
          type: "string"
        message:
          type: "string"
externalDocs:
  description: "Find out more about Swagger"
  url: "http://swagger.io"
```
