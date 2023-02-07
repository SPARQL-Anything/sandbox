query:

```sparql
PREFIX ex: <http://example/> 
PREFIX fx:  <http://sparql.xyz/facade-x/ns/>
PREFIX xyz: <http://sparql.xyz/facade-x/data/>

CONSTRUCT {
 ?bnode ex:p ?A
} WHERE {
 SERVICE <x-sparql-anything:> {
	fx:properties fx:location "./data.csv" ; fx:csv.headers true .
 	[] xyz:c1 ?b0 ; xyz:c2 ?A
 }
 BIND ( fx:bnode ( ?b0 ) as ?bnode ) 
}
```
and data:

```csv
c1,c2
b0,A
b0,B
b0,C
b0,D
b0,E
b1,A
b2,B
b3,C
b4,D
b5,E
```


With `fx -q query.sparql -f ttl` you get:

```turtle

@prefix ex:  <http://example/> .
@prefix fx:  <http://sparql.xyz/facade-x/ns/> .
@prefix xyz: <http://sparql.xyz/facade-x/data/> .

[ ex:p    "D" ] .

[ ex:p    "A" ] .

[ ex:p    "C" ] .

[ ex:p    "E" ] .

[ ex:p    "B" , "C" , "E" , "D" , "A" ] .

[ ex:p    "B" ] .
```

with `fx -q query.sparql -f nq` you get:

```n-quads

```

with `fx -q query.sparql -f json` you get:

```json
{
  "@graph" : [ {
    "@id" : "_:b0",
    "p" : "A"
  }, {
    "@id" : "_:b1",
    "p" : "C"
  }, {
    "@id" : "_:b2",
    "p" : "A"
  }, {
    "@id" : "_:b3",
    "p" : "D"
  }, {
    "@id" : "_:b4",
    "p" : "E"
  }, {
    "@id" : "_:b5",
    "p" : "B"
  }, {
    "@id" : "_:b6",
    "p" : "D"
  }, {
    "@id" : "_:b7",
    "p" : "E"
  }, {
    "@id" : "_:b8",
    "p" : "C"
  }, {
    "@id" : "_:b9",
    "p" : "B"
  } ],
  "@context" : {
    "p" : {
      "@id" : "http://example/p"
    },
    "fx" : "http://sparql.xyz/facade-x/ns/",
    "ex" : "http://example/",
    "xyz" : "http://sparql.xyz/facade-x/data/"
  }
}

```

