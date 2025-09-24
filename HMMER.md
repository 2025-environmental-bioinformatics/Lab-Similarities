# 🧮 Lab HMMER

[HMMER](http://hmmer.org/) implements methods using probalistic models (profile Hidden Markov Models, HMMs) to search sequence databases for sequence homologs. HMMER is designed to detect remote homologs as sensitively as possible, relying on the strength of its underlying probability models. HMMER can also work with query sequences, not just profiles, just like BLAST.

HMMER can be run [interactively](https://www.ebi.ac.uk/Tools/hmmer/) or through the command line. The complete manual of the software can be found [here](http://eddylab.org/software/hmmer/Userguide.pdf). Briefly:

- The programs `hmmbuild`, `hmmsearch`, `hmmscan`, and `hmmalign` are the core functionality for protein domain analysis and annotation pipelines, for instance using profile databases like Pfam (now incorporated in [Interpro](https://www.ebi.ac.uk/interpro/)).

  **`hmmbuild`** builds profile from input multiple alignment

  **`hmmalign`** makes multiple sequence alignment using a profile
  
  **`hmmsearch`** searches profile against sequence database
  
  **`hmmscan`** searches sequence against profile database

- `phmmer` and `jackhmmer` search a single protein sequence against a protein sequence database, akin to BLASTP and PSI-BLAST.(Internally, they just produce a profile from the query sequence, then run profile searches.)

- `nhmmer` is the equivalent of `hmmsearch` and `phmmer`, but is capable of searching long, chromosome-size target DNA sequences. `nhmmscan` is the equivalent of hmmscan, capable of using chromosome-size DNA sequences as a query into a profile database.

For today's short exercise, we will search a manually constructed database located in `/proj/omics/env-bio/2025/collaboration/common_material/SPO-all-DCM-0.8-5.00.proteins.faa`. The database `SPO-all-DCM-0.8-5.00.proteins.faa` consist of all genes from the Tara Ocean metagenomes corresponding to the deep chlorophyl maximum samples from the Southern Pacific Ocean, 0.8 - 5.00um fraction. We want to detect the nitrogenase iron protein (nifH) gene.


### Set up the hmmer environment through mamba
*start a screen session and create your conda environment*
```
conda create -n hmmer
conda activate hmmer
conda install -c bioconda hmmer
```

### Create an HMM profile from an alignement
*navigate to your user directory inside the class folder and make two directories: one to store the hmmer output and the other to store the profile*

Activate you hmmer environment

and create the profile using the alignment
```
hmmbuild nitrogenase.hmm /proj/omics/env-bio/2025/collaboration/common_material/nitrogenase.aln
```

### Perform search 
```
hmmsearch -o SPO-all-DCM-0.8-5.00_nitrogenase.out /proj/omics/env-bio/2025/collaboration/common_material/nitrogenase.hmm /proj/omics/env-bio/2025/collaboration/common_material/SPO-all-DCM-0.8-5.00.proteins.faa
```


### Check out the output file!
*Is it easy to parse out the information you need (e.g. the number of hits)? If not, check the help menu and modify the command to save the parseable table of per-sequence hits to file, the multiple alignment of all hits to another file, and adjust the e-value to be more strigent. We typically use e-3 but in case of nitrogenases e-40 needs to be used due to functional similarity of this protein to other proteins)*

