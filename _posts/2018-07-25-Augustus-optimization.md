*******

*“We don't want to focus on the trees (or their leaves) at the expense of the forest.”*         
**― Douglas R. Hofstadter, I Am a Strange Loop**

![Kristina](img/IMG_20180701_124136trees.jpg)

***************

I am recently working with the Augustus colossus which is one of the most important gene prediction tools. It's actually even more important in my case: Augustus, if properly optimized, is able to predict genes with very diverse features. The spruce average intron size, for example, is quite large when compared to the other plant species and Augustus nees to grasp this feature.    
Augustus relies on a species-specific parameters which are provided by the author. Augustus comes with a ```config``` directory containing several species but the closest to spruce is *Arabidopsis thaliana* which genome is quite different from conifers. Given that, I decided to optimize Augustus parameters for having a better prediction during my genome annotation. I want to share the pipeline which I have followed and give some tips for the future adventurers who want to do the same.

First of all you need to define a gene data set which you want to apply for parameters optimizaton. This can be bot used for the HMM metaparameters and the model. 

1. **Gene polishing:** be sure to have a well curated genes data set. The genes should be at maximum 1000 but not below 200. The majority of those do not need to have misassemblies or incomplete gene coordinates. Some "mistakes" can also be included but in a small percentage. You will both need the ```gff``` and the ```fasta``` files of those genes. I've used the genes predicted by Maker which came from *Arabidopsis* parameters, the "closest" species. In this case it's the chicken and the egg story, just pick a close model to start with it.        
  **Validate gene quality** - [gag](https://github.com/genomeannotation/GAG) or Maker QI scores (you can find them in the Maker gff annotation files or the fasta headers). Use long, complete (start and stop codons), introns > 10bp and look for those genes that have long five and three prime UTRs    
  **Check completeness** - [gffread](https://github.com/gpertea/gffread) is a very handy tool that helps you to extract complete gene or transcript sequences. I have used the following options for validating and extracting the HQ genes: ```-UVNJC``` for discarding single exons transcripts (which are not very important for Augustus), CDS with in-frame stop codons, introns with non-canonical splice sites, incomplete or lacking CDS     
  **Remove overlapping genes** - ```bedtoools intersect``` to filter for overlapping genes. Augustus discourages to use those for optimization          
  **Discard similar** - ```Blastp``` to discard genes coding for very similar peptides. The identity threshold I have used is 70% without considering the overall sequence coverage     
  **Format input** - ```gff2gbSmallDNA.pl``` is an Augustus script that helps you to convert to GeneBank format which is the input to ```optimize_augustus.pl```

2. **Multiple runs of parameters optimization:** If you'll still have a large amount of genes, as in my case, you could try to randomly subset several times your dataset and see if you can build a better model. I had around 2,200 genes and I decided to explore several gene combinations. I have used ~600 genes using the others ~1500 as a test set.     
  **Divide training and test sets** with ```randomSplit.pl``` in the Augustus scripts

3. **Make a smooth and possibly fast optimization:** depending by your genome this step can take several days.     
  **Create new species config dir** with ```new_species.pl``` in Augustus        
  **Remember this step!**: train your model with the same training set. Use ```etraining``` in Augustus and the name of the "new" species. This is very important since you only optimize your parameters but it's the gene model that allows you to perform predictinos since it "learns" from your data. Both need to be performed                    
  **Check your accuracy** with ```augustus``` on the test set. I have mainly used the *exon and gene* sensibility as reference

4. **Compare to a reference:** I have indeed used the other species parameters as reference and saw an increase of sensibility for the optimized parameters. Sometimes it is not really necessary to perform optimization since there may be other close species in the Augustus ```config``` directory. The author suggests to check their gene space similarity and syntheny. If it's more similar than 70% than it's not necessary to do go through optimization

Cheers,

### References

- [Augustus](http://bioinf.uni-greifswald.de/augustus/)        
- [Augustus retraining](http://augustus.gobics.de/binaries/retraining.html)
