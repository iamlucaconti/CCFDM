# Sample-efficient Reinforcement Learning through Curiosity Contrastive Forward Dynamics Model


This project is an educational implementation developed for the Reinforcement Learning course (Fall–Winter 2025–26), taught by Roberto Capobianco.

The work reproduces and implements an existing research paper by T. Nguyen et al. (2021). The goal of the project is didactic: to understand, implement, and experimentally analyze the core ideas of the original paper.

The contributors are:
- **Riccardo D'Aguanno** (https://github.com/ricdag8)
- **Luca Conti** (https://github.com/iamlucaconti)


# Introduction
In many real-world tasks, agents observe the world through **raw pixels**. But learning directly from images is **sample inefficient** and **hard to generalize**. Most methods learn spatial features, but ignore **temporal structure** and **curiosity-driven exploration**.

*How can we learn good representations from pixels that make RL sample-efficient and stable?*

# Curiosity Contrastive Forward Dynamics Model
The core idea of **Curiosity Contrastive Forward Dynamics Model** (**CCFDM**) is to learn visual representations by combining:
- **contrastive learning**
- **forward dynamics**
- **curiosity-driven exploration**.

## Contrastive representation learning
The goal of contrastive learning is to learn a latent space where **positive pairs are close** and **negative pairs are far apart**.
Thus, the encoder is forced to learn:
- Physically meaning features
- **Spatial invariances** (augmentation)
- **Temporal structure** (dynamics)

## Curiosity module
Curiosity is derived from Forward Dynamics Model (FDM) prediction error: it transforms the prediction error in the latent space (namely $||q'-k'||$) into an **intrinsic reward** $r_{int}$. The latter is proportional to the **dissimilarity** $||q'-k'||$: novel or unpredictable transitions produces high intrinsic reward.\
 $r_{int}$ is **decayed** during trainign thanks to the term $e^{-\gamma t}$.\
The standard task reward is augmented with intrinsic curiosity.This leads to a more diverse and less repetitive set of observations that improves both representation learning and generalization

# Instruction

The repository contains two Jupyter notebooks:
- one compatible with Gymnasium environments,
- one compatible with DeepMind Control Suite (DM Control) environments.

To run a training session:
- Open the notebook corresponding to the desired environment.
- Navigate to the Training section.
- Modify the training hyperparameters as needed.
- Run the notebook cells sequentially.

During training, the following log line is printed periodically: 
```
EL 00:12:49 | EP 0006 | ts 0003000 | AR_10 -212.9±047.2 | CO_L 1.657 | CR_L 1.428 | A_L -13.960 | EV -38.7±049.2 | 
```

Log abbreviation mapping:

```
EL - elapsed training time
EP - total number of episodes
ts - total number of environment steps
AR_10 - Moving average of episode reward over the last 10 training episodes
CO_L - mean episode contrastive loss
CR_L - mean episode critic loss
A_L - mean epsiode actor loss
EV - moving average reward over the last 10 evaluation episodes
```


# References
1. T. Nguyen, T. M. Luu, T. Vu, and C. D. Yoo, Sample-efficient reinforcement learning representation learning with curiosity contrastive forward dynamics model, 2021

2. T. Haarnoja, A. Zhou, P. Abbeel, and S. Levine, Soft actor-critic: Offpolicy maximum entropy deep reinforcement learning with a stochastic actor, ICML, 2018.
