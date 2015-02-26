Guidelines for OKE-challenge@ESWC2015
=========

This folder contains guidelines an materials for the Open Knowledge Extraction challenge at ESWC2015.

**Example data**, is available in folder [example_data](./example_data)

**Training data**, will be available in folder [training_data](./training_data)

After the initial paper submission the participants will be able to test their systems on [GERBIL](http://gerbil.aksw.org/gerbil/config), where the three tasks will be added. The take advantage of the the facility, participants must provide their annotators as webservice URI, with input/output provided in [NIF](http://persistence.uni-leipzig.org/nlp2rdf/) format. 

Task 1
=========

*Named Entity Resolution, Linking and Typing for Knowledge Base population.*

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

We will evaluate three aspects on this task, independently:

- Ability to recognize entities: we will check if all strings recognizing entities are identified, using the offsets returned by the systems. **Only full matches are counted as correct** (e.g. if the system returns "Art School" instead of "National Art School" is counted as a miss).
- Ability to **assign the correct type**: evaluation will be carried out only on the 4 target DOLCE types.
- Ability to **link individuals to DBpedia 2014**: participants must **link** entities to DBpedia **only when relevant** (in the example sentence, the referred Douglas Robert Dundas is not present in DBpedia)

We will calculate Precision, recall and F1 for the three subtasks and the winner for task 1 will be the system with higher average F1 for all three.

Task 2
=========

*Class Induction and entity typing for Vocabulary and Knowledge Base enrichment.*

This task consists in producing rdf:type statements, given definition texts. The participants will be given a dataset of sentences, each defining an entity (known a priori), e.g. the entity: dpedia:Skara_Cathedral and its definition "Skara Cathedral is a church in the Swedish city of Skara".

Participants are expected to (i) identify the type(s) of the given entity as they are expressed in the given definition, (ii) create a owl:Class statement for defining each of them as a new class in the target knowledge base, (iii) create a rdf:type statement between the given entity and the new created classes, and (iv) align the identified types, if a correct alignment is available, to a set of given types.

In the task we will evaluate the extraction of all strings describing a type and the alignment to any of the subset of [DOLCE+DnS Ultra Lite classes](http://ontologydesignpatterns.org/ont/wikipedia/d0.owl)


As an example, for the sentence: 

> Brian Banner is a fictional villain from the Marvel Comics Universe created by Bill Mantlo and Mike Mignola and first appearing in print in late 1985..

*Brian Banner* will be given as the *input target entity*. We want the system to recognize any possible type for it. Correct answers include:


| Recognized string for the type    | Generated Type     | rsubClassOf|
| ------------- |:-------------| -----:|
| fictional villain      |http://www.ontologydesignpatterns.org/data/oke-challenge/task-2/FictionalVillain| dul:Personification | 
| villain      | http://www.ontologydesignpatterns.org/data/oke-challenge/task-2/Villain|dul:Person    |  

The results must be provided in [NIF](http://persistence.uni-leipzig.org/nlp2rdf/) format, including the offsets of recognized string describing the type. The expected output for the example sentence can be found in [task2.ttl](./example_data/task2.ttl)

We will evaluate two aspects on this task, independently:

- Ability to **recognize strings that describe the type of a target entity**. As string describing types often include adjectives as modifiers (in the example above, "fictional" is a modifier for villain), in the Gold Standard we will include all possible options; the system answer will be counted **correct as long as at least one of the possibility is returned**.
- Ability to align the identified type with a reference ontology, which for this evaluation will be the subset of [DOLCE+DnS Ultra Lite classes](http://ontologydesignpatterns.org/ont/wikipedia/d0.owl). 

We will calculate Precision, recall and F1 for the two subtasks and the winner for task 2 will be the system with higher average F1 for the two of them.


Task 3
=========

*Relation extraction and naming, and triple generation for Ontology and Knwoledge Base enrichment.*

The participants will be given as input a sentence and two entities contained in the sentence. The task consists in (i) assessing whether the sentence contains an evidence of a relation between the two input entities and if true (ii) the creation of a OWL property representing the relation, including a value for its rdf:label annotation statement, and (iii) the production of a statement for the relation.
The triple must be of the form <entity1> <relation> <entity2>; where: 
a. <entity1>, <entity2> are the input URIs, i.e., the given pair of entities as subject and object of the statement 
b. <relation> is the learnt OWL property as predicate. 
The URI for the predicate must be created by the participants; we will not require the linking with a reference KB, but we will provide a formalism to produce the URI for the relation and use string similarity measure to assess the results against a Gold Standard.
