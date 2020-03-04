# PLANNED ANALYSES FOR PHYLOGENETIC ANALYSES OF HOLOTHUROID MELANOTRANSFERRINS 
 Principle Investigators: Joseph Ryan and Joshua Medina Feliciano  
 Draft or Version Number: v.1.0
 Date: 4 March 2020
 Note: this document will be updated (updates will be tracked through GitHub)

## LIST OF ABBREVIATIONS

* mtf  - melanotransferrin
* *Hglab* - *Holothuria glaberrima*
* *Ajapo* - *Apostichopus japonicus*
* *Spurp* - *Strongylocentrotus purpuratus*
* *Skowa* - *Saccoglossus kowalevskii*
* *Hsapi* - *Homo sapiens*
* *Bmori* - *Bombyx mori*

## 1 INTRODUCTION: BACKGROUND INFORMATION AND SCIENTIFIC RATIONALE

### 1.1 _Background Information_

The melanotransferrins of Holothuria glaberrima have been described from RNA transcripts. 

### 1.2 _Rationale_

This paper investigates the genomic organization and architecture of these genes.

### 1.3 _Objectives_

Accurately classify holothurid melanotransferrins and identify when in evolutionary time did this family expand.

## 2 STUDY DESIGN AND ENDPOINTS

#### 2.1 Build dataset.

We will start with the four melanotransferrins identified in *Holothuria glaberrima* and use these sequences to identify recipricol best BLASTP hits. We will align these sequences MAFFT and remove columns that fall upstream, downstream and between the two transferin domains. We will provide the commandline used to trim these columns. 

```
mafft all_mtf.fa
```

#### 2.2 Run IQTREE tree

```
iqtree-omp -s [infile.mafft-gb] -nt AUTO -bb 1000 -m TEST -pre [output prefix] > iq.out 2> iq.err
```

#### 2.3  RAXML with 25 starting parsimony trees and 25 random starting trees; the best fit model will be determined from the previous IQTREE run.

```
raxmlHPC-SSE3.PTHREADS -f a -x 420 -# 100 -T 25 -p 420 -# 25 -m PROTGAMMA[best-fit_model] -s [alignment_file] -n [name]_mp
```
```
raxmlHPC-SSE3.PTHREADS -f a -x 420 -# 100 -T 25 -d -p 420 -# 25 -m PROTGAMMA[best-fit_model] -s [alignment_file] -n [name]_rt
```

#### 2.4 COMPARE Iqtree and 50 rax trees using rax to report the likelihood values; generate a likelihood score using RAxML for Iq-tree and grep for the likelihood values from RAxML_info files for RAxML runs.

```
raxmlHPC-SSE3 -f e -m PROTGAMMA[best-fit_model] -t [single-gene_tree] -s [alignment_file] -n [output_name]
grep 'Starting final GAMMA-based' *info*
```

#### 2.5 How we will report results

* Report the best tree from previous step as a figure in the main paper. Report all other trees in this repository. Mention any difference in topology in the main paper if they exist.

## 3 WORK COMPLETED SO FAR WITH DATES

A phylogeny was published in 2017 (Hernandéz-Pasos, 2017). We have not conducted any of these analyses prior to March 4, 2020.

## 4 LITERATURE REFERENCED

Hernández‐Pasos J, Valentín‐Tirado G, García‐Arrarás JE. Melanotransferrin: new homolog genes and their differential expression during intestinal regeneration in the sea cucumber Holothuria glaberrima. Journal of Experimental Zoology Part B: Molecular and Developmental Evolution. 2017 May;328(3):259-74.

## APPENDIX


