Suggestions for addressing some of the weed evolution questions
===============================================================

Note: These are some suggestions from my conversation with Ben Furman, a PhD Candidate in the Evans lab (and Ben Evans before that). 

## *THE GOAL*
What are we trying to achieve? Given our evidence of the relationship between native ("wild") and non-native ("agricultural weedy") radish (*Raphanus rapnanistrum*), we are trying to better understand the phylogenetic relationship between *R. raphanistrum* natives and weeds and closely allied (sub)species like *R. sativus* (the crops) and *R.r. landra* and *R.r.maritimus* (which may be one closely related species/sub-species). While our genetic analysis based on SNPs and SSR markers suggest (using STRUCTURE and smartPCA) that the weeds are reasonably similar to *R. raphanistrum* native populations, they (the weeds) do appear (in the smartPCA plots) to be somewhat intermediate between *R.r.r*, *R.s* and *R.r.l*. There could be multiple explanations for this. First, it could be simply an artefact of some sort of bottleneck in the weed lineages (which we ought to be able to detect from genome wide reduction in diversity). More likely it could be due to the weed origin either being through a hybridization event or subsequent (after some initial divergence of the weed lineage) introgression from some of the other sub-species. Finally, there remains a formal possibility of the genetic similarity being due to convergence (but seemingly unlikely in this scenario). I think it is worth pointing out that we also do not know whether the weeds are all from a single evolutionary origin (i.e. whether all populations we describe as weeds have a shared common ancestor).

In initial collaboration with David Tank we did attempt to address this. The Tank lab examined multiple nuclear and chloroplast genes and assembled some initial phylogenies. While the support seperating *Raphanus* from *Brassica* (and even what has been called Raphanus confusus) is strong, within the *Raphanus* lineage (including *R.r.r* (weeds and natives), *R.s*, *R.r.l*, *R.r.m*) is not great.

Thus we would like to try to accomplish a few additional things. 
1. Build a good species level phylogeny
2. Distinguish between any of these evolutionary hypotheses regarding the evolution of weeds?
3. Examine discordance for individual gene trees from the species tree to help assess an understanding of possible hybrid origins or patterns of introgression (assuming an R.r. native like ancestor to the weeds, followed by weed evolution and introgression).
4. Test patterns of molecular evolution along the weed branch of the tree (in particular for genes involved with flowering time).

## What do we have to use
We sequenced ESTs from multiple tissues from 6 individuals (see the [RadishDB](http://radish.plantbiology.msu.edu/index.php/Main_Page)). Three from *R. sativus* domesticated cultivars (*convars, sativus, causatus, oleifera*). One from a New York weedy population of *R.r* (same population that we used for the genome sequence as described in [Moghe et al. 2014](http://www.plantcell.org/content/26/5/1925.long), one *R.r.r* from Spain in the presumed native range, and one each from *R.r.m* and *R.r.l* from Coastal Spain and France respectively. As Described in Moghe et al, these ESTs were assembled into contigs (and orthology, although not at the population level, was initially assessed in that paper).Also, there is lots of available data for *Brassica* spp. which may be useful as for outgroups.

After a very fruitful conversation with Ben Furman (who also mentioned that we consider using [CLUMPP](https://web.stanford.edu/group/rosenberglab/clumpp.html) for our STRUCTURE runs to help correct for label switching and compute meaningful averages across runs). I think our goals (in general are as follows).

1. Align sequences and identify orthologs for further "gene"/"ortholog" level analyses.
2. Build Gene trees
3. Build Species trees from gene trees.
4. Identify discordant gene trees (discordant from gene trees) to help(?) assess introgression/hybridization hypotheses.
5. Examine patterns of molecular evolution along particular branches (i.e. the "weed" branch of the tree) to identify potential targets of selection (in particular for flowering time genes).


## Details for each step (based on my conversations with BF).

### Step 1. Align sequences and identify orthologs.
Given that there was the "recent" genome duplication ~ 
