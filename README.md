# Bioinfo Project 2023
## UPDATE DATE: 15 March 2023
This repository contains materials for the bioinfomatics project (2023 L3 INFO Paris-Saclay).
The goal of this project is to identify biomarkers associated with ALS disease. 
To do this, you have access to RNA-Seq sequencing data from post-mortem brain cortex biopsies from individuals who had ALS and others who did not.

The data for this project comes from the study "Postmortem Cortex Samples Identify Distinct Molecular Subtypes of ALS: Retrotransposon Activation, Oxidative Stress, and Activated Glia" by Tam et al. The full study can be found [here](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6866666/).

## Introduction

This README will guide you throughout the project and your analyses. All steps below must be completed. Unless explicitly stated otherwise in the document (E.g., the mandaotry instructions), you have full freedom regarding the different options available to accomplish all tasks, especially concerning the coding.
This document will be updated at each session. 
Refer to the update date above.

You will work in pairs, from the begining. 
You are allowed to discuss with other pairs, but no direct code sharing (copy/paste etc). 
During all the project, note precisely your personnal contribution and the contribution of your pair.
You be asked for this during the last session (~15 min oral presentation). 

During each of the first sessions, you will be given lessons/introductions on notions you may not have yet. 
Once this lessons start, stop all of your activities and follow the lessons, even if you are familar with the concept.

At the end of your project, you must send by email (phd.rinaudo@gmail.com):
- All your code,
- A report containing the result of your analyses,
- A text file (.csv, .txt...) contaning the ordered list of your top 100 genes (first = better).

The email must have the subject: "Projet_bioinfo_2023_nom1_prenom1_nom2_prenom2" and contains an archive named: "nom1_prenom1_nom2_prenom2" with all the listed requirements.

Note: It is possible to mix code and report in a notebook, and to mix notebook and independent code. 
However, the report must be contained in a single document.
The criteria for evaluation will be (in order):
- Compliance with instructions,
- Clarity of code,
- Clarity of the report,
- Relevance of the code,
- Results found.

## Mandatory general instructions:
- The programming language used must be Python (and only Python),
- No dependencies other than Python modules should be used (Jupiter notebooks accepted),
- Unzipping your archive will produce a folder name "nom_prenom", this is "your folder",
- The code should run once your folder is placed in this repository (i.e. use relative paths only!!),
- The code should not produce any file outside of your folder,
- The code must be commented,
- The code must follow PEP 8 as much as possible,
- The code must contain unit tests,
- The code must be object-oriented.

Note: the objective is to perform an analysis. Therefore, you should not (necessarily) aimed to produce a bioinformatic pipeline robust to changes in the data format for example.
However, it is expected that you ensure that all analyses are correct, in a way or in another.

## Final note:
You will find in the following several steps to help you for the analysis of the data. 
Some steps will tell you exactly what to do, and some will be very open, requiring an investigation and a reflexion. 
Before coding an analysis you could have imagined, present it to me so that I can advise you. 
Also do not rush the avalaible steps, follow the cadence of the sessions. 
For difficult steps, I will initiate and conduct the reflexion. 

# Step 1 - Data Preprocessing
You have access to the raw data of the study in the folder "Data".
This folder contains two information:
- The RNA counts of each sample,
- An annotation file, giving information on the experiment, and (more interestingly) the samples.

Download the data and start to preprocess them.

## Gather RNA counts
To analyze the samples, you will need to merge them into a single Python object.
One standard way to do this is to build a dataframe (or any "table like" struture) such as each row is "sample" and each column is a "gene". Make sure to test your dataset, so that if you change something later on, errors can be catch easily.

Don't forget that the code should be object-oriented.

## Gather sample annotations
The sample annotations are all placed in a unique "xml" file. First, open the file with any text editor, and try to understand its architecture. Then, identify the information that could be relevant for your analysis. 

Finally, create a dataframe (or any "table like" structure) such as each row is a samples and each column an annotation. Make sur to test your dataset (gene counts+annotations) so that you can catch any error in the next steps.
## Make first preprocessing functions
By now, you should already have at least one class in your code, with associated getters and setters. 
Think about other preprocessing functions that could usefull for the next steps. 

# Step 2 - Descriptive analysis
The descriptive analysis covers all kind of analyses that are direct description of the data, such as computing mean, standard deviation, histogram, boxplot...

## RNA counts description:
For each gene, compute the mean, the median and the standard deviation. Find a way to efficiently report all those data, and make your first interpretation. *Spoiler* : you may have to transform/manipulate the data.

Samples correspond to different individuals, to ALS or control individuals etc... Think about what kind of subsets you could analyse and why (and do the analysis!).

## Samples description:
For each sample, compute the mean, the median, the standard deviation. Find a way to efficiently report all those data. As for the RNA counts, think about which subsets you can analyse. 

## Start your report
At this step, you should have already begin your report. 
Before going futher, clean your code and refine your report.

# Step 3 - PCA
As you may have observed, the number of genes is far too high to compare all samples using all genes with simple analyses. 
The PCA is a classical first step analysis in those cases, and offers (among other things) a good way to visualize your data.
To understand what a PCA is, let's check at my favorite youtube channel:
[StatQuest: PCA Step-by-Step.](https://www.youtube.com/watch?v=FgakZw6K1QQ) 
We will review the video together, wait for me please.

To implement a PCA in python, a simple way is to use the PCA function in the sklearn.decomposition package. 
Scikit-learn is a wonderfull Python library, and contains a lot of "must-have" features needed for a data-scientist. 
Take some time to visite the official [website.](https://scikit-learn.org/stable/)
For a pratical python PCA tutorial, let's check again a [Josh Starmer's video](https://www.youtube.com/watch?v=Lsue2gEM9D0&ab_channel=StatQuestwithJoshStarmer).

Now, perform a PCA and plot the samples using their coordinates in the first PCs. 
TIPs: to select the good number of PCs, compute the percenatage of variance their capture.
Use the annotations to color your plots, and see if you can already observe some kind of signal.

PCA is also good way to find outliers. 
Outliers are samples that are greatly different from the other samples. 
The difference should be "huge", so that only experimental errors could explain it.
Using the PCA and visualization, look at possible outliers.

# Step 4 - tSNE and UMAP
Another (more recent) good vizualization tool for high dimensional data is the [t-SNE](https://www.youtube.com/watch?v=NEaUSP4YerM&ab_channel=StatQuestwithJoshStarmer), and it's little brother, the [UMAP](https://www.youtube.com/watch?v=eN0wFzBA4Sc&t=482s&ab_channel=StatQuestwithJoshStarmer). 
The advantage of this two methods is that they can reduce the dimension of your data using a desired number of of component (2 most of the time), not leaving alway a part of your data variability (in theory). 
On the other hand, they do not preserve large distance interpretation, so that only "local similarities" must be interpreted (e.g., outliers are much more difficult to spot). 
UMAP tends to preserve much better large distances, but still not reach the PCA in this topic.

Try to implement a t-SNE and/or a UMAP. 
UMAP can be implemented using the "umap" module, whereas t-SNE has a scikit-learn implementation. 

Compare this visualition vs the PCA one.


# Step 5 - Univariate analysis
We have started to explore our data by computing basic statistics, making visualizations etc... 
Now it's time to perform more advanced analyses, making use of more advanced statistical background. 

In modern datascience, we are used to manipulate complexe algorithm, like ensemble methods or even more complex methods, like deep learning algorithms. 
However, results found using those algorithms can be hard to interpret.
Therefore, standard univariate analyses are always a good idea to start a data analysis. 
From all univariate analyses, the student-test, or t-test, (and in less extend the wilcoxon test) is one of the simplest and powerful method. 
This test rests on [hypothesis testing](https://www.youtube.com/watch?v=0oc49DyA3hU), making interpretation extremely straightforward (thanks to the sacrosanct [p-value](https://www.youtube.com/watch?v=vemZtEM63GY))

The t-test compare the means of a selected variable (here RNA counts) of two different groups (e.g., control vs ALS persons). 
Therefore, to investigate the data using a test, you will have to perform one t-test per gene, resulting in as many results as genes.
In your opinion, could this be a problem? 
To implement a t-test and other frequestist tests, [scipy.stats](https://docs.scipy.org/doc/scipy/reference/stats.html) contains a good sets of functions.

## TO BE CONTINUED# ALS_project
