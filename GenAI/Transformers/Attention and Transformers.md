#genai  

## Attention

* Helps the computer resolve ambiguity in word meanings by enhancing embeddings with context.
$$Attention(Q,K,V) = softmax(\frac{QK^T}{\sqrt d_k})V$$
$$\text {Multi Head Attention} = Concat(head1, head2...)W^O$$
Here $$head_i = Attention(QW_i^Q, KW_i^K, VW_i^V)$$

* We can get more embeddings for Multi Head through linear transformations of the original embeddings.
* These transformations are achieved through Keys and Queries (QK^T).
* After attention performs similarity identification through Q and K, Values matrix is used to perform another transformation on the original embeddings for predicting next word.


![[Pasted image 20250130174104.png]]

![[Pasted image 20250130174147.png]]



