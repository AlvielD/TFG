# TFG

Bachelor's Final Project, also known as *Trabajo de Fin de Grado* (TFG) in spanish.

## Title of the proyect
(ES) **Detección de noticias falsas mediante técnicas de Deep Learning.**  
(EN) **Fake news detection with Deep Learning technics.**

## Configuration
Although most of the libraries are already installed in the google colab environment, here is a list of requirements:
    
    pandas
    numpy
    sklearn
    keras
    torch
    transformers
    datasets
    sentencepiece
    wandb
    functools
    
Keep in mind you need to have the dataset on your google drive, so you will need to give the colab notebook access to your cloud:

    from google.colab import drive
    drive.mount('/content/drive')
    
This notebook assumes you will have the files in

    '/content/drive/MyDrive/Colab Notebooks/TFG/datasets/fakeNews_spanish/'
    
Try to keep them on that folder, change the code lines where the files path is set otherwise.

## Usage:

In the notebook [train_model](https://github.com/AlvielD/TFG/blob/main/notebooks/train_model.ipynb) it is indicated step by step how to train the models to solve the task. There is a list of models I tested. You can simply uncomment the one you want to try and even change parameters.

    #MODEL_CHECKPOINT = "PlanTL-GOB-ES/roberta-large-bne"
    MODEL_CHECKPOINT = "bertin-project/bertin-roberta-base-spanish" --> Uncomment the model you want to use
    #MODEL_CHECKPOINT = "bert-base-uncased"

There are some options you can change depending exactly on what you want to do.

    # CONFIGURATION OF THE PREPROCESSING AND TRAINING
    # ----------------------------------------------
    SUMMARIZE_DATA = False
    USE_SUMMARIZED_DATA = False
    CREATE_DATASETS = True
    SAVE_MODEL = False
    GENERATE_GRAPHIC = True
    PREPROCESS = 1
    # ----------------------------------------------
    
These options work as follows:
- `SUMMARIZE_DATA`: Previously summarizes the data before training the model. This should usually be combined with `USE_SUMMARIZED_DATA` if you want to use the data you summarized, otherwise you will summarize the data but won't use it.
- `USE_SUMMARIZED_DATA`: Uses the path to the summarized data instead of the default one. If there is no summarized data among your dataset files (this happend when you have never executed the `SUMMARIZE_DATA` option) then it will raise an exception.
- `CREATE_DATASETS`: Create the datasetdict from the splitted files. This is usually needed when you have never executed this task before.
- `SAVE_MODEL`: This saves the model in the path specified by the `SAVE_PATH` variable. Keep an eye on this, you coul **overwrite** a model you don't want to lose.
- `GENERATE_GRAPHIC`: Wether generate a plot on the [weight and biases](https://wandb.ai/site) page or not.
- `PREPROCESS`: Type of preprocessing to be performed on the dataset. Basically, what columns to take from the data, since is not possible to take all of them.
  - `PREPROCESS = 1` - Source + Headline + Text
  - `PREPROCESS = 2` - Source + Topic + Link + Text
  - `PREPROCESS = 3` - Source + Link + Text
  - `PREPROCESS = 4` - Source + Link + Headline + Text
  
There are two other models that uses more complex techniques. These are the "Head and Tail embeding" [[notebook](https://github.com/AlvielD/TFG/blob/main/notebooks/trunc_head%26tail.ipynb)] and the "Ensembles models" [[notebook](https://github.com/AlvielD/TFG/blob/main/notebooks/Ensembles.ipynb)].

To use the *head & tail* notebook you can just choose the model to be used in the same way you did with the previous one.

For the *Ensembles models* notebook instead you have some more personalization freedom:
  - `WEIGHT_RESULT`: Determines wether to weight the results or not. When set to false is the same as giving each model the same weight. If you set it to true you should then define each weight with the variables `WEIGHT1`, `WEIGHT2` and `WEIGHT3`.

You can also define a different preprocessing for each model with the variables `PREPROCESS_MODEL1`, `PREPROCESS_MODEL2` and `PREPROCESS_MODEL3`. 

---

## Documents

There is a technical [report](https://github.com/AlvielD/TFG/blob/main/documents/TechnicalReport.pdf) which describes in depth the objectives of the project, the results and conclusions. It is highly suggested to take a look at it.

You can also check the [presentation](https://github.com/AlvielD/TFG/blob/main/documents/DefencePresentation.pdf). I made to defend the project in front of the jury.

---

## Links

The dataset used for the project is the *[Fake News Spanish Corpus](https://github.com/jpposadas/FakeNewsCorpusSpanish)*
The models used for the fine-tuning on the task are taken from the *[Hugging Face](https://huggingface.co/)* community.

## Special thanks

I want to thank all of the team of $I^2C$ of the University of Huelva for giving me an environment where to work and for standing me every morning. Special thanks to my coordinator Jacinto Mata Vázquez for the corrections on the report and for the support.

I want also to give special thanks to Laura Vázquez Ramos for helping me with the presentation and the support.

Special thanks also to Rainui Ly for introducing me on the use of python and github.

I want to dedicate the cum laude on this project to G.C.
