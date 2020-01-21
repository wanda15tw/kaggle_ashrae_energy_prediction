project_temp
==============================

Project template for data science project

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── conf
    │   ├── base           <- Space for shared configurations like parameters
    │   └── local          <- Space for local configurations, usually credentials
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── 01_raw         <- Imutable input data
    │   ├── 02_intermediate<- Cleaned version of raw
    │   ├── 03_processed   <- The data used for modelling
    │   ├── 04_models      <- trained models
    │   ├── 05_model_output<- model output
    │   └── 06_reporting   <- Reports and input to frontend    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── d00_utils      <- Functions used across the project
    │   │   └── remove_accents.py
    │   │
    │   ├── d01_data       <- Scripts to reading and writing data etc
    │   │   └── load_data.py
    │   │
    │   ├── d02_intermediate<- Scripts to transform data from raw to intermediate
    │   │   └── create_int_payment_data.py
    │   │
    │   ├── d03_processing <- Scripts to turn intermediate data into modelling input
    │   │   └── create_master_table.py
    │   │
    │   ├── d04_modelling  <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   └── train_model.py
    │   │
    │   ├── d05_model_evaluation<- Scripts that analyse model performance and model selection
    │   │   └── calculate_performance_metrics.py
    │   │
    │   └── d06_visualisation<- Scripts to produce reporting tables and to create frequently used plots
    │       └── visualise_patient_journey.py    │
    └── tox.ini            <- tox file with settings for running tox; see tox.testrun.org

# Workflow

The typical workflow to develop code is the following:

- Prototype code in a jupyter notebook
- Move code into a function that takes data and parameters as inputs and returns the processed data or trained model as output.
- Test the function in the jupyter notebook
- Move the function into the src folder
- Import the function in the jupyter notebook 
- Test the function is working

Functions can be imported into a notebook as follows.
First we tell the notebook where the functions are

    import os
    import sys
    src_dir = os.path.join(os.getcwd(), '..', 'src')
    sys.path.append(src_dir)

Then we state which functions to import

    from d00_utils.my_fun import my_fun

Try it!

# Code pipeline

The code that produces the different layers of the data pipeline should be abstracted into functions.

A *code pipeline* is a set of code that handles all the computational
tasks your project needs from beginning to end. The simplest
pipeline is a set of functions strung together.

For example,

    int_data = create_int_data(raw_data)
    pro_drug_features = create_pro_drug_features(int_data)
    pro_patient_features = create_pro_patient_features(int_data)
    pro_master_table = create_pro_master_table(pro_drug_features, pro_patient_features)
    model = train_model(pro_master_table)
    rpt_report = produce_report(model)
--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
