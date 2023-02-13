# VocPatterns

This website is a catalogue of patterns for the modelling and delivery of [SKOS](https://www.w3.org/TR/skos-primer/) vocabularies, very much modelled on [Leigh Dodds' excellent Linked Data Patterns](https://patterns.dataincubator.org/).

## Aim

The aim of this catalogue is to list, and then provide answers for, a series of common questions we've seen in a decade of working with vocabularies.

## Introduction

If you are new to the SKOS data mode or vocabulary modelling in general, you should probably read this:

* [Introduction to SKOS](./intro-to-skos.md).

## Questions & Patterns

The questions are given below with links to one or more _patterns_ - common ways of working - that we think address them.

```{eval-rst}
.. csv-table::
   :header: "Question", "Pattern(s)"

   "How do I create and maintain versions of Cocepts within a vocabulary?", "`Concept Versioning <patterns/concept-versioning.html>`_"
   "How to I indicate the source of my vocabulary?", "`Vocab Derivation <patterns/vocab-derivation.html>`_, `Provenance <patterns/provenance.html>`_"
   "How do I indicate the provenance/lineage of Concepts, Collections & ConceptSchemes?", "`Provenance <patterns/provenance.html>`_"
   "How do I reuse others' vocabularies, with or without alteration?", "`Vocab Derivation <patterns/vocab-derivation.html>`_"
   "How do I indicate a non-Linked Data source for my vocab?", "`Provenance <patterns/provenance.html>`_"
   "How do I describe people and organisations related to my vocab? ", "`Agent Referencing <patterns/agent-referencing.html>`_, `Qualified Role <patterns/qualified-role.html>`_"
```

```{eval-rst}
.. toctree::
   :maxdepth: 1

   intro-to-skos.md
   patterns/agent-referencing.md   
   patterns/concept-reuse.md   
   patterns/concept-versioning.md
   patterns/provenance.md
   patterns/qualified-role.md
   patterns/vocab-derivation.md
```

## Contact

If you'd like to contact us, the authors of these patterns, please go to:

* [Kurrawong AI's Contact Page](https://kurrawong.net/pages/contact.html)