# Candida_auris: Supplemental information on *Candida auris* reference genome patches, current state-of-the-art, and best-practice recommendations

If referencing this resource, please cite:\
(1) Alejandro R. Gener and Peera Hemarajata. "Status of public Candida auris whole genome assemblies." American Society 
of Microbiology Conference on Rapid Applied Microbial Next-Generation Sequencing and Bioinformatic Pipelines. Baltimore, 
Maryland. 16-19 October 2022.\
(2) Alejandro R. Gener. "Supplemental information on *Candida auris* reference genome patches, current state-of-the-art, 
and best-practice recommendations." 16 Occtober 2022. https://github.com/GenerGener/Candida_auris.

# Insights from mitochondrial mapping

TODO: explain that most reference genomes' assemblies were made without mitochondria. However, despite *C. auris* being haploid compared to other *Candida*, each are eukaryotic and as such should have mitochondria.

TODO: cite paper about B8441 MT..

| ![B11205 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/929480bfb93d163b4ab38c94c9cba3e6def0f1ae/B11205_clade1_SAMN05379594%200.51f.png) |
|-|
***B11205 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain B11205 is the recommended Clade I reference genome. Its biosample is [SAMN05379594](https://www.ncbi.nlm.nih.gov/biosample/SAMN05379594/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). PacBio (PB) CCS were much more common in these datasets than Oxford Nanopore (ONT). Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project (e.g., [Nucleotide:CP060339.1](https://www.ncbi.nlm.nih.gov/nuccore/CP060339.1)).

| ![B11220 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/ba3a672e335aabe750ff806937b329590cc6175f/B11220_clade2_SAMN05379608%200.51f.png) |
|-|
***B11220 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain B11220 is the recommended Clade II reference genome. Its biosample is [SAMN05379608](https://www.ncbi.nlm.nih.gov/biosample/SAMN05379608/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). PacBio (PB) CCS were much more common in these datasets than Oxford Nanopore (ONT). Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project.

Note a COX1 deletion in Clade II supported by read data, not an intron as is reported in the B8441 paper and the associated annotation track. 

TODO: How does the Clade II paper treat the COX1 locus?

| ![B11220 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/ac0b5346724a785e74550fa67c233b0cbcdedb99/BB120378_clade3_SAMN13294188%200.51f%20.png) |
|-|
***test***

| ![B120378 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/52f5753b66a8e807f4596799a743ae1cb3f09f70/BB12342_clade4_SAMN09111895%200.51f.png) |
|-|
***test***

| ![IFRC2087 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/238da38607e20125e13e4bd31af9ab29c9004ce6/IFRC2087_clade5_SAMN11570381%200.51f.png) |
|-|
***test***

# *Candida auris* exhibits high structural variability between clades

[Clade I vs. Clade II as in poster](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_003013715.2/GCA_016772135.1/21335/498019#)\
[Clade I vs. Clade III as in poster](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_016772135.1/GCA_016772215.1/21295/498019#)\
[Clade I vs. Clade IV as in poster](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_016772135.1/GCA_016772155.1/21315/498019#)\
[Clade I vs. Clade V as in poster](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_016772135.1/GCA_016809505.1/21345/498019#)\
[Clade II vs. Clade III](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_003013715.2/GCA_016772215.1/21255/498019#)\
[Clade II vs. Clade IV](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_003013715.2/GCA_016772155.1/21325/498019#)\
[Clade II vs. Clade V](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_003013715.2/GCA_016809505.1/21265/498019#)\
[Clade III vs. Clade IV](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_016772155.1/GCA_016772215.1/21305/498019#)\
[Clade III vs. Clade V](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_016772215.1/GCA_016809505.1/21275/498019#)\
[Clade IV vs. Clade V](https://ncbi.nlm.nih.gov/genome/cgv/browse/GCA_016772155.1/GCA_016809505.1/21285/498019#)

# Acknowledgements

Thanks to *C. auris* working group made up of CDC MDB, State and local PHLs, and the folks at Theiagen.

Special thanks to the development team (Sanjida Rangwala, Joel Virothaisakun, and Valerie Schneider) at NCBI working on 
the Comparative Genome Viewer (CGV) (https://ncbi.nlm.nih.gov/genome/cgv). CGV was developed as part of the NIH Comparative 
Genomics Resource (CGR), a National Library of Medicine project to establish an ecosystem to facilitate reliable comparative 
genomics analyses for all eukaryotic organisms.

# Funding 
This work was supported by Cooperative Agreement Number NU60OE000104-02 funded by the Centers for Disease Control 
and Prevention through the Association of Public Health Laboratories, and US CDC Epidemiology and Laboratory Capacity (ELC) 
for Infectious Diseases grant (6 NU50CK000498) to Los Angeles County. Its contents are solely the responsibility of the 
authors and do not necessarily represent the official views of the Centers for Disease Control and Prevention or the 
Association of Public Health Laboratories. 

# Conflicts of interest statement
ARG received poster bursaries from Oxford Nanopore Technologies (UK) in 2019. ARG is on the editorial board of *AIDS*
