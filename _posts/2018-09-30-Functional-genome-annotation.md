*******

*“Because in the end, you won’t remember the time you spent working in the office or mowing your lawn. Climb that goddamn mountain.”*       
**― Jack Kerouac**
![Kristina](img/PassAthenley02.jpg)

***************

The genome annotation includes two main steps, structural and functional genome annotation. The first one defines the coordinates of the genes in the genome assembly while the latter assigns putative functions to the discovered genes. Maker-P performs only the first step, the structural genome annotation. The functional genome annotation is performed later through different software that can be combined with the available Maker utilities.          
The functional annotation can be performed in different ways, there are however two main direction where you can go.                   
The first strategy for assigning gene names to your annotations is through the use of functional or structural domains. The most popular database is Pfam which is a collection of protein families based on functional domains. Those are obtained from both HMMs and/or Multiple Sequence Alignments and can be quite handy if your proteins are divergent from other well known species. The most popular tool for functional annotation is [InterProScan](http://www.ebi.ac.uk/interpro/interproscan.html) that looks for sequence signatures. It annotates against other databases such as Panther, Prosite, CDD, etc. and allows the user to include several other features. If you are more interested to know about protein families please check the references on the bottom of the page, there is an extensive tutorial by EMBL-EBI that covers most of the principles.     
The second strategy is to align the annotated genes to genes from other organisms and look for similar sequences. In this case use high identity and coverage if you compare to nucleotide sequences with Blastn (DNA or mRNA), let's say at least 75%; in case you compare to protein sequences with Blastx or tBlastx the threshold for homology is lower, >= 30%. I have compared my annotation to "protein data bank" (pdb) which contains high quality proteins.                 
In the spruce genome annotation I included both the strategies mentione before, both using a Pfam and Blast alignment approaches. The Pfam domains approach covered most of the annotated genes and the Blast alignemnts encompassed the "golden genes data set". The Pfam annoatation covered about 80% of my annotated genes and the Pdb-golden-quality annotation covered 30%.      
Cheers,

### References
* [InterPro, EMBL-EBI](https://www.ebi.ac.uk/training/online/course/interpro-functional-and-structural-analysis-protei)

[![Time to break free](img/GammRay.jpg)](https://www.youtube.com/watch?v=Lq3-6rkCjXw)
