---
title: "Lab 6"
author: "Jeffrey Miller"
date: "2026 Feb 27"
output: pdf_document
---


### Today
1. Review, fastqc
2. Redirection and pipes lesson
3. Script writing

## review
which for programs
conda environments
chmod for permissions
fastqc


## keypoints
Employ the grep command to search for information within files.
Print the results of a command to a file.
Construct command pipelines with two or more stages.
Use for loops to run the same command for several input files.


## questions for practical
How can I search within files?
How can I combine existing commands to do new things?



## HELP: Nucleotide abbreviations
The four nucleotides that appear in DNA are abbreviated A, C, T and G. Unknown nucleotides are represented with the letter N. An N appearing in a sequencing file represents a position where the sequencing machine was not able to confidently determine the nucleotide in that position. You can think of an N as being aNy nucleotide at that position in the DNA sequence.


## Exercise 1

1. Search for the sequence `GNATNACCACTTCC` in the `SRR098026.fastq` file.
  Have your search return all matching lines and the name (or identifier) for each sequence
  that contains a match.

```
grep GNATNACCACTTCC SRR098026.fastq -B1

@SRR098026.245 HWUSI-EAS1599_1:2:1:2:801 length=35
GNATNACCACTTCCAGTGCTGANNNNNNNGGGATG
```

2. Search for the sequence `AAGTT` in both FASTQ files.
  Have your search return all matching lines and the name (or identifier) for each sequence
  that contains a match.

```
grep AAGTT -B1 *.fastq
SRR097977.fastq-@SRR097977.11 209DTAAXX_Lenski2_1_7:8:3:247:351 length=36
SRR097977.fastq:GATTGCTTTAATGAAAAAGTCATATAAGTTGCCATG
--
SRR097977.fastq-@SRR097977.67 209DTAAXX_Lenski2_1_7:8:3:544:566 length=36
SRR097977.fastq:TTGTCCACGCTTTTCTATGTAAAGTTTATTTGCTTT
--
SRR097977.fastq-@SRR097977.68 209DTAAXX_Lenski2_1_7:8:3:724:110 length=36
SRR097977.fastq:TGAAGCCTGCTTTTTTATACTAAGTTTGCATTATAA
--
SRR097977.fastq-@SRR097977.80 209DTAAXX_Lenski2_1_7:8:3:258:281 length=36
SRR097977.fastq:GTGGCGCTGCTGCATAAGTTGGGTTATCAGGTCGTT
--
SRR097977.fastq-@SRR097977.92 209DTAAXX_Lenski2_1_7:8:3:353:318 length=36
SRR097977.fastq:GGCAAAATGGTCCTCCAGCCAGGCCAGAAGCAAGTT
--
SRR097977.fastq-@SRR097977.139 209DTAAXX_Lenski2_1_7:8:3:703:655 length=36
SRR097977.fastq:TTTATTTGTAAAGTTTTGTTGAAATAAGGGTTGTAA
--
SRR097977.fastq-@SRR097977.238 209DTAAXX_Lenski2_1_7:8:3:592:919 length=36
SRR097977.fastq:TTCTTACCATCCTGAAGTTTTTTCATCTTCCCTGAT
--
SRR098026.fastq-@SRR098026.158 HWUSI-EAS1599_1:2:1:1:1505 length=35
SRR098026.fastq:GNNNNNNNNCAAAGTTGATCNNNNNNNNNTGTGCG
```

3. How do the search results differ when matching in one file vs. both files? If you wanted to keep the original FASTQ format, how would you get around this?

It puts the file name before each line output.

4. Make a file called 'bad-reads.fastq' made up of reads with 10 Ns or more in a row

## Exercise 2

How many sequences are there in `SRR098026.fastq`? Remember that every sequence is formed by four lines.

## Exercise 3

How many sequences in `SRR098026.fastq` contain at least 3 consecutive Ns?

## Exercise 4

Print the file prefix of all of the `.txt` files in our current directory.

## Exercise 5

After renaming the fastqs as demonstrated, remove `_2026` from all of the `.txt` files.

## Exercise 6

We want the script to tell us when it's done.

1. Open `bad-reads-script.sh` and add the line `echo "Script finished!"` after the `grep` command and save the file.
2. Run the updated script.




## keypoints

- `grep` is a powerful search tool with many options for customization.
- `>`, `>>`, and `|` are different ways of redirecting output.
- `command > file` redirects a command's output to a file.
- `command >> file` redirects a command's output to a file without overwriting the existing contents of the file.
- `command_1 | command_2` redirects the output of the first command as input to the second command.
- `for` loops are used for iteration.
- `basename` gets rid of repetitive parts of names.





```bash
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_2.fastq.gz
```
```bash
$ cd
$ wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```

or

```bash
$ cd
$ curl -O ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```