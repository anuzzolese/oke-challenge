# GERBIL integration for the evaluation

The following is an example of a cURL POST request that GERBIL performs to an annotation system.<br>
The URL http://system_end_point should be replaced with the actual publicly accessible URL of the system.<br>
The NIF-compliant turtle provided as input contains the sentence to be annotated.

```
curl -H "Content-Type:application/x-turtle" -H "Accept:application/x-turtle"
-d "<http://www.ontologydesignpatterns.org/data/oke-challenge/task-1/sentence-1#char=0,146>
              a                     <http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#RFC5147String> , <http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#String> , <http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#Context> ;
              <http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#beginIndex>        \"0\"^^<http://www.w3.org/2001/XMLSchema#nonNegativeInteger> ;
              <http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#endIndex>          \"146\"^^<http://www.w3.org/2001/XMLSchema#nonNegativeInteger> ;
              <http://persistence.uni-leipzig.org/nlp2rdf/ontologies/nif-core#isString>          \"Florence May Harding studied at a school in Sydney, and with Douglas Robert Dundas , but in effect had no formal training in either botany or art.\" ." 
http://your-systems-URL
```
(Note, that you might have to remove the linebreaks to get the example running.)
  
An annotation system should produce a valid NIF-compliant turtle as output. Such a turlte contains the annotations produced by 
an annotation system, cf. https://github.com/anuzzolese/oke-challenge/blob/master/example_data/task1.ttl for details.

So the participants to the challenge should take care that their systems:
* expose REST interface compliant with the cURL example above;
* produce NIF-compliant outputs for their annotations.
