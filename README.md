# language-detection

In this project, we build a language specific RNN using LSTM units for generating sequences of characters and then combine them into a single language detector. We experiment with binary language detection (English vs French) and multi-language detection (variable number of languages).

We trained the data on the text of the ‘Universal declaration of Human rights’ and then randomly sampled 5-character sequences from the test set to test the language detectors.

For binary classification, with a window of length 40 and testing on 5-character sequences we achieved an AOC value of 81%. When we increased the test sequence length to 20 (i.e. allowed the model to work with more contextual information), the accuracy jumped to 97% and with a 30-character sequence we achieved near perfect classification.

For multi-language classification, we built a language detector to detect among multiple languages. With an input sequence length of 40, and a test sequence length of 20 the accuracy was 95%. We explored various tuning efficiencies, like early stopping of the training based on monitoring the validation loss.

We also built a language detector based on the tri-gram language detection technique (code not included). Without optimizing on the parameters, we achieved an accuracy of 72%, much lower than the LSTM, which was expected since the ‘n-gram’ technique does not learn contextual information but is much simpler and computationally less expensive.

LSTMS are typically used as a generative model for generating sequences of characters. In this project, we used LSTM models as language detectors. LSTMS are an implementation of RNNs which avoids the vanishing (exploding gradient) problem. The training set was the ‘Universal declaration of human rights’ in two languages, English and French.

Packages/Libraries used: Keras

Model Compilation settings: 
    Single LSTM layer with 128 memory units
    Input is the sliced sequences of length 40 (input shape is (40, len(charset))  - one hot encoding
Dense layer (len(charset)) as the output layer with softmax activation function since we wanted to predict the normalized probabilities of the characters as output
Loss function: categorical cross-entropy
Optimizer: RMSprop (usually a good choice for recurrent neural networks)

Train each language model separately (i.e. each model during the training was exposed to the text from one particular language only) on sequences of length 40. So essentially, the model during training was fed 40 character sequences while the target was the 41st character.

