# Agent Referencing

*How to I refer to the people and organisations involved with my vocabulary?*

## Context

It is often important to list people and organisations, _agents_, related to vocabularies and sub-vocabulary elements. For example, listing the _publisher_ of a vocabulary or its _creator_. We may also want to list a _contributor_ to a specific `Concept` within a vocabulary.

## Solution

### 1. Refer to an Agent in one of three ways

In order of preference:

#### a. By a given IRI

Identify an Agent with a known IRI, e.g. a catalogue entry or public ID.

#### b. With an IRI within this vocab's namespace

Encapsulate information such as type, name, URL or email, titles etc. of the Agent as an Agent element entry in your vocab.

See the examples for what a good Agent Entry might look like.

#### c. With a Blank Node

Encapsulate information such as type, name, URL or email, titles etc. of the Agent as a Blank Node in your vocab.

**_Do NOT refer to the agent using a text literal_**

### 2. Indicate the role of the Agent with a simple, well-known, predicate

Use a predicate such as `dcterms:creator` to indicate an Agent with role of "creator".

Use the following predicate only, in preferred ontology order:

**Ontology** | **Predicate** | **Role**
--- | --- | ---
[schema.org](https://schema.org) | `author` | creator / author
&nbsp; | `creator` | creator, when author seems to not fit
&nbsp; | `contributor` | contributor / co-author
&nbsp; | `copyrightHolder` | copyright holder
&nbsp; | `editor` | editor
&nbsp; | `funder` | funder
&nbsp; | `maintainer` | maintainer
&nbsp; | `provider` | supplier but not creator of the resource
&nbsp; | `sponsor` | sponsor
&nbsp; | `translator` | translator
[Dublin Core Terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/) | `creator` | creator / author
&nbsp; | `contributor` | contributor / co-author
&nbsp; | `mediator` | supplier but not creator of the resource
&nbsp; | `publisher` | publisher
&nbsp; | `rightsHolder` | rights holder

### 2. Indicate a Role for the Agent using the [Qualified Role](qualified-role.md) pattern

Link the Agent to a _role_, taken from a roles vocab.

## Examples

If you want to say that Vocab X was created by Person Y and published by Organisation Z, refering to the Agents "By a given IRI":

```
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX sdo: <https://schema.org/>

<http://example.com/vocab/x>
    a skos:ConceptScheme ;
    sdo:creator <http://example.com/agent/y> ;
    dcterms:publisher <http://example.com/agent/z>
    ...
.
```

To use roles from the [ISO's 19115-1 _Role Codes_ vocabulary](http://def.isotc211.org/iso19115/-1/2018/CitationAndResponsiblePartyInformation/code/CI_RoleCode) with the [Qualified Role](qualified-role.md) pattern for the same vocab & agents:
```
PREFIX iso: <http://def.isotc211.org/iso19115/-1/2018/CitationAndResponsiblePartyInformation/code/CI_RoleCode/>

<http://example.com/vocab/x>
    a skos:ConceptScheme ;
    prov:qualifiedAttribution [
        prov:agent <http://example.com/agent/y> ;
        dcat:hadRole iso:author ;  # no creator in ISO vocab
    ] ,
    [
        prov:agent <http://example.com/agent/z> ;
        dcat:hadRole iso:publisher ;
    ] ;
    ...
.
```

The advantage of the above is that there are many more roles to choose from.

If the creator Agent you are referring to has no IRI but your vocab has the namespace `<http://example.com/vocab/x>`:

```
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX sdo: <https://schema.org/>

<http://example.com/vocab/x>
    a skos:ConceptScheme ;
    sdo:creator <http://example.com/vocab/x/person-y> ;  # namespace IRI + ID for Person Y
    dcterms:publisher <http://example.com/agent/z>
    ...
.

<http://example.com/vocab/x/person-y>
    a sdo:Person ;
    sdo:name "Person Y" ;
    ...
.
```

If you want to quote the details of Organisation Z, don't have an IRI for it and don't want to create one in your vocab's namespace, use a Blank Node:

```
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX sdo: <https://schema.org/>

<http://example.com/vocab/x>
    a skos:ConceptScheme ;
    sdo:creator <http://example.com/agent/y>
    dcterms:publisher [
        a sdo:Organization ;
        sdo:name "Organization Z" ;
        sdo:url "https://www.org-z.com"^^xsd:anyURI ;
        sdo:parentOrganization <http://example.com/agent/other-org> ;
    ] ;
    ...
.
```

Be sure to indicate the type of Agent if using a Blank Node. Above this is `a sdo:Organization`.

## Discussion

You really should find a public, stable, IRI for Agents and use that, if possible. See if people have [ORCIDs](https://orcid.org) and organisations [RORs](https://ror.org/) or similar.

If you can't find an IRI for an Agent, try to use your vocab's namespace and define an Agent object with basic properties, such as those for Person/Organization in [schema.org](https://schema.org/Organization).

It's easy to use common role predicates to link a Concept Scheme or a Concept to an Agent and know the role they played. However, if a specialised role is wanted - perhaps you even want to define your own roles - they use the [Qualified Role](qualified-role.md) pattern .

## Related

* [Qualified Role](qualified-role.md)

## Further Reading

* [DCAT's Qualified Attribution](https://www.w3.org/TR/vocab-dcat/#Property:resource_qualified_attribution)
* [PROV-O's Qualified Attribution](https://www.w3.org/TR/prov-o/#qualifiedAttribution)
