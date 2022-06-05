# De Novo Assembly

In this assignment, we will practice the task of de novo assembly. We will use data from the following paper: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6639603/ which aimed to sequence Mycobacterium ulcerans CSURP7741, a French Guianan
Clinical Isolate.
Your task is to use Spades assembler to assemble CSURP7741 from the raw fastq files. You are then to answer several questions about the generated assembly.

---


## **Initialize conda**
```sh
#Step 1 - run bash
bash
#Step 2 - initialize conda
/home/wail.ba-alawi/miniconda3/bin/conda init bash
#Step 3 - acess conda list
conda list
```
-----

## **Spades tool**

Spades - St. Petersburg genome assembler - is an assembly toolkit containing various assembly pipelines and it can also be downloaded through bioconda. (https://github.com/ablab/spades)
    
Parameters:

 - --meta : required for metagenomic data (Basic option)
 - -1 <'filename'>  : file with forward paired-end reads
 - -2 <'filename'> : file with reverse paired-end reads'
 - --only-assembler : runs assembly module only
    (I didnt use error correction because based on litreture this option is mainly used for long-reads and our expirement is with short-reads sequenced by illumina)

```sh
# Open the **spades.py** file
cd /home/wail.ba-alawi/miniconda3/bin python3 spades.py
# Run
spades.py --meta -1 /home/wail.ba-alawi/BioII_Assignment2/P7741_R1.fastq.gz \
-2 /home/wail.ba-alawi/BioII_Assignment2/P7741_R2.fastq.gz \
--only-assembler -o denovo_spades
```

----
## **Quast tool**

Quast: A tool to get different statistics and information of the generated assembly. (http://quast.sourceforge.net/docs/manual.html)

Parameters:

- -o : output directory
- -r : specify a reference genome (optional)
- -g gene: File with genomic feature coordinates in the reference (GFF)
- contings.fasta file
```sh
# Open the **quast.py** file
cd /home/wail.ba-alawi/miniconda3/bin python3 quast.py
# Run 
quast.py -o quast_output \
        -r /home/fatima.farhan/Denovo_assembly/sra_data.fasta.gz \
        -g  gene:/home/fatima.farhan/Denovo_assembly/GCF_900683785.1_PRJEB30628-2_genomic.gff.gz \
        /home/fatima.farhan/Denovo_assembly/contigs.fasta
```
**quast report**

All statistics are based on contigs of size >= 500 bp, unless otherwise noted (e.g., "# contigs (>= 0 bp)" and "Total length (>= 0 bp)" include all contigs).

|Assembly|contigs|
|---|---|
|\# contigs (>= 0 bp)|2344|
|\# contigs (>= 1000 bp)|559|
|\# contigs (>= 5000 bp)|332|
|\# contigs (>= 10000 bp)|195|
|\# contigs (>= 25000 bp)|39|
|\# contigs (>= 50000 bp)|3|
|Total length \(>= 0 bp)|5819334|
|Total length \(>= 1000 bp)|5341308|
|Total length \(>= 5000 bp)|4748807|
|Total length \(>= 10000 bp)|3772082|
|Total length \(>= 25000 bp)|1358673|
|Total length \(>= 50000 bp)|211567|
|\# contigs|659|
|Largest contig|87628|
|Total length|5413079|
|Reference length|123630247|
|GC \(%)|65\.57|
|Reference GC \(%)|64\.99|
|N50|15053|
|NG50|-|
|N90|4548|
|NG90|-|
|L50|110|
|LG50|-|
|L90|358|
|LG90|-|
|\# misassemblies|15915|
|\# misassembled contigs|659|
|Misassembled contigs length|5413079|
|\# local misassemblies|2|
|\# scaffold gap ext. mis.|0|
|\# scaffold gap loc. mis.|0|
|\# unaligned mis. contigs|0|
|\# unaligned contigs|0 + 57 part|
|Unaligned length|325678|
|Genome fraction \(%)|3\.350|
|Duplication ratio|1\.000|
|\# N's per 100 kbp|0\.00|
|\# mismatches per 100 kbp|13\.86|
|\# indels per 100 kbp|0\.92|
|\# genomic features|0 + 0 part|
|Largest alignment|367|
|Total aligned length|4141152|
|NA50|251|
|NGA50|-|
|NA90|-|
|NGA90|-|
|LA50|10783|
|LGA50|-|
|LA90|-|
|LGA90|-|

---
## **Questions**

1.	Perform de novo assembly of CSURP7741 using Spades (read
Spades manual for usage)

    - Done ☑️

2.	What is the sequencing technology used and how many reads were generated

     - They used illumina Miseq and it generated 273071 reads.

3.	What is the GC content of the assembled genome? How does that compare to what is mentioned in the paper above?

    - The GC content of the assembled genome is **65.57 %** as calculated by quast tool. The measured GC% value is relatively similar to the one mentioned in the paper (65%)..

4.	How many contigs were generated?

    - Total number of generated contgs is **2344**, as indicated by quast report. 

5.	What is N50 and NG50 of the assembled genome and what do they mean?

    - **N50** is the length for which the collection of all contigs of that length or longer covers at least half an assembly. In our experiment N50 is 15053.
    - **NG50** is the length for which the collection of all contigs of that length or longer covers at least half the reference genome. In our experiment NG50 is not calculated, although both fasta and gff files of the reference genome are provided.



6.	What is the size of the assembled genome?
    
    - It size it **123630247** bp
