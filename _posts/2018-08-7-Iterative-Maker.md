*******

*“For me, the best description of hunger is the description of bread. A poet said that once I think. For me, the best description of freedom is what you have in front of you. You're travelling a lot.”*         
**― Werner Herzog, Encounters at the End of the World**

Seriosuly, if you haven't seen it, you should open Netflix immediately... Philosophy and peotry in science.  

![Мистерията на българските гласове  - soundtrack from the movie](https://www.youtube.com/watch?v=aXkdKwHckjU&list=RDMMaXkdKwHckjU&start_radio=1)

![](http://lwlcdn.lwlies.com/wp-content/uploads/2017/03/encounters-at-the-end-of-the-world-penguins-1108x0-c-default.jpg)

***************

I have been working on the improvement of genome annotation pipelinne and I want to share the approach that I have adopted to refine and polish my gene preditions.

Maker can be run in an iterative way and the output from one run can be used to run the second iteration. This can be both done for the gene output and the gene predictor models. I have only improved my predictor models so far but using the genes from one run as evidence for the next run can be also applied.

Maker provides the option ```est2genome``` and ```prot2genome``` which "upgrades" the pure gene evidence to a complete prediction: whenever there is a transcript or a protein that blasts to the genome without the support of the predictors, this will be labelled as "maker_exonerate_est2genome" or "maker_exonerate_prot2genome" and output as predicted gene. This approach is ment to create a draft set of genes that can be used for the creation of models to use in Augustus or SNAP. Notice that this can be only used for the first steps of Maker and that the pipline needs to be run afterwards with the default parameters so setting ```est2genome``` and ```prot2genome``` to 0.

Remember that if you want to use the predicted genes for a HQ model you'll need to check them for completeness and integrity.

Cheers,
