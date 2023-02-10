# vocpatterns.kurrawong.net

This repository contains the source code for the website <http://vocpatterns.kurrawong.net>. 

<http://vocpatterns.kurrawong.net> is a website that lists questions & answers relating to the modelling, management and delivery of vocabularies.

So please don't dwell here but visite the website itself instead!


## License

This work - all the items in this repository and the published website they support - are licensed under the [Creative Commons BY 4.0](https://creativecommons.org/licenses/by/4.0/) license, a text and an RDF copy of which are availabile in this repository:

* [CC BY 4.0 text](LICENSE)
* [CC BY 4.0 RDF](LICENSE.ttl)


## Copyright

This work is &copy; KurrawongAI 2023, all rights reserved.


## Contact

If you want to contact the creators and maintainers of this for any reason, please see:

[KurrawongAI's Contact Page](https://kurrawong.net/pages/contact.html)


## Technical use

This site is a [Python Sphinx](https://www.sphinx-doc.org/en/master/) with [Myst Parser](https://myst-parser.readthedocs.io/en/latest/index.html) -generated static website that uses to following commands:

- sphinx-autobuild -a source _build/
- live at http://127.0.0.1:8000/

Deploy:

- sphinx-build -b html source _build
