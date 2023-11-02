
Download SPARQL Anything CLI [from the release page](https://github.com/SPARQL-Anything/sparql.anything/releases/tag/v0.8.2) -- the jar file is called `sparql-anything-v0.8.2.jar`.

Run the command:

```bash
$ java -jar -Xmx=4G sparql-anything-v0.8.2.jar [...]
```

To triplify the musicmoz xml and write the output on the musicmoz.ttl file:

```bash
java -jar -Xmx=4G sparql-anything-v0.8.2.jar -q triplify.sparql -o musicmoz.ttl
```

To query for the list of band names:

```bash
java -jar -Xmx=4G sparql-anything-v0.8.2.jar -q list-bands.sparql -l musicmoz.ttl
```

[See docs for more info](https://sparql-anything.readthedocs.io/en/v0.8.2/)
