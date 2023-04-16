##INFO 7255 - Project to demonstrate Indexing of Structured JSON objects

### Features
- Authentication using Bearer Token generated by JWT
- Validate request JSON object with JSON Schema
- Cache Server Response and validate cache using ETag
- Support POST, PUT, PATCH, GET and DELETE Http Methods for the REST API
- Store JSON Objects in Redis key-value store for data persistence
- Index the JSON Objects in Elastic Server for Search capabilities
- Queueing indexing requests to Elastic Server using RabbitMQ


### Tech Stack
- Spring Boot (Java)
- Docker
- Redis 
- Elastic Search
- RabbitMQ


### Features
- Authentication using Bearer Token generated by JWT
- Validate request JSON object with JSON Schema
- Cache Server Response and validate cache using ETag
- Support POST, PUT, PATCH, GET and DELETE Http Methods for the REST API
- Store JSON Objects in Redis key-value store for data persistence
- Index the JSON Objects in Elastic Server for Search capabilities
- Queueing indexing requests to Elastic Server using RabbitMQ


### Data Flow
1. Generate token using the `/token` endpoint
2. Validate further API requests using the Bearer Token
3. Create JSON Object using the `POST` HTTP method
4. Validate incoming JSON Object using the respective JSON Schema
5. De-Structure hierarchial JSON Object while storing in Redis key-value store
6. Enqueue object in RabbitMQ queue to index the object
7. Dequeue from RabbitMQ queue and index data in ElasticServer
8. Implement Search queries using Kibana Console to retrieve indexed data
[**Architecture diagram**](https://github.com/hazellobo/INFO7255-demo/blob/master/ArchitectureDiagram.pdf)


### Build and Run 
1. Run docker-compose.yml file to start the services - Elasticsearch, Kibana, and RabbitMQ defined in the file
2. Run as Spring Boot Application in any IDE

This would start the server. Create the data using the REST API endpoints and query the indexed data on Kibana Console.


### API Endpoints

- GET `/token` - This generates a RSA-signed JWT token used to authenticate requests
- POST `/addPlan` - Creates a new plan provided in the request body
- PUT `/plan/{objectId}` - Updates an existing plan provided by the objectId
    - A valid Etag for the object should also be provided in the `If-Match` HTTP Request Header
- PATCH `/plan/{objectId}` - Patches an existing plan provided by the objectId
    - A valid Etag for the object should also be provided in the `If-Match` HTTP Request Header
- GET `/plan/{objectId}` - Fetches an existing plan provided by the objectId
    - An Etag for the object can be provided in the `If-None-Match` HTTP Request Header
    - If the request is successful, a valid Etag for the object is returned in the `ETag` HTTP Response Header
- DELETE `/plan/{objectId}` - Deletes an existing plan provided by the id
    - A valid Etag for the object should also be provided in the `If-Match` HTTP Request Header