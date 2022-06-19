### Question 1

Data compression is often used in data storage and transmission. Suppose you want to use data compression in conjunction with encryption. Does it make more sense to:

- [ ]  The order does not matter -- neither one will compress the data. 
- [X] Compress then encrypt.
- [ ]  Encrypt then compress.
- [ ]  The order does not matter -- either one is fine.

<i> Motivation </i>: 

### Question 2

Let <b>G:{0,1}<sup>s</sup>→{0,1}<sup>n</sup></b> be a secure PRG. Which of the following is a secure PRG  (there is more than one correct answer):
- [X] G'(k) = G(k) ⨁ 1<sup>n</sup>
- [X] G'(k1, k2) = G(k1) || G(k2)
- [X] G'(k) = reverse(G(k))
- [ ] G'(k) = G(0)
- [ ] G'(k) = G(k) || 0
- [ ] G'(k) = G(k) || G(k)
 
<i> Motivation </i>: 
 
### Question 3

Let <b> G:K→{0,1}<sup>n</sup></b> be a secure PRG.\
Define <b>G'(k1,k2) = G(k1) & G(k2)</b>.\
Consider the following statistical test <b>A on {0,1}<sup>n</sup></b>: 
A(x) outputs LSB(x), the least significant bit of x.\

What is the PRG_ADV[A,G'] ?

<i> Answer </i>: 0.25

<i> Motivation </i>: 

### Question 4

Let (E,D) be a (one-time) semantically secure cipher with key space K={0,1}<sup>ℓ</sup>. A bank wishes to split a decryption key k∈{0,1}<sup>ℓ</sup> into two pieces p1 and p2 so that both are needed for decryption. The piece p1 can be given to one executive and p2 to another so that both must contribute their pieces for decryption to proceed.

The bank generates random k1 in {0,1}<sup>ℓ</sup> and sets k1'←k⊕k1. Note that k1⊕k1'=k. The bank can give k1 to one executive and k1' to another. Both must be present for decryption to proceed since, by itself, each piece contains no information about the secret key k (note that each piece is a one-time pad encryption of k).

Now, suppose the bank wants to split k into three pieces p1,p2,p3 so that any two of the pieces enable decryption using k. This ensures that even if one executive is out sick, decryption can still succeed. To do so the bank generates two random pairs (k1,k1') and (k2,k2') as in the previous paragraph so that k1⊕k1'=k2⊕k2'=k. How should the bank assign pieces so that any two pieces enable decryption using k, but no single piece can decrypt?

- [ ] `p1=(k1,k2),  p2=(k1,k2),    p3=(k2')`
- [ ] `p1=(k1,k2),  p2=(k1',k2'),  p3=(k2')`
- [ ] `p1=(k1,k2),  p2=(k2,k2'),   p3=(k2')`
- [ ] `p1=(k1,k2),  p2=(k1'),      p3=(k2')`
- [X] `p1=(k1,k2),  p2=(k1',k2),   p3=(k2')`

<i> Motivation </i>: 


### Question 5

Let M=C=K={0,1,2,…,255} and consider the following cipher defined over (K,M,C): 
`E(k,m)=m+k(mod 256); D(k,c)=c−k(mod 256)`
Does this cipher have perfect secrecy?
- [ ] No, there is a simple attack on this cipher.
- [X] Yes
- [ ] No, only the One Time Pad has perfect secrecy.
- [ ] 
<i> Motivation </i>: 

### Question 6

Let (E,D) be a (one-time) semantically secure cipher where the message and ciphertext space is {0,1}<sup>n</sup>. Which of the following encryption schemes are (one-time) semantically secure?
- [ ] E'(k,m)=E(k,m)||k
- [X] E'(k,m) compute c = E(k,m) and output c || c (i.e., output cc twice)
- [X] E'((k,k'), m)=E(k,m)||E(k', m)
- [ ] E'(k, m)=E(0<sup>n</sup>, m)
- [X] E'(k,m)=0||E(k,m)     (i.e. prepend 0 to the ciphertext)
- [ ] E'(k,m)=E(k,m)||LSB(m)

<i> Motivation </i>: 

### Question 7
Suppose you are told that the one time pad encryption of the message <i> "attack at dawn" </i> is <i> 09e1c5f70a65ac519458e7e53f36 </i>
(the plaintext letters are encoded as 8-bit ASCII and the given ciphertext is written in hex). What would be the one time pad encryption of the message "attack at dusk" under the same OTP key?

<i> Answer </i>: 9e1c5f70a65ac519458e7e53f36

<i> Motivation </i>:

### Question 8

The movie industry wants to protect digital content distributed on DVD’s. We develop a variant of a method used to protect Blu-ray disks called AACS.

Suppose there are at most a total of n DVD players in the world (e.g. n=2<sup>32</sup>). We view these n players as the leaves of a binary tree of height log2n. Each node in this binary tree contains an AES key k<sup>i</sup>. These keys are kept secret from consumers and are fixed for all time. At manufacturing time each DVD player is assigned a serial number i∈[0,n−1]. Consider the set of nodes Si along the path from the root to leaf number i in the binary tree. The manufacturer of the DVD player embeds in player number i the keys associated with the nodes in the set S<sub>i</sub>. A DVD movie m is encrypted as 

E(k<sub>root</sub>,k)||E(k,m) 

where k is a random AES key called a content-key and kroot is the key associated with the root of the tree. Since all DVD players have the key kroot all players can decrypt the movie m. We refer to E(k<sub>root</sub>,k) as the header and E(k,m) as the body. In what follows the DVD header may contain multiple ciphertexts where each ciphertext is the encryption of the content-key k under some key k<sub>i</sub> in the binary tree.

Suppose the keys embedded in DVD player number r are exposed by hackers and published on the Internet. In this problem we show that when the movie industry distributes a new DVD movie, they can encrypt the contents of the DVD using a slightly larger header (containing about log<sub>2</sub>n keys) so that all DVD players, except for player number r, can decrypt the movie. In effect, the movie industry disables player number r without affecting other players.

As shown below, consider a tree with n=16 leaves. Suppose the leaf node labeled 25 corresponds to an exposed DVD player key. Check the set of keys below under which to encrypt the key k so that every player other than player 25 can decrypt the DVD. Only four keys are needed.
![image](https://user-images.githubusercontent.com/24388880/174452429-90e82c0d-6914-4252-bf69-09e92cafe49f.png)
- [X] 1
- [ ] 21
- [ ] 17
- [ ] 5
- [X] 26
- [X] 6
- [ ] 24
- [X] 11

<i> Motivation </i>: 

### Question 9

Continuing with the previous question, if there are n DVD players, what is the number of keys under which the content key k must be encrypted if exactly one DVD player's key needs to be revoked?
- [ ] n - 1
- [ ] √n
- [ ] n/2
- [ ] 2
- [X] log<sub>2</sub>n

<i> Motivation </i>: 

### Question 10

Continuing with question 8, suppose the leaf nodes labeled 16, 18, and 25 correspond to exposed DVD player keys. Check the smallest set of keys under which to encrypt the key k so that every player other than players 16,18,25 can decrypt the DVD. Only six keys are needed.

- [X] 4
- [X] 6
- [X] 11
- [X] 15
- [X] 17
- [X] 26
- [ ] 2
- [ ] 5
- [ ] 10
- [ ] 27


<i> Motivation </i>:
