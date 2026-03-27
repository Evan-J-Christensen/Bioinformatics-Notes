# Evan Christensen Bioinformatics Notebook
## Navigation & File System
__Commands:__
- ```pwd``` — present working directory
- ```ls``` — list contents
    - ```-F``` — distinguish directories
    - ```-l``` — long format (permissions, size)
    - ```-h``` — human-readable sizes
    - ```lrth``` — sorted, readable
- ```cd``` — change directory
    - ```cd ..``` — move up one level
    - ```cd ~``` — home directory
- ```clear``` — clear terminal
```Bash
pwd
ls -lh
cd ~/gen711-811
cd ../
```
## File Viewing & Inspection
__Commands:__
- ```head``` — first lines
- ```tail``` — last lines
- ```less``` — scrollable viewer
- ```cat``` — print entire file
- ```wc -l``` — count lines
__Examples:__
```Bash
head -n 4 file.fastq
tail -n 4 file.fastq
wc -l file.fastq
less file.fastq
```
__Key Concept:__
- FASTQ files = __4 lines per read__
```Bash
echo $(($(wc -l < file.fastq)/4))
```
## File Management
__Commands:__
- ```cp``` — copy files
- ```mv``` — move/rename
- ```mkdir``` — make directory
- ```rm``` — remove files
    - ```-r``` — recursive (allows for directory removal)
__Examples:__
```Bash
cp file.fastq backup.fastq
mv *.fastq backup/
mkdir results
rm -r backup
```
## File Size & Disk Usage
```Bash
ls -lh
du -sh *
```
## Permissions
__Commands:__
- ```ls -l``` — view permissions
- ```chmod``` — change permissions
__Examples:__
```Bash
chmod -w file.txt
chmod u-w file.txt
ls -l
```
__Key Concepts:__
- User Classes:
    - ```u``` = owner
    - ```g``` = group
    - ```o``` = others
    - ```a``` = all
- Permissions:
    - ```r``` = read
    - ```w``` = write
    - ```x``` = execute
## Searching & Pattern Matching
__Command:__
- ```grep``` — search within files
    - ```-i``` — ignore case
    - ```-v``` — exclude matches
    - ```-n``` — show line numbers
    - ```-c``` — count matches
    - ```-A``` — lines after match
    - ```-B``` — lines before match
__Examples:__
```Bash
grep pattern file.txt
grep -i pattern file.txt
grep -v pattern file.txt
grep -n pattern file.txt
grep -c pattern file.txt
```
__Beginning of line search:__
```Bash
grep '^@' file.fastq
```
## Working with FASTQ Files
__Structure:__
1. Header (```@```)
2. Sequence
3. ```+```
4. Quality scores
## Extract Components
```Bash
sed -n '1~4p' file.fastq   # headers
sed -n '2~4p' file.fastq   # sequences
```
## Convert FASTQ → FASTA
__Preview:__
```Bash
grep '^@' -A1 --no-group-separator file.fastq | head
```
__Convert:__
```Bash
grep '^@' -A1 --no-group-separator file.fastq | sed 's/^@/>/' > file.fasta
```
## Find Bad Reads
__≥10 Ns:__
```Bash
grep -E 'N{10,}' file.fastq -B1 -A2 > bad-reads.fastq
```
__≥3 Ns count:__
```Bash
grep -c 'N\{3,\}' file.fastq
```
__≥15 Ns count:__
```Bash
grep -c 'N\{15,\}' *.fastq
```
## Pipes & Redirection
- ```>``` overwrite output
- ```>>``` append output
- ```|``` pass output to next command
__Examples:__
```Bash
command > file.txt
command >> file.txt
command1 | command2

cat file | grep pattern | wc -l
```
## Sorting & Counting
```Bash
sort file.txt
uniq -c file.txt
sort file.txt | uniq -c | sort -nr
```
## Loops
__Basic Loop:__
```Bash
for name in *.fastq
do
  echo ${name}
done
```
__Example with processing:__
```Bash
for infile in *_1.fastq.gz
do
  base=$(basename ${infile} _1.fastq.gz)
  echo $base
done
```
## Filename Handling
```Bash
basename file.txt .txt
```
## Conda Environments
__Commands:__
```Bash
conda create -n myenv fastqc
conda activate myenv
conda deactivate
which fastqc
```
## FASTQC
```Bash
fastqc *.fastq.gz
```
## Trimmomatic
__Basic Structure:__
```Bash
trimmomatic PE input_1.fastq input_2.fastq \
output_1P.fastq output_1U.fastq \
output_2P.fastq output_2U.fastq \
SLIDINGWINDOW:4:20 MINLEN:25
```
## Convert to FASTA
```Bash
grep '^@' -A1 --no-group-separator Sample1.fastq | sed 's/^@/>/' > Sample1.fasta
```
## Count Reads with Ns
```Bash
grep -c 'N\{15,\}' *.fastq
```
## Specific line Extraction
```Bash
head -n 100 Sample1.fasta | tail -n 1
```
## Checksums
```Bash
md5sum Sample1.fasta
md5sum Sample1.fasta > my_md5sums.txt
md5sum Sample2.fasta >> my_md5sums.txt
echo "Your Name" >> my_md5sums.txt
```
## Extra Commands
```
file filename
stat filename
history
man command
```
