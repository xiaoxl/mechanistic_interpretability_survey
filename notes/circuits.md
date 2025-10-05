
# mathematical framework
[ref](https://transformer-circuits.pub/2021/framework/index.html)


# Example

[ref](https://www.lesswrong.com/posts/CJsxd8ofLjGFxkmAP/explaining-the-transformer-circuits-framework-by-example)


## Definition


::: {.callout-note}
## Circuit
A subset of a transformer's operations that can be understood in isolation and are interpretable is called a **circuit**.
:::

## A single-layer transformer

Flow chart:
1. tokens: $t$.
2. embed: $x_0=tW_E$, where $W_E$ is of size $N\times d$.
3. Attention head is denoted by $h$. We have multiple heads. $x_1=x_0+\sum_{h\in H} h(x_0)$.
4. The final logits are unembedding: $T(t)=x_1W_U$, where $W_U$ is of size $d\times N$.

### Tokens and embedding
A token is an integer $t\in\mathbb N$, which represents the index in the vocabulary of size $V$. The embedding maps it into a continuous vector: $x_0=tW_E\in\mathbb R^d$, where $W_E\in Mat(V,d)$.

$x_0$ is a row vector of shape $1\times d$. In pratical, $x_0$ is stored as in a tensor of size `(batch, seq_len, d)`. That is to say, suppose we have $B$ sentences, each with $L$ tokens, and embedding dimension is $d$. Then the embedding is of size $B\times L\times d$, where 

- `batch` axis $B$ shows which sentence
- `seq_len` axis $L$ shows token position
- embedding axis $d$ shows the vector representation of the token.

### Multi-head Attention



Each attention involves:

1. Query matrix $W_Q$ and Key matrix $W_K$ of size $d\times d_k$, where $d_k$ is the dimension of the queries and keys 
2. Value matrix $W_V$ of size $d\times d_v$, where $d_v$ is the dimension of the values
3. Usually $d_k=d_v=d/H$, where $H$ is the number of heads.
   
For each embedding $x_0$ of dimension $B\times d\times L$, we have projections
$$
\begin{split}
Q&=x_0W_Q,\quad dim Q=B\times L\times d_k,\\
K&=x_0W_K,\quad dim K=B\times L\times d_k,\\
V&=x_0W_V,\quad dim V=B\times L\times d_v.
\end{split}
$$

Then 
$$
\begin{split}
scores&=\frac{QK^T}{\sqrt{d_k}},\quad \text{ of size }B\times L\times L,\\
h(x_0)&=Attn(Q,K,V)=softmax_{rowwise}(scores)V,\quad \text{ of size }B\times L\times d_v,\\
H(x_0)&=\oplus_{h\in H}h(x_0),\quad \text{ of size }B\times L\times (Hd_v),\\
MHA(x_0)&=H(x_0)W_O,\quad \text{ of size }B\times L\times d,\\
x_1&=x_0+MHA(x_0),
\end{split}
$$
where $W_O$ is of size $(Hd_v)\times d$. This formula can be treated as a weighted total of $h(x_0)$. The rowwise softmax function means that we need each row to sum to be 1.

The above formula can be written as

$$
T(t) = tW_EW_U+\sum_hA^htW_EW_V^hW_O^hW_U,
$$
where $A^h=softmax(tW_EW^h_QW_K^{hT}W_E^Tt^T)$. The two matrices are our first two circuits.

- $QK$-circuit $C^h_{QK}=W_EW^h_QW_K^{hT}W_E^T$: this is a $V\times V$ matrix. It describes the attention that the token $i$ in query pays to token $j$ in keys, with respect to the head $h$. Row represents queries and column represents keys. The biggest entry in each row is corresponding to the key that is activated.
  - Row: query token
  - Column: key token
  - Entry(i,j): how much $i$ pays attention ot $j$
- $OV$-circuit $C^h_{OV}=W_EW_V^hW_O^hW_U$: this is a $V\times V$ matrix. It tells what payload of information is delivered once attention has selected a token. So it can be intepreted as: if $i$ decide to pay attention to $j$, this is how all information are gathered together. 
  - Row: the source of values
  - Column: output vocabulary
  - Entry(i,j): if $i$ is attended, how much that contributes to increasing the logit for token $j$

- QK-circuit = where to look (attention pattern).
- OV-circuit = what happens when you look there (value → logit effect).


::: {.callout-note}
If $i$ pays attention to $j$ (based on QK-circuit), then OV-circuit decides how $j$'s information modifies the logits for the next token.
:::

# Open problems
[ref](https://www.lesswrong.com/posts/LbrPTJ4fmABEdEnLf/200-concrete-open-problems-in-mechanistic-interpretability)