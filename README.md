Dutch Linked Data Strategy
==========================

Contents
--------

1. [Introduction](#introduction)
2. [Registry](#registry)
3. [Data sources](#data-sources)
4. [Connectors](#connectors)
5. [Glossary](#glossary)

Introduction
------------

This document describes an architecture for Dutch linked data sources. 

### General principles

1. Curators remain in control of their data.

2. Do not aggregate.

3. Focused on application of linked data.

4. As opposed to [Aggregators](#aggregator), a separation of concerns between
   data discovery, retrieval and search. 

Registry
--------

The registry is a directory of all Dutch linked data sets available. Its aim 
is to enable *discovery* of linked data sets in a central location. 

It differs from [Aggregators](#aggregator) in three ways.

1. While the Registry contains URIs to entities, it does not store any entity
   data. The [data source](#data-source) remains the authoritative place for 
   entity data. 
2. Because the Registry stores no entity data, it places no restrictions on the
   structure and terms of metadata other than those described under 
   [Data sources](#data-sources).
3. The Registry offers no advanced search capabilities of the data itself. 
   Searching the data should be done through [Connectors](#connector).   
    
This enables the Registry to combine the ideal of decentralized data storage 
and retrieval with the pragmatism of having a single location to discover 
data sets.

The Registry is a directory of all available Dutch linked data sources. It 
contains data on:

- organisations
- [data sets](#data-set)
- [entities](#entity).

Data sources
------------

[Data sources](#data-source) can register data sets with the Registry only if 
they adhere to the following standards.

1. Data sources MUST offer linked data on persistent URIs.
2. Data sources SHOULD offer realtime or near-realtime data at those URIs.

### Linked data on persistent URIs

> Data sources MUST offer linked data on persistent URIs.

The persistent URIs MAY be based on some meaningful domain name (such as the 
name of the organisation or dataset) or it MAY be a handle URI.

For the dataset to be considered linked, it:
- MUST contain a persistent URI for each entity in the dataset 
- MUST use predicate URIs for its descriptions  
- MAY offer links to other datasets.

### Request an entity

#### Request an entity from a custom domain name

When the URI is a custom domain name, such as 
`https://zuiderzeecollectie.nl/collect/52829`:

```http
GET /collect/52829 HTTP/1.1
Host: zuiderzeecollectie.nl
Accept: application/ld+json
```

The server could respond:

```json
HTTP/1.1 200 OK 
Content-Type: application/ld+json; charset=UTF-8

{
    "@id": "https://zuiderzeecollectie.nl/collect/52829",
    "@type": "http://dbpedia.org/ontology/victim",
    "http://purl.org/dc/terms/created": "2006-02-28T18:23:16+00:00",
    "http://purl.org/dc/terms/modified": "2016-07-31T10:19:25+00:00",
    "http://purl.org/dc/terms/issued": "2006-02-28T18:23:00+00:00",
    "http://purl.org/dc/terms/date": "1910-12-19T00:00:00+00:00",
    "http://xmlns.com/foaf/0.1/familyName": "Lovelace",
    "http://xmlns.com/foaf/0.1/firstName": "Ada",
    "http://purl.org/dc/terms/title": "Ada Lovelace",
    "http://purl.org/dc/terms/abstract": "",
    "http://purl.org/dc/terms/description": "",
    "http://purl.org/dc/terms/publisher": {
        "@id": "https://zuiderzeecollectie.nl
    }
}
```

#### Request an entity from a handle URI 

If the URI is a handle, e.g. `http://hdl.handle.net/11259/collection.38743` the 
server MUST return that handle as the resource URI (instead of the internal URI 
that the handle refers to):

```http
GET /11259/collection.38743 HTTP/1.1
Host: hdl.handle.net
Accept: application/ld+json
```

Responds with:

```json
HTTP/1.1 200 OK 
Content-Type: application/ld+json; charset=UTF-8

{
    "@id": "http://hdl.handle.net/11259/collection.38743"
    ...
}
```

### Realtime data

An important objection against [Aggregators](glossary.md#Aggregator) and 
[data dumps](glossary.md#Data-dumps) is that they lag behind updates in the 
original data. To prevent this, 

> Data sources SHOULD offer realtime or near-realtime data at these URIs.

### Linked data wrapper

Not all data source software is capable of above requirements. Therefore, a 
linked data wrapper MAY be introduced that takes care of:

- converting proprietary data to linked data
- serving the linked data at persistent URIs.

In this scenario, the requirements for data sources apply to the linked data
wrapper rather than directly to the source.

Connectors
----------





Glossary
--------

### Aggregator

TODO

Examples: [Europeana](http://www.europeana.eu). 

TODO 

### Collectiebeheersysteem (CBS)

See [data source](#data-source).

### Data dumps

TODO

### Data set

Or ‘collection’. Consists of [entities](#entity).

### Data source

TODO. See [Data source](source.md) chapter.

### Entity

The items (or objects) in a [dataset](#data-set).

### Registry

TODO
