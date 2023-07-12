# Entity Legal Forms Code List

## Content
This folder includes the material used to generate the Entity Legal Forms in RDF to be published by the Publications Office for the [classification of Legal Entity](https://semiceu.github.io/Core-Business-Vocabulary/releases/2.1.0/#LegalEntity%3AlegalFormType)  .

The folder includes:
1. The file [2021-10-21-elf-code-list-v1.4.1.csv](2021-10-21-elf-code-list-v1.4.1.csv) downloaded from [GLEIF Entity Legal Forms](https://www.gleif.org/en/about-lei/code-lists/iso-20275-entity-legal-forms-code-list)
2. The file [countries-skos.rdf](countries-skos.rdf) downloaded from [Publications Office Country Authority Table](https://op.europa.eu/en/web/eu-vocabularies/dataset/-/resource?uri=http://publications.europa.eu/resource/dataset/country)
3. The file [SPARQL-query-for-ELF.rq](SPARQL-query-for-ELF.rq) created to generate the Entity Legal Forms in RDF
4. The file [SPARQL-query-for-ELF-columns.rq](SPARQL-query-for-ELF-columns.rq) useful to get the columns names extracted from 1. 

## Process
### Analysis of the GLEIF Entity Legal Forms

#### Format
The GLEIF Entity Legal Forms are provided in 3 formats: PDF, Excel and CSV.

In order to perform a transformation, a structured format is preferred, therefore the choice is between Excel and CSV.

The Excel file:
* has 1 sheet only
* does not contain excel/macros formulas
* has the same content as the CSV file

Therefore the CSV is the preferred format for the transformation.

#### Content
The CSV file contains a list of legal forms:
* that are not logical linked (no order/ranking)
* that are not physically linked (no referenced between each other)
* that are grouped via the "ELF Code" column because of multiple translations, see for example the ELF Code [1TX8](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L99-L101)

In addition the legal forms:
* depend on a country (Column "Country of formation")
* have a status (Column "ELF Status ACTV/INAC") active or inactive
* might have, for each single translation, a transliteration in Latin (see for example the ELF Code for Greece [R3HO](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L1388) ) and multiple abbrevations (see for example the ELF Code for Belgium [Y1Q4](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L234) )

### Transformation

The transformation has been performed via the tool [SPARQL-Anything](https://github.com/SPARQL-Anything/sparql.anything), which:
* does not need to adapt the GLEIF Code list to be used every time
* allows to perform just a SPARQL Construct query
* allows to query multiple files, the GLEIF ELF Code list in CSV format and the Publications Office Country Authority Table in RDF format, via the SERVICE directive
* can leverage the [string split function](https://jena.apache.org/documentation/query/library-propfunc.html) from the underlying Jena Fuseki

The [server version of SPARQL-Anything](https://github.com/SPARQL-Anything/sparql.anything#using-the-server) has been downloaded directly in this folder so it can access to the GLEIF ELF Code list and to the Publications Office Country Authority Table

### Validation
