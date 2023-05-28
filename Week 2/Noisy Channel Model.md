In this model, we use the Bayesian Theorem to calculate the highest probability of  `w`  given  `x` .
`w` -> correct word
`x` -> misspelled word
Real Corpus -> text containing the spelling error.
Corrected Corpus -> corrected text.

-  80% of  errors are within edit distance  1.
- Almost all errors are within edit distance 2.
- 25 - 40% of spelling errors are real words.

`w`  --------------Noisy Channel--------------->  `x`

Using Bayesian theorem we can use P(x|w) to calculate P(w|x) as shown below.  Here we can see that P(x) is constant for all words in dictionary therefore it can be ignored as we are comparing the values between each word in a dictionary.

![[Pasted image 20230522183158.png]]

-  del [x,y] :  count (`xy`  typed as  `x`) - Probability is calculated as the frequency of  `xy` typed as  `x`  in the real corpus divided by the frequency of  `xy`  in corrected corpus.
  
-  ins [x,y] :  count (`x`  typed as  `xy`) - Probability is calculated as the frequency of  `x` typed as  `xy`  in the real corpus divided by the frequency of  `x`  in corrected corpus.
  
-   sub [x,y] :  count (`x`  typed as  `y`) - Probability is calculated as the frequency of  `x` typed as  `y`  in the real corpus divided by the frequency of  `x`  in corrected corpus.
  
-   trans[x,y] :  count (`xy`  typed as  `yx`) - Probability is calculated as the frequency of  `xy` typed as  `yx`  in the real corpus divided by the frequency of  `xy`  in corrected corpus.


## Example of non-word spelling error
#### Without Context
`x`  -> acress  and we have a candidate set containing all the possible correct spelling.


![[Pasted image 20230522185017.png]]
**Note** :  acres is included  twice because the probability of insertion of  `s`  is different for 
inserting it before the last  `s`  or  after the last  `s` .

--> Now we calulate P(x|w) and P(w) 

![[Pasted image 20230522134559.png]]
**Note**:  P(w) i s the probability of the word to occur in the corpus. Here we can see that  **across** is the correct word without considering the context as it has the highest probability value  x 10$^9$.  



#### With Context
Same example 
Sentence --> "....versatile acress whose"
Our candidate set consist of two of the highest probability valued words = {actress, across}.

Suppose,
P(actress|versatile) = 0.000021,   P(across | versatile) = 0.000021.
P(whose|actress) = 0.001, P(whose | across) = 0.000006.
then,
P("versatile actress whose") = 0.000021 x 0.001 = 210 x 10^-10.
P("versatile across whose") = 0.000021 x 0.000006 = 1 x 10^-10.

P("versatile actress whose")  >  P("versatile across whose")  therefore the correct spelling may be **actress** in this context.



## Noisy  channel  model  for  real-word  spelling  correction.


![[Pasted image 20230522194935.png]]

Here in the sentence X, we do not know which word is incorrect as they all can come under real word spelling error.
So we have to maximize P(W | X) by choosing  optimal sequence of words W.

![[Pasted image 20230522195446.png]]

Correct sequence is "two of the".

If we try all possible sequences here then it will be 4^5 sequences, which is exponential. Therefore we select two words and keep them constant and only change the third word.
By doing this we will have 4 + 3 + 4 sequences, which is much better than exponential. 

**Note**: Here we are making a general assumption that a sentence does not have more than one error.

**P(X | W) = P(w' 1 | w1)  x  P(w2 | w2)  x  P(w3  | w3)**

**P(w'1 | w1)**  --> same as how we calculated individual word probability in without context section.
**P(w2 | w2),  P(w3 | w3)** -->  Average number of error per 10/100 words also denoted as  'α'.


[Stanford  resource on Noisy Channel](https://web.stanford.edu/~jurafsky/slp3/B.pdf)



