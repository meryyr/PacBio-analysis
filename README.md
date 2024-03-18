# PacBio Analyses for fusion transcripts detection in RNAseq data

Two different analyses were developed to detected fusion transcripts in long read PacBio data (Iso-Seq data). 

1. The first one aimed to find MATCHES of previously identified short reads fusion transcripts (592 filtered fusions transcripts detected by FusionCatcher tool) in long reads. The __long_read_seq_analysis.R__ R code was employed for this purpose.

2. The second anaylsis aimed to find fusion transcripts in long read data employing the __pbfusion__ tool (https://github.com/PacificBiosciences/pbfusion/tree/master?tab=readme-ov-file).

# Selected datasets to perform the two analyses

1. First PacBio dataset: https://downloads.pacbcloud.com/public/dataset/Kinnex-full-length-RNA/. Three cerebellum samples were used for 'toy' analysis. Therefore these samples were used to perform the two analyses previously explained in order to develop and test the codes for the real anaylsis. In particular the first anaylsis was performed on a 'toy' set, which is a small set of fusion transcripts detected by FusionCatcher (32, the one selected for the PCRs).

2. Second dataset [Bioproject 975746] (https://www.ncbi.nlm.nih.gov/bioproject/975746). RNA was extracted from 4 individuals in the temporal cortex, hypothalamus, and cerebellum. The 12 samples were used to perform the real anaylses.


# FIRST ANALYSIS: find matches of short read fusions in long reads

The R code found in the repository (long_read_seq_analysis.R) was implemented to look for MATCHES (with a maximum mismatch of 2) of each short read fusion transcript in long reads RNA seq data, employing the "Biostrings" library in R. For each match found, a new FASTA file is created, so that all the matches (long-reads) found for each fusion transcripts are stored in a single FASTA file.

# SECOND ANALYSIS: pbfusion analysis

The PacBio tool pbfusion was used to look for fusion transcripts in long reads Iso-Seq (PacBio) data. Differently from the analysis performed before, which looks for matches of short read fusions in long read data, this tool allows the discovery of novel fusion transcripts (https://github.com/PacificBiosciences/pbfusion/tree/master?tab=readme-ov-file). 
The __pipeline_pbfusion__ script was used to find fusion transcripts in the samples (the general pipeline used can be found in the GitHub repository of pbfusion); in particular a BED file is generated with all the information about the detected fusion. 

Since we want to visualize the fusions in genome browser, the BED file is cleaned and adapted to the interact track format of Genome Browser (https://genome.ucsc.edu/goldenPath/help/interact.html). This track format is used to displays pairwise interactions, therefore the BED file was cleaned from interactions between more than 3 genes (fusions which resulted from the joining of exons of 3 or more genes). The __bed_gb_interact.R__ script was used for this purpose
