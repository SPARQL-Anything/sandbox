# append
This parameter tells the command line to not overwrite to an existing file but simply append to it. 
Here we test the behaviour in different configurations.

The following use case works nicely, multiple runs append to the same file:
```
fx -q construct.sparql -o out.nt --append
fx -q construct.sparql -o out.nt --append
fx -q construct.sparql -o out.nt --append
```

The following use case works nicely, multiple runs append to the same file:
```
fx -q construct-quads.sparql -o out.nq --append
fx -q construct-quads.sparql -o out.nq --append
fx -q construct-quads.sparql -o out.nq --append
```

This should work with .ttl as well (repeating prefixes are not an issue):
```
fx -q construct.sparql -o out.ttl --append
fx -q count-triples.sparql (20)
fx -q construct.sparql -o out.ttl --append
fx -q count-triples.sparql (40)
```

This will not work with rdf/xml, json, csv, etc... shall we alert and stop the process when this happens?

## Interaction with `-v`
In the following case, the system creates a file for each parameter bindings (--append has no effect):
```
fx -q construct.sparql -v params.csv -o out.ttl --append

out-1.ttl
out-2.ttl
out-3.ttl
out-4.ttl
...
```
Question: should we instead append to the same file?

Interesting how this may be useful with CSV (but it will require to crop out the header after the first run)
```
fx -q query.sparql -v params.csv -o out.csv --append

out-1.csv
out-2.csv
out-3.csv
out-4.csv
...
```
