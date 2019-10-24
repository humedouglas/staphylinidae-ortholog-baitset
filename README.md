# *Staphylinidae* Ortholog Target Enrichment Baits

The bait-stringent-RM25pc-all.fas bait set contains 39938 100nt baits designed from 10 diverse *Staphylinidae* species targetting 1229 orthologs.  

### Acknowledgements ###
This bait set was made possible by the significant data contributions of Janina L. Kypke, Statens Naturhistoriske Museum, Denmark. 
Dr. Adam Brunke, Agriculture & Agri-Food Canada was instrumental in guiding the design of the bait set. 
Dr. Jeremy Dettman, Julie Chapados, Robyn Wright, Wayne McCormick (AAFC) for validation and implementation

### Files ###
* bait-stringent-RM25pc-all.fas: Final bait set with OrthoDB v9 headers
* bait-stringent-RM25pc-all.fasta: Final bait set with Phyluce compatible UCE headers
* input.seq.fas: Final file generated by staphylinidae_baits.py submitted to Arbor. 
* priorities.txt: File used to curate orthogroups into diverse species 

### Design Methodology
Input Files: 3814 amino acid (Protein) and nucleotide (DNA) orthologs generated using 28 *Coleoptera* transcriptomes with OrthoDB v9 and Orthograph. Provided species are outlined in priorities.txt
1) Amino acid orthologs were aligned using T_Coffee 11.0.8 with default settings, additionally outputting score_ascii files
2) Nucleotide alignments were generated using Tranalign from EMBOSS 6.6.0
3) staphylinidae_baits.py performed the following steps:
    * Scanned each score_ascii file with sliding window starting with a length of 2000 AA to a minimum of 75 AA. 
    Each alignment position has a TSC score from 1-9 so a max score of 300 AA is 2700. The largest window with a sum above 95% of the max TCS score was considered a conserved block.
    * Corresponding conserved blocks were excised from the nucleotide alignments by multiplying the start and stop indices of protein alignments by 3. 
    * Any sequences with at least 20% gapped bases were removed from conserved blocks
    * Due to budget constraints, the 28 Staphylinidae species were curated down to 10 priority *Staphylinidae* species outlined in priorities.txt, representing a diverse sampling of the family. Examined nucleotide conserved blocks for the presence of the following priority *Staphylinidae* species:
        * *Acidota crenata*
        * *Deinopsis erosa*
        * *Deleaster dichrous*
        * *Lordithon lunulatus*
        * *Nicrophorus vespilloides*
        * *Paederus cruenticollis*
        * *Philonthus decorus*
        * *Quedius fuliginosus*
        * *Silphotelus sp*
        * *Stenus bimaculatus*
    * 1229 conserved blocks were found containing 5-10 priority *Staphylinidae* with a minimum size of 300bp
    * Curated blocks were created by removing all non priority *Staphylinidae* from conserved blocks
    * Curated blocks were appended into a multi-fasta and submitted to Arbor Biosciences for MyBaits manufacturing

### Arbor BioSciences Bait Design
The following procedures were performed by Brian Brunelle of Arbor Biosciences
1) 7,985 loci provided for bait design (Ns were replaced with Ts if they occurred consecutively for
1-10 bases)
2) Using RepeatMasker, soft-masked the input sequences for simple repeats and repeats found in
the Staphylinidae database; 0.12% masked (all simple repeats)
3) Optimal 100 nt bait from every 120 nt interval based on GC, ΔG, etc = 40,127 raw baits
4) Each bait candidate was BLASTed against the 8 provided genomes;
    * ref01 = GCF_001937115.1_Atum_1.0_genomic.fas
    * ref02 = GCF_000699045.2_Apla_2.0_genomic.fas
    * ref03 = GCF_000648695.1_Otau_2.0_genomic.fas
    * ref04 = GCF_000500325.1_Ldec_2.0_genomic.fas
    * ref05 = GCF_000390285.2_Agla_2.0_genomic.fas
    * ref06 = GCF_000355655.1_DendPond_male_1.0_genomic.fas
    * ref07 = GCF_000002335.3_Tcas5.2_genomic.fas
    * ref08 = GCF_001412225.1_Nicve_v1.0_genomic.fas 
     
    A hybridization melting temperature (Tm, defined as temperature at which 50% of molecules are hybridized) was estimated for each hit assuming standard myBaits® buffers and conditions.

5) For each bait candidate, one BLAST hit with the highest Tm is first discarded from the results
(allowing for 1 hit in the genome), and only the top 500 hits (by bit score) are considered. Based
on the distribution of remaining calculated Tm's, we filtered out non-specific baits using the
following criteria:
    * Stringent (only specific baits pass). Bait candidates pass if they satisfy one of these conditions:
        - No hits with Tm above 60°C
        - At most 2 hits 62.5 – 65°C
        - At most 10 hits 62.5 – 65°C and at least 1 failing flanking bait
        - At most 10 hits 62.5 – 65°C, 2 hits 65 – 67.5°C, and fewer than 2 passing flanking baits
        - At most 2 hits 62.5 – 65°C, 1 hit 65 – 67.5°C, 1 hit 70°C or above, and < 2 passing flanking baits
    * Moderate (some non-specific baits pass)
        - Additional candidates pass if they have at most 10 hits 62.5 – 65°C and 2 hits above 65°C, and fewer than 2 passing baits on each flank.
    * Relaxed (more non-specific baits pass)
        - Additional candidates pass if they have at most 10 hits 62.5 – 65°C and 4 hits above 65°C, and fewer than 2
passing baits on each flank.

6) Optimal bait design, keep only baits that passed “Moderate” BLAST filtering for all 8 genomes and were ≤25% Repeat
Masked

7) Final bait set, bait-stringent-RM25pc-all.fas: 100 nt baits after recommended filtration = 39938 baits

### Phyluce Prediction of Bait Effectiveness
In order to provide a rough idea on effectiveness, the bait set was compared against 18 *Coleoptera* assemblies available on NCBI as of November 2018.
Bait set fasta headers were converted to Phyluce "UCE" format and processed via Phyluce, outlined in [Tutorial IV: Identifying UCE Loci and Designing Baits To Target Them: In-silico test of the bait design](https://phyluce.readthedocs.io/en/latest/tutorial-four.html#in-silico-test-of-the-bait-design)

Table 1. Target Hits Among NCBI Coleoptera Assemblies

| GenBank Accession     | Species                   | Post Filtered "UCEs" |
|-----------------------|---------------------------|----------------------|
| gca_000002335_3.fasta | Tribolium castaneum       | 873                  |
| gca_000281835_1.fasta | Priacma serrata           | 530                  |
| gca_000346045_2.fasta | Dendroctonus ponderosae   | 727                  |
| gca_000355655_1.fasta | Dendroctonus ponderosae   | 775                  |
| gca_000390285_2.fasta | Anoplophora glabripennis  | 775                  |
| gca_000500325_2.fasta | Leptinotarsa decemlineata | 621                  |
| gca_000648695_2.fasta | Onthophagus taurus        | 841                  |
| gca_000699045_2.fasta | Agrilus planipennis       | 748                  |
| gca_001012855_1.fasta | Hypothenemus hampei       | 854                  |
| gca_001412225_1.fasta | Nicrophorus vespilloides  | 992                  |
| gca_001443705_1.fasta | Oryctes borbonicus        | 718                  |
| gca_001937115_1.fasta | Aethina tumida            | 730                  |
| gca_002278615_1.fasta | Pogonus chalceus          | 691                  |
| gca_002938485_1.fasta | Sitophilus oryzae         | 688                  |
| gca_003013835_1.fasta | Diabrotica virgifera      | 420                  |
| gca_003054995_1.fasta | Aleochara bilineata       | 896                  |
| gca_003402655_1.fasta | Harmonia axyridis         | 756                  |
| gca_003568925_1.fasta | Coccinella septempunctata | 769                  |

### Built With

* [Python](https://www.python.org/doc/) - Programming language
* [Conda](https://conda.io/docs/index.html) - Package, dependency and environment management
* [Phyluce](https://phyluce.readthedocs.io/en/latest/index.html) - Target enrichment data analysis
* [BioPython](https://biopython.org/) - Tools for biological computation
* [T_Coffee](http://www.tcoffee.org/Projects/tcoffee/) Multiple sequence alignment
* [Tranalign](http://emboss.sourceforge.net/apps/release/6.6/emboss/apps/tranalign.html) Nucleotide alignments from protein alignments
* [Orthograph][https://github.com/mptrsen/Orthograph] Orthologous gene detection
* [OrthoDB](https://www.orthodb.org/) Ortholog Database

### Contact
Jackson Eyres, Bioinformatics Programmer, Agriculture & Agri-Food Canada  
jackson.eyres@canada.ca

### Copyright
Agriculture & Agri-Food Canada, Government of Canada

### License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

### Citations

Janina L. Kypke, (2019). Phylogenetics of the world's largest beetle family (Coleoptera: Staphylinidae) A methodoligcal exploration (PhD thesis, University of Copenhagen)
