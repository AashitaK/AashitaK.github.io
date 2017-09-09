Lagrange's four-square theorem says every natural number can be written as a sum of four integer squares. Let $S = \{ a^2+b^2+c^2+d^2: a,b,c,d \in N \}$, then set $S$ is effectively the set of natural numbers with each number repeating a certain number of times. Given any power of $2$ no matter how high say $v$, there are infinitely many natural numbers that are divisible by $2^v$ spread out at regular intervals of length $2^v$ in the number line. Consequently, there are infinitely many numbers divisible by any high power of $2$ in the set $S$ as well. 

If we put a restriction on this set $S$, say we fix one of the four squares $a^2$ while letting $b,c$ and $d$ vary over all natural numbers as above, the we obtain a subset say $S(a) = \{ a^2+b^2+c^2+d^2: b,c,d \in N \}$. In the paper, we asked the same question whether there are numbers in the set $S(a)$ divisibile by large enough powers of $2$ and counterintuitively, the answer is in the negative. For any number $a$, there is a large enough power of $2$ say $v$ such that no number in the set $S(a)$ is divisible by $2^v$. For example, ------ . On the other hand, given any power of $2$, no matter how big, there exists infinitely many natural numbers $a$ such that the set $S(a)$ has infinitely many numbers divisible by that power. The existence of such an $a$ such that $S(a)$ has numbers divisible by a given power of $2$ is not surprising since the union of the sets $S(a)$ as $a$ vary over natural numbers gives back the set $S$ that has numbers divisible by all powers of $2$. However, the existence of infinitely many such $a$'s regularly spaced in the number line (?) and also the fact that in each of such set $S(a)$ there are infinitely many numbers divisible by that power of $2$ points to the inherent pattern of divisibility by $2$ similar to that of the number line. We also found out that for a fixed power of $2$ say $v$, what proportion of sets $S(a)$ has numbers divisible by $2^v$. For example, as we look at sets $S(a)$ for different values of the natural number $a$, exactly half of the sets contains no numbers divisible by $16$.


Like the sets $S(a)$ obtained by fixing one of the four squares in the sums of four squares, we also consider two more kinds of sets obtained by fixing two or three sqaures respectively. The similar analysis is done for the sets $S(a,b) = \{ a^2+b^2+c^2+d^2: c,d \in N \}$ and $S(a,b,c) = \{ a^2+b^2+c^2+d^2: d \in N \}$ and results obtained are similar in nature. 

It is noteworthy to mention that this phenomena occurs only when we consider the sums of four squares some of which are fixed and the divisibility is studied with respect to $2$. If we consider the sets of sums of five or more squares, then even in the case when we fix four of the squares and let only one vary, for example $-----$ we see the set contains numbers divisible by all powers of $2$. Similarly, if we consider the sums of four squares, but instead consider the divisibility by an odd prime, then again the phenomena no longer holds. For example, ------ 

The combination of $p=2$ and sums of four squares is special in view of the following facts:
* Hensel's lemma does not hold true for certain cases and the quadratic $x^2+a$ and $p=2$ precisely fits the criteria.
* For a fixed number $a$, the set of integer polynomials $\{x^2+k : x \in N \}$ has numbers divisible by any high power of $2$ if and only if $k$ is of the form $4^m(8b+7)$.
* Legendre's three-square theorem: An integer $a$ can be written as sum of three or less squares if and only if $k$ is not of the form $4^m(8l+7)$.

Though the idea and exploration of the questions studied in this paper came from working on another paper that involved the study of the valuations of integer polynomials $\nu_2(x^2+k)$, the proofs presented here are straighforward, elementary and self-sufficient to appreciate the results. The first section of the paper lists all the results. The second section gives lemmas that needs to be used later and can be skipped altogether to go to the more insightful analysis in the third, fourth and fifth sections that studies the divisibility of sums of four squares by powers of $2$ while fixing one, two and three of the squares respectively. There are interesting connections with triangular numbers and so on in the proofs. The last section studies why the phenomena fails for any other combination of primes and the sums of squares.



Q: can N be replaced with Z?
Q: Mistake in Thm 3.9
Put fixing one at the top.











The highest power of 2 that divides a natural number $n$ is called valuation of $n$ with respect to 2, denoted by $\nu_2(n)$. 

So, for every $a$, we can find the highest power of $2$ that divides atleast one number in the set, call it as $\lambda(a)$. For the sets like $S(a)$, the $\lambda(a)$ is directly proportional to the highest power of $2$ that divides $a$. In view of this and the fact that the union of the sets $S(a)$ over natural numbers $a$ gives the set $S$, it is not surprising 
On the other hand, if we ask the question whether there exist a high enough power say $v$ such that no set $S(a)$ has any number divisible by $2^v$. The answer is negative. That is for any large numberThe highest power of $2$ that will divide any number of this subset depends on $a$, in particular related to the power of $4$ that divides $a$.

The divisibility by $2$ of the sequence of natural numbers follows a very predictable pattern. Every second number is 
divisible by $2$. Out of those numbers, that are even, every second is divisible by 4 and so on. In fact, . On the other hand,  Obviously this set will have infinitely many numbers divisible by any high power of $2$.   For example, fixing  

This paper studies the basic question of divisibility by $2$ of the subsets of the set $S$ obtained by fixing one or more of the squares and the results are counterintutitive.

For example, $\nu_2(12)=2$ since $4$ divides $12$ but not $8$. In view of above, the valuation with respect to 2 of the 
sequence of natural numbers is 0 for every other number, then out of the remaining numbers it is 1 for every other number and 
so on. It can be summarized as a valuation tree, pasted here:




This valuation tree is non-terminating, that is In this paper we study the valuations for sets that are composed of natural numbers coming from sums of four squares. The results again follows predictible, though somewhat non-intuitive patterns. However, this kind of predictibility in patterns is unwarranteed given that if we either change $p=2$ to any odd prime or increasing the number of squares to more than 4, then the pattern no longer holds. So, the combination of $p=2$ and sum of four squares is special, as discussed in the later part of the introduction. 

Lagrange's four-square theorem says every natural number can be written as a sum of four squares or less. Let $S = \{ a^2+b^2+c^2+d^2: a,b,c,d \in Z \}$, the question studied is very basic: what can we say about the valuation wrt $2$ 
of numbers in this set. For a natural number, say $n$, there are multiple ways to represent $n$ as sums of four squares given by a function denoted as $r_4(n)$. So, set $S$ effectively the set of natural numbers with each number repeating $r_4(n)$ number of times. As we know in case of the set of natural numbers, a fourth of them are divisible by $4$ but not $8$. What proportion of numbers in this set are divisible by $4$ but not $8$. It turns out that the answer is not the same as for the natural numbers but it is also very *regular* in the sense defined later. 

We go a step further and consider a collection of sets. So, essentially this collection of sets is obtained thru set $S$ by rearranging the numbers into boxes. If we unfold it, do we get the same S. No? There will be sets in this collection which no number is divisible by 

Moreover, the same analysis is done for the subsets of the above set S obtained by fixing one of the squares, we again get a 
pattern. The same is also true for even smaller subsets obtaining by fixing two or three squares. 
So, one might think whats so interesting about such sets having terms divisible by higher powers of $2$, it is but natural. 
But, no that is not the case. There is something special about $p=2$ and the sum of four squares. 
Consider the set $A = \{ n^2 + 1 + 0 + 0\}$ with $n$ taking all the integer values. This set has no term divisible by 3. 
Similarly, the set $B = \{ n^2 + 4 + 1 + 1\}$ has terms divisible by $3$ but not by $9$.

So what happens when we take five or more squares. It so happens that we might end up with a huge set with no numbers divisible
by certain high enough powers of 2, give example for $8$........


This special relation between sums of squares and prime $p=2$ happens for a reason. The valuations of all our above sets can be linked to the valuation of the polynomial $x^2+a$ where $a$ is a constant number and $x$ varies over natural numbers. There are certain facts:

This analysis is deeply connected to the function $r_k(n)$, the number of ways to represent $n$ as sum of $k$ squares, that distinctly re-appears at many interesting places in number theory and combinatorics.


Divide blog into sections with headings
