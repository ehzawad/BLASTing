# BLASTing

### installation

install blast+

Blast is not just a tool, rather a collection of tools. And two main important tools of blast are blastn, Nucleotide-Nucleotide blast, and blastp, Protein-Protein blast.

To check whether they are properly install or not:

Protein-Protein Blast
```bash
blastp -h
```

Nucleotide-Nucleotide Blast
```bash
blastn -h
```

Folder Structure:

bioinformatics

        - Procholorococcus
        - SARC-CoV-2


### Additional tools

wget or curl (basic downloader)

### important file format

fasta

fastaq

### file extensions

      > .faa (fasta amino acid)

      > .fna (fasta nucleic acid)

      > .gff (genomic feature format)


### inside Procholorococcus

First, download the procholo_genomic_nucleotide file

then, download the procholo_genomic_feature_format file

Finally, procholo_protein file

### Query sequences

Do a blast search against the genome (.fna) and proteome (.faa)

The genome and proteome will set up as BLAST DATABASES that are to be searched  against


> a query gene sequence: E. coli 16S ribosomal RNA -> e.coli.17.gene.fna

> a query protein sequence: E. coli 16S ribosomal RNA -> e.coli.17.protein.faa

### Formatting the genome and proteome for BLAST

makeblastdb makes the fasta file a "indexed" database and it makes the file searchable

Set up blast database for the protein

```bash
 makeblastdb -in procholo_protein.faa -dbtype prot
 ```

Set up blast database for the nucleotide

```bash
 makeblastdb -in procholo_nucloetide.fna -dbtype nucl
 ```

 makeblast -h


### retrieving specific entries and regions from your BLAST database

use **-parse_seq_ids** flag, and if this option is set, this makes it very easy to retrieve specific sequences from the database using their name or id.


Set up blast database for the protein

```bash
 makeblastdb -in procholo_protein.faa -dbtype prot -parse_seqids
 ```

Set up blast database for the nucleotide

```bash
 makeblastdb -in procholo_nucloetide.fna -dbtype nucl -parse_seqids
 ```

### Sample sequence print

And now if someone wants to print out to the screen the sequence of protein  **AAP99047.1**, they can use the blastdbcmd

```bash
blastdbcmd -entry AAP99047.1 -db procholo_protein.faa
```

for a specefic region, for example, the first 10 **AMINO acids** from this entry, it is also possible to use the **-range** parameter

To run a **blastp** search using the protein query against a protein database:

```bash
blastp -query e.coli.17.protein.faa -db procholo_protein.faa
```
to stream the output into a separate file


```bash
blastp -query e.coli.17.protein.faa -db procholo_protein.faa > ecoli_prot_against_procholo_prot.txt
```

Similarly, it is possible to do a nucleotide query against a nucleotide database

```bash
blastn -query e.coli.17.gene.fna -db procholo_nucloetide.fna
```
to stream the output into a separate file

```bash
blastn -query e.coli.17.gene.fna -db procholo_nucloetide.fna > ecoli_nucl_against_procho_nucl.txt
```


### You discovered a random sequence

Search for this fragment of DNA in the genome of *Prochlorococcus*

```bash
touch discovered_DNA_sequence.fna
vim discovered_DNA_sequence.fna
```

Discovered DNA sequence
```bash
ACTGGCATTGATAGAACAACCATTTATTCGAGATAGTTCAATTACTGTAGAGCAAGTTGTAAAACA
```
Copy and past this into discovered_DNA_sequence.fna

And

```bash
makeblastdb -in discovered_DNA_sequence.fna -dbtype 'nucl'
```

Now search that discovered sequence against the genome of Prochlorococcus marinus

```bash
blastn -query discovered_DNA_sequence.fna -db procholo_nucloetide.fna
```


