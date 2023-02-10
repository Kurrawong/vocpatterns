# Vocabulary Derivation Pattern

*How to I indicate the source of my vocabulary?*

*How do I reuse others' vocabularies, with or without alteration?*

## Context

Often many vocabularies are needed for use within a particular environment, and of those, often some are well-known or standardised vocabs, others are local: things we have to create ourselves. We may want to store all the vocabs we use - ours and others' - locally to provide for easy or managed use.

To ensure users know which vocabs can be extended or altered locally - with 'our' authority - compared with those that cannot and perhaps require involvement in a larger management regime, we need to indicate vocabs origins and also the _derivation mode_: the way in which we use external vocabs. 

## Solution

Store all vocabularies locally but use several properties for the vocabulary to indicate a vocab's:

* publisher/maintainer
* provenance
* derivation mode

### 1. publisher/maintainer

There are several properties commonly used to indicate a publisher and also a [Qualified Role Pattern](qualified-role.md). The common properties indicated for use here are:

* [schema.org's](https://schema.org) `publisher`
* [Dublin Core Term's](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/) `publisher`
* [Qualified Role Pattern](qualified-role.md) using [DCAT's](https://www.w3.org/TR/vocab-dcat/) `hadRole` with a role from a vocab
  * such as the [ISO's 19115-1 Role Codes](http://linked.data.gov.au/def/iso19115-1/RoleCode)

### 2. provenance

Use the [Provenance Pattern](provenance.md).

### 3. derivation mode

Indicate the way in which this vocabulary derives from its source using the [Vocabulary Derivation Modes vocab](https://linked.data.gov.au/def/vocab-derivation-modes).

_This property is only relevant if the source is a controlled vocabulary, as opposed to a textual source from which this vocab ie extracted. Ideally , the source should be a SKOS vocab too._

## Example(s)

### 1. publisher/maintainer

This example uses `<https://schema.org/publisher>`, so we understand that `<http://example.com/agent/y>` publishes this vocabulary.

```
PREFIX sdo: <https://schema.org/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

<https://example.com/vocab/x>
    a skos:ConceptScheme ;
    skos:prefLabel "Vocab X"@en ;
    ...
    sdo:publisher <http://example.com/agent/y> ;
    ...
.
```
Note that in this example, the _agent_, the publisher, is referred to by IRI, not by text, as per the pattern [Agent Referencing](agent-referencing.md).

If we wanted to indicate another role for the agent, other than `publisher`, we could either look for other schema.org/Dublin Core properties, such as Dublin Core's `creator` or we could use a role vocabulary within the [Qualified Role Pattern](qualified-role.md) like this where `<http://example.com/agent/y>` is indicated as the vocabulary's `custodian`:

```
PREFIX dcat: <https://www.w3.org/ns/dcat#>
PREFIX isorole: <http://linked.data.gov.au/def/iso19115-1/RoleCode/>
PREFIX prov: <http://www.w3.org/ns/prov#>
PREFIX sdo: <https://schema.org/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

<https://example.com/vocab/x>
    a skos:ConceptScheme ;
    skos:prefLabel "Vocab X"@en ;
    ...
    prov:qualifiedAttribution [
        prov:agent <http://example.com/agent/y> ;
        dcat:hadRole isorole:custodian ;
    ] ;
    ...
.
```

### 2. provenance

When the source vocab is a Linked Data object, Vocab M:
```
PREFIX sdo: <https://schema.org/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

<https://example.com/vocab/x>
    a skos:ConceptScheme ;
    skos:prefLabel "Vocab X"@en ;
    ...
    prov:wasDerivedFrom <https://example.com/vocab/m> ;
    ...
.
```

3. **derivation mode**

When this vocab is a subset - not an extension - of the source vocab from which it is derived, Vocab M:
```
PREFIX sdo: <https://schema.org/>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

<https://example.com/vocab/x>
    a skos:ConceptScheme ;
    skos:prefLabel "Vocab X"@en ;
    ...
    prov:qualifiedDerivation [
      prov:entity <https://example.com/vocab/m> ;
      dcat:hadRole <https://example.com/vocab/m> ;
    ] ;
    ...
.
```

## Discussion

With the specification of these properties, it is clear to users whether _we_ are the authors of this vocab and, if not, who is. Also, we users can see that if this vocab is derived from another, just how it is so derived. 

The [Vocabulary Derivation Modes vocab](https://linked.data.gov.au/def/vocab-derivation-modes) includes the following derivation modes:

* Direct
* Extension
* Relabelling
* Subsetting
* Subsetting and Extension

The vocab itself defines these modes but just for example: use _Subsetting_ when "the reusing vocabulary only subsets the original but does not extend it". use of this derivation mode indicator will assure the user that any terms found in this derived vocab are also present in the original, thus any use of this vocab is conformant with use of the original.

## Related

* [Provenance](provenance.md)
* [Concept Reuse](concept-reuse.md)

## Further Reading

* [Vocabulary Derivation Modes vocab](https://linked.data.gov.au/def/vocab-derivation-modes)