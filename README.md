# pyCancerSig

#### A comprehensive package to perform tumor mutation profiling and cancer signature analysis from whole genome and/or whole exome sequencing data.

## Installation

Dependencies - Currently, feature extraction of structural variants was based on data generated by FindSV and feature extraction of microsatellite instability was based on data generated by MSIsensor
- FindSV - https://github.com/J35P312/FindSV
- MSIsensor - https://github.com/ding-lab/msisensor

Install the dependencies, then download and install pyCancerSig

```
git clone https://github.com/jessada/pyCancerSig.git
cd pyCancerSig
python setup.py install
```

## Workflow steps

The workflow consists of 4 steps

1. Preprocessing - The purpose of this step is to generate list of variants and/or information related. This step has to be performed by third party software.
    - Single nucleotide variant (SNV) - recommending MuTect2, otherwise Muse, VarScan2, or SomaticSniper.
    - Structural variant (SV) - dependency on FindSV
    - Microsatellite instability (MSI) - dependency on MSI sensor
2. Feature extraction - `cancersig feature` - The purpose of this step is to turn information genereated in the first step into matrix features usable by the model in the next step. The output of this stage has similar format as https://cancer.sanger.ac.uk/cancergenome/assets/signatures_probabilities.txt, which consists of at least 3 columns.
    1. Column 1, Variant type (Substitution Type in COSMIC) 
    2. Column 2, Variant subgroup (Trinucleotide in COSMIC)
    3. Column 3, Feature ID (Somatic Mutation Type in COSMIC)
    4. From column 4 onward, each column represent one sample

    There are subcommand to be used for each type of genetic variation
    - `cancersig feature SNV` is for extraction single nucletide variant feature
    - `cancersig feature SV` is for extraction structural variant feature
    - `cancersig feature MSI` is for extraction microsatellite instability feature
    - `cancersig feature merge` is for merging all feature profiles into one single profile ready to be used by the next step
3. Deciphering mutational signatures - `cancersig signature` - The purpose of this step is to use unsupervised learning model to find mutational signature components in the tumors.
4. Visualizing profiles `cancersig visualize` - The purpose of this step is to visualize mutational signature component for each tumor.

## Usage

```
usage: cancersig <command> [options]
```

Key commands:
```
feature             extract mutational profile
signature           extract mutational sigantures from mutational profiles
visualize           visualize mutational signatures identified in tumors
```

cancersig feature key commands:
```
snv         extract SNV mutational profile
sv          extract SV mutational profile
msi         extract MSI mutational profile
merge       merge all mutaitonal profile into a single profiles
```

## Example

## Feature file format

## Contact

