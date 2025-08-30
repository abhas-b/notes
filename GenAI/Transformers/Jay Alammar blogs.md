
#genai [[Attention and Transformers]] 

# Attention

[Link](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)

[Link2](https://jalammar.github.io/illustrated-transformer/)
## RNN based Seq to Seq

* Sequence to Sequence models are basically composed of encoder and decoder.
* The encoder processes each item in the input sequence, it compiles the information it captures into a vector (called the context). After processing the entire input sequence, the encoder sends the context over to the decoder, which begins producing the output sequence item by item.
* Encoder and decoder both tend to be RNNs.
* Size of the context vector is basically the number of hidden units in the encoder.
* The last hidden state is simply the context which is passed to the decoder.


## Limitations

* Due to the context vector the models had trouble with long sequences.


## Attention:

* Attention allows the model to focus on the relevant parts of the input sequence as needed.
* The presence of hidden states in the RNNs allows self-attention to incorporate representation of previous words/vectors with current word.
* **Encoder**: The encoder passes all the hidden states to the decoder (instead of simply the last state, context).
* **Decoder**: In order to focus on the parts of the input that are relevant to a decoding time step the decoder:
	* Look at the set of encoder states it received.
	* Each encoder hidden state is associated with a certain word in the input sequence.
	* Give each hidden state a score.
	* Softmax the score and multiply each state with its softmaxed score. This amplifies the high scoring hidden states.
	* Sum up the weighted vectors which now act as the context vector.
	* This scoring exercise is done at each time step on the decoder.


### Paying Attention
* The last token and an initial hidden state goes into the decoder at first time step. The RNN produces an output and a new hidden state (h_d1). The output is discarded.
* We now use the encoder hidden states and h_d1 to calculate a context vector C1 for this time step.
* h_d1 and C1 are concatenated into one vector.
* This is passed through a feedforward neural network.
* The output from this is the output from this time step.
* Repeat for the next time steps.


# Transformers

* We have an encoding component, a decoding component and connections between them
* Encoder
	* A stack of encoders.
	* The decoder layer will have the same number of decoders.
	* All encoders are identical in structure but do not share any weights.
	* Each encoder has two components
		* Self Attention 
			* Entry point for the inputs
		* Feedforward neural network
			* Input = Output from self attention layer.
			* The exact same network is independently applied to each position.
	* Decoder
		* The decoder has both the above layers but between them is another attention layer which helps the decoder focus on the relevant parts of the input sequence.


![[Pasted image 20250129123649.png]]

* Each encoder receives an input of size 512.
* The first (lower most) encoder receives the embeddings.
	* The other encoders receive outputs from the encoder which is directly below it.
* The feed forward network for each word is independent and can be executed in parallel. Attention cannot.

## Self Attention in Detail

1. For each word we create 3 vectors (dimensionality 64):
	* Query Vector
	* Key Vector
	* Value Vector
* These are obtained by multiplying the embeddings with W_q, W_k, W_v (weight vectors created during training).
* These vectors are essentially query, key and value projections of each word in the input sequence.
2. Then we calculate attention score for each word.
	* We need to score each word of the input sequence against each word.
	* This score determines how much focus to place on other parts of the sequence as we encode a word at a certain position.
	* Score: (query vector).(key vector of the word under processing) (dot product)
3. Divide the scores by sqrt(key vector dimensionality)
	* This leads to having mode stable gradients.
4. Then pass the result through softmax.
	* This normalizes the scores so they're all positive and add up to 1.
5. Multiply value vector by the softmax score from #4
	1. This drowns out irrelevant words 
	2. Input of softmax is called logit.
6. Sum up the weighted value vectors.
	1. This is the output of the self attention layer.
	2. Essentially embeddings are converted into a value vector.
7. The output is sent to feed forward network.


$$Z = Softmax(\frac{Q.K^T}{sqrt(d_k)}).V$$

## Multi Headed Attention

* It expands the model's ability to focus on different positions. 
* With multi head attention we have multiple sets of Query/Key/Value weight matrices (Transformer uses 8, leading to 8 sets of encoders/decoders).
* Each of the sets is randomly initialized and is used to project the input embeddings into different representational subspaces.
* We end up getting 8 different Z matrics.
* For the feed forward network we still need to pass a single matrix.
	* We do this by concatenating the 8 matrices and then multiplying them with additional weights matrix WO.

![[Pasted image 20250129131623.png]]


## Representing The Order of The Sequence Using Positional Encoding

* To take word order into consideration the transformer adds a vector to each input embedding.
	* These vectors let the model learn the distance between different words in the sequence.


## Residuals

* Each sub-layer (self attention, ffnn) in each encoder has a residual connection around it and is followed by a layer normalization step.


![[Pasted image 20250129144209.png]]




![[Pasted image 20250129144350.png]]


# Decoder

1. Encoder starts by processing input sequence.
2. The output of top encoder is then transformed into a set of attention vectors K and V. These go into the encoder-decoder attention layer which helps the decoder focus on the relevant places in the input sequence.
	1. The encoder decoder attention layer creates Q from layers below it and takes K and V from encoder stack output.
3. The steps are repeated until a special symbol is reached which tells the transformer that the decoder has completed its output.
4. The self attention layer in the decoder is only allowed to attend to earlier positions in the output sequence.
	1. This is done by masking future positions before the softmax step in the self attention calculation.



![[Pasted image 20250129131836.png]]


* The final linear layer is a fully connected neural network that projects the decoder output to a much larger vector called a logits vector.
	* The logits vector has a dimensionality equal to vocabulary size (based on training dataset)
* There is another softmax layer which turns the output of linear layer into probabilities. The cell with the highest probability is chosen and the word corresponding to this cell is chosen as the output.
* 








