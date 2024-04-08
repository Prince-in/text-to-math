# text-to-math



Text to Math program
In Math Word Problem solving[3], given a mathematical problem specified in
text, the goal is to find the solution to the problem by applying mathematical
reasoning on the input text. See Figure 1 for an example.
3
Figure 1: Sample data
Answering math word problems is a difficult task, and requires logical reasoning over implicit or explicit quantities expressed in text. In this assignment, our
goal is develop an automatic converter, which would convert the textual narrative into executable program. One of the ways to generate executable programs
from their textual description is to make use of Encoder-Decoder architecture. For this part of assignment, we will make use of seq2seq architectures
to convert input text into the corresponding symbolic form. We will be using
operation representation language provided in [1] to represent the executable
program.
Note that training recurrent architectures like LSTMs can be slightly tricky.
Therefore, look into various tricks that people have employed for this purpose.
Some of them can be found in [11]. Try to optimize your training pipeline as
much as possible.
2.1 Data
Dataset and checker file link
The folder contains the train, test and dev json files along with a checker file.
Each json contains a P rogram, linear formula and answer fields for each
example. The train split contains 19791 samples, dev contains 2961 and test
contains 1924 samples. We would be generating the linear formula given the
P roblem, the example of same is given in 1.
2.2 Metrics
Evaluation metrics are critical for any system to be evaluated. For this task we
will use 2 different metrics.
• Exact Match : If all the predicted sequence matches the ground-truth
sequence exactly it’s 1 else 0.
• Execution Accuracy : If the executed answer of your predicted sequence
is within 2% of true answer then the score is 1 else 0. You are provided
4
with the an evaluation script in the dataset. You must run this script
on generated outputs to get the evaluation scores. The script will do the
substitution of variables in the predicted sequence and will also execute
the sequence to generate answer. Please read the checker file for more
details.
2.3 Models
For your experiments you are supposed to train the following models.
2.3.1 Architectural experiments
1. A Seq2Seq model with GloVe embeddings [8], using an Bi-LSTM encoder
and an LSTM decoder. For details of an LSTM refer [4]
2. A Seq2Seq+Attention model with GloVe embeddings, using an Bi- LSTM
encoder and an LSTM decoder.
3. A Seq2Seq+Attention model using a pre-trained frozen BERT-base-cased
encoder and an LSTM decoder
4. A Seq2Seq+Attention model with pre-trained BERT-base-cased encoder
and an LSTM decoder, where the BERT encoder can now be fine-tuned
along with the remaining network.
You must report the following:
• Loss curves on the training and dev set
• Exact Match Accuracy and Execution Accuracy (see evaluation metrics) on the dev/test set.
• All hyper-parameter settings used in your experiments.
• Any findings observed from any potential grid search performed
• Any other insights that you gained from the training procedure and
the outputs of your model.
In this part, we will implement the models with teacher forcing with a
ratio of 0.6 during training. During inference we will use beam search with k
= 10 to generate output. You must implement beam search in python/pytorch
from scratch.
2.3.2 Effect of Teacher Forcing probability
Train the second model (Seq2Seq+Attention BiLSTM-LSTM) again with teacher
forcing probabilities in {0.3, 0.6, 0.9}. Report the exact match accuracy and
token match accuracy on test data with beam size k = 10. Comment your
observations.
5
2.3.3 Effect of Beam Size
For the fourth model (Seq2Seq+Attention with fine-tuned Bert) trained with
teacher forcing probability 0.6, generate the output for test data with beam
sizes {1, 10, 20}. Report the exact match accuracy and token match accuracy
on test data. Comment your observations.

