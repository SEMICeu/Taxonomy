# Entity Legal Forms Code List

## Content
This folder includes the material used to generate the Entity Legal Forms in RDF to be published by the Publications Office for the [legal form type of a Legal Entity](https://semiceu.github.io/Core-Business-Vocabulary/releases/2.1.0/#LegalEntity%3AlegalFormType) in the Core Business vocabulary.

The folder mainly includes:
1. The file [2023-09-28-elf-code-list-v1.5.csv](2023-09-28-elf-code-list-v1.5.csv) downloaded from [GLEIF Entity Legal Forms](https://www.gleif.org/en/about-lei/code-lists/iso-20275-entity-legal-forms-code-list)
2. The file [countries-skos.rdf](countries-skos.rdf) downloaded from [Publications Office Country Authority Table](https://op.europa.eu/en/web/eu-vocabularies/dataset/-/resource?uri=http://publications.europa.eu/resource/dataset/country) version 20230915-0
3. The file [ELF_OP_matching.csv](ELF_OP_matching.csv) that matches the countries in GLEIF with those in Publications Office
4. The file [SPARQL-query-for-ELF-v1.5.rq](SPARQL-query-for-ELF-v1.5.rq) created to generate the Entity Legal Forms in RDF
5. The file [output-v1.5_validated.ttl](output-v1.5_validated.ttl) generated as output containing the Entity Legal Forms in RDF

## Process

The process is divides in 4 steps:
1. Analysis of the GLEIF Entity Legal Forms
2. Finding and evaluate matches between GLEIF and Publications Office countries
3. Transformation
4. Validation

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
* that are grouped by the "ELF Code" column because of multiple translations, see for example the ELF Code for Belgium [1TX8](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2023-09-28-elf-code-list-v1.5.csv#L115-L117) in Dutch, French and German

In addition, the legal forms:
* depend on a country (Column "Country of formation") which name might be different from the countries published by the Publications Office, for example GLEIF uses "Brunei Darussalam" while Publications Office uses "Brunei" that is why the matching file [ELF_OP_matching.csv](ELF_OP_matching.csv) is needed
* have a status (Column "ELF Status ACTV/INAC") active or inactive
* might have, for each single language:
  *  a transliteration in Latin, see for example the ELF Code for Greece [3RHO](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2023-09-28-elf-code-list-v1.5.csv#L1413) 
  *  multiple abbrevations, see for example the ELF Code for Belgium [Y1Q4](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/2023-09-28-elf-code-list-v1.5.csv#L250), where they are concatenated via the ";" delimiter such as "PRIV ST.;PS"
 
### Finding and evaluate matches between GLEIF and Publications Office countries

As GLEIF and Publications Office publish their list of countries which differ, [SPARQL-Anything](https://github.com/SPARQL-Anything/sparql.anything) [version 0.9.DEV-5](https://github.com/SPARQL-Anything/sparql.anything/releases/tag/v0.9-DEV.5) has been used to generate candidate correnspondences. The candidate correspondences are then evaluated by the user and the exact correspondences are then created.

![](find_correspondences.jpg)

Sparql-Anything executes the [ELF_OP_matching.rq](ELF_OP_matching.rq) which uses the [Jaro-Winkler](https://en.wikipedia.org/wiki/Jaro%E2%80%93Winkler_distance) string distance to find the closest matches.
Jaro-Winkler resulted better than other string distances in finding closest matches, see [string_distance_comparison.csv](string_distance_comparison.csv), generating only 2 false positives. Therefore the file is reviewed so that it can be used in the transformation step.

### Transformation

The transformation has been performed via the tool [SPARQL-Anything](https://github.com/SPARQL-Anything/sparql.anything) [version 0.9.DEV-5](https://github.com/SPARQL-Anything/sparql.anything/releases/tag/v0.9-DEV.5), which:
* does not need to change the structure of the GLEIF CSV file, provided as input for the transformation
* allows to perform just a SPARQL CONSTRUCT query, see [line 15](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L15), and can leverage SPARQL functions such as [STRLANG](https://www.w3.org/TR/sparql11-query/#func-strlang) to combine a string with a language tag, see [line 65](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L65)
* allows to query multiple files in different format via the SERVICE directive:
  * the GLEIF ELF Code list in CSV format, see [line 46](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L46)
  * the ELF OP matching in CSV format, see [line 87](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L87)
  * the Publications Office Country Authority Table in RDF format, see [line 92](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L92) 
* can leverage the [string split function](https://jena.apache.org/documentation/query/library-propfunc.html) from the underlying Jena Fuseki, to split a string using a delimiter, see [line 105]( https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L105)

The transformation execution at the core of the process:
![](transformation.jpg)

![extracting values from the ELF code list file](sparql-anything.jpg)

The SPARQL query:
* adds the transliteration to Latin only for certain languages like Bulgarian (bg) or Greek (el), see [line 73](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L73)
* make sure to have the same countries present in the Publications Office Country Authority Table by using the matching retrieved in [lines 82-84](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L82-L84) with the filter in [lines 113-114](https://github.com/SEMICeu/Taxonomy/blob/master/Entity_Legal_Form/SPARQL-query-for-ELF-v1.5.rq#L113-L114)

The [SPARQL-Anything server](https://github.com/SPARQL-Anything/sparql.anything#using-the-server) [version 0.8.2](https://github.com/SPARQL-Anything/sparql.anything/releases/tag/v0.8.2) has been downloaded directly in this folder so it can access to the GLEIF ELF Code list and to the Publications Office Country Authority Table and, via a web interface (pointing the browser to http://localhost:3000/sparql), it helps to type in the SPARQL query and to execute it. 

Due to it's size (200 MB), SPARQL-Anything was not included in this repository, so, in order to run the query, one must download the server version of SPARQL-Anything themselves.

### Validation

The output of the transformation is a RDF file [output-v1.5.ttl](output-v1.5.ttl) containing skos:ConceptScheme pointing to all skos:Concept generated.

The RDF file is validated manually against:

* [https://skos-play.sparna.fr/skos-testing-tool/](https://skos-play.sparna.fr/skos-testing-tool/)
* the shapes downloaded from [https://github.com/skohub-io/shapes](https://github.com/skohub-io/shapes) and used [jena shacl](https://jena.apache.org/documentation/shacl/index.html) to validate

The validation against the skos testing tool find out errors concerning the content:
* ilc - Incomplete Language Coverage	Finds concepts lacking description in languages that are present for other concepts.	FAIL (2645): the concepts are described in the languages of their respective countries
* ipl - Inconsistent Preferred Labels	Finds resources with more then one prefLabel per language.	FAIL (1): The code [X0SD](2023-09-28-elf-code-list-v1.5.csv#L338-L339) is under investigation, currently resolved manually by changing the preferred label in alternative label
* ncl - No Common Languages	Checks for common languages in all concept literals.	FAIL: the concepts are described in the languages of their respective countries
* oc - Orphan Concepts	Finds all orphan concepts, i.e. those not having semantic relationships to other concepts.	WARNING (2645): relationships are not created in the CSV and the creation of such relations would need legal analysis
* ol - Overlapping Labels	Finds concepts with similar (identical) labels.	FAIL (234): it happens that certain countries uses same labels such as the codes 5WU6 (Netherlands) and 7SJP (Belgium) that use the same label "Europees economisch samenwerkingsverband", it doesn't necessarily mean that the concepts are the same.

The validation against the shacl shapes highlights only the problem of overlapping labels.

