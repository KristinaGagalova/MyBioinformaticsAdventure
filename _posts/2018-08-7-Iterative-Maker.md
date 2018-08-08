*******

*“For me, the best description of hunger is the description of bread. A poet said that once I think. For me, the best description of freedom is what you have in front of you. You're travelling a lot.”*         
**― Werner Herzog, Encounters at the End of the World**

Seriosuly, if you haven't seen this documentary, you should open Netflix immediately... 
[Мистерията на българските гласове  - soundtrack from the movie](https://www.youtube.com/watch?v=aXkdKwHckjU&list=RDMMaXkdKwHckjU&start_radio=1)

![Kristina](img/IterativeMaker.jpg)

***************

I have been working on the improvement of genome annotation pipeline and I want to share the approach that I have adopted to refine and polish my gene annotation in Maker.

Maker can be run in an iterative way and the output from one run can be used in the second iteration. This can be both done by using the gene output as an evidence or for the gene predictor models. I have only improved my predictor models so far and this is how I've done it.

Maker provides the option ```est2genome``` and ```prot2genome``` in the maker_opt.ctrl comand file which "upgrades" the pure gene evidence to a complete prediction: whenever there is a transcript or a protein that Blasts to the genome without the support of the predictors, this will be labelled as "maker_exonerate_est2genome" or "maker_exonerate_prot2genome" and annoatted as predicted gene. This approach is ment to create a draft set of genes that can be used for the creation of models in Augustus or SNAP. This is a sort of boothstrapping that allows you to perform the annotation even if you don't have a suitable gene model to start with.    

Notice that this can be only used for the first steps of Maker and that the pipline needs to be run afterwards with the default ```est2genome``` and ```prot2genome``` parameters. Iterative Maker is a powerful tool to start your annotation from a closer species and guide your annotation through a progressive refinement of you gene data set.

Remember that if you want to use the predicted genes for HQ models, you'll need to check them for completeness and integrity too.

Cheers,
