![LOGO](Logo_Metexplore.png)
# PathwayEnrichement

Version:1.0

## Short description
Predicts pathway enrichment in human metabolic bionetwork (Recon 2v3) from a dataset of pre-selected metabolites

## Description
Metabolites extracted from the input file are mapped on a Recon network ([1]) by providing either INCHI or CHEBI informations. Pathway enrichment is calculated with an exact Fisher one-tailed test and a correction test.
Two files are provided in output: 
- a first one containing for each metabolites from the input file: the sucess or the failure of the mapping, their names, those of one or several elements of the network in mapping case.
- a second one containing for each pathway containing the mapped metabolites: their names, the Fisher's P value, the Bonferoni (or other test correction) value, the list of mapped metabolites, the number of mapped metabolites and the coverage of mapped metabolites on the total of metabolites contained by the studied pathway.

## Key features
- Metabolic network
- Modeling
- Pathway analysis
- Prediction

## Functionality
- Post-processing
- Statistical Analysis

## Tool Authors
- MetExplore Group contact-metexplore@inra.fr

## Container Contributors
- Etienne Camenen (INRA Toulouse)

## Git Repository
- https://github.com/phnmnl/container-pathwayEnrichment.git

## Installation
For local installation of the container:
```
docker pull docker-registry.phenomenal-h2020.eu/phnmnl/pathwayEnrichment
```

## Usage Instructions
For direct usage of the docker image:
```
docker run docker-registry.phenomenal-h2020.eu/phnmnl/metaboliteidconverter -i  <input file> [-o1 <output file 1>] [-o2 <output file 2>] [-s <sbml file>] [-chebi <CHEBI column>] [-inchi <InChI column>]  [-f <filtered column>] [-l <layer selection>] [-c <test correction>] [-h]
```

- ```-i```, ```-o1```, ```-o2``` and ```-s``` could be used to customize file's name respectively for the input file, the output file resulting from mapping (default: "mapping.tsv", the one resulting from pathway enrichment (default: "pathwayEnrichment.tsv") and the sbml file where the bionetwork is extracted (by default: those corresponding to Recon 2v3). Only ```-i``` is required. 
- ```-chebi```, ```-inchi``` and ```-f```options set column number where CHEBI, InChI and discriminant informations are among the input file. By default, they are setted respectivly to 2, 5 and 0 ("1" is considered as the first column). 0 or negative values are used to disable an option if the corresponding information is missing. ```-chebi``` and ```-inchi``` options could not be both disabeled.
with ```-f``` option, lines containing empty values among the selected column are discarded from the anlysis (for exemple : after a statistical pre-selection)
- ```-l``` selects the InChI's layers used for mapping among : connections, hydrogenes atoms, charge, protons, double-bond stereo, tetrahedral sp3 stereo, isotopic atoms, fixed hydrogenes and reconnected layers. These layers must be setted as a list of character containing the number separated by comma. By default this option is setted on ```c,h``` for a mapping only on connections and hydrogenes atoms layers. A whole layers selected must be ```c,h,q,p,b,t,i,f,r```. For mapping on formula only, select ```-l``` option with no parameters after.
- ```-c``` select a test correction. Bonferoni is setted by default. 2 could be choosed for Benjamini-Hochberg correction and 3 for Holm-Bonferroni one.
- ```-h``` option prints a help.

## References
- Thiele I, Swainston N, Fleming RMT, et al. A community-driven global reconstruction of human metabolism. Nature biotechnology. 2013;31(5):10.1038/nbt.2488. doi:10.1038/nbt.2488. 
