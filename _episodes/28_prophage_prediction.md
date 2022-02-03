---
title: "Prophage Prediction"
teaching: 10
exercises: 30
questions:
- ""
- "" 
objectives:
- ""
- ""
keypoints:
- ""
- ""
---

Identifying viral sequences from assembled metagenomes is not limited to entirely viral or entirely microbial sequences. Another important identification use case is detecting prophages. In fact, tools for detecting prophages were some of the first virus identification tools.

>## Discussion: Detecting prophages
> Can you think of reasons why prophages might be easier to detect than free phages?
{: .discussion}

After you have though about why prophages might be easier to detect that free phages, read the section "Identification of virus-host boundraries" in [this](https://www.nature.com/articles/s41587-020-00774-7) paper. The paper is about a tool called checkV that you will hear more about on Thursday. It estimates completeness and contamination of a viral genome, and it also predicts the boundraries between prophage and host genomes.

Look back at the evidence that VirSorter uses to determine whether a contig is viral or not. Which of these types of evidence are also suitable to identify prophages?


>## Challenge: Prophage annotation
>As you have seen in the file *VIRSorter_global-phage-signal.csv*, VirSorter doesn't just determine which contigs are viral, it also detects prophages. Go back to the file and look at the detected prophages (categories 4, 5, and 6). Can you find out whether they are complete or partial prophages? Or where the boundraries are?
>
> > ## Solution
> > 
> > Let's look at category 4 (sure). We will focus on the first x columns of this section, for which the headers are:
> >
> > "Contig_id, Nb genes contigs,   Fragment,   Nb genes,Category, Nb phage hallmark genes, Phage gene enrichment sig"
> > 
> > The corresponding values for the first contig are:
> >
> > Contig_id: VIRSorter_NODE_50_length_17040_cov_25_975213
> >
> > Nb genes contigs: 19
> >
> > Fragment: VIRSorter_NODE_50_length_17040_cov_25_975213-gene_4-gene_16
> >
> > Nb genes: 13
> >
> > Category: 1
> >
> > Nb phage hallmark genes: 2
> >
> > Phage gene enrichment sig: gene_4-gene_16:2.21652167838327
> >
> > So, we can see that genes 4-16 show phage gene enrichment and are predicted to be from a prophage. since we know that there are 19 genes that are classified "Nb" (Non-bacterial), we can assume that this phage is complete.
> {: .solution}
>
> Next, try to find out, where the host-phage boundrary is in terms of nucleiotide position. This information is not available from *VIRSorter_global-phage-signal.csv*, so try to find it in the rest of the results. Are all the genes encoded on the same strand? How many nucleotides are between the genes?
>
> > ## Solution
> >
> > This is a little bit complicated. Sometimes we have to dig to get the information that we want. As you have seen, for contig 50, the prophage is predicted to range from gene 4 to gene 16. In the folder "Metric_files", there is a file which contains the coordinates of each gene on the contig. VirSorter recommends to use the coordinates for all the genes plus 50 nucleotides upstream of the most 3' gene and 50 nucleotides downstream of the most 5' gene. In the case of contig NODE_50, this means that the prophage coordinates would be 1014-15338.
> >
> > Out of the 13 genes, in this region, there is only one gene on the +-strand, while twelve others are on the --strand.
> >
> > The intergenic spaces between the genes are very short, sometimes they even overlap. If you compare the length of the intergenic regions of the predicted prophage to the lenght of the intergenic regions outside of the predicted prophage, you will see that they are very similar. This is probably due to the fact that our dataset is a virome and so we expect almost all of our contigs to be viral and have short intergenic regions.
> >
> {: .solution}
{: .challenge}


{% include links.md %}
