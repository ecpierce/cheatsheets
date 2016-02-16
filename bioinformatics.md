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


