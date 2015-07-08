Suggestions for addressing some of the weed evolution questions
===============================================================

Note: These are some suggestions from my conversation with Ben Furman, a PhD Candidate in the Evans lab (and Ben Evans before that). 

## *THE GOAL*
What are we trying to achieve? Given our evidence of the relationship between native ("wild") and non-native ("agricultural weedy") radish (*Raphanus rapnanistrum*), we are trying to better understand the phylogenetic relationship between *R. raphanistrum* natives and weeds and closely allied (sub)species like *R. sativus* (the crops) and *R.r. landra* and *R.r.maritimus* (*R.r.m* and *R.rl* may represent one closely related species/sub-species). While our genetic analysis based on SNPs and SSR markers suggest (using STRUCTURE and smartPCA) that the weeds are reasonably similar to *R. raphanistrum* native populations, they (the weeds) do appear (in the smartPCA plots) to be somewhat intermediate between *R.r.r*, *R.s* and *R.r.l*. There could be multiple explanations for this. First, it could be simply an artefact of some sort of bottleneck in the weed lineages (which we ought to be able to detect from genome wide reduction in diversity). More likely it could be due to the weed origin either being through a hybridization event between species (creating the weed progenitor) or subsequent (after some initial divergence of the weed lineage) introgression from some of the other sub-species. Finally, there remains a formal possibility of the genetic similarity being due to convergence (but seemingly unlikely in this scenario). I think it is worth pointing out that we also do not know whether the weeds are all from a single evolutionary origin (i.e. whether all populations we describe as weeds have a shared common ancestor).

In initial collaboration with David Tank we did attempt to address some of these questions. The Tank lab examined multiple nuclear and chloroplast genes and assembled some initial phylogenies. While the support seperating *Raphanus* from *Brassica* (and even what has been called Raphanus confusus) is strong, within the *Raphanus* lineage (including *R.r.r* (weeds and natives), *R.s*, *R.r.l*, *R.r.m*) is not great.

Thus we would like to try to accomplish a few additional things. 

1. Build a good species level phylogeny
2. Distinguish between any of these evolutionary hypotheses discussed above regarding the evolution of weeds?
3. Examine discordance for individual gene trees from the species tree to help assess an understanding of possible hybrid origins or patterns of introgression (assuming an R.r. native like ancestor to the weeds, followed by weed evolution and introgression).
4. Test patterns of molecular evolution along the weed branch of the tree (in particular for genes involved with flowering time).

## What do we have to use
We sequenced ESTs from multiple tissues from 6 individuals (see the [RadishDB](http://radish.plantbiology.msu.edu/index.php/Main_Page)). Three from *R. sativus* domesticated cultivars (*convars, sativus, causatus, oleifera*). One from a New York weedy population of *R.r* (same population that we used for the genome sequence as described in [Moghe et al. 2014](http://www.plantcell.org/content/26/5/1925.long), one *R.r.r* from Spain in the presumed native range, and one each from *R.r.m* and *R.r.l* from Coastal Spain and France respectively. As Described in Moghe et al, these ESTs were assembled into contigs (and orthology, although not at the population level, was initially assessed in that paper). Also, there is lots of available data for a number of *Brassica* spp. which may be useful for outgroups (?).

After a very fruitful conversation with Ben Furman (who also mentioned that we consider using [`CLUMPP`](https://web.stanford.edu/group/rosenberglab/clumpp.html) for our STRUCTURE runs to help correct for label switching and compute meaningful averages across runs). I think our goals (in general are as follows).

1. Align sequences and identify orthologs for further "gene"/"ortholog" level analyses.
2. Build Gene trees
3. Build Species trees from gene trees.
4. Identify discordant gene trees (discordant from gene trees) to help(?) assess introgression/hybridization hypotheses.
5. Examine patterns of molecular evolution along particular branches (i.e. the "weed" branch of the tree) to identify potential targets of selection (in particular for flowering time genes).


## Details for each step (based on my conversations with BF).

### Step 1. Align sequences and identify orthologs.
Given that there was the "recent" genome duplication prior to the split of *Raphanus* and *Brassica* ~25MYA, one important issue to deal with is assignment of orthology. [Moghe et al. 2014](http://www.plantcell.org/content/26/5/1925.long) describes two pipelines to assess orthologs (see methods and Supplementary Figure 3). I am not enough of a genome duplication wizard to know whether this is sufficient. However, BF suggested a few alternatives. The mostly widely used approach is from [`OrthoMCL`](http://www.orthomcl.org/orthomcl/), although BF suggested that the results are "unsatisfiying" (presumably not very reliable or robust). He suggested an alternative pipeline based on building and parsing gene trees using [`RAxML`](http://sco.h-its.org/exelixis/software.html). 

First align sequences using [`MAFFT`](http://mafft.cbrc.jp/alignment/software/) or [`MACSE`](http://bioweb.supagro.inra.fr/macse/). While `MACSE` is slower, it is codon aware (which would be useful). BF suggests first aligning with `MAFFT`, then `MACSE` to improve the alignment (which slightly speeds up the whole process). After sequences are aligned, use `RAxML` to build the gene trees and assess paralogs from orthologues.  

### Step 2. Build gene trees.
General note (from BF). For building gene trees only use genes that have at least 300bp of aligned sequences. Also, some tools downstream from here can handle missing data (i.e. no sequence for a particular gene for a particular species), while others cannot. One thing to keep in mind for our data is that we can probably use either the sequence from *R.r.m* or *R.r.l* (and can substitute one for the other if the sequence is missing from one of the two individuals). However, we likely do not need to include both.

Once orthologous sets of genes are determined and aligned you can re-build the gene trees in `RAxML` (or can you use the ones from step 1). I gather there is some approach (bootstrapping?) to assess uncertainty, and this uncertainty can be used to propogate error downstream for the species tree assessment.  There are also some Bayesian approaches (where the uncertainty can be assessed from the posterior distribution generated from the MCMC iterations). One of these is [`BEAST`](http://beast.bio.ed.ac.uk/) which builds time calibrated gene trees (chronograms), and thus additioanl information (about the timing of divergence?) may be required. An alternative is [`MrBayes`](http://mrbayes.sourceforge.net/) where the clock is optional. I think one of these can handle missing data, and one cannot (BF, can you clarify?).

A lot of computer time later, and now we have gene trees.

### Step 3. Build species trees from gene trees.

There are a number of tools that can be used to build the species trees from the gene trees. BF particularly like [`mp-est`](http://code.google.com/p/mp-est/). This just takes in the gene trees as inputs (i.e. from `RAxML`). You can also use the consensus tree from `BEAST` and sample from the posterior to generate support for branches on the species tree. In additional to the command line version there is [`STRAW`](http://bioinformatics.publichealth.uga.edu/SpeciesTreeAnalysis/) which seems to be a webserver for this and a few other tools.

BF also suggested that `*BEAST` (q for BF.. is this part of BEAST?) is very useful (and the *BEAST paper has a useful discussion on discordant gene trees) to build a time calibrated phylogeny. In its model it allows for incomplete lineage sorting. However it is quite slow. I can't remember but this may not be able to handle missing data (i.e. missing sequences from particular lineages). 

Other tools (STAR, bucky). However these seemed to get a bit of a meh from BF.

### Step 4. Discordance of gene trees from species trees.

BF suggested that he was unaware of specific tools to assess discordance. BF has written a number of custom scripts and suggests looking at many of the tools in the `R` libraries `ape` and `phytools` (and Liam Revell's blog on all things phylogenetics in `R` with many examples... also R-sig-phylo). However, BF may have some scripts that can also help us along the way. Basically we can count the number of gene trees that are discordant and see if there is a systematic bias (i.e. if most of the discordant gene trees actually share a particular typology). We could then overlay these onto the syntenic map (to assess introgression).  He suggested a paper from Rosenberg and Dagnan (but I could not find it) for some useful discussion on these issues.

### Step 5. Assess branches for change in rates along the gene trees 

To examine whether the branch of the phylogeny leading to the weeds shows accelerated substitution rates (etc) BF suggested [`PAML`](http://abacus.gene.ucl.ac.uk/software/paml.html). In particular using codeML (branch model) to detect such variation in rate. We can then assess if there is an over-representation of flowering time genes (etc..)

