# Part of Speech Tagging Experiments

This project tests three ways to train a part of speech (POS) tagger using the UD English EWT dataset. We compared a fully trained DistilBERT model, a DistilBERT model with its lower layers frozen, and a CharCNN + BiLSTM model trained from scratch.

We measured overall accuracy and accuracy on counter prior words. A counter prior word is a word whose correct tag in the test sentence differs from its most common tag in the training data.

## How We Trained the Models

**Full DistilBERT:** We trained all model layers and the POS tagging head.

**Frozen DistilBERT:** We kept the embeddings and first three transformer blocks fixed. We trained the remaining blocks and the POS tagging head.

**CharCNN + BiLSTM:** We trained the model from scratch without pretrained weights. We ran four experiments with different learning rates and dropout values.

## Scratch Model Data

| Item | Value |
| :--- | ---: |
| Dataset | UD English EWT |
| Training sentences | 2,000 |
| Validation sentences | 300 |
| Test sentences | 500 |
| Test words | 6,096 |
| Counter prior test words | 354 |
| Pretrained weights | None |

## Model Comparison

| Model | Overall Accuracy | Counter Prior Accuracy |
| :--- | ---: | ---: |
| Full DistilBERT | **94.7%** | **82.5%** |
| Frozen DistilBERT | 94.0% | 79.7% |
| Scratch model, Run 1 | **92.5%** | 76.0% |
| Scratch model, Run 2 | 92.2% | 74.6% |
| Scratch model, Run 3 | 92.3% | **76.6%** |
| Scratch model, Run 4 | 92.1% | 74.6% |

## Scratch Model Training Settings

| Run | Learning Rate | Dropout | Word Dropout | Overall Accuracy | Counter Prior Accuracy |
| :---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 0.002 | 0.35 | 0.15 | **92.5%** | 76.0% |
| 2 | 0.001 | 0.35 | 0.15 | 92.2% | 74.6% |
| 3 | 0.0015 | 0.35 | 0.15 | 92.3% | **76.6%** |
| 4 | 0.0015 | 0.30 | 0.15 | 92.1% | 74.6% |

## Scratch Model Results by Word Group

| Word Group | Run 1 | Run 2 | Run 3 | Run 4 |
| :--- | ---: | ---: | ---: | ---: |
| Counter prior | 76.0% | 74.6% | **76.6%** | 74.6% |
| Frequent ambiguous | 95.0% | 94.6% | **95.1%** | 94.9% |
| Prior consistent | 98.1% | 97.9% | 98.1% | **98.2%** |
| Unseen words | 77.5% | **78.2%** | 75.9% | 75.4% |
| Rare seen words | **87.2%** | 85.4% | **87.2%** | 87.0% |

## What We Found

The full DistilBERT model had the highest overall accuracy at **94.7%** and the highest counter prior accuracy at **82.5%**.

For the scratch model, Run 1 had the best overall accuracy at **92.5%** using a learning rate of **0.002**. Run 3 had the best counter prior accuracy at **76.6%** using a learning rate of **0.0015**.

Run 2 had the highest unseen word accuracy at **78.2%**. Reducing dropout from **0.35** to **0.30** in Run 4 did not improve overall accuracy or counter prior accuracy.

These are the results from the four scratch runs. They show which settings worked best in these tests, not which settings will always work best.
