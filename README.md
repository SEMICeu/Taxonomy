# Taxonomies

This repository aims to collect all the work done in SEMIC around taxonomies to be published:

* Taxonomy of public services (CPSV-AP)
* Business and Life events (CPSV-AP)
* Entity Legal Forms (Core Business)

## Taxonomy of public services (CPSV-AP)

### Context
While CPSV-AP is a data model thought to harmonise description of  public services in Europe, it happens that most of the catalogues and egovernment portals are following different taxonomies when classifying public services. 
This leads to additional work for harmonising multiple catalogues, for instance for mapping the different terms. While each catalogue of services contains specific services offered to citizens, business and other organisations, generic public services common to most of the catalogues exist but use different names and definitions. A commonly agreed taxonomy of generic public services would help public administrations to align their catalogue of services.

In addition, following the CSPV-AP data model, public services deal with events, such as busines and life events which follow other types of classification.

### Public Service taxonomy file
Follow the ReadMe directly included within the taxonomy file [here](https://github.com/catalogue-of-services-isa/Taxonomy/blob/master/Taxonomy%20proposal%20v0.10.xlsx).

## Business and Life events (CPSV-AP)

The spreadsheet containing classification of Businees and Life events can be found [here](https://github.com/SEMICeu/Taxonomy/blob/master/Business_Life-Events_controlled_vocabulary_v1.00.xlsx)

The file aims to align the currently recommended controlled vocabularies in [annexes IV and V of the previous CPSV-AP specification document](https://github.com/SEMICeu/CPSV-AP/blob/master/releases/2.2.1/SC2015DI07446_D02.02_CPSV-AP-2.2.1_v1.00.pdf) and [Annexes I and II of the SDGR](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32018R1724&from=EN#d1e32-31-1). 

### Life Events

The spreadsheet includes three key columns in which the mapping is made:

* Proposed controlled vocabulary: Life Events (in green). This is the result of the alignment exercise (e.g. the new proposed controlled vocabulary for Life Events).

* Annex IV: Description of 1st level life events (in grey). This is the controlled vocabulary currently recommended for Life Event in the CPSV-AP 2.2.1 specification document. 

* Annex II: SDGR (in blue). This is Annex II in the SDGR, containing the life events and procedures.

The document also includes a column where feedback can be given by Member States (column A).


The main logic that is followed to create the new (in green) controlled vocabulary is as follows:

 * No information from the “current” controlled vocabulary in Annex IV should be lost
 * All information from the SDGR Annex II should be included in the new controlled vocabulary
 * Main focus at this stage is on level 1 Life Events (column C). Level 2 Life Events are significantly more complex, since Member States have many different categories and degrees of detail on their portals. Furthermore, the wording and approach in the two source lists are different. The SDGR provides narrowly defined procedures, whereas Annex IV groups life events on a higher level. More feedback is needed to determine the way these two sources can be consolidated. 
 * Related to the point above, wording of the Annex IV descriptions was changed. Specifically, “this life event groups..” was deleted in most cases to better align with the SDGR life events. The content changes made from the previous version are indicated in red. 

### Business Events

The spreadsheet for Business Events follows the same structure as for Life Events, organised in the three columns where the mapping is made. 

Furthermore, the logic also remains the same. However, the mapping here is less complex. All business events from Annex II are added under the newly proposed first level Business Event: “Running a business”. 

## Entity Legal Forms (Core Business)

Within Core Business, there is a need to classify Legal Entities. GLEIF provides a list of legal entities that have been converted into RDF and linked with other Publications Office lists (countries and status). The documentation relative to this work can be found [here](/Entity_Legal_Form/README.md).
