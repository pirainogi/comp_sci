- Represents data as a network of related nodes or objects in order to facilitate  data visualizations and graph analytics
- Node or object contains free-form data that is connected by relationships and grouped according to  labels
- GODBMS (*Graph-Oriented Database Management Systems*) are designed with an emphasis on illustrating connections between data points
  - typically used when analysis of the relationships between heterogeneous data points is the end goal
    - examples: fraud prevention, enterprise operations, FB friend graph

### Examples
- Neo4J
- Datastax
- Enterprise Graph

## Search Engines
- store data using schema-free JSON objects
- similar to document stores but greater emphasis on unstructured or semi-structured data being easily accessible via text-based searches  

### Examples
- Elasticsearch
- Splunk
- Solr

# GraphQL
- Open-source data query and manipulation language for APIs, and a runtime for fulfilling those queries with existing data
- Send a single query to the GraphQL server that includes the concrete data requirements, and the server responds with a JSON object where these requirements are fulfilled
  - For example: instead of `user/:id/followers`, can get the last three followers of a given user
