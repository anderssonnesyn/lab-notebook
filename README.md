# lab-notebook
Lab notebook for GEN 811

# Lab Notebook

# # # # LAB 1 # # # #
ssh username@servername.edu
# connects my terminal to the teaching cluster RON
# aws1020@ron.sr.unh.edu
# password: love2SKI

ls
# this lists all of the files in my current working directory

ls -F
# We can make the ls output more comprehensible by using the flag -F, which tells ls to add a trailing / to the names of directories
# Output:
>sra_metadata/  untrimmed_fastq/
# Anything with a “/” after it is a directory. Things with a “*” after them are programs. If there are no decorations, it’s a file.

pwd
# this stands for print working directory

ctrl-c
# cancel the command line and get a new one

clear
# clear will clear everything in terminal

PS1='$'
# setting a variable to get rid of the text on the command line

cd
# change directory

rm dir
# remove directory forever

# If having problems, open new terminal
# # # # END OF LAB 1 # # # # 



# # # # CATCHING UP FROM MISSING LABS 2, 3, AND 4 # # # #

*
# Download anything that ends in for example "fastq.gz" if you type *fastq.gz after perhaps cp /tmp/

conda
# program for managing environments

fastqc -h
# Gives options to run fastqc

#  .
# copy  and save all the things in the CURRENT directory ("space" then "period")

cp
# copy
# # # # END OF CATCHING UP FROM MISSED LABS 2, 3, 4 # # # #




# # # # LAB 2 # # # #

ls -1
# Use the -l option for the ls command to display more information for each item in the directory.
# What is one piece of additional information this long format gives you that you don’t see with the bare ls command?
# output:
>total 8
>drwxr-x--- 2 dcuser dcuser 4096 Jul 30  2015 sra_metadata
>drwxr-xr-x 2 dcuser dcuser 4096 Nov 15  2017 untrimmed_fastq
# The additional information given includes the name of the owner of the file, when the file was last modified, and whether the current user has permission to read and write to the file.

# Most commands take the options, which is a dash- followed by a letter. Or many letters for multiple options:
ls -ltrh
# output:
>total 184
>-rw-r--r--@ 1 jeffreymiller  staff    42K Nov 15  2017 SRR098026.fastq
>-rw-r--r--@ 1 jeffreymiller  staff    46K Nov 15  2017 SRR097977.fastq

# Lets again change directories to work on our untrimmed_fastq sequences. Once you are in the untrimmed directory, what is in there?
ls
> sra_metadata    untrimmed_fastq
cd untrimmed_fastq
ls -F
> SRR097977.fastq  SRR098026.fastq

# The next command you’ll memorize by using it a bunch is head. Head gives you a peek at the first few lines of a file.
head SRR097977.fastq
# output:
>@SRR098026.1 HWUSI-EAS1599_1:2:1:0:968 length=35
NNNNNNNNNNNNNNNNCNNNNNNNNNNNNNNNNNN
+SRR098026.1 HWUSI-EAS1599_1:2:1:0:968 length=35
!!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
@SRR098026.2 HWUSI-EAS1599_1:2:1:0:312 length=35
NNNNNNNNNNNNNNNNANNNNNNNNNNNNNNNNNN
+SRR098026.2 HWUSI-EAS1599_1:2:1:0:312 length=35
!!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
@SRR098026.3 HWUSI-EAS1599_1:2:1:0:570 length=35
NNNNNNNNNNNNNNNNANNNNNNNNNNNNNNNNNN

# We have a special command to tell the computer to move us back or up one directory level.
cd ../
ls
# output:
>sra_metadata    untrimmed_fastq

cd untrimmed_fastq
# To navigate out two folders from here, we can double it up with
cd ../../
ls
# output:
> lab1_notes.md            lab1_notes.sh            pre-lab-instructions.md  shell_data

# # # # END OF LAB 2 # # # #




# # # # LAB 3 # # # #

# Having touble changing directories in terminal to your lab folder? Try:
cd ~ cd gen811

# The tilda shortcut takes you home
# If you end up in the wrong directory, or something that you do not recognize, remember that the (~, green/yellow/esc)
cd -
# The /, ~, and .. characters represent important navigational shortcuts.
# Will be on exam:
# If the path starts with ‘/’, it is an absolute path.
# If the path starts with ‘../’ or a names of a directory, it is a relative path.
# Relative paths specify the location starting from the current location,
# While absolute paths specify a location from the root of the file system.
# Relative path:
cd untrimmed_fastq
cd ../
# Absolute path:
cd /Users/jeffreymiller/Desktop/gen711_lab/shell_data/untrimmed_fastq

# Now that we know how to navigate around our directory structure, let’s start working with our sequencing files. We did a sequencing experiment and have two results files, which are stored in our untrimmed_fastq directory.
cd ~/shell_data/untrimmed_fastq
# Lets say that we did some grepping here and made a new text file for an analysis.
grep '@' SRR097977.fastq > textfile.txt
ls
# Pipe is for making the output of one command go into another. The ‘>’ command is directing the output to a file. People get tripped up on this. It will be on the exam.
# We might have many files in here, but we are omly interested in looking at the FASTQ files in this directory.
# We can list all files with the .fastq extension using the fastq part of the file, and something called a wildcard or glob:
ls *.fastq
 > SRR097977.fastq  SRR098026.fastq
# The wildcard works with more than just the file extension name. Similar to the way the tab works by filling in as much as it can without making decisions for you.
ls *977.fastq
 > SRR097977.fastq
 # Just for fun, lets do this with an absolute path as well. You can use this to see files that match in far directories too
 ls /Users/jeffreymiller/Desktop/gen711_lab/shell_data/untrimmed_fastq/*fastq


# To cancel something that wont run:
# ctrl + c (cancel command when stuck) 
# ctrl + r (find in your command history) 
# ctrl + L (clear)

# EXCERCISE: Do each of the following tasks from your current directory using a single ls command for each:
# List all of the files in /Applications that start with the letter ‘c’.
# List all of the files in /Applications that contain the letter ‘a’.
# List all of the files in /Applications that end with the letter ‘o’.
# Bonus: List all of the files in /Applications that contain the letter ‘a’ or the letter ‘c’.
ls /usr/bin/c ls /usr/bin/a ls /usr/bin/o Bonus: ls /usr/bin/[ac]

# EXCERCISE: ‘echo’ is a built-in shell command that writes its arguments, like a line of text to standard output. The ‘echo’ command can also be used with pattern matching characters, such as wildcard characters. Here we will use the echo command to see how the wildcard character is interpreted by the shell. What does echo say when you try to match something that is not there? What about ls?
echo .fastq > SRR097977.fastq SRR098026.fastq echo .missing ls *.missing

# EXCERCISE: Find the line number in your history for the command that listed all the .fastq files using the absolute path . Rerun that command. history | grep -n ‘grep’
cd ~/shell_data/untrimmed_fastq
grep NNNNNNNNNN SRR098026.fastq
grep -B1 -A2 NNNNNNNNNN SRR098026.fastq

# # # # END OF LAB 3 # # # #



# # # # LAB 4 # # # #

# REVIEW: Do word find in files with grep:
grep 'GNATNACCACTTCC' SRR098026.fastq

# Interconvert between absolute and relative paths.
ls gen711/shell_data/
realpath gen711

# Work with hidden directories and hidden files and perform operations on files in directories outside your working directory
pwd
ls -a gen711/shell_data/
ls -a gen711/shell_data/.hidden

# EXCERCISE: How many programs in /bin 1. Start with the letter c 2. Start with the letter a 3. Start with the letter o
ls /bin/c*

# Pipe is for making the output of one command go into another.
ls /bin/c* | wc -l
grep 'GNATNACCACTTCC' gen711/shell_data/untrimmed_fastq/SRR098026.fastq | wc -l
The ‘>’ command is directing the output to a file
# The ‘>’ command is directing the output to a file
grep 'GNATNACCACTTCC' gen711/shell_data/untrimmed_fastq/SRR098026.fastq > the readifound.match
grep -B1 -A2 NNNNNNNNNN gen711/shell_data/untrimmed_fastq/*.fastq > bad_reads.fastq

# To open a file, we used head, tail, and catas well as a program called ‘less’
cat bad_reads.fastq
less bad_reads.fastq

# NEW MATERIAL: Make a new directory for new project files, change directories to there, and then use a command called curl to download a fastq from the internet:
cd ~
mkdir -p ~/dc_workshop/data/untrimmed_fastq/
cd ~/dc_workshop/data/untrimmed_fastq
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_2.fastq.gz
# The data comes in a compressed format, which is why there is a .gz at the end of the file names. This makes it faster to transfer, and allows it to take up less space on our computer. Let’s unzip one of the files so that we can look at the fastq format.
gunzip SRR2584863_1.fastq.gz
ls
head -n 4 SRR2584863_1.fastq
# Quality encoding: !"#$%&’()*+,-./0123456789:;<=>?@ABCDEFGHIJ | | | | | Quality score: 01........11........21........31........41

# EXCERCISE: What is the last read in the SRR2584863_1.fastq file? How confident are you in this read?
# Lets copy the rest of the files from tmp on RON 
cp /tmp/*fastq.gz .
# Q: How big are the files? (Hint: Look at the options for the ls command to see how to show file sizes.) hint, it involves ‘ls’
# Lets activate the environment. A conda environment is . . .
conda activate genomics
# At this point, lets validate that all the relevant tools are installed. Test with
fastqc -h
# FastQC can accept multiple file names as input, and on both zipped and unzipped files, so we can use the .fastq wildcard to run FastQC on all of the FASTQ files in this directory
fastqc *.fastq*
# After that has finished, see the files and size:
ls -lh
# Lets organize these files a bit. Sep. the fastqc files from the data by making a directory and moving the fastq files into it.
mkdir -p ~/dc_workshop/results/fastqc_untrimmed_reads
mv *.zip ~/dc_workshop/results/fastqc_untrimmed_reads/
mv *.html ~/dc_workshop/results/fastqc_untrimmed_reads/
# lets head into the fastqc results folder and take a look into one of the summary files:
cd ~/dc_workshop/results/fastqc_untrimmed_reads/
# The output files are zipped up. Lets see if we can unzip them with all in one command.
unzip *.zip
# Then, we will use less to look a the summary
less SRR2584863_1_fastqc/summary.txt
# Lastly, lets try to download one of those html files to our computer with sftp
realpath SRR2589044_1_fastqc.html
sftp jtmiller@ron.sr.unh.edu
get
# Q: Which samples failed at least one of FastQC’s quality tests? What test(s) did those samples fail?
cat */summary.txt > ~/dc_workshop/docs/fastqc_summaries.txt

# # # # END OF LAB 4 # # # #



# # # # LAB 5 # # # #

# Trimming and Filtering:

# Quick edits to VSCODE keybiindings to make runninig things easier Code –> preferences –> profile –> Show Contents. Then, click on the ‘keybindings.json’
[
    {
        "key": "ctrl+enter",
        "command": "workbench.action.terminal.runSelectedText"
    }
]


ls
# list all files in current working directory

ssh
# login to ssh, then open new terminal

# Download the results of fastqc to your computer with sftp. Open a new, seperate terminal and and connect with
 cd ~/Desktop
sftp username@jtmiller@ron.sr.unh.edu
sftp
# type sftp and then type ssh login and password in new terminal
# new line should say sftp>

# We will use the absolute path of the files to ‘get’ the *png files.
realpath
realpath /tmp/fastqc_output/*fastqc/Images/*png

# y the realpath of one of the files, and paste it into the the sftp connection after ‘get’, and view
get 
# "get" the images by typing: 
get /tmp/fastqc_output/*fastqc/Images/*png .
# Notice the " ." at the end – that will save the images to the CURRENT working directory
get /tmp/fastqc_output/SRR2584863_2_fastqc/Images/per_sequence_quality.png

# Can close all terminals except one logged in by ssh after you get the images

conda activate genomics
# activates conda program(s)
# should now say (genomics) instead of (base) at the front of the line you are typing in right before aws1020@ron:

# Trimmomatic has a variety of options to trim your reads. If we run the following command, we can see some of our options.
trimmomatic
# Now we will run Trimmomatic on our data. Navigate to your untrimmed_fastq data directory:
cd ~/dc_workshop/data/untrimmed_fastq
# Zip up your fastqs if they aren’t already
gzip *.fastq
# copy the illumina adapters that are packaged with trimmomatic into your fastq directory:
cp /opt/anaconda/anaconda/pkgs/trimmomatic-0.39-1/share/trimmomatic-0.39-1/adapters/NexteraPE-PE.fa .

# In lab:
# type cp /tmp/*fastq.gz to copy the files that we are going to run trimmomatic on 
# type ls to list all files
# type ls *fastq.gz to list only the ones that are fastq.gz files (should be 6 of them)
# type cp /opt/anaconda/anaconda/pkgs/trimmomatic-0.39-1/share/trimmomatic-0.39-1/adapters/NexteraPE-PE.fa . to copy the adapters

trimmomatic
# Example of running trimmomatic on a single fastq
# this will trim up reads
trimmomatic PE -threads 4 SRR_1056_1.fastq SRR_1056_2.fastq  \
    SRR_1056_1.trimmed.fastq.gz SRR_1056_1un.trimmed.fastq.gz \
    SRR_1056_2.trimmed.fastq.gz SRR_1056_2un.trimmed.fastq.gz \
    ILLUMINACLIP:SRR_adapters.fa SLIDINGWINDOW:4:20
# 1. What percent of reads did we discard from our sample? 2. What percent of reads did we keep both pairs?
# We can confirm that we have our output files:
ls SRR2589044*
# Copy and paste this ‘for’ loop to run it on each:
for infile in *_1.fastq.gz
do
    base=$(basename ${infile} _1.fastq.gz) 
    trimmomatic PE ${infile} ${base}_2.fastq.gz \
        ${base}_1.trim.fastq.gz ${base}_1un.trim.fastq.gz \ 
        ${base}_2.trim.fastq.gz ${base}_2un.trim.fastq.gz \ SLIDINGWINDOW:4:20 MINLEN:25 ILLUMINACLIP:NexteraPE-PE.fa:2:40:15
done

# For loop will replace names of our fastq's (not on practical)
# Copy this from Professor Miller's folder to save time
# make new folder 

# EXCERCISE: 1. make a folder called ‘trimmed_fastq’ in data
# 2. move all files that we made (hint: .trim and the move command, and the destination directory will work)
# 3. Re-run fastqc on the trimmed fastqs in the trimmed_fastq folder.
# Solution to Lab 5 exercise
cd ~/dc_workshop/data/untrimmed_fastq/
mkdir ../trimmed_fastq
cd ../trimmed_fastq
cp /tmp/trimmed/*fastq.gz .
ls
fastqc *fastq.gz

# grab .html file and find the realpath of it
# type get and then the .html file

# Variant Calling:

# How do I find sequence variants between my sample and a reference genome?

# Download Ref. Genome
cd ~/dc_workshop
mkdir -p data/ref_genome
curl -L -o data/ref_genome/ecoli_rel606.fasta.gz ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/017/985/
gunzip data/ref_genome/ecoli_rel606.fasta.gz
# Download more fastq files
curl -L -o sub.tar.gz https://ndownloader.figshare.com/files/14418248
tar xvf sub.tar.gz
mv sub/ ~/dc_workshop/data/trimmed_fastq_small
# Make directories
mkdir -p results/sam results/bam results/bcf results/vcf

# Index the reference genome
bwa index data/ref_genome/ecoli_rel606.fasta
# Align your reads to reference genome
bwa mem data/ref_genome/ecoli_rel606.fasta data/trimmed_fastq_small/SRR2584866_1.trim.sub.fastq data/
# View the SAM/BAM format with samtools view
samtools view -S -b results/sam/SRR2584866.aligned.sam > results/bam/SRR2584866.aligned.bam
# Sort BAM file by coordinates
# Type into command: $ samtools sort -o results/bam/SRR2584866.aligned.sorted.bam results/bam/SRR2584866.aligned.bam

# Use flagstat to get stats on alignment
samtools flagstat results/bam/SRR2584866.aligned.sorted.bam

# Variant Calling
# Step 1: Calculate the read coverage of positions in the genome
bcftools mpileup -O b -o results/bcf/SRR2584866_raw.bcf \
-f data/ref_genome/ecoli_rel606.fasta results/bam/SRR2584866.aligned.sorted.bam
# Step 2: Detect the single nucleotide variants (SNVs)
# Type into command: $ bcftools call --ploidy 1 -m -v -o results/vcf/SRR2584866_variants.vcf results/bcf/SRR2584866_raw.bcf
{: .bash}
# Step 3: Filter and report the SNV variants in variant calling format (VCF)
# Type into command: $ vcfutils.pl varFilter results/vcf/SRR2584866_variants.vcf  > results/vcf/SRR2584866_final_variants.vcf
{: .bash}
# Explore the VCF format:
# Type into command: $ less -S results/vcf/SRR2584866_final_variants.vcf
{: .bash} 
# Remember: use ‘q’ to exit less

# EXCERCISE: Use the grep and wc commands you have learned to assess how many variants are in the vcf file.
# Assess the alignment (visualization):
# Type into command: $ samtools index results/bam/SRR2584866.aligned.sorted.bam
{: .bash}
# Viewing with tview
# Samtools implements a very simple text alignment viewer based on the GNU ncurses library, called tview.
# Type into command: $ samtools tview results/bam/SRR2584866.aligned.sorted.bam data/ref_genome/ecoli_rel606.fasta
{: .bash}

# EXCERCISE: Download the reference genome (ecoli_rel606.fasta), .bams, .bai, and .vcf to your desktop into a ‘files_for_igv’ folder with sftp. Bonus for doing it all on command line.
# Download IGV from the Broad Institute’s software page, double-click the .zip file to unzip it, and then drag the program into your Applications folder.
# 1. Open IGV.
# 2. Load our reference genome file (ecoli_rel606.fasta) into IGV using the “Load Genomes from File. . . ” option under the “Genomes” pull-down menu.
# 3. Load our BAM file (SRR2584866.aligned.sorted.bam) using the “Load from File. . . ” option under the “File” pull-down menu.
# 4. Do the same with our VCF file (SRR2584866_final_variants.vcf).

# # # # END OF LAB 5 # # # #




# # # # LAB 6 # # # #

mkdir -p data/ref_genome
curl -L -o data/ref_genome/ecoli_rel606.fasta.gz ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/017/985/GCA_000017985.1_ASM1798v1/GCA_000017985.1_ASM1798v1_genomic.fna.gz
gunzip data/ref_genome/ecoli_rel606.fasta.gz
# gunzip took name of reference genome and will make a new copy of the reference genome file to make it .gz
curl -L -o sub.tar.gz https://ndownloader.figshare.com/files/14418248
tar xvf sub.tar.gz
# get hub copilot – can install for free
mkdir -p results/sam results/bam results/vcf
# put in new results folder, -p is so you can make a path
sam
# alignment files
bam
# compressed version of alignment files
conda activate genomics-plus
# conda is environment manager
bwa
# shows commands (help page)
bwa index data/ref_genome/ecoli_rel606.fasta
# index genome
ls -ltrh data/ref_genome/
# organizes files
bwa mem data/ref_genome/ecoli_rel606.fasta data/trimmed_fastq_small/SRR2584866_1.trim.sub.fastq data/trimmed_fastq_small/SRR2584866_2.trim.sub.fastq > results/sam/SRR2584866.aligned.sam
# first thing after bwa mem is reference genome file, second is path to forward read files, then third is paired-end read files (above is not correct, has the wrong file numbers; see below)
bwa mem data/ref_genome/ecoli_rel606.fasta 
 > results/sam/SRR2584866.aligned.sam
 # above is correct
 mv
 # move
 ls sub
 # lists files in sub folder
 mkdir -p ~/dc_workshop/data/trimmed_fastq_small/
 # makes trimmed_fastq_small folder
 mv sub/* ~/dc_workshop/data/trimmed_fastq_small/
 # moves files from sub folder to trimmed_fastq_small folder
 cd ../../
 # moves two steps back (to dc_workshop in this case)
bwa mem \
    data/ref_genome/ecoli_rel606.fasta \ 
    data/trimmed_fastq_small/SRR2589044_1.trim.sub.fastq \ 
    data/trimmed_fastq_small/SRR2589044_2.trim.sub.fastq \
    > results/sam/SRR2589044.aligned.sam
# doing the alignments
# saved into file results/sam/SRR2589044.aligned.sam
head
cat
less -S
# shows what is saved (head is the safe option)
less -S results/sam/SRR2589044.aligned.sam
# shows alignment reads
wc -l results/sam/SRR2589044.aligned.sam
# counts number of reads in a file
# hit q to go back to command line
grep -v '^@' results/sam/SRR2589044.aligned.sam | head
grep -v '^@' results/sam/SRR2589044.aligned.sam | wc -l
# shows number of reads
samtools view -S -b results/sam/SRR2589044.aligned.sam > results/sam/SRR2589044.aligned.bam
# takes alignment file as input, uses view command, -b uses bam format, converts to bam file and saves to that location
samtools sort -o results/bam/SRR2589044.aligned.sorted.bam \
results/sam/SRR2589044.aligned.bam
# sort bam file but save into that location, took aligned file and sorted it (new name of file includes "sorted")
samtools flagstat results/bam/SRR2589044.aligned.sorted.bam
# output shows PCR duplicates, how many are properly paired, etc.
bcftools mpileup -Ob -o results/bam/SRR2589044_raw.bcf \
-f data/ref_genome/ecoli_rel606.fasta results/bam/SRR2589044.aligned.sorted.bam &
# bcftools is optional program similar to samtools, will look at reads see how they align to genomes and tell us about the genetic information, calculates read coverage
&
# & symbol allows us to run something in the background while using the command line, put at the end of command
jobs
# shows what is running, will say "running" unless it is done
# will pick up here for next lab

# # # # END OF LAB 6 # # # #


# # # # LAB 7 # # # #

# Variant Calling
# Align your reads to reference genome
# Pick up from last week where we left off with our SRR2584866 sample.
bwa mem data/ref_genome/ecoli_rel606.fasta data/trimmed_fastq_small/SRR2584866_1.trim.sub.fastq data/trimmed_fastq_small/SRR2584866_2.trim.sub.fastq > results/sam/SRR2584866.aligned.sam
# align fastq's to reference genome

# View the SAM/BAM format with samtools view:
samtools view -S -b results/sam/SRR2584866.aligned.sam > results/bam/SRR2584866.aligned.bam
# Turn file into compressed binary file

# Sort BAM file by coordinates
samtools sort -o results/bam/SRR2584866.aligned.sorted.bam results/bam/SRR2584866.aligned.bam
# Use samtools to sort BAM alignment file

conda activate genomics-plus

# Variant calling:
bcftools mpileup -O b -o results/bcf/SRR2584866_raw.bcf -f data/ref_genome/ecoli_rel606.fasta results/bam/SRR2584866.aligned.sorted.bam
# calculate read coverage of positions in the genome
bcftools call --ploidy 1 -m -v -o results/vcf/SRR2584866_variants.vcf results/bcf/SRR2584866_raw.bcf
# detect the single nucleotide variants (SNVs)
vcfutils.pl varFilter results/vcf/SRR2584866_variants.vcf  > results/vcf/SRR2584866_final_variants.vcf
# Filter and report the SNV variants in variant calling format
samtools index results/bam/SRR2584866.aligned.sorted.bam
# Index the alignment
samtools tview results/bam/SRR2584866.aligned.sorted.bam data/ref_genome/ecoli_rel606.fasta
# Viewing with the alignment with tview
# Type into command: $ samtools tview results/bam/SRR2584866.aligned.sorted.bam data/ref_genome/ecoli_rel606.fasta

^D
# cancels (control D)

realpath results/bam/SRR2589044.aligned.sorted.bam
realpath results/bam/SRR2589044_final_variants.vcf
realpath data/ref_genome/ecoli_rel606.fasta

# In sftp do this below (after first exercise of lab 7)
get /home/unhAW/jtmiller/dc_workshop/results/bam/SRR2589044.aligned.sorted.bam*
get /home/unhAW/jtmiller/dc_workshop/results/vcf/*
get /home/users/aws1020/dc_workshop/data/ref_genome/ecoli_rel606.fasta*
# Try to redo lab 7; had quite a few problems

# # # # END OF LAB 7 # # # #



# # # # LAB PRACTICAL PRACTICE # # # #

# Notes:
grep -A2 -B1 "NNNNN" *.fastq
grep -B1 "NNNNN" SRR098026.fastq | grep -v '\-\-' | grep -v '@' > newfile
# Look for anything after backslash (i.e. '\-\-' will search for - symbol)
# -v = inverse
# Look for anything except for @ (i.e. grep -v '@')
grep -B1 "N[:alpha:]NNN" SRR098026.fastq

cp SRR097977.fastq dir_dont_exs/newerfile.fastq

mv SRR097977.fastq ../newerfile.fastq


## Practice practical
### Change your working directory to your gen711 folder with an absolute path
pwd
ls
cd /Users/anderssonnesyn/Desktop/GEN 811/
# may pop up as /GEN\ 811/ after hitting tab
# To get into lab folder with absolute path:
cd /Users/anderssonnesyn/Desktop/gen811/gen811_lab/

### 1. Change your working directory to the 'shell data' folder
cd shell_data
# Above is relative path, below is absolute path
cd /Users/anderssonnesyn/Desktop/gen811/gen811_lab/shell_data

### 2. Use grep to search for a bad read ( any read with 7 uncalled bases in a row )
# First, get into untrimmed_fastq
cd untrimmed_fastq
grep -E 'N{7,}' SRR098026.fastq
# -E flag tells grep to use extended regular expressions (N means number of characters)

### 3. Use the 'B' option to get line above each match
# Use one of the commands in "Notes" above, or do:
grep -B 1 -E 'N{7,}' SRR098026.fastq

### 4. How many lines below each grep line belong to a read?
grep -B 1 -E 'N{7,}' SRR098026.fastq | awk '/^@/{getline; getline; getline; print}' | wc -l
# Answer: 125
# In this code, the grep command with the -B 1 option finds all lines containing the pattern "N{7,}" and displays the line before each match (the read ID line). The output of grep is then piped to the awk command, which searches for lines starting with "@" and prints the next three lines (the sequence line, the "+" line, and the quality score line). Finally, the wc -l command counts the number of lines in the output, which corresponds to the number of lines between the read ID line and the quality score line for each match.
# Note that the output of the wc -l command is the total number of lines between the read ID and quality score lines for all matches. To see the number of lines for each match, you can remove the wc -l command and examine the output. Each line of the output corresponds to one match and shows the number of lines between the read ID and quality score lines for that match.

### 5. Use the 'A' and 'B' options with grep to return the read and info lines for each match
grep -B 1 -A 2 -E 'N{7,}' SRR098026.fastq
# In this code, the -B 1 option tells grep to display the line before each match (the read ID line), and the -A 2 option tells it to display two lines after each match (the read sequence line and the "+" line).The N{7,} pattern searches for 7 or more "N" characters in a row, and the output of grep will include the read ID line, the read sequence line, the "+" line, and the next two lines (which could be additional information for the read or the read quality scores, depending on the format of the FASTQ file). Replace your_file.fastq with the name of your FASTQ file. The output will include the read and info lines for each read that contains 7 or more uncalled bases in a row.
# Can also use command from notes above

### 6. Redirect the bad reads in SRR098026.fastq to a file called bad_reads.fastq
grep -B 1 -A 2 -E 'N{7,}' SRR098026.fastq > bad_reads.fastq
# In this code, the > symbol redirects the output of the grep command to the file "bad_reads.fastq" instead of displaying it on the screen. Replace your_file.fastq with the name of your FASTQ file. The output of this code will be a new FASTQ file called "bad_reads.fastq" containing only the bad reads (i.e., reads that contain 7 or more uncalled bases in a row).


### 7. How many lines are in this file? Paste the command below
wc -l bad_reads.fastq
# output: 996 bad_reads.fastq
# To count the number of lines in a file, you can use the wc (word count) command with the -l option, which counts the number of lines.

### 8. Redirect the bad reads for both fastqs into bad_reads.txt using grep and pipes
grep -B 1 -A 2 -E 'N{7,}' file1.fastq file2.fastq > bad_reads.txt
# In this command, the grep command is used to search for bad reads with 7 or more uncalled bases in a row in both "file1.fastq" and "file2.fastq". The -B 1 and -A 2 options are used to display one line before and two lines after each match, which includes the read ID, sequence, and quality score lines. The -E option specifies that an extended regular expression pattern is used.The grep command is then piped into the output redirection operator >, which writes the output to the "bad_reads.txt" file.Replace "file1.fastq" and "file2.fastq" with the actual names of your FASTQ files. The output of this command will be a new file called "bad_reads.txt" containing the bad reads from both files.


### 9. Determine how many bad read lines are in each of the fastq lines, and compare that with the number of lines in bad_reads.fastq
# First, count the number of bad read lines in each FASTQ file:
grep -c -E 'N{7,}' file1.fastq
# 249 in SRR098026.fastq
grep -c -E 'N{7,}' file2.fastq
# 0 in SRR097977.fastq
# These commands use grep with the -c option to count the number of bad read lines with 7 or more consecutive Ns in file1.fastq and file2.fastq.
# Next, count the total number of lines in bad_reads.fastq
wc -l bad_reads.fastq
# 996 bad_reads.fastq, which is a lot more than the others

### 10. Examine the file to find if there are any extra lines that might be throwing off your count. What did you use to look at the file?
# To examine the bad_reads.fastq file for any extra lines that might be throwing off the line count, you can use a text editor or a command-line tool such as less or head.For example, you can use the less command to view the file and search for any unexpected lines by typing / followed by a search term and pressing enter:
less bad_reads.fastq
# less opens the file
# Then, once the file is open, type the following search command followed by Enter
/^[^@]/
# Or type:
/-
# This will search for any - symbol

### 11. Add your name to the bottom of the bad_reads.fastq
echo "Your Name Here" >> bad_reads.fastq
echo "Anders Sonnesyn" >> bad_reads.fastq

### 12. Add your name to the top of the bad_reads.fastq
echo "Your Name Here" | cat - bad_reads.fastq > temp && mv temp bad_reads.fastq
echo "Anders Sonnesyn" | cat - bad_reads.fastq > temp && mv temp bad_reads.fastq

### 13. Make a script that makes a file of bad reads and then puts your name at the end of new bad reads file:
# You can create a shell script to perform the tasks of finding bad reads, creating a file of bad reads, and adding your name to the end of the file
#!/bin/bash
# Find bad reads
grep -B 1 -A 2 -E 'N{7,}' file1.fastq file2.fastq > bad_reads.fastq
# Add name to end of file
echo "Your Name Here" >> bad_reads.fastq
# To create this script, open a text editor and copy the code above into a new file. Save the file with a meaningful name, such as bad_read_finder.sh.
# Make the file executable by running the following command in the terminal:
chmod +x bad_read_finder.sh
# This command sets the executable bit on the file, allowing you to run it as a script.
# To run the script, simply navigate to the directory where the script is located and type the following command:
./bad_read_finder.sh
# This will execute the script and perform the tasks of finding bad reads, creating a file of bad reads, and adding your name to the end of the file.

### 14. Change the permissions of the file and run the script
# you can change the permissions of a file using the chmod command in the terminal.
chmod +x my_script.sh
# This command sets the executable bit on the file my_script.sh, allowing you to run it as a script.
# To run the script, navigate to the directory where the script is located and type the following command in the terminal:
./my_script.sh
# This will execute the script and perform the tasks defined in the script. Make sure you have the necessary permissions to execute the script. If you receive a permission denied error, try running the chmod command first to set the necessary permissions.

### 15. Run md5sum on scripted_bad_reads.txt and write the output to my_md5sum.txt
# To run md5sum on the scripted_bad_reads.txt file and write the output to a new file called my_md5sum.txt, you can use the following command:
md5sum scripted_bad_reads.txt > my_md5sum.txt
# This command uses the md5sum command to compute the MD5 checksum of the scripted_bad_reads.txt file, and redirects the output to a new file called my_md5sum.txt. The > symbol tells the shell to redirect the output of the md5sum command to a file instead of printing it to the terminal.
# After running this command, you can use a text editor or the less command to view the contents of my_md5sum.txt and verify that the checksum was calculated correctly.

# # # # END OF LAB PRACTICAL PRACTICE # # # # 




# # # # LAB 8 # # # #

git version
# output prints which version of github you have

git clone
# type git clone and paste the copied URL from github on the web
git clone https://github.com/anderssonnesyn/lab-notebook.git

https://github.com/jthmiller/gen711-811-example

# Project: Metabarcoding to compare fish species across US estuaries
/tmp/gen711_project_data/fish

# These are the addresses for the repo's for my lab notebook and project
https://github.com/anderssonnesyn/Fish.git
https://github.com/anderssonnesyn/lab-notebook.git

# # # # END OF LAB 8 # # # #




# # # # LAB 9 # # # #

# ssh into ron
# Metabarcoding to compare fish species across US estuaries
/tmp/gen711_project_data/fish/fastqs

cd Fish/
trouch testfile.txt
echo 'a test' > testfile.txt
ls
git add testfile.txt
git commit -m
git push
# Did not do any of the commands above

# Step 1:
cp /tmp/gen711_project_data/fastp.sh ~/fastp.sh
chmod +x ~/fastp.sh
# ~ will apply the command to your 'home' directory

cd ~
mkdir trimmed_fastqs
# <path to github directory>/fastp.sh <1.poly-g length> <1.path to fastq directory>  <3.path to your output directory>
# Did not do the step in the comment above this line
./fastp.sh 150 /tmp/gen711_project_data/fish/fastqs trimmed_fastqs

# Step 2:

conda env list
conda activate qiime2-2022.8

qiime tools import \
   --type "SampleData[PairedEndSequencesWithQuality]"  \
   --input-format CasavaOneEightSingleLanePerSampleDirFmt \
   --input-path <path to your output directory of trimmed fastqs> \
   --output-path <path to an output directory>/<a name for the output files> \

qiime tools import \
   --type "SampleData[PairedEndSequencesWithQuality]"  \
   --input-format CasavaOneEightSingleLanePerSampleDirFmt \
   --input-path </home/users/aws1020/trimmed_fastqs> \
   --output-path </home/users/aws1020/trimmed_fastqs>/<Output_Files> \
# Have not done this step above

# Step 3:
qiime cutadapt trim-paired \
    --i-demultiplexed-sequences <path to the file from step 2> \
    --p-cores 4 \
    --p-front-f <the forward primer sequence> \
    --p-front-r <the reverse primer sequence> \
    --p-discard-untrimmed \
    --p-match-adapter-wildcards \
    --verbose \
    --o-trimmed-sequences <path to an output directory>/<name for the output files>.qza

qiime demux summarize \
--i-data <path to the file from step above> \
--o-visualization  <path to an output directory>/<a name for the output files>.qzv 

# Denoising step:
qiime dada2 denoise-paired \
    --i-demultiplexed-seqs qiime_out/${run}_demux_cutadapt.qza  \
    --p-trunc-len-f ${trunclenf} \
    --p-trunc-len-r ${trunclenr} \
    --p-trim-left-f 0 \
    --p-trim-left-r 0 \
    --p-n-threads 4 \
    --o-denoising-stats <path to an output directory>/denoising-stats.qza \
    --o-table <path to an output directory>/feature_table.qza \
    --o-representative-sequences <path to an output directory>/rep-seqs.qza

qiime metadata tabulate \
    --m-input-file <path to an output directory>/denoising-stats.qza \
    --o-visualization <path to an output directory>/denoising-stats.qzv

qiime feature-table tabulate-seqs \
        --i-data <path to an output directory>/rep-seqs.qza \
        --o-visualization <path to an output directory>/rep-seqs.qzv
