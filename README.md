# Sustainable genetics project

This repo contains the data and code for a project evaluating the reuseability of 96 well microplates for microsatellite genotyping using DNA from Antarctic fur seals (Arctocephalus gazella).

## Overview

### SGP folder

-   **SGP.qmd**: contains the script for processing and analysing the data, and producing the tables and figures

    -   The code chunks **setup** and **packages** sets up the file.paths and packages used in the script

    -   Each code chunk is marked with a *#\| label* related to the action or outcome of that specific chunk

    -   The entire code is written with **R**

-   **Data/Raw**: contains the raw data (*Genemarker* allele reports) from Rack 154-156 for all treatments (**Do not change**)

-   **Data/Working_data**: contains the .csv files of the allele reports from Rack 154-156 for all treatments in the format fitting the code

    -   **Data/Working_data/Processed_data**: contains the processed data output from the *label: rawdata* code chunk and the Nanodrop_SGP.csv file with DNA quality values

-   **Results/Tables**: contains the tables produced by the script

-   **Results/Figures**: contains the figures produced by the script

### Data

**R154_R1.csv**

An example of the processed data used for the script. All other files of the same name format contain the same elements!

-   Columns: Rack_location, ID, all loci

    -   Rack_location: the location on the microwell plate the individual had in the wet lab

    -   ID: individual identification tag of the animal the DNA sample stems from

    -   \_a and \_b denotes the first and second allele of all loci

**Nanodrop_SGP.csv**

-   Columns: ID and Nanodrop.

    -   ID: individual identification tag of the animal the DNA sample stems from

    -   Nanodrop: the DNA concentration in ng/µl

**Analysis.data**

The dataframe created by the script and later used for the bayesian models **model.match** and **model.missing**

-   Columns: Loci, Mix, Rack, Treatment, Well, ID, Row, Match, Missing and Nanodrop

    -   Loci: One of 39 loci for which the genotype of the samples were evaluated

    -   Mix: One of 5 mixes the loci were sorted in

    -   Rack: One of three racks (R154, R155, R156) the samples were on

    -   Treatment: One of four treatments (Standard procedure, Internal control, Reused detection plate, Reused PCR plate)

    -   Well: One of 96 wells (excluding E3, total = 95) the sample was in during fragment analysis

    -   ID: individual identification tag of the animal the DNA sample stems from

    -   Row: One of eight rows the sample was in

    -   Match: Binomial (0,1)

        -   0 = A mismatch was observed for either allele in the locus

        -   1 = A match was observed for both alleles in the locus

    -   Missing: Binomial (0,1)

        -   0 = An unscored allele was observed for the locus

        -   1 = Both alleles were scored for the locus

    -   Nanodrop: the DNA concentration in ng/µl

### Terminology and annotations used in the script:

-   Standard procedure (SP): The first treatment and standard protocol for microsatellite genotyping

-   Internal control (IC): The second treatment, which is identical to SP

-   Reused detection plate (RD): The third treatment, for which the detection plate had been cleaned and this is the second use of that particular plate

-   Reused PCR plate (RP): The fourth treatment, for which the PCR plate has been cleaned and this is the second use of that particular plate

*Note*: The plates were circled so that R154 would go on a plate, that previously held R156 samples, R155 on a cleaned R154 plate and R156 on a cleaned R155 plate.

-   Mismatch: The genotype value at a given allele or locus does not match with the standard procedure value

-   Missing: The genotype value at a given allele or locus is NA

-   Contamination: The genotype value for a mismatch matches with the standard procedure for the original use of the same plate
