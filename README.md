# GeReT

**GeReT** (*Gender-Fair Rewriting Transformer*) is a prototype for rewriting German sentences with generic masculine person terms into context-appropriate, gender-fair alternatives.

The project was developed as part of a bachelor's thesis on transformer-based approaches to gender-fair language rewriting.

## Overview

GeReT fine-tunes the German decoder-only model [`LSX-UniWue/LLaMmlein_120M`](https://huggingface.co/LSX-UniWue/LLaMmlein_120M) on German source–rewrite pairs.

The prototype:

* combines gender-fair reformulation datasets,
* prepares instruction-style training examples,
* splits the data into training, validation, and test sets,
* fine-tunes LLaMmlein with supervised fine-tuning,
* uses a dictionary of gender-neutral alternatives as additional rewriting guidance, and
* supports manually marking relevant terms with double brackets, for example `[[Zuschauer]]`.

## Repository Contents

| File                                      | Description                                                              |
| ----------------------------------------- | ------------------------------------------------------------------------ |
| `lamm_proto.ipynb`                        | Main Google Colab notebook for data preparation, training, and rewriting |
| `lamm_proto.py`                           | Python export of the Colab notebook                                      |
| `gender_dict_geschicktgendern.json`       | Dictionary containing possible gender-neutral alternatives               |
| `data_gendergerechte_begriffe_final.xlsx` | Study data used for the human evaluation                                 |

## Example

Input:

```text
Bei allen Sportarten sind wieder [[Zuschauer]] erlaubt.
```

The marked term is detected and matching dictionary alternatives are added to the model prompt. The model then generates a context-sensitive gender-fair rewrite.

## Setup

The easiest way to run the project is in Google Colab with a GPU runtime.

Install the required packages:

```bash
pip install -U datasets transformers accelerate trl sentencepiece
```

The main dependencies are:

* Python 3
* PyTorch
* Hugging Face Transformers
* Hugging Face Datasets
* TRL
* SentencePiece

## Running the Prototype

1. Open `lamm_proto.ipynb` in Google Colab.
2. Select a GPU runtime.
3. Upload the required local JSONL datasets and `gender_dict_geschicktgendern.json`.
4. Adjust the file paths in the notebook if necessary.
5. Run the cells in order to prepare the data, fine-tune the model, and test the rewriting functions.

Some training files referenced by the notebook are not included in this repository and must be provided separately.

## Data Sources

The training pipeline uses reformulation data from the [Lou gender-fair reformulations repository](https://github.com/UKPLab/lou-gender-fair-reformulations).

The lexical alternatives in `gender_dict_geschicktgendern.json` were collected from [Geschickt gendern – Das Genderwörterbuch](https://geschicktgendern.de/). Please consult the original sources for their respective usage conditions.

## Project Status

This repository contains a research prototype rather than a production-ready application. Model outputs may be grammatically incorrect, alter the intended meaning, or fail to produce a suitable gender-fair formulation. Generated rewrites should therefore be reviewed manually.

## Author

Alexandra Esmundo
::: 
