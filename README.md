# Sustainable genetics project

This repo contains the data and code for a project evaluating the reuseability of 96 well microplates for microsatellite genotyping using DNA from Antarctic fur seals (Arctocephalus gazella).

## Overview

### SGP folder

-   **0_Raw_data_processing.qmd**: contains the script for processing the raw data files 

-   **1_SGP.qmd**: contains the script for processing and analysing the data, and producing the tables and figures

    -   The code chunks **setup** and **packages** sets up the file.paths and packages used in the script

    -   Each code chunk is marked with a *#\| label* related to the action or outcome of that specific chunk

    -   The entire code is written with **R**

-   **2_SGP_extra**: contains the script for further exploration of the data and additional figures 

-   **3_SGP_Gapfilling**: contains the script to locate missing data for manual inspection and a function to detect loci > 20% missing data. 

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

A dataframe created by the script and later used for the bayesian model **model.mismatch**

-   Columns: Loci, Mix, Rack, Treatment, Well, ID, Row, Match, Missing and Nanodrop

    -   Loci: One of 39 loci for which the genotype of the samples were evaluated

    -   Mix: One of 5 mixes the loci were sorted in

    -   Rack: One of three racks (R154, R155, R156) the samples were on

    -   Treatment: One of three treatments (Internal control, Reused detection plate, Reused PCR plate)

    -   Well: One of 96 wells (excluding E3, total = 95) the sample was in during fragment analysis

    -   ID: individual identification tag of the animal the DNA sample stems from

    -   Row: One of eight rows the sample was in

    -   Mismatch: Binomial (0,1)

        -   0 = A match was observed for both alleles in the locus

        -   1 = A mismatch was observed for either allele in the locus

    -   Missing: Binomial (0,1)

        -   0 = An unscored allele was observed for the locus

        -   1 = Both alleles were scored for the locus

    -   Nanodrop: the DNA concentration in ng/µl
**Mismatches**
A dataframe created by the script and later used to calcualte per treatment single-locus genotype error rates. 

-   Columns: Rack.1, Rack.2, Treatment, No..of.mistyped.alleles, No..of.mistyped.reactions, No..of.reactions, Allelic.error.rate, Genotype.error.rate

    -   Rack.1: One of three racks (R154, R155, R156) from the standard protocol

    -   Rack.2: One of three racks (R154, R155, R156) from one of the other treatments (e.g. R154_R2, R154_R3, R154_R4)

    -   Treatment: One of three treatments (Internal control, Reused detection plate, Reused PCR plate)
    
    -   No..of.mistyped.alleles: Number of mismatched alleles within one treatment group, within a DNA plate

    -   No..of.mistyped.reactions: Number of mismatched single-locus genotypes within one treatment group, within a DNA plate

    -   No..of.reactions: Number of single-locus genotypes within one treatment group, within a DNA plate
    
    -   Allelic.error.rate: Error rate per allele

    -   Genotype.error.rate: Error rate per single-locus genotypes
    
### Terminology and annotations used in the script:

-   Standard procedure (SP): The first treatment and standard protocol for microsatellite genotyping

-   Internal control (IC): The second treatment, which is identical to SP

-   Reused detection plate (RD): The third treatment, for which the detection plate had been cleaned and this is the second use of that particular plate

-   Reused PCR plate (RP): The fourth treatment, for which the PCR plate has been cleaned and this is the second use of that particular plate

*Note*: The plates were circled so that R154 would go on a plate, that previously held R156 samples, R155 on a cleaned R154 plate and R156 on a cleaned R155 plate.

-   Mismatch: The genotype value at a given locus does not match with the standard procedure value

-   Missing: The genotype value at a given locus is NA

-   Contamination: The genotype value for a mismatch matches with the standard procedure for the original use of the same plate
