Guidelines for OKE-challenge@ESWC2015
=========

This folder contains guidelines an materials for the Open Knowledge Extraction challenge at ESWC2015.

**Example data**, is available in folder [example_data](./example_data)

**Training data**, will be available in folder [training_data](./training_data)

After the initial paper submission the participants will be able to test their systems on [GERBIL](http://gerbil.aksw.org/gerbil/config), where the three tasks will be added. The take advantage of the the facility, participants must provide their annotators as webservice URI, with input/output provided in [NIF](http://persistence.uni-leipzig.org/nlp2rdf/) format. 

Task 1
=========

Named Entity Resolution, Linking and Typing for Knowledge Base population.
This task consists of (i) identifying Named Entities in a sentence and create an OWL individual (owl:Individual statement) representing it, (ii) assigning a type to such individual (rdf:type statement) selected from a set of given types and (iii) link (owl:sameAs statement) such individual, when possible, to a reference KB (DBpedia).

In the task we will evaluate the extraction of four specific types, from [DOLCE Ultra Lite classes](http://stlab.istc.cnr.it/stlab/WikipediaOntology/): 

- Person
- Place
- Organization
- Role

As an example, for the sentence: 

> Florence May Harding studied at the National Art School in Sydney, and with Douglas Robert Dundas , but in effect had no formal training in either botany or art.	

we want the system to recognize four entities:

| Recognized Entity    | generated URI | Type     | SameAs|
| ------------- |:-------------|:-------------:| -----:|
| Florence May Harding      |http://www.ontologydesignpatterns.org/data/oke-challenge/Florence_May_Harding| dul:Person | dbpedia:Florence_May_Harding |
| National Art School      | http://www.ontologydesignpatterns.org/data/oke-challenge/National_Art_School|dul:Organization    |   dbpedia:National_Art_School |
| Sydney | http://www.ontologydesignpatterns.org/data/oke-challenge/Sydney| dul:Place      |    dbpedia:Sydney  |
| Douglas Robert Dundas |http://www.ontologydesignpatterns.org/data/oke-challenge/Douglas_Robert_Dundas| dul:Person      |      |

The results must be provided in [NIF](http://persistence.uni-leipzig.org/nlp2rdf/) format, including the offsets of recognized entities. The expected output for the example sentence can be found in [task1.ttl](./example_data/task1.ttl)

We will evaluate three aspects on this task:
- Ability to recognize entities: we will check if all strings recognizing entities are identified, using the offsets returned by the systems. Only full matches are counted as correct (e.g. if the system returns "Art School" instead of "National Art School" is counted as a miss).
- Ability to assign the correct type: evaluation will be carried out only on the 4 target DOLCE types.
- Ability to link individuals to DBpedia: participants must link entities to DBpedia only when relevant (in the example sentence, the referred Douglas Robert Dundas is not present in DBpedia)

Task 2
=========

Task 3
=========
