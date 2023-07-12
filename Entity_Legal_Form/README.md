# Entity Legal Forms Code List

## Content
This folder includes the material used to generate the Entity Legal Forms in RDF to be published by the Publications Office for the [legal form of a Legal Entity](https://semiceu.github.io/Core-Business-Vocabulary/releases/2.1.0/#LegalEntity%3AlegalFormType)  .

The folder includes:
1. The file [2021-10-21-elf-code-list-v1.4.1.csv](2021-10-21-elf-code-list-v1.4.1.csv) downloaded from [GLEIF Entity Legal Forms](https://www.gleif.org/en/about-lei/code-lists/iso-20275-entity-legal-forms-code-list)
2. The file [countries-skos.rdf](countries-skos.rdf) downloaded from [Publications Office Country Authority Table](https://op.europa.eu/en/web/eu-vocabularies/dataset/-/resource?uri=http://publications.europa.eu/resource/dataset/country)
3. The file [SPARQL-query-for-ELF.rq](SPARQL-query-for-ELF.rq) created to generate the Entity Legal Forms in RDF
4. The file [SPARQL-query-for-ELF-columns.rq](SPARQL-query-for-ELF-columns.rq) useful to get the columns names extracted from 1. 

## Process
### Analysis of the GLEIF Entity Legal Forms

#### Format
The GLEIF Entity Legal Forms are provided in 3 file formats: PDF, Excel and CSV.

In order to perform a transformation, a structured format is preferred, therefore the choice is between Excel and CSV.

The Excel file:
* has 1 sheet only
* does not contain excel/macros formulas
* has the same content as the CSV file

Therefore the CSV is the preferred format for the transformation.

#### Content
The CSV file contains a list of legal forms:
* that are not logical linked (no order/ranking)
* that are not physically linked (no reference between each other)
* that are grouped by the "ELF Code" column because of multiple translations, see for example the ELF Code for Belgium [1TX8](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L99-L101) in Dutch, French and German

In addition, the legal forms:
* depend on a country (Column "Country of formation")
* have a status (Column "ELF Status ACTV/INAC") active or inactive
* might have, for each single translation
  *  a transliteration in Latin, see for example the ELF Code for Greece [R3HO](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L1388)
  *  multiple abbrevations, see for example the ELF Code for Belgium [Y1Q4](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L234), where they are concatenated via the ";" delimiter such as "PRIV ST.;PS"

### Transformation

The transformation has been performed via the tool [SPARQL-Anything](https://github.com/SPARQL-Anything/sparql.anything), which:
* does not need to adapt the GLEIF Entity Legal Forms file provided as input for the transformation
* allows to perform just a SPARQL CONSTRUCT query, see [line 10](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L10), and can leverage SPARQL functions such as STRLANG to combine a string with a language tag, see [line 39](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L39)
* allows to query multiple files, the GLEIF ELF Code list in CSV format and the Publications Office Country Authority Table in RDF format, via the SERVICE directive, see [line 27](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L27) and [line 47](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L47) 
* can leverage the [string split function](https://jena.apache.org/documentation/query/library-propfunc.html) from the underlying Jena Fuseki, to split a string using a delimiter, see [line 55]( https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L55)

The SPARQL query:
* filters only the legal forms in ACTIVE status, see [line 42](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L42)
* make sure to have the same countries present in the Publications Office Country Authority Table with the filter in [line 62](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF.rq#L62)

The [server version of SPARQL-Anything](https://github.com/SPARQL-Anything/sparql.anything#using-the-server) has been downloaded directly in this folder so it can access to the GLEIF ELF Code list and to the Publications Office Country Authority Table

### Validation
