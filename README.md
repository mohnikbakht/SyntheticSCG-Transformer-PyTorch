# Neural SCG Synthesis Transformer Network

Contributions: 
<p/>
(1) elucidating a
transformer-based generative model that can be used to generate synthetic SCG beats more similar to real human SCG beats
than porcine SCG beats, random noise, and skeleton SCG (see section \ref{Results}) 
<p/>
(2) demonstrating that our synthetic SCG generator model
can generate SCG beats with AO and AC timings that are strongly
correlated with the desired AO and AC parameters input to the model
<p/>
(3) demonstrating that MODWT embedding is superior to other standard 1-D signal embedding schemes for SCG signals,
improving the translation of natural language processing approaches to the SCG realm.
<p/>

## Dataset

For this task we used 5 IRB approved datasets containing SCG recordings from 82 healthy participants (32 females, and 50 males). 

## Motivation

<!-- <p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/motivation.svg" width="700"/>
</p> -->

<p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/figure1.png" width="700"/>
</p>

## Architecture

<!-- <p align="center">
<img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/architecture.svg" width="400" />
</p> -->
<p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/figure2.png" width="400"/>
</p>

1. Noam style learning rate warmup was used as suggested in the Attention is all you need paper.
2. In the post-net, a ResNet was used with one layer linear and 5 layer CNN for better reconstruction of the details.

## Results

For validation, distance metrics were used to calculate distances between the 6 datasets. Sliced Wasserstein, Maximum Mean Discrepency (MMD) were used to measure distance between distributions, and Dynamic-time feature matching (DTFM) was used for waveform based distance which is a metric specialized for SCG signals.

<!-- <p align="center"> 
<img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/results.svg" width="900"/>
</p> -->
<p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/figure3.png" width="900"/>
</p>

## Embedding comparison

Three different Embeddings for SCG beats were explored:

  1. Pretrained tokenizer: Trained an AE to compress SCG beats. Then used the pretrained encoder and decoder fromthisAEto tokenize and detokenize SCG beats, respectively.
  2. Spectrogram: converted SCG beats to spectrogram images
  3. maximum overlap discrete wavelet transform (MODWT): converted SCG beats to MODWT images
<!-- 
<p align="center">
<img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/tokenizer_compare.svg" width="600"/>
</p> -->
<p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/figure4.png" width="900"/>
</p>

## Dimistifying the model

As shown below, the attention matrices show that the s1 and s2 complexes (first and second heart sounds) from the SCG beat are attending to each other and themselves which shows the model has learned the structure of these beats. Also the decoder self attention shows diagonal alignment as well as one of the heads (Head 8) attending to the random subject ID token which introduces morphology randomness for the generate beat.

<!-- <p align="center">
<img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/latent.svg" width="900"/>
</p> -->
<p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/figure5.png" width="900"/>
</p>

## Sample of a generated sequence  

The figure below shows an SCG sequence generated by the model with AO and AC location increasing linearly:

<p align="center">
<img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/sequence.png" width="800"/>
</p>

The figure below shows the ability to vary the morphology using the random ID token while keeping other parameters constant:
<p align="center">
  <img src="https://github.com/mohnikbakht/SyntheticSCG-Transformer-PyTorch/blob/main/figs/morphology.png" width="600"/>
</p>

## Steps taken for each model

1. Hyperparameter tuning using the train and validation set
    - Regularization strength
    - Network architecture
    - Learning rate warmup hyperparameters
2. Retrain on the whole train + validation set
3. Test on held-out test set and record evaluation metrics
    - Distances, t-SNE

<!-- 
### Reports:
- will be added after  -->
