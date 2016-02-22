# Bioinformatics

This is a cheat sheet for bioinformatics command line programs.
#git init can be used to make a repository-isn't that great!
## HOMER motif finding

Use [HOMER](http://homer.salk.edu/homer/ngs/peakMotifs.html) for finding motifs in the genome given bed files.

### For RNA

Build a command using Python

```python
# Search for short motifs, lenghts 4,5,6,7 with up to 1 mismatch
n_processors = 4
homer_flags = '-rna -len 4,5,6,7 -mset vertebrates -mis 1 -p {}'.format(n_processors)
findMotifsGenome = '/home/yeo-lab/software/homer/bin/findMotifsGenome.pl'
command = '{} {} hg19 {} -bg {} {}'.format(
        findMotifsGenome, bedfile, out_dir, background, homer_flags)
```
 
The final command looks like this:

```
findMotifsGenome.pl peaks.bed out_dir hg19 -bg background.bed -rna -len 4,5,6,7 -mset vertebrates -mis 1 -p 4
```

unix:
cd change directory
clear clears screen 
mkdir make directory
rm remove file
rm -rf remove directory
chmod --- <filename> 1st _ is you, 2nd is group, 3rd is others. to set read write execute for all is 777
which <name> can be used to find the full path 

bash profile:
if edit bash profile, have to source to update it in terminal. or open a new window it opens automatically 
bash profile has aliases, env variables. can make alias to change into different directory
nano ~/.bash_profile edit bash profile

viewing files:
cat, less, more.  more spits out everything, less allows to space and scroll, once exit goes back to command prompt, more stays on screen. cat can view but can also join things. cat <x> <y> > <z> combines x and y to output z. if use 2 >> signs, appends. doesnt delete existing z, just adds x and y to end.

text editors- nano, vi, vim

for data movement:
scp fileA tscc... . can also scp from server to IP address 
can scp from tscc onto your computer. scp source destination
ftp server, one way access, doesnt require electronic handshake
wget : can put url to big file, it streams it to you, dont need password. can move large data 
ln -s source destination. soft links allow to access data without moving into home directory. makes a portal. also means you dont have to type the whole path to the data. 


check data integrity:
md5 checks file, see if data is moved properly
ls -ltr can check size of file

git:
git checkout use to change branches
git status tells you what has been modified 
git commit -m "meassage"
git pull upstream branchname(master)

scratch is just someone has given you space on a server somewhere, it has a different origin, a different tree

ucsc genome browser, table, someone has taken peaks and put into bed file? 
pandas is set upthat make dataframe manipulation easier than it is in python 
alignment- need an input dataset "query" and also an index "reference" . alignment algorithms - STAR, kallisto, bowtie, BWA, mozaic.  most align to reference genome. if you want to abundance counts, dont really need to map to everything, found way to not mapping to whole genome, kallisto does psuedoalignment, only maps to subset of expressed things. if want to align to a new exon, use star because aligns to the genome. if looking for something known, use kallisto because only want to map to a subset

databases:
seq datasets:
GEO
SRA
structural info:
Ensemble
UCSC

RNAseq workflow- map, count, stats, analyze
got fastq from the sequencer, want to get biological relevance- find differentially expressed genes with fold changes (gene ontology, compare to exisiting datasets,compare to KEGG look for disease correlation. basically compare to databases
to get to fold change, need to get quantification and do some significance tests 
fastq file align to STAR, give it an index mm8(mouse) or whatever you want to use and also input files (need both index and query
gets to sam, compress it using samtools view otherwise it would take forever,get bam, use samotools sort to get sorted.bam   
can use samtools index for viewing
once get sorted, use featurecounts. featurecounts -a option= annotation (we used gtf file, important ingredient, without it is just genome coordinate, we chose to use basic, could use comprehensive). featurecounts uses the sorted bam and the annotation file as inputs
after featurecounts, do stats

For kallisto, 
fastq, then kallisto quant with annotation of transcripts (annotation is already extracted into smaller file)

if want to do dna seq, still aligning to genome, get different stats, for rna seq care about abundance but for dna seq, interested in variants, need some kind of reference annotation and a tool to call variation. 
if do chip, still map to genome, want abundance, still care about annotaion, where is it mapping (promoter, etc), but not counting on exons, looking for peaks so need a peak calling algorithm
ribo seq- basically the same as rna seq but then do different stats

ctrl a jumps to beginning of line
ctrl e goes to end of line

screen used to start screen. exit to exit screen session. 

boolean false means 0

fastq then align with star then sam file then get sorted indexed bam file then to quantify used featurecounts. kallisto goes directly from fastq to gene expression counts. if use different aligner, may get different results. also if use something other than featurecounts they have their own biases, youll get different numbers. for featurecounts used gencode basic which has lincrna, trna, mirna, protein coding, but for kallisto we only used protein coding. if had used gencode basic with only the protein coding, would have gotten more similar results 

