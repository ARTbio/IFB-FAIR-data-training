---
title: "Choix des métadonnées et soumission à l'EBI"
numeroSequence: 3
numeroModule: 3
type: "tp"
description: "L'objectif est de se familiariser avec les métadonnées etsoumettre des données et des métadonnées sur ENA (EBI)"
temps: 1h

prerequisites:
     - Avoir un compte personnel sur l'ENA

tools:
     - omicsBroker
     - Navigateur web

formateurs:
     - heleneChiapello
     - thomasdenecker
     - jeanfrancoisDufayard
     - gauthierSarah
     - fredericdeLamotte
     - pauletteLieby

objectifs:
    - Se familiariser avec les métadonnées
    - (Re)découvrir la structure des métadonnées
    - Identifier les métadonnées indispensables
    - Soumettre des données accompagnées de métadonnées
  
questions:
    - A quoi ressemblent des métadonnées en biologie ?
    - Existe-t-il une architecture à ces métadonnées ? 
    - Comment identifier les métadonnées obligatoires à la soumission des données ?
    - Quels est le lien avec le PGG ?

messages:
    - Collecter/stocker les métadonnées au cours du projet est capital
    - Remplir Opidor régulièrement vous fera gagner du temps lors de la soumission 
    - Les outils de brokering (comme omicsBroker) simplifient grandement la soumission des données et métédonnées

homework:
---

## Introduction

Dans ce TP, nous allons réaliser les différentes étapes entre la collecte des données et la soumission dans une banque internationnale. Nous vous proposons trois jeux de données de séquences pour ce TP :

- Dataset 1 : Un génome bactérien de la bactérie *S. salivarius* ([Télécharger l'archive](https://github.com/IFB-ElixirFr/IFB-FAIR-data-training/raw/main/assets/data/S_salivarius.zip));
- Dataset 2 : Un transcriptome de plante ([Télécharger l'archive](https://github.com/IFB-ElixirFr/IFB-FAIR-data-training/raw/main/assets/data/plante.zip));
- Dataset 3 : Un génome du virus SARS-Cov2 ([Télécharger l'archive](https://github.com/IFB-ElixirFr/IFB-FAIR-data-training/raw/main/assets/data/SARS_Covv2.zip)).

Vous trouverez dans le dossier une fois décompressé, deux fichiers `.fastq.gz`.

**Important** : Ces données sont des données fictives extraites de METAGENOTE. Elles ne sont en rien significatives.

Comme ces données sont des données de séquences, nous allons les soumettre sur l'ENA, la banque européenne de séquences.  

## Partie 1 : Exploration de l'European National Archive (ENA)

![Figure 1](https://www.ebi.ac.uk/ena/browser/assets/ENA-logo.png)

L'European National Archive est une plateforme ouverte et soutenue pour la gestion, le partage, l'intégration, l'archivage et la diffusion de données de séquences. Pour en [savoir plus](https://www.ebi.ac.uk/ena/browser/about).

### Connection à l'ENA

Lors d'un dépôt de données sur l'ENA, il est nécessaire de créer un compte. Lors de ce TP, vous aurez besoin d'un compte personnel si vous souhaitez essayer de soumettre des données TEST. Vous pouvez cliquer [ici pour vous connecter à l'instance de test de l'ENA](https://wwwdev.ebi.ac.uk/ena/submit/webin/). 

## Comment sont gérées les métadonnées sur l'ENA ?

Chaque base de données organise ses données différement. Concernant l'ENA, vous trouverez ci-dessous son modèle d'organisation des données et métadonnées de l'ENA :

![Figure modele ENA](https://ena-docs.readthedocs.io/en/latest/_images/metadata_model_whole.png)

{% include documentation.html 
titre="Extrait de la documentation de l'ENA"
doc = "
- **Study**: A study (project) groups together data submitted to the archive and controls its release date. A study accession is typically used when citing data submitted to ENA. Note that all associated data and other objects are made public when the study is released.
- **Sample**: A sample contains information about the sequenced source material. Samples are associated with checklists, which define the fields used to annotate the samples. Samples are always associated with a taxon.
- **Experiment**: An experiment contains information about a sequencing experiment including library and instrument details.
- **Run**: A run is part of an experiment and refers to data files containing sequence reads.
- **Analysis**: An analysis contains secondary analysis results derived from sequence reads (e.g. a genome assembly),
- **Submission**: A submission contains submission actions to be performed by the archive. A submission can add more objects to the archive, update already submitted objects or make objects publicly available.
" 
source="https://ena-docs.readthedocs.io/en/latest/submit/general-guide/metadata.html"
%}

{% include qcm.html qcmNumber="1" 
question = "Quels sont le ou les objets de l'ENA qui sont associés à un vocabulaire contrôlé domaine dépendant appelé *Checklist* par l'ENA ?"
choices="Study|Sample|Experiment|Run|Analysis|Submission"
reponse="Sample"
%}

## Choisir une checklist correpondant au jeu de données choisi

Une quantité minimale d'informations est requise lors de l'enregistrement des échantillons sur l'ENA et tous les échantillons doivent être conformes à une liste de contrôle (checklist) définissant des valeurs de métadonnées attendues. La liste de contrôle la plus appropriée pour l'enregistrement des échantillons dépend du type de l'échantillon. L'ensemble des checklists de l'ENA sont disponible [ici](https://www.ebi.ac.uk/ena/browser/checklists). 

- Pour le Dataset 1 de la bactérie *S. salivarius* utiliser le mot-clé `pathogen` ;
- Pour le Dataset 2 du transcriptome de plante utiliser le mot-clé `plant` ;
- Pour le Dataset 3 du virus SARS-Cov2 utiliser le mot-clé `virus` ;

{% include question.html
numQuestion=2
question="Quel est le numéro d'accession de la checklist à utiliser pour le jeu de données choisi ?" 
solution="
- Pour le Dataset 1 (le génome bactérien de *S. salivarius*) : [ERC000028](https://www.ebi.ac.uk/ena/browser/view/ERC000028)
- Pour le Dataset 2 (transcriptome de plante) : [ERC000037](https://www.ebi.ac.uk/ena/browser/view/ERC000037)
- Pour le Dataset 3 (génome du virus SARS-Cov2) : [ERC000033](https://www.ebi.ac.uk/ena/browser/view/ERC000033)"
%}

Les checklists sont disponibles au format XML. Vous avez par exemple ci-dessous un extrait de la checklist `ERC000028` :

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<CHECKLIST_SET>
<CHECKLIST accession="ERC000028" checklistType="Sample">
          <IDENTIFIERS>
               <PRIMARY_ID>ERC000028</PRIMARY_ID>
          </IDENTIFIERS>
          <DESCRIPTOR>
               <LABEL>ENA prokaryotic pathogen minimal sample checklist</LABEL>
               <NAME>ENA prokaryotic pathogen minimal sample checklist</NAME>
               <DESCRIPTION>Minimum information required for a prokaryotic pathogen sample</DESCRIPTION>
               <AUTHORITY>ENA</AUTHORITY>
               <FIELD_GROUP restrictionType="Any number or none of the fields">
                    <NAME>Collection event information</NAME>
                    <FIELD>
                         <LABEL>isolation_source</LABEL>
                         <NAME>isolation_source</NAME>
                         <DESCRIPTION>describes the physical, environmental and/or local geographical source of the biological sample from which the sample was derived</DESCRIPTION>
                         <FIELD_TYPE>
                              <TEXT_FIELD/>
                         </FIELD_TYPE>
                         <MANDATORY>mandatory</MANDATORY>
                         <MULTIPLICITY>multiple</MULTIPLICITY>
                    </FIELD>
                    <FIELD>
                         <LABEL>lat_lon</LABEL>
                         <NAME>lat_lon</NAME>
                         <DESCRIPTION>geographical coordinates of the location where the specimen was collected</DESCRIPTION>
                         <FIELD_TYPE>
                              <TEXT_FIELD/>
                         </FIELD_TYPE>
                         <MANDATORY>recommended</MANDATORY>
                         <MULTIPLICITY>multiple</MULTIPLICITY>
                    </FIELD>
                    [...]
                </FIELD_GROUP>
          </DESCRIPTOR>
     </CHECKLIST>
</CHECKLIST_SET>
```

## Partie 2 - Utilisation de l'outil **omicsBroker**

Pour ce TP, nous allons utiliser omicsBroker, un outil de *brokering* développé par l'IFB. Il s'agit d'un prototype permettant d'annoter des données de séquences et de les soumettre à l'ENA.

Pour vous connecter à une instance de démonstration, cliquer sur le lien suivant : [ici](#). Cette instance sera fermer dès la fin du TP. Si vous souhaitez refaire le TP, l'ensemble des étapes d'installation sont décrites sur [GitHub](https://github.com/IFB-ElixirFr/omicsBroker).

- **Attention 1** : omicsBroker est un un prototype qu'il ne faut pas utiliser avec des vraies données pour une vraie soumission !
- **Attention 2** : Avez vous bien lu le attention 1 ?

### Section *Annotation* du menu lattéral gauche

Cette section vous permet de créer un projet, de choisir une Checklist et remplir les métadonnées décrivant vos échantillons.

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/sidebar.png"
alias="Screenshot sidebar"
%}

#### Cliquer sur le lien *Project*.

Créer un projet en renseignant uniquement les champs **obligatoires** : `Title`, `Alias` et `Description`.

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/project.png"
alias="Screenshot Project"
%}

#### Cliquer sur le lien *Samples*

Sélectionner la  checklist identifiée à la question précédente.
{% include rappel.html
text="
- Pour le Dataset 1 (le génome bactérien de *S. salivarius*) : [ERC000028](https://www.ebi.ac.uk/ena/browser/view/ERC000028)
- Pour le Dataset 2 (transcriptome de plante) : [ERC000037](https://www.ebi.ac.uk/ena/browser/view/ERC000037)
- Pour le Dataset 3 (génome du virus SARS-Cov2) : [ERC000033](https://www.ebi.ac.uk/ena/browser/view/ERC000033)
"
%}

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/checklist.png"
alias="Screenshot checklist"
%}

Le tableau dans la partie inférieure de la page 'Metadata table' s'est mis à jour avec les champs correspondant à la Checklist sélectionnée.

Renseigner les champs **obligatoires** demandés en utilisant le contenu du DMP Opidor du Dataset que vous avez choisi :

- [lien DMP Dataset 1](#)  
- [lien DMP Dataset 2](#)  
- [lien DMP Dataset 3](#)


Pour savoir quel type d'information vous devez renseigner dans une cellule, cliquez sur la cellule en question et une notice vous donnera les informations nécessaires dala partie `Descriptions` (droite). Par exemple, ici les informations nécessaires dans la colonne `Platform` :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/metadataDescription.png"
alias="Screenshot metadata table"
%}

Ci dessous, un exemple d'une table remplie :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/metadataTable_withData.png"
alias="Screenshot metadata table with data"
%}

#### Cliquer sur le lien *Files*

Vous avez à votre disposition 2 fichiers une fois l'archive décompressées.
{% include rappel.html
text="
**Pour obtenir ces fichiers** : 
  
1- Vous devez télécharger une des archives suivantes :

  - Dataset 1 : Un génome bactérien de la bactérie *S. Salivarius* ([Télécharger l'archive](https://github.com/IFB-ElixirFr/IFB-FAIR-data-training/raw/main/assets/data/S_salivarius.zip));
  - Dataset 2 : Un transcriptome de plante ([Télécharger l'archive](https://github.com/IFB-ElixirFr/IFB-FAIR-data-training/raw/main/assets/data/plante.zip));
  - Dataset 3 : Un génome du virus SARS-Cov2 ([Télécharger l'archive](https://github.com/IFB-ElixirFr/IFB-FAIR-data-training/raw/main/assets/data/SARS_Covv2.zip)).
  
2- Extraire les deux fichiers présents dans l'archive.
"
%}

Ces deux fichiers vont devoir être *uploader* dans cette onglet (N°1 figure ci-dessous). 

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/fileImport.png"
alias="Screenshot File import"
%}

Une fois *uploader*, vous devez renseigner le md5sum pour s'assurer qu'aucune donnée n'a été perdue lors de l'*upload*. Pour obtenir le md5sum, nous vous conseillons la lecture [suivante](https://knowledge.autodesk.com/search-result/caas/sfdcarticles/sfdcarticles/Checking-the-MD5-checksum-of-a-Downloaded-File.html). Enfin, chaque fichier doit être associé à un `Experience name` (que vous avez renseigné dans la partie précédente). Une fois toutes ces informations renseignées, vous devez avoir quelque chose de similaire à la capture d'écran ci-dessous. 

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/fileImportValide.png"
alias="Screenshot File import complet"
%}

### Section *Publish* du menu latéral gauche

Cette section permet de soumettre les fichiers de données et de métadonnées à l'instance de test de l'ENA
Cliquer sur le lien *ENA*.

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/publishENA_vide.png"
alias="Screenshot Publish in ENA"
%}

Puis renseigner votre webin et votre mot de passe : 

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/publishENA_Ident.png"
alias="Screenshot Publish in ENA connexion"
%}

#### Envoyer les fichiers de données brutes sur l'instance de test de l'ENA

Cliquer sur "Upload data" (Step 3). En cas de succès, un message vous sera envoyé :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/publishENA_data_success.png"
alias="Screenshot File import complet"
%}

#### Envoyer les métadonnées sur l'instance de test de l'ENA 

Cliquer sur "Upload metadata" (Step 4) En cas de succès, un message vous sera envoyé :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/publishENA_metadata_success.png"
alias="Screenshot File import complet success"
%}

#### Décrire les fichiers XML de métadonnées générés 

Cliquer sur les différents fichiers XML générés par la soumission et commenter.

#### Vérifier que la soumission test s'est bien passée

Pour cela, se connecter sur l'instance de test de l'ENA [ici](https://wwwdev.ebi.ac.uk/ena/submit/webin/). Une fois connecté, votre interface doit est comme ci-dessous :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/ENA_home.png"
alias="Screenshot ENA"
%}

En cliquant sur `Studies Report` :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/ENA_StudiesReport.png"
alias="Screenshot ENA Studies Report"
%}

En cliquant sur `Samples Report` :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/ENA_SamplesReport.png"
alias="Screenshot ENA Samples Report"
%}

En cliquant sur `Runs Report` :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/ENA_RunsReport.png"
alias="Screenshot ENA Runs Report"
%}

En cliquant sur `Run Files Report` :

{% include repoImage.html
pathInRepo="/assets/img/TPs/session3_tp1/ENA_RunFilesReport.png"
alias="Screenshot ENA Run Files Report"
%}

{% include question.html numQuestion="3" question="Quel est le numéro d'accession attribué à votre projet par l'ENA ?" %}

### Question Bonus : importation de métadonnées depuis le PGD

Via l'export du PGD en HTML, il est possible de pré-remplir certains items dans omicsBroker. Pour cela, vous devez :

1) Exporter votre PGD au format HTML depuis Opidor.  
2) Importer le fichier HTML dans omicsBroker.  

Commenter les champs importés.