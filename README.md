Dutch Linked Data Strategy
==========================

Contents
--------

1. [Registry](#registry)
2. [Data sources](#data-sources)
3. [Glossary](#glossary)

Registry
--------

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
    },
        "http://purl.org/vocab/relationship/childOf": {
        "@id": "https://www.joodsmonument.nl/rsc/224332"
    },
        "http://dbpedia.org/ontology/residence": {
        "@id": "https://www.joodsmonument.nl/rsc/45385"
    },
    "http://xmlns.com/foaf/0.1/thumbnail": {
    "@id": "https://www.joodsmonument.nl/image/2016/7/31/442n00007006_jpg_mediaclass_admin_media_d320edb0ac6a9e3b6d8f3f57c001c114986dcb01.jpg%28mediaclass-foaf-thumbnail.56b969f0e8c1e384a0390286354b597588085f90%29.jpg"
    },
    "http://xmlns.com/foaf/0.1/depiction": [
    {
      "@id": "https://www.joodsmonument.nl/image/2016/7/31/442n00007006_jpg_mediaclass_admin_media_d320edb0ac6a9e3b6d8f3f57c001c114986dcb01.jpg%28%29%28E879AD7950E0BBFC79017B3345DC15AA%29.jpg"
    },
    {
      "@id": "https://www.joodsmonument.nl/rsc/127447"
    }
    ]
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

Linked data wrapper
-------------------

Not all data source software is capable of above requirements. Therefore, a 
linked data wrapper MAY be introduced that takes care of:

- converting proprietary data to linked data
- serving the linked data at persistent URIs.

In this scenario, the requirements for data sources apply to the linked data
wrapper rather than directly to the source.

Glossary
--------

### Aggregator

TODO

Examples: [Europeana](http://www.europeana.eu). 

TODO 

## Collectiebeheersysteem (CBS)

See [data source](#data-source).

## Data dumps

TODO

## Data set

Or ‘collection’. Consists of [entities](#entity).

## Data source

TODO. See [Data source](source.md) chapter.

## Entity

The items (or objects) in a [dataset](#data-set).

## Registry

TODO
