# Knowledge Graphs: Architecture and Information

Speaker: Brian Sletten

- [Knowledge Graphs: Architecture and Information](#knowledge-graphs-architecture-and-information)
  - [Introduction](#introduction)
    - [Questions](#questions)
    - [Data](#data)
  - [RDF](#rdf)
  - [SPARQL](#sparql)
  - [Linked Data](#linked-data)
  - [JSON-LD](#json-ld)
  - [Other Resources](#other-resources)
    - [References](#references)

## Introduction

### Questions

- What do you know?
  - Not always clear
  - You may have a lot of data but it may not be easily discovered or in a useable state
- How do you accumulate data?
  - Need a strategy that doesn't involve lumping everything together into one place
- How do you exchange data?
  - Probably an API
- How do you deal with storage differences?
  - Data across relational dbs, nosql, blob storage, etc.
- How do you deal with name conflicts?
- How do you deal with structural differences?
- How do you deal with differing scopes and levels of detail?
- Is consensus possible?
  - Probably not

### Data

- Data isn't all that useful in and of itself
- Data becomes information when it is understandable and relevant to your needs
- Information becomes knowledge in context
- Knowledge becomes wisdom in practice

## RDF

- Resource Description Framework
- Open standard designed around problem-space thinking, as opposed to solution-space thinking
- A graph model designed to learn new things, eminently extensible
- Allows you to easily integrate many facts in different formats without custom code
- Concepts
  - Subjects aka non-information resources
  - Predicates aka relationships
  - Objects aka information resources

## SPARQL

- SPARQL Protocol and RDF Query Language
- Graph-oriented
- Queries
  - SELECT matching graph patterns
  - ASK questions
  - CREATE new graphs
  - DESCRIBE nodes
- Protocol
  - Push queries to servers
- Can query across combined datasets, local and remote

## Linked Data

- Use URIs as names for things
- Use HTTP URIs so that people can look up those names
- When someone looks up a URI, provide useful information (not just raw json)
- Include links to other URIs

## JSON-LD

- 100% Compatible with JSON
- Zero Edits Where Possible
- Bring Linked Data to Web Development
- No knowledge of RDF required
- Interoperable with RDF
- Can be stored in JSON database engines

## Other Resources

### References

- [Graph? Yes! Which one? Help!](https://arxiv.org/abs/2110.13348)
- [Most important query ever](http://tinyurl.com/n9hhs68)
- [SPARQL query examples](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/queries/examples)
- [JSON-LD](https://json-ld.org/)
- [Knowledge graph evolution: Platforms that speak your language](https://www.zdnet.com/article/knowledge-graph-evolution-platforms-that-speak-your-language/)
- [Awesome Knowledge Graph: A curated list of Knowledge Graph related learning materials, databases, tools and other resources](https://github.com/totogo/awesome-knowledge-graph)
