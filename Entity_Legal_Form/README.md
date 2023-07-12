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
* that are grouped via ELF Code because of multiple translations, see for example the ELF Code [1TX8](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2021-10-21-elf-code-list-v1.4.1.csv#L99-L101)

### Transformation

### Validation
