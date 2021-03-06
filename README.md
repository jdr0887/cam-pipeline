# AOP-CAM Knowledge Provider database pipeline

This repository contains a makefile and resources for constructing the RDF triplestore used in the AOP-CAM Knowledge Provider prototype for NCATS Data Translator. Source code for the web service API used to query this data can be found at [TranslatorIIPrototypes/cam-api](https://github.com/TranslatorIIPrototypes/cam-api). The web service API can be tested from within [its Swagger API documentation](http://robokop.renci.org:6434/docs#/). The current version of this database can queried with SPARQL using the endpoint `https://stars-app.renci.org/cam/sparql`.

Development of the prototype is led by Jim Balhoff (RENCI, UNC-Chapel Hill) and Stephen Edwards (RTI International), funded by the [National Center for Advancing Translational Sciences](https://ncats.nih.gov).

## Data sources

### Ontologies

This resources integrates a broad set of ontologies developed as part of the OBO Library. The complete list can be see in the OWL imports declarations within https://github.com/TranslatorIIPrototypes/cam-pipeline/blob/master/ontologies.ofn.

### Data

The data sets integrated into the database consist of independent OWL instance models making use of the terms and relations defined within the combined ontology (as described in ['Gene Ontology Causal Activity Modeling (GO-CAM) moves beyond GO annotations to structured descriptions of biological functions and systems'](https://doi.org/10.1038/s41588-019-0500-1)). Currently three main types of data are included:

- Causal Activity Models annotated by Gene Ontology biocurators (see http://geneontology.org/go-cam)
- Causal Activity Models automatically translated from Reactome pathways (see [geneontology/pathways2GO](https://github.com/geneontology/pathways2GO))
- Causal Activity Models automatically translated from Comparative Toxicogenomics Database chemical–gene interactions (see [balhoff/ctd-to-owl](https://github.com/balhoff/ctd-to-owl))

## Building the database

### Prerequisites

- A Unix-like environment with the GNU Make workflow tool
- Java 8 or higher
- These tools on your PATH:
  - [blazegraph-runner](https://github.com/balhoff/blazegraph-runner)
  - [ctd-to-owl](https://github.com/balhoff/ctd-to-owl)
  - [ncit-utils](https://github.com/NCI-Thesaurus/ncit-utils)
  - [Apache Jena arq](https://jena.apache.org)
- Clone the [Gene Ontology Noctua models repo](https://github.com/geneontology/noctua-models) in `../noctua-models`
- Clone the [Gene Ontology Noctua models repo](https://github.com/geneontology/noctua-models) in `../noctua-models-dev` and `git checkout dev` in that directory (this is to obtain the converted Reactome pathways, which are not yet officially released)

### Running

- First ensure enough memory is available for all the commands:
  ```bash
     export JVM_ARGS=-Xmx256G
     export ROBOT_JAVA_ARGS=-Xmx256G
     export JAVA_OPTS=-Xmx256G
  ```
- Run `make cam-db-reasoned.jnl`
- Wait a few days...
