# Love of Lucene

Speaker: Erik Hatcher

- [Love of Lucene](#love-of-lucene)
  - [Concepts](#concepts)
    - [Inverted Index](#inverted-index)
    - [Text Analyzers](#text-analyzers)
    - [Index Types](#index-types)
    - [Query Parsers](#query-parsers)
    - [Searching](#searching)
  - [Ecosystem](#ecosystem)
  - [Other Resources](#other-resources)
    - [References](#references)

## Concepts

### Inverted Index

- Mapping of tokens with metadata (e.g. number of occurrences, character offsets, etc.)
  
### Text Analyzers

- Rules for tokenizing and normalizing fields
- Runs at index time and on the queries themselves
- Standard
  - Lowercase
  - Break on special characters and whitespace
- Whitespace
  - Lowercase
  - Break on whitespace
- Simple
  - Lowercase
  - Break on special characters and whitespace
  - Ignore non-text (e.g. numeric)
- Keyword
  - Entire field is used as token, unmodified
- English
  - Lowercase
  - Break on special characters and whitespace
  - Stems words
- WordDelimiter
  - Break on special characters, whitespace, and uppercases
- Phonetic
  - Break on special characters and whitespace
  - Translates tokens to phonetic consonant sounds of term
- StandardEdgeNGram
  - Emits tokens from the left edge of the term up to a limit
  - Be careful, can explode the index
- StandardNGram
  - Emits every ngram token up to a limit from within the term
  - Be careful, can explode the index
  
### Index Types

- Numeric
- Spatial
  - Search spatially (e.g. point contained in shape, shape intersects)
- Finite State Transducer
- Vector

### Query Parsers

- Classic
  - Must specify a default field for when not specified in query
  - `foo` => TermQuery using default field
  - `foo*` => PrefixQuery using default field
  - `foo~` => FuzzyQuery using default field
  - `size:[5 TO 10]` => TermRangeQuery using default field
  - `"foo bar"` => PhraseQuery using default field
  - `"foo bar"~3` => PhraseQuery with "slop factor" (i.e. terms with a distance of each other) using default field
  - `loose terms` -> BooleanQuery with OR'ed TermQueries using default field
  - `genre:drama AND cast:keanu` => BooleanQuery with AND'ed TermQueries using non-default fields
  - `actor:keanu reeves` => BooleanQuery with OR'ed TermQueries using default and non-default fields
    - `reeves` not tied to `actor` field

- Simple
  - Can provide a default field or a map of field names to weights
  - Ignores query parsing issues and does what it can

- ComplexPhrase
  - Allows for nested queries (e.g. wildcard inside a phrase query)

- Surround
  - More complex querying on spans
  - `3W(a, b)` => DistanceRewriteQuery to find `a` and `b` within 3 words

### Searching

- Filtering
  - Excludes results based on expression
  - Does not effect relevance scores
  - Cacheable
  - Efficient

- Relevancy Scoring
  - TF/IDF
  - BM25
  - Function boosting

## Ecosystem

- Highlighting
- Suggest
- Spatial
- Facets
- Lucene Monitor
  - Queries as documents
  - Alerts on indexed docs that match saved queries
  - [OpenSearch document monitors](https://opensearch.org/docs/latest/observing-your-data/alerting/monitors/#per-document-monitors)
- MLT
  - Find similar docs in the index to a given doc
- Expressions
- Grouping
- Block join, parent/child
- Luke
  - GUI for Lucene
- Vector Search
  - Uses HNSW
  - KNN
  - Euclidean or Cosine similarity

## Other Resources

### References

- [Signals](https://doc.lucidworks.com/fusion-ai/4.2/469/signals)
