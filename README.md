# Simulating, Detecting, and Annotating Reversions in BRCA1 Exon 11

The development of cancer is an evolving process, with the accumulation of somatic mutations that can change the functions and properties of cells. As mutations can cause the growth of cancer, it can also adapt to treatment and lead to resistances to therapy. One such example is the concept of reversions. A patient may acquire a mutation that inserts or deletes (indels) nucleotides that creates a frameshift of the genome, causing a pathological effect. Later, a secondary indel is acquired that restores the reading frame, causing a non-frameshift and potentially restoring protein function. This phenomenon has been particularly noted in BRCA1 and BRCA2 in relation to resistance to PARP inhibitors (Ganesan, 2018). 

For the scope of the project, I chose to analyze BRCA1 exon 11. Due to the length of the exon at 3,426 bases and importance to processes in DNA repair, this exon has been commonly impacted in the context of reversion (Raponi et al., 2014). An analysis of 327 patients discovered that approximately 22% of patients had BRCA1 reversions, with a noted hotspot located in exon 11 and primarily composed of deletions (Fig 2., Tobalina et al., 2021). Therefore, in this project, I utilized the NCBI Reference Sequence (NM_007294) to simulate the presence of deletions. This is a format that would already be aligned, as the primary goal was to detect reversions rather than the entire process of variant detection. 

## METHODS

Tools Used
- Python 3
- Regex
- NCBI Reference Sequences
- HGVS coding nucleotide nomenclature

The script requires Python 3 and no other dependencies, with the command python3 tav_reversion_finder.py to run. The reference sequence of BRCA1 exon 11 is already loaded into the script for the scope of the project. There are two main aspects of the script, simulating the presence of mutations and detecting reversions. 

For each loop, two mutations are simulated, a primary and secondary mutation. For the purposes of this simulation, both of these mutations are deletions simulated to be between 1 and 25 base pairs in length with a random position in the sequence. Once the position of the deletion is determined, an annotation is generated using the HGVS coding nucleotide nomenclature. Due to the NCBI reference sequence of exon 11, the beginning of the sequence is at c.903. The deletion is simulated twice, to account for the primary and secondary mutation. In addition to the annotation, a mutated sequence is generated where deletions are represented by the - symbol. 

In order to detect the reversion, it requires an input of the mutated sequence and the reference sequence. The positions and length of deletions are detected by using regular expressions for -. If the length of the combined deletions are divisible by 3, it is considered a reversion due to it being a non-frameshift and not changing the reading frame. Otherwise, the deletions are not considered a reversion. 

A tab-delimited text report is generated that summarizes the results of the simulation. The report has 9 columns, where the first four columns contain the sequence. The first column ‘FullReferenceSequence’ is the NCBI reference sequence without alterations. The second column ‘ImpactedReferenceSequence’ is a truncated version of the reference sequence that only includes the segments that were deleted as well as the region in between the deleted areas. The third column ‘FullMutatatedSequence’ is the sequence that includes the simulated mutations, where the deleted regions are represented by the - symbol. The fourth column ‘ImpactedMutatedSequence’ is similar to the second column, but only includes the region between the deletions. The next five columns detail the mutations. Columns five and six contain the HGVS annotation of the deletion and length of the deletion of the primary mutation respectively, and columns seven and eight contain information on the secondary mutation. The last column reports if the two deletions consist of a reversion “Y” or no reversion “N”. An example output is included in the submitted files, “reversion_report_seed50.txt” which uses the random package seed 50.


## LIMITATIONS AND FURTHER IMPROVEMENTS
 
One improvement is to incorporate other situations where a reversion can occur, such as insertions and splice sites. In actual data, there may be additional variants, both somatic and germline, that need to be accounted for. This script uses the input of a reference sequence FASTA file. Starting from an earlier state would allow for more customization and realism to how variations are seen in patients. Other improvements could allow for integration with other available tools that simulate genomic variants with additional parameters to customize, such as SimuSCoP which simulates Illumina sequencing data (Yu et al., 2020). In addition to the improvements in simulation, integrating genomic variant databases can improve the annotations. Since the script is currently limited to BRCA1 exon 11, expanded use could locate reversions in other genes by accessing external information to determine the location of the mutation and expand the annotation to also include the protein effect. For example, the Catalogue Of Somatic Mutations In Cancer (COSMIC) could be used to include information on tissue distribution and references to literature regarding the mutation.

While there is further potential to improve and expand the current script, it currently is able to identify reversions in FASTA files regardless of the distance between mutations and outputs the annotation and impacted sequences, which will be greatly beneficial for my work. With the importance of reversions for clinical decisions and interaction with therapeutic resistances, being able to accurately identify them in patient data has been critical for genomic testing and the use of a script would allow for more objective identification. 

## REFERENCES

Cheng, H.H., Salipante, S.J., Nelson, P.S., Montgomery, B. and Pritchard, C.C., 2018. Polyclonal BRCA2 reversion mutations detected in circulating tumor DNA after platinum chemotherapy in a patient with metastatic prostate cancer. JCO Precision Oncology, 2.
Ganesan, S., 2018. Tumor suppressor tolerance: reversion mutations in BRCA1 and BRCA2 and resistance to PARP inhibitors and platinum. JCO Precision Oncology, 2, pp.1-4.
Raponi, M., Smith, L.D., Silipo, M., Stuani, C., Buratti, E. and Baralle, D., 2014. BRCA1 exon 11 a model of long exon splicing regulation. RNA biology, 11(4), pp.351-359.
Tobalina, L., Armenia, J., Irving, E., O'Connor, M.J. and Forment, J.V., 2021. A meta-analysis of reversion mutations in BRCA genes identifies signatures of DNA end-joining repair mechanisms driving therapy resistance. Annals of Oncology, 32(1), pp.103-112.
Yu, Z., Du, F., Ban, R. and Zhang, Y., 2020. SimuSCoP: reliably simulate Illumina sequencing data based on position and context dependent profiles. BMC bioinformatics, 21, pp.1-18.
