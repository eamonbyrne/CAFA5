# CAFA5 Protein Function Prediction competition on Kaggle
https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/overview

## Erdos Institute Data Science Bootcamp, May 2023

### Project team: Eamon Byrne, Ness Mayker Chen, Dustin Nguyen, Salma Bassem

### Introduction

**Motivation:**
Proteins are important. Accurate assignment of biological function to a specific protein is critical to understanding life at the molecular level. This is ultimately required for curing diseases and making developments towards improving overall human and animal health.

**Problem:**
Proteins can have multiple functions, and may be dependent on interaction with other proteins. There is a huge amount of complexity in assigning function with respect to sequence or structure. Fundamentally, proteins consist of sequences of amino acids, similar to words in a sentence. 
- 142,246 proteins          
- 31,466 functions
- Most labeled-protein has 815 functions
- Most proteined-function has 92,912 proteins 

**Data Label Organisation**
Gene Ontology (GO) data maps out protein functions as “parent”/”child” relationships. This is a directed acyclic graph (DAG). Each "child" node can have multiple "parents", each "parent" can have multiple "children".

Top-level labels are Molecular Function (MF), Biological Process (BP) and Cellular Component (CC).

**Challenge:**
Accurately assign the function of each protein, including all parent functions.

**Goal:**
Develop a model that is able to predict the biological function of a set of proteins based on their amino acid sequence and other data. 

**Evaluation:**
The evaluation statistic of the CAFA5 competition, “F-measure”, is a modified F1-score, that takes into account the precision and recall of the model, as well as the information content of each label (given the relative location of that label within the directed acyclic graph, called "information accretion" (IA)), for each of three test sets (MF, BP, CC).

### Outline of Computational Pipeline
Each *instance* is a protein with a particular amino acid sequence. 
The *features* are the embeddings that have been pre-trained upon the amino acid sequences. 
Each *label* is a biological function that has been experimentally determined.

1. Labels - Generate a (truncated) array of labels (multi- one-hot encoded) from the starting data (a list of protein+function pairings).
2. Features - Load pre-trained embeddings as features.
3. Model - Train a multilabel classification model using the embeddings as inputs.
4. Evaluation - Evaluate model on held-out set of protein sequences.

Example Notebook file for computational pipeline: https://github.com/eamonbyrne/CAFA5/blob/1bef5ca919da4793379f7efb5a36e1204c5f9ca4/30may2023-t5-neuralnetwork.ipynb

 ### Deeper dive into structure within protein sequence embeddings

Notebook for UMAP analysis and visualisations for protein sequence embeddings: https://github.com/eamonbyrne/CAFA5/blob/main/embeddings-esm2-vs-t5-vs-protbert.ipynb
