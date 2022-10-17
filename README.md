# Thanks for stopping by our poster and repo!

# Candida_auris: Supplemental information on *Candida auris* reference genome patches, current state-of-the-art, and best-practice recommendations

If referencing this resource, please cite:\
(1) Alejandro R. Gener and Peera Hemarajata. "Status of public Candida auris whole genome assemblies." American Society 
of Microbiology Conference on Rapid Applied Microbial Next-Generation Sequencing and Bioinformatic Pipelines. Baltimore, 
Maryland. 16-19 October 2022.\
(2) Alejandro R. Gener. "Supplemental information on *Candida auris* reference genome patches, current state-of-the-art, 
and best-practice recommendations." 16 Occtober 2022. https://github.com/GenerGener/Candida_auris.

# Background
Candida auris is an opportunistic fungal pathogen discovered in 2009 (Satoh  et al. 2009). Infection can range from assymptomatic to invasive candidemia. It is often highly drug-resistant. Five clades (I-V) are currently recognized. One species-level single linear reference was used:
- Initially from strain B8441.
- When CDC Mycotics Disease Branch (MDB) started developing a variant calling workflow called MycoSNP, another Clade I B11221 reference was chosen.
- Clade I was chosen at the time because it was thought to be the predomenant form in US.
- Current reference is strain B11205 (Clade I)

However, state PHLs noticed non-Clade I case clusters. A high-quality clade reference set was needed for surveillance. Quality control standards were lacking for reference and production genomes.

# State-of-the-art *Candida auris* NCBI genome assembly stats

![Figure 1](https://github.com/GenerGener/Candida_auris/blob/main/ASM%20NGS%20Figure%201.png) |
|-|
**Figure 1: Candida auris genome assembly stats.** 
Coloring of categories same for A-D: contig =  blue; "complete" genome = yellow; chromosome = gray; scaffold = orange. 
A: Most genomes available in GenBank were Scaffold or Complete Genomes. 
B: Assembly lengths approximated 12.5 Mb, likely because of reference-guided methods. 
C: Illumina-only assemblies were over-represented in the Contig assemblies. 
D: Complete assemblies were often PacBio + Illumina. Sample metadata in NCBI varied.

# Insights from mitochondrial mapping

## Method for *Candida auris* mitochondrial assemblies.

Most reference genomes' assemblies were made without mitochondria. However, despite *C. auris* being haploid compared to other *Candida*, each are eukaryotic. As such, they should have mitochondria. The first paper to comment on the mitochondria of an early reference sequence was Misas et al. 2020. This was used as illustrated in Figure 2 for reference-guided assembly finished with manual curration.

| ![Figure 2](https://github.com/GenerGener/Candida_auris/blob/0105e68d5d53fa9429399d72c9891c8077605d8e/ASM%20NGS%20Figure%202.png) |
|-|
**Figure 2: C. auris mitogenome assembly**
1: "Complete" genome assemblies with reads were evaluated. None with reads had mitogenome chromosomes.  
2:  Reads were mapped onto B8441 mitogenome (GenBank:MT849287.1). Minimap2 was implemented with default settings for either PacBio (PB), Illumina (ILM), or Oxford Nanopore (ONT).
3: Sample alignments were evaluated for quality, and samples with discordant variants were set aside.
4: Assemblies were made by consensusing guided by reference. 
5: INDELs were curated manually.
6: Final asseemblies were annotated in SnapGene based on MT849287.1 (Misas et al. 2020).
7: Reference set will be made available in public databases.

An alternative approach might be to convert reads mapping to MT849287.1 to fastq and feed these into a de novo assembly approach. This orthogonal analytical method should yield similar results.

Assemblies will be made available here as .dna files. Assemblies as .dna may be viewed for free with [SnapGene](https://www.snapgene.com). Notable changes to annotations include correcting COX1 and COB introns for the Clade I reference and for other mitochondrial assemblies. These are not introns. They are likely artifacts from interpretting sequencing errors. They are likely deletions in Clade II and V strains. The extent of these deletions has yet to be evaluated, possibly in part to lack of including mitochondrial assemblies in "complete" genomes.

To annotate assemblies, the B8441 mitochondrial assembly GenBank:MT849287.1 was downloaded as a genbank file and openned with SnapGene (version 6.1.2 HEAD-26640). A new .dna file was created for the consensus called from mapping Illumina reads from SRA to GenBank:MT849287.1 with minimap2 (v2.24-r1122) and calling consensus with a simple script using samtools (v1.12) and bcftools (v1.14-58-g310cd8c). The above is simple and open-source, but does not take into account structural variation (e.g., INDELS). So, these assemblies were corrected manually by comparing their alignments with IGV. See Supplemental figure for example.

| ![Feature annotation of Clade I reference genome mitochondria.](https://github.com/GenerGener/Candida_auris/blob/main/Candida_auris_Clade_1_mitochondria_draft_v3%20Map.png) |
|-|
**Supplemental figure: Feature annotation of Clade I reference genome mitochondria.** 
Crimson line above black double line represents MT849287.1 mapped to output consensus in addition to manual curration (annotated as miscalleneous features). Red introns are annotation errors that this work corrects. Fuchsia arrows are intronless features. "Introns in COX1 and COB may be deletions in Clade II (COX1) and Clade V (COX1 and COB).

## Results

**Figure 3: Coverage plots of runs passing QC.**
(Expanded) Each clade's mitochondria is distinct relative to MT849287.1. Divergent allele frequencies > 0.51f highlighted in coverage tracks. Clade II and V samples have deletions in COX1, and Clade V has an additional deletion in COB. These are incorrectly annotated as introns in the B8441 assembly. This may have been due to consensusing which ignored INDELs and low-depth areas may have been called as "N" instead of as gaps "-". Visualized in IGV.

| ![B11205 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/929480bfb93d163b4ab38c94c9cba3e6def0f1ae/B11205_clade1_SAMN05379594%200.51f.png) |
|-|
***B11205 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain B11205 is the recommended Clade I reference genome. Its biosample is [SAMN05379594](https://www.ncbi.nlm.nih.gov/biosample/SAMN05379594/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). PacBio (PB) CCS were much more common in these datasets than Oxford Nanopore (ONT). Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project (e.g., [Nucleotide:CP060339.1](https://www.ncbi.nlm.nih.gov/nuccore/CP060339.1)).

| ![B11220 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/ba3a672e335aabe750ff806937b329590cc6175f/B11220_clade2_SAMN05379608%200.51f.png) |
|-|
***B11220 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain B11220 is the recommended Clade II reference genome. Its biosample is [SAMN05379608](https://www.ncbi.nlm.nih.gov/biosample/SAMN05379608/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). These experiments generated Oxford Nanopore (ONT) long reads. Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project (e.g., [Nucleotide:CP043531.1](https://www.ncbi.nlm.nih.gov/nuccore/CP060339.1)).

Note a COX1 deletion in Clade II supported by read data, not an intron as is reported in the B8441 paper and the associated annotation track.
TODO: How does the Clade II paper treat the COX1 locus?

| ![B120378 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/ac0b5346724a785e74550fa67c233b0cbcdedb99/BB120378_clade3_SAMN13294188%200.51f%20.png) |
|-|
***B120378 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain B120378 is the recommended Clade III reference genome. Its biosample is [SAMN13294188](https://www.ncbi.nlm.nih.gov/biosample/SAMN13294188/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). These experiments generated Oxford Nanopore (ONT) long reads. Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project (e.g., [Nucleotide:CP060339.1](https://www.ncbi.nlm.nih.gov/nuccore/CP060339.1)).

| ![B12342 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/52f5753b66a8e807f4596799a743ae1cb3f09f70/BB12342_clade4_SAMN09111895%200.51f.png) |
|-|
***B12342 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain B12342 is the recommended Clade IV reference genome. Its biosample is [SAMN09111895](https://www.ncbi.nlm.nih.gov/biosample/SAMN09111895/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). These experiments generated Oxford Nanopore (ONT) long reads. Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project (e.g., [Nucleotide:CP060346.1](https://www.ncbi.nlm.nih.gov/nuccore/CP060346.1)).

| ![IFRC2087 mitochondrial reads](https://github.com/GenerGener/Candida_auris/blob/238da38607e20125e13e4bd31af9ab29c9004ce6/IFRC2087_clade5_SAMN11570381%200.51f.png) |
|-|
***IFRC2087 mitochondrial reads mapped to GenBank:MT849287.1***
*C. auris* strain IFRC2087 is the recommended Clade V reference genome. Its biosample is [SAMN11570381](https://www.ncbi.nlm.nih.gov/biosample/SAMN11570381/). Coverage plot emphasis set to allele frequency of 0.51f. This facilitates comparison between noisier long-read methods and more accurate short-read methods (Illumina, ILM). These experiments generated Oxford Nanopore (ONT) long reads. Note that the assemblies were originally made with PB and polished with ILM. The metadata in NCBI just mentions PB. These contigs were noted as "unpublished" as of 14 October 2022 in the genbank records for this project (e.g., [Nucleotide:CP050673.1](https://www.ncbi.nlm.nih.gov/nuccore/CP050673.1)).

TODO: read feature

# *Candida auris* exhibits high structural variability between clades

| ![Figure 4](https://github.com/GenerGener/Candida_auris/blob/529d85a4dee8e8b36495332dd996443a55536cad/ASM%20NGS%20Figure%204.png) |
|-|
**Figure 4: Diffential synteny between Candida auris Clade I and other clade-specific reference genomes.** 
(Poster Top: Clade I vs. Bottom: Clade II, III, IV, and V.) Use of  a single reference may have unintended consequences for structurally variable species. Chromosome numbering by size or sequence length (e.g., Chromosome 1 = longest ) was not informative because chromosomes could have distinct gene content. Viewed with Comparative Genome Viewer (CGV).

CGV sessions:\
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

# Recommendations

## Clade-specific reference genomes

|![Table 1](https://github.com/GenerGener/Candida_auris/blob/main/ASM%20NGS%20Table%201.png) |
|-|
**Table 1: Five Recommended C. auris Clade-Specific Reference Genome Assemblies.**
*Selected by CDC. **Selected by ARG during this study. ***Reads from respective BioProjects were mapped to B8441 mitochondrial reference genome assembly (GenBank:MT849287.1) for consensusing.

## Recommendations

Conclusions: Sequencing methods have improved since *C. auris* was discovered. With the advent of HiFi PB and improved ONT, reference-level assemblies need not rely on short-reads for polishing. Assemblies must have reads for quality assurance. Assemblies without reads have limited utility to the global community. Production-level genomes such as reference-guided consensuses are not interchangeable with de novo and ideally long-read methods. Annotations remain a challenge for both reference and production genomes. Mitogenomes were previously neglected, and the scope of their diversity is unknown. They are small enough to visually inspect, and can in theory be used to support clade assignment (Sekizuka et al. 2019). Future work could determine the extent of inter- and intraclade mitochondrial variability. Reference-guided approaches should use references with mitochondrial chromosomes. The present work developed patches to the 5 recommended clade-specific reference genomes, and helped standardize the clade reference set. 

# References 

Satoh, Kazuo, Koichi Makimura, Yayoi Hasumi, Yayoi Nishiyama, Katsuhisa Uchida, and Hideyo Yamaguchi. 2009. “Candida Auris Sp. Nov., a Novel Ascomycetous Yeast Isolated from the External Ear Canal of an Inpatient in a Japanese Hospital.” Microbiology and Immunology 53(1):41–44.
* Important because first identification of *C. auris.* 
Misas, Elizabeth, Nancy A. Chow, Oscar M. Gómez, José F. Muñoz, Juan G. McEwen, Anastasia P. Litvintseva, and Oliver K. Clay. 2020. “Mitochondrial Genome Sequences of the Emerging Fungal Pathogen Candida Auris.” Frontiers in Microbiology 11(October):1–12.
* Important because established annotation for B8441 mitochondria. However, annotations had errors (e.g., introns).

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

# Conflict(s) of interest
ARG received poster bursaries from Oxford Nanopore Technologies (UK) in 2019. ARG is on the editorial board of *AIDS*. No other conflicts.

# Feedback
This is currently a work in progress. Feedback welcomed! Please submit feedback as an Issue.
