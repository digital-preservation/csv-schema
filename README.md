CSV Schema
==========

A Schema Language for CSV (Comma Separated Value) files.

This repository holds the code for creating the CSV Schema specification document, which
is then published as HTML. The Schema language is formally expressed in EBNF.

You can find the the documentation and latest published specification here:
	http://digital-preservation.github.io/csv-schema.

* Examples of CSV Schemas can be found in the [`example-schemas`](https://github.com/adamretter/csv-schema/tree/master/example-schemas) folder.


Repository Organisation
-----------------------
* `master` branch holds the source code for producing the specification.

* `gh-pages` holds the documentation and copies of each published version of the specification.

* There is one tag from master each time a version of the specification is published. The tag name reflects
the specification version number.

Released under the [Mozilla Public Licence version 2.0](http://www.mozilla.org/MPL/2.0/).


Philosophy
----------
A few bullet-points that guide our thinking in the design of the CSV Schema Language:

* Simple CSV Schema Language.
A DSL (Domain Specifc Language) was desired that could be expressed in plain text and should be simple enough that Metadata experts could easily write it without having to know a programming language or data/document modelling language such as XML or RDF. Note, the CSV Schema Language is **NOT** itself expressed in CSV, it is expressed in a simple text format.

* Context is King!
Schema rules are written for each column of the CSV file. Each set of column rules is then asserted against each row of the CSV file in turn. Each rule in the CSV Schema operates on the current context (e.g. defined Column and parsed Row), unless otherwise specified. Hopefully this makes the rules short and concise.

* Streaming.
Often the Metadata files that we receive are very large as they contain many records about a Collection which itself can be huge. The CSV Schema Language was designed with an eye to being able to write a Validation tool which could read the CSV file as a stream. Few steps require mnenomization of data from the CSV file, and where they do this is limited and should be easily optimisable to keep memory use to a minimum.

* Sane Defaults.
We try to do the right thing by default, CSV files and their bretheren (Tab Separated Values etc.) can come in many shapes and sizes, by default we parse CSV according to [RFC 4180](http://tools.ietf.org/html/rfc4180 "Common Format and MIME Type for Comma-Separated Values (CSV) Files"), of course we allow you to customize this behaviour in the CSV Schema.

* CSV Schema is ***NOT*** a Programming Language.
This is worth stressing as it was something we had to keep site of ourselves during development; CSV Schema is a simple data definition and validation language for CSV!