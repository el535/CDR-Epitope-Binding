# TCR-Epitope-Binding

The recognition of antigens by T-cells and B-cells are a core part of the human immune system's protection against viruses, bateria, and even cancer. This project sets out to predict the binding of T-cells Receptors (TCR) with an Epitope, a part of an antigen that is recognized by the T-cell.

## Data
Three publicly available datasets are used for this project: Adaptive Biotechnologies’ ImmuneCODE database containing putative SARS-CoV-2-specific TCR sequences and their corresponding epitopes [1]; VDJdb: a collection of paired TCR sequences and epitopes from previously published studies, largely in infectious diseases [2]; and McPAS-TCR, a manually curated database of TCR sequences associated with various pathologies and antigens [3]. 

Each entry of the dataset consists of a TCR and an Epitope sequence. Each letter in the sequence represents an unique animo acid. The longest TCR sequence is 36 amino acids long, while the longest Epitope sequence is 18 animo acids long. Examples of TCR and Epitope sequence pairs as well as their Antigen type are shown here:

![Sample Sequences](https://github.com/el535/TCR-Epitope-Binding/blob/main/Project_Images/Sample_TCR_Epitope_Sequences.JPG)

The data only consists of highly tested TCR and Epitope sequences that are known to bind to one another. To balance out the class distribution of the labels, for each valid TCR-Epitope pair, a negative TCR-Epitope pair is created. A unique fact about the datasets is that if a TCR-Epitope pair is not listed in the dataset, it means that said pair does not bind to one another. The negative TCR-Epitope pairs are created using this fact about the dataset. 

## Model
The goal of the project is that given an input of a TCR and Epitope sequence, provide an estimate of the probability that this TCR will recognize this epitope. This probability is then used to predict whether the TCR and Epitope pair binds to each other. An output of 1 denotes that the model predicts that the TCR and Epitope binds to each other, while an output of 0 denotes that the model predicts that the TCR and Epitope does not bind to each other.

Three types of models are created: one baseline Multilayer Perceptron n-gram model, one LSTM model, and two similar Transformer (BERT) models. The LSTM model mimics the model architecture presented in ERGO [4], the previous State of the Art model for predicting TCR-Epitope pairs. A table of hyperparameters and model architecture are shown here:

![Table of models](https://github.com/el535/TCR-Epitope-Binding/blob/main/Project_Images/Model_Table.JPG)

Diagrams of the BERT and LSTM models are shown here:
![BERT_LSTM](https://github.com/el535/TCR-Epitope-Binding/blob/main/Project_Images/Model_Diagram.JPG)

## Results
The main evaluation metrics used for the models are average precision, ROC AUC, and accuracy. Precision-Recall curves and ROC curves for all models are shown here:
![Curves](https://github.com/el535/TCR-Epitope-Binding/blob/main/Project_Images/Curves.JPG)

The BERT-mini model created performs the best overall, having the best Average Precision and ROC AUC out of all the models. The model also beats the LSTM model that represents the previous State of the Art model. 

The model can also provide predictions for amino acid predictions for TCR sequences for a specific Epitope, which is useful in many practical applications of finding TCR-Epitope pairs. Some sample real (left) and BERT-mini model learned (right) TCR sequence motifs are shown below, where the height each letter represents the prediction probability of the animo acid at a given position.

![Sequence_Motifs](https://github.com/el535/TCR-Epitope-Binding/blob/main/Project_Images/Sequence_Motifs.JPG)

Two practical applications for this project are identification of molecular (TCR) biomarkers of viral disease or immune response, such as response to vaccination, and identification of tumorspecific TCRs for potential CAR-T cell therapy.

## References
- [1] Nolan S, Vignali M, Klinger M, Dines JN, Kaplan IM, Svejnoha E, Craft T, Boland K, Pesesky M, Gittelman RM, Snyder TM, Gooley CJ, Semprini S, Cerchione C, Mazza M, Delmonte OM, Dobbs K, Carreño-Tarragona G, Barrio S, Sambri V, Martinelli G, Goldman JD, Heath JR, Notarangelo LD, Carlson JM, Martinez-Lopez J, Robins HS. A large-scale database of T-cell receptor beta (TCR) sequences and binding associations from natural and synthetic exposure to SARS-CoV-2. Res Sq [Preprint]. 2020 Aug 4:rs.3.rs-51964. doi: 10.21203/rs.3.rs- 51964/v1. PMID: 32793896; PMCID: PMC7418738
- [2] Shugay M, Bagaev DV, Zvyagin IV, Vroomans RM, Crawford JC, Dolton G, Komech EA, Sycheva AL, Koneva AE, Egorov ES, Eliseev AV, Van Dyk E, Dash P, Attaf M, Rius C, Ladell K, McLaren JE, Matthews KK, Clemens EB, Douek DC, Luciani F, van Baarle D, Kedzierska K, Kesmir C, Thomas PG, Price DA, Sewell AK, Chudakov DM. VDJdb: a curated database of T-cell receptor sequences with known antigen specificity. Nucleic Acids Res. 2018 Jan 4;46(D1):D419-D427. doi: 10.1093/nar/gkx760. PMID: 28977646; PMCID: PMC5753233.
- [3] Tickotsky N, Sagiv T, Prilusky J, Shifrut E, Friedman N. McPAS-TCR: a manually curated catalogue of pathology-associated T cell receptor sequences. Bioinformatics. 2017 Sep 15;33(18):2924-2929. doi:10.1093/bioinformatics/btx286. PMID: 28481982.
- [4] Ido Springer, Hanan Besser, Nili Tickotsky-Moskovitz, Shirit Dvorkin, Yoram Louzoun: Prediction of specific TCR-peptide binding from large dictionaries of TCR-peptide pairs. BioRxiv, 2020.https://doi.org/10.1101/650861
