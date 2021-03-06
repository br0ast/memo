# Formal Competency Questions (Iteration 3)

## CQ_3.1
Return the entities cited by the textual metadata in time of `ex:manuscript_2`.

```
PREFIX ex: <https://w3id.org/irnerio/data/memo/>
PREFIX memo: <https://w3id.org/irnerio/ontology/memo/>

SELECT ?entity

WHERE {
  ?tmit ^memo:hasTextualMetadata ex:manuscript_2 ;
        memo:cites ?entity .
}
```

***

## CQ_3.2
Return all the titles of the critical editions cited by second-level glosses that cite or annotate `ex:text_2`.

```
PREFIX ex: <https://w3id.org/irnerio/data/memo/>
PREFIX memo: <https://w3id.org/irnerio/ontology/memo/>

SELECT ?title

WHERE {
  ?gloss a memo:Gloss ;
         (memo:cites|memo:annotates) / (memo:cites|memo:annotates) ex:text_2 ;
         memo:cites ?edition .
  ?edition a memo:CriticalEditionVolume ;
           ^memo:hasRealization ?editionwork .
  ?editionwork memo:hasTitle ?title
}
```

***

## CQ_3.3
Return all the manuscripts in which at least a second-level gloss that annotates a text cites the same critical edition.

```
PREFIX ex: <https://w3id.org/irnerio/data/memo/>
PREFIX memo: <https://w3id.org/irnerio/ontology/memo/>

SELECT ?manuscript

WHERE {
  ?text a memo:Text .
  ?gloss a memo:Gloss ;
           ^memo:hasPart ?manuscript ;
           memo:annotates / memo:annotates ?text ;
           memo:cites ?edition .
  ?edition a memo:CriticalEditionVolume .
}
```