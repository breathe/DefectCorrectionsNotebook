[![Build Status](https://travis-ci.org/skw32/DefectCorrectionsNotebook.svg?branch=master)](https://travis-ci.org/skw32/DefectCorrectionsNotebook)
[![Coverage Status](https://coveralls.io/repos/github/skw32/DefectCorrectionsNotebook/badge.svg?branch=master)](https://coveralls.io/github/skw32/DefectCorrectionsNotebook?branch=master)

# ** UNDER CONSTRUCTION **

To-do:

- Integration with pylada-defects for LZ icc calculations
- Add tests for LZ Ecor, new pa steps and new functions
- Finish writing paper.md (with sample outputs)

# DefectCorrectionsNotebook: Overview

This project contains a workflow which aims to allow for convenient and explanatory post-processing of charged defect supercells from electronic structure calculations with the all-electron electronic structure software package [FHI-aims](https://aimsclub.fhi-berlin.mpg.de/). There are two major components to the workflow:

1. **DefectCorrectionsNotebook.ipynb** contains all of the processing steps (and explanations) for performing finite-size correction schemes to obtain the defect formation energy for charged defect supercells, for one defect at a time. More information on the correction schemes and processing steps is contained in the notebook. To view a demo of the notebook see [here](https://nbviewer.jupyter.org/github/skw32/DefectCorrectionsNotebook/blob/master/DefectCorrectionsNotebook.ipynb).

2. **DefectCorrectionsDataset.py** allows for running the notebook from the command line for a set of defect supercells data. Further instructions are contained in comments at the top of the script.

Other components of this project include:

- DefectSupercellAnalyses.py: This contains functions used in the notebook workflow that were written for reading in structural information of defect supercells in the geometry file format of FHI-aims ('geometry.in').
- CoffeeConvenienceFunctions.py: This contains functions used in the notebook workflow to automatically generate input files for the [CoFFEE](https://www.sciencedirect.com/science/article/pii/S0010465518300158) software package for performing processing steps for applying corrections to charged defect supercells.
- AtomPotentialAlignment.py: This file contains functions used for performing the potential alignment method with atom-centres and the Kumagai-Oba sampling region (doi: 10.1103/PhysRevB.89.195205) with outputs from FHI-aims, as an alternative to the default in CoFFEE to use planar averages.
- PyladaDefectsImageCharge.py: This file contains functions used for calculating the image-interaction correction from the LZ correction scheme using functions adapted with permission from [pylada-defects](https://github.com/pylada/pylada-defects).
- LogFileSetup.py: This file contains the default format of the log file used to store intermediate processing results from the notebook.
- PlottingFunctions.py: This contains functions called in the notebook to generate various plots.
- DefectCorrectionsCondaEnv.yml: This file stored the conda environment used to run this workflow (see installation instructions below).
- coffee.py: This is the main executable for the [CoFFEE](https://www.sciencedirect.com/science/article/pii/S0010465518300158) package (from version 1.1) that is used in this workflow.
- tests: This directory contains tests for functions written for this workflow and sample data to use with the tests.
- sample_data contains some sample defect data for running the notebook.
- conftest.py is a configuration file for pytest to define the root directory for the testsuite.
- .travis.yml and .coveragerc are files required for Travis-CI and test coverage respectively.

## Installation instructions

First download a copy of the repository. All analysis should be performed from the directory containing the notebook file (DefectCorrectionsNotebook.ipynb). The following information is also contained within the notebook, but is repeated here for completeness.

This workflow uses python3. The most convenient way to setup the python environment for this workflow is to use [Anaconda](https://www.anaconda.com/distribution/). The notebook should be run within this conda environment.

### Option 1: Create your conda env directly from the .yml file

All dependencies present when testing this workflow are listed in DefectCorrectionsCondaEnv.yml. This environment can be re-created using conda with

`conda env create -n chooseYourEnvName --file DefectCorrectionsCondaEnv.yml`

To use this workflow you must then activate this conda environment with

`conda activate YourChosenEnvName`

### Option 2: Create your conda env manually

Alternatively, a conda environment can be created for this workflow and the necessary packages installed one at a time, as outlined below

`conda create -n chooseYourEnvName python=3.6`

`conda activate YourChosenEnvName`

`conda install -c suzannekwallace -c conda-forge coffee_poisson_solver_ko pylada jupyter pytest pytest-cov notebookscripter coveralls`

## License

This software has been made available under a 3-Clause BSD License.

## Code contributions

Contributions to extend the functionality of this workflow are very much welcomed! For this, we welcome contributors to fork their own copy of this repository for local developments before submitting a pull request to merge with this repository. See [here](https://guides.github.com/activities/forking/) for more details on this procedure.

## Relevant citations

Methods used in this workflow are taken from a number of publications and so these should be cited when making use of this workflow. For using the LZ correction scheme, please cite doi: 10.1088/0965-0393/17/8/084002 and pylada-defects for the implementation in this workflow with doi: 10.1016/j.commatsci.2016.12.040. For using the FNV correction scheme, please cite doi: 10.1103/PhysRevLett.102.016402 and the CoFFEE package for the implementation in this workflow with doi: 10.1016/j.cpc.2018.01.011. When using atom centres for the potential alignment with the sampling region proposed by Kumagai and Oba, please cite doi: 10.1103/PhysRevB.89.195205.

## Authors

- Tong Zhu
- Suzanne K. Wallace

## Contact

For any queries or bugs to report, please contact suzywallace501@gmail.com

## Acknowledgements

- Volker Blum (Duke University)
- Nathaniel Cohen for support in the development of this workflow and for the [NotebookScripter](https://github.com/breathe/NotebookScripter) library
- Many useful discussions on defect correction techniques were provided by [Stephan Lany, Anuj Goyal, Prashun Gorai and Vladan Stevanovic](https://github.com/pylada/pylada-defects) (NREL)
- Software packages: [CoFFEE](https://www.sciencedirect.com/science/article/pii/S0010465518300158) and [pylada-defects](https://github.com/pylada/pylada-defects) are used for implementing finite-size corrections to defect supercells with different correction schemes
