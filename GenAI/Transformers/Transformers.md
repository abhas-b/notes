#genai [[Attention and Transformers]]

[Link](https://www.youtube.com/watch?v=wjZofJX0v4M)


* First the input is broken into tokens which are then converted to numbers using word embeddings.
* Attention basically lets the vectors talk to each other and provide information for updating their values for incorporating context.
* Converting a transformer into a chatbot:
	* System prompt: establishes the setting of user interaction with the transformer.
	* User prompt: Seed text

Types of matrices:
* Embedding: one column for each word in the vocabulary
	* Context size: the number of vectors the network can process at a time
	* n_dimensions x n_vocab
* Key
	* Keys potentially answer the queries
	* Also model parameters.
* Query
	* Much smaller than Embedding vector
	* encapsulates some questions/queries about the token
	* The values are model parameters.
* Value
* Output
* Up-Projection
* Down-Projection
* Unembedding
	* Used to map decoder output to vocabulary.
	* Its output goes into softmax (which gives the word probability distribution)
	* n_vocab x n_embedding_dimensions
