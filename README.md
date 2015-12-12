### (Unofficial) Openrdf Sesame Triplestore Docker Image
--------------------------------------------------------------------

Docker image to run a Sesame Triplestore inside a Tomcat application server

#### Image tags
--------------------
  - latest, 2.7.8 => [Dockerfile](https://github.com/subotic/docker-sesame/tree/master/2.7.8/Dockerfile)

#### Usage
---------------

To run the image and bind to port :

````
docker run -d -p 8080:8080 subotic/openrdf-sesame
````

#### Sources
----------------

See [RDF4J.org](http://www.rdf4j.org) for Sesame's source code.