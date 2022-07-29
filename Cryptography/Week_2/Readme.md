### Question 1
Consider the following five events:

1.  Correctly guessing a random 128-bit AES key on the first try.
    
2.  Winning a lottery with 1 million contestants (the probability is 1/106 1/10^6\\ 1/106 ).
    
3.  Winning a lottery with 1 million contestants 5 times in a row (the probability is (1/106)5 (1/10^6)^5\\ (1/106)5 ).
    
4.  Winning a lottery with 1 million contestants 6 times in a row.
    
5.  Winning a lottery with 1 million contestants 7 times in a row.
    

What is the order of these events from most likely to least likely?

- [ ] 2, 3, 5, 4, 1

- [ ] 2, 3, 1, 5, 4

- [ ] 3, 2, 5, 4, 1

- [X] 2, 3, 4, 1, 5

Correct

-   The probability of event (1) is 1/2^128.
    
-   The probability of event (5) is 1/(10^6)^7 which is about 1/2^{139}. Therefore, event (5) is the least likely.
    
-   The probability of event (4) is 1/(10^6)^6 which is about 1/2^{119.5} which is more likely than event (1).
    
-   The remaining events are all more likely than event (4).
    

### Question 2

Suppose that using commodity hardware it is possible to build a computer

for about $200 that can brute force about 1 billion AES keys per second.

Suppose an organization wants to run an exhaustive search for a single

128-bit AES key and was willing to spend 4 trillion dollars to buy these

machines (this is more than the annual US federal budget). How long would

it take the organization to brute force this single 128-bit AES key with

these machines? Ignore additional costs such as power and maintenance.



- [ ] More than a 100 years but less than a million years

- [ ] More than a month but less than a year

- [ ] More than a million years but less than a billion (10^9) years

- [ ] More than a day but less than a week

- [X] More than a billion (10^9) years

Correct

The answer is about 540 billion years.

-   \# machines = 4\*10^12/200 = 2\*10^10
    
-   \# keys processed per sec = 10^9 \* (2\*10^10) = 2\*10^19
    
-   \# seconds = 2^128 / (2\*10^19) = 1.7\*10^19
    

This many seconds is about 540 billion years.

### 3.

Question 3

Let <b>F:{0,1}<sup>n</sup>×{0,1}<sup>n</sup>→{0,1}<sup>n</sup></b> be a secure PRF (i.e. a PRF where the key space, input space, and output space are all <b>{0,1}<sup>n</sup></b> and say n = 128.

Which of the following is a secure PRF (there is more than one correct answer):


- [X] F′(k,x)=F(k,x)[0,…,n−2] (i.e., F′(k,x) drops the last bit of F(k,x))
- [X] F′(k, x)=k ⨁ x
- [ ] F'(k, x) = F(k,x) || 0
- [ ] F'(k, x) = F(k, x) when x != 0<sup>n</sup> and 0<sup>n</sup> otherwise
- [ ] F'((k1, k2), x) = F(k1, x) when x != 0<sup>n</sup> and k2 otherwise
- [x] F'(k, x) = reverse(F(k, x))


### 4.

Question 4

Recall that the Luby-Rackoff theorem discussed in [The Data Encryption Standard lecture](https://www.coursera.org/learn/crypto/lecture/TzBaf/the-data-encryption-standard) states that applying a **three** round Feistel network to a secure PRF gives a secure block cipher. Let's see what goes wrong if we only use a **two** round Feistel.

Let <b> F:K×{0,1}<sup>32</sup>→{0,1}<sup>32</sup></b> be a secure PRF.

Recall that a 2-round Feistel defines the following PRP

<b> F:K×{0,1}<sup>64</sup>→{0,1}<sup>64</sup></b>

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/doq9qiaTEeWroAqDv8_clw_5793d1725051e0c7cf36eade7a812448_Screen-Shot-2015-07-09-at-4.37.09-PM.png?expiry=1659225600000&hmac=u7kTDSaxYoDHa09dd6BEL69QCOklh4RJmluL-tkKJJ4)

Here R<sub>0</sub> is the right 32 bits of the 64-bit input and L<sub>0</sub> is the left 32 bits.

One of the following lines is the output of this PRP F<sub>2</sub> using a random key, while the other three are the output of a truly random permutation f:{0,1}<sup>64</sup>→{0,1}<sup>64</sup>. All 64-bit outputs are encoded as 16 hex characters.

Can you say which is the output of the PRP? Note that since you are able to distinguish the output of F<sub>2</sub> from random, F<sub>2</sub> is not a secure block cipher, which is what we wanted to show.

**Hint:** First argue that there is a detectable pattern in the xor of F<sub>2</sub>(⋅, 0<sup> 64 </sup>) and F<sub>2</sub>(⋅, 1<sup> 32 </sup>0<sup> 32 </sup>). Then try to detect this pattern in the given outputs.

- [X] On input 0<sup>64</sup> the output is "e86d2de2 e1387ae9". 
      On input 1<sup>32</sup>0<sup>32</sup> the output is "1792d21d b645c008".
- [ ] On input 0<sup>64</sup> the output is "5f67abaf 5210722b". 
      On input 1<sup>32</sup>0<sup>32</sup> the output is "bbe033c0 0bc9330e".
- [ ] On input 0<sup>64</sup> the output is "7c2822eb fdc48bfb". 
      On input 1<sup>32</sup>0<sup>32</sup> the output is "325032a9 c5e2364b".
- [ ] On input 0<sup>64</sup> the output is "7b50baab 07640c3d". 
      On input 1<sup>32</sup>0<sup>32</sup> the output is "ac343a22 cea46d60".
   
### 5.

Question 5

Nonce-based CBC. Recall that in [Lecture 4.4](https://www.coursera.org/learn/crypto/lecture/wlIX8/modes-of-operation-many-time-key-cbc) we said that if one wants to use CBC encryption with a non-random unique nonce then the nonce must first be encrypted with an **independent** PRP key and the result then used as the CBC IV.

Let's see what goes wrong if one encrypts the nonce with the **same** PRP key as the key used for CBC encryption.

Let <b>F:K×{0,1}<sup> ℓ </sup>→{0,1}<sup> ℓ </sup></b> be a secure PRP with, say, ℓ=128. Let n be a nonce and suppose one encrypts a message m by first computing IV=F(k,n) and then using this IV in CBC encryption using F(k,⋅). Note that the same key k is used for computing the IV and for CBC encryption. We show that the resulting system is not nonce-based CPA secure.

The attacker begins by asking for the encryption of the two block message m=(0<sup> ℓ </sup>,0<sup> ℓ </sup>) with nonce n = 0<sup> ℓ </sup> It receives back a two block ciphertext (c0,c1). Observe that by definition of CBC we know that c1 = F(k,c0).

Next, the attacker asks for the encryption of the one block message m1 = c0 ⨁ c1 with nonce n = c0n. It receives back a one block ciphertext c0′.

What relation holds between c0, c1, c0′ ? Note that this relation lets the adversary win the nonce-based CPA game with advantage 1.

- [ ] c1 = 0<sup> ℓ </sup>
- [ ] c1 = c0 ⨁ c0'
- [ ] c0 = c0'
- [X] c1 = c0'


### 6.

Question 6

Let mmm be a message consisting of ℓ AES blocks

(say ℓ = 100). Alice encrypts m using CBC mode and transmits

the resulting ciphertext to Bob. Due to a network error,

ciphertext block number ℓ/2 is corrupted during transmission.

All other ciphertext blocks are transmitted and received correctly.

Once Bob decrypts the received ciphertext, how many plaintext blocks

will be corrupted?

- [ ] 1
- [ ] ℓ/2
- [ ] 1 + ℓ/2
- [X] 2
- [ ] 0

### 7.

Question 7

Let mmm be a message consisting of ℓ AES blocks (say ℓ =100). Alice encrypts m using randomized counter mode and

transmits the resulting ciphertext to Bob. Due to a network error,

ciphertext block number ℓ/2 is corrupted during transmission.

All other ciphertext blocks are transmitted and received correctly.

Once Bob decrypts the received ciphertext, how many plaintext blocks

will be corrupted?

- [ ] 3
- [ ] ℓ/2
- [ ] 0
- [X] 1
- [ ] 1 + ℓ/2


### 8.

Question 8

Recall that encryption systems do not fully hide the **length** of

transmitted messages. Leaking the length of web requests [hasbeen used](http://research.microsoft.com/apps/pubs/default.aspx?id=119060) to eavesdrop on encrypted HTTPS traffic to a number of

web sites, such as tax preparation sites, Google searches, and

healthcare sites.

Suppose an attacker intercepts a packet where he knows that the

packet payload is encrypted using AES in CBC mode with a random IV. The

encrypted packet payload is 128 bytes. Which of the following

messages is plausibly the decryption of the payload:



- [ ] 'To consider the resistance of an enciphering process to being broken we should

assume that at same times the enemy knows everything but the key being used and

to break it needs only discover the key from this information.'

- [X] 'In this letter I make some remarks on a general principle

relevant to enciphering in general and my machine.'

- [ ] 'We see immediately that one needs little information to

begin to break down the process.'

- [ ] 'The most direct computation would be for the enemy to try

all 2^r possible keys, one by one.'


### 9.

Question 9

Let <b> R = {0, 1}<sup> 4 </sup> </b> and consider the following PRF <b> F:R<sup> 5 </sup>×R→R </b> defined as follows:
 <b>
   
          t=k[0] 
  
          for i=1 to 4 do
  
                if (x[i−1]=1) t = t ⊕ k[i] 
  
          output t
 </b>
That is, the key is k = (k[0], k[1], k[2, k[3], k[4]) in R<sup> 5 </sup>  and the function at, for example, 0101  is defined as F(k,0101) = k[0] ⊕ k[2] ⊕ k[4]

For a random key kkk unknown to you, you learn that

F(k,0110) = 0011  and  F(k,0101) = 1010 and  F(k,1110) = 0110 

What is the value of F(k,1101) ? Note that since you are able to predict the function at a new point, this PRF is insecure.

Answer: 1111


