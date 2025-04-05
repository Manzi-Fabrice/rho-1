# Tokenization Project – Rho-1 Implementation

This project implement the Rho-1 model, a method proposed in the paper [*"Not All Tokens Are What You Need."*](https://arxiv.org/abs/2404.07965) Rho-1 is a targeted training approach where a language model is trained only on **hard tokens**, aiming to reduce number of tokens needed and the convergent time. 


> Hard tokens are those tokens where a language model is performing poorly—specifically, tokens that show a large difference between the target model's loss and a reference model's loss.

## Training Procedure

### 1. Reference Model Training

We begin by training a distilled GPT-2 model as our reference model. The model is fine-tuned on high-quality token data sourced from a curated dataset. This is in line with what is proposed in th original paper.

### 2. Selective Token Training with Target Model

A second distilled GPT-2 model is initialized as the *target model*. At each iteration:

- The target model is evaluated using the same input data.
- Loss is calculated between the reference and target model outputs.
- The top **N** tokens with the highest loss are selected as the "hard" tokens.
- The target model is then trained **only** on those hard tokens.

## Limitations

Due to resource constraints, this implementation has some modifications: 

- Uses very smaller subset of tokens
- Fewer training iterations
- A very lightweight architecture

---

