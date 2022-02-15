```
# Find list of distinct (that is do not repeat same name) directors in DB - movies/Neo4j Sandbox
MATCH (p:Person)-[d:DIRECTED]-(m:Movie) RETURN DISTINCT p

# Find list of distinct (that is do not repeat same name) actors in DB - movies/Neo4j Sandbox
MATCH (p:Person)-[d:ACTED_IN]-(m:Movie) RETURN DISTINCT p
```
