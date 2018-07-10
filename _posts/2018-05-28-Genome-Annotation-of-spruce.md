



## Structural genome annotation of White spruce

*******

*“So Zeno is most famous for his tortoise paradox. Let us imagine that you are in a race with a tortoise. The tortoise has a ten-yard head start. In the time it takes you to run that ten yards, the tortoise has moved one yard. And then in the time it takes you to make up that distance, the tortoise goes a bit farther, and so on forever. You are faster than the tortoise but you can never catch him; you can only decrease his lead.”* 
**― John Green, The Fault in Our Stars**
![ouroboros](http://ichef.bbci.co.uk/wwfeatures/wm/live/624_351/images/live/p0/5q/2d/p05q2dlr.jpg)

***************

I have recently started the genome annotation of White Spruce - strain WS77111. For those who does not know: conifers are defined as Gymnosperms and have diverged from the Angiosperm plants in an independent clade.
This is a picture that shows the plants evolution, on the final branches you can see the distinction between angiosperms and gymnosperms, both seed plants, which occurred 290 million years ago.
![PlantsEvolution](https://langdalelab.files.wordpress.com/2015/07/untitled.jpg)
*Langdale Lab - Department of plant sciences*  

The vast majority of the genome assembly and annotations that we have today is made by angiosperms species. At the current moment we only have draft reference genomes of several spices which is a great resource to start exploring the spruce genomics. There are also several genome annotations available on NCBI but those are bound to the current state of the assembly. If it's fragmented and incomplete and also its annotation is partial. Being a pioneer is however something exciting! 

Being a small Lab and not an important consortium, we can oly use one validated software for genome annotation... The best method so far is Maker2 which is a perl wrapper combining other software. Being this my first time running a whole genome annotation I've realized that apparently the most difficult part is to start the software and prepare all the opt/exe scripts. Maker2 has several dependencies and there are different perl libraries that need to be downloaded. Furthermore, in case of an error it is quite complicated to figure out which software did not work. This was only the most apparent difficulty at the beginning of my test runs. There are many-many issues related to genome annnotation and my advise for anyone who wants to start such a big job is to really check the intermediate output and never(-never) automate the pipeline without making a check on the results. Also: even if the software marks the genes as "high quality", those still need to be validated for being complete, protein coding, long enough introns etc.
The flavor of Maker that I run is Maker-P. It took me one week to understand what is that. There is only one page from Yandell lab that explains the pipeline, there is a pubblication coupled to that. It is not much different from Maker2 except that it has more advanced software for repeat masking, detection for tRNA and snoRNA and Pseudogenes. Unfortunately, not all those tools are combined together in an unique scripts and the user needs to assemble the pipeline. Some of the features are already embedded in Maker2 but some others, such as the Pseudogenes pipeline, is totally independent and needs to be run after a first-step of Maker.

My strategy in this case was to perform 2 passes of Maker2. I have tried a couple of approaches that I wanted to compare. 
During the first pass of Maker I tried to run with the default mode - evidence + prediction based (see more details at the bottom of the page with exact maker options). I have also tried the pipeline with only the Evidence base mode and the total number of genes that Maker2 was able to find was higher (for the high quality ones, eAED < 1) for the Evidence based mode. I was able to detect almost the double of genes through the second approach. Probably the model that I have used in Augustus, Genemark and SNAP is not well suiting to spruce genome. I have indeed used the standard species models which belong to A.thaliana for the default evidence + prediction based method.
I will run a second step of Maker and use the best genes from my first step to improve the final annotation.

If you are also a student/staff or new to genome annotation and you need to annotate a highly divergent genome, I have some advises which I have learnt during my self-studying time in the past months:
- Know your genome in terms of expected repeats, gene structure and quality. This is fundamental to succeed
- Be patient and well-prepared. Maker2 is a pipeline that is supposed to run very easily but do not let Maker2 to do everything for you! Check, check, check. Most of the steps can be customized and adapted to the features of your genome
- Compile a list of high quality genes which you have validated with ifferent methods or other tools. The top-notch can be used to train models
- Compare your annotation to others performed by Maker2 to see how good is your performance.
- Put some love and passion in this job even if it looks like very technical. Remember that someone will use your annotated genes and that your work is IMPORANT. 

Cheers,

### References

Genome annotation - Maker2
- [Maker-P](http://www.yandell-lab.org/software/maker-p.html)
- [Maker-dev group](https://groups.google.com/forum/#!forum/maker-devel)
- [Maker training resources](http://weatherby.genetics.utah.edu/MAKER/wiki/index.php/MAKER_Tutorial_for_GMOD_Online_Training_2014)
- [More details about a two step genome annotation with Maker2](https://gist.github.com/darencard/bb1001ac1532dd4225b030cf0cd61ce2)

### Maker2 - opts  
```
#------Gene Prediction - default
* est2genome=0 #infer predictions directly from the EST, 1=yes, 0=no
* protein2genome=0 #infer predictions from protein homology, 1=yes, 0=no
```
