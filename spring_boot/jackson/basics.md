Jackson data binding good documentation

* *** https://github.com/FasterXML/jackson-databind/?tab=readme-ov-file
* *** https://github.com/FasterXML/jackson-docs?tab=readme-ov-file



1) What is the difference between ObjectNode and JsonNode in Jackson?
   
JsonNode is a base class that ObjectNode and ArrayNode extend. JsonNode represents any valid Json structure whereas ObjectNode and ArrayNode are particular implementations for objects (aka maps) and arrays, respectively.

ArrayNode has specific methods for dealing with arrays such as get(index i) E.g. you cannot get an item at a specific index in a JsonNode or ObjectNode but you can in an ArrayNode.
