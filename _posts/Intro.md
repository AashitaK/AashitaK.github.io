Lagrange's four-square theorem says every natural number can be written as a sum of four squares or less. Let $S = \{ a^2+b^2+c^2+d^2: a,b,c,d \in N \}$, then set $S$ is effectively the set of natural numbers with each number repeating a certain number of times. Given any power of $2$ no matter how high say $v$, there are infinitely many natural numbers that are divisible by $2^v$ spread out at regular intervals of length $2^v$. Consequently, there are infinitely many numbers divisible by any high power of $2$ in the set $S$ as well. However, if we put a restriction on this set $S$, say we fix one of the four squares $a^2$ while letting $b,c$ and $d$ vary over all natural numbers as above, then the study of the divisibility by powers of $2$ of the subset we thus obtained say $S(a)$ gives counterintuitive results. We no longer have numbers divisible by high enough powers of $2$ in the set $S(a)$. On the other hand, if we ask the question whether there exist a high enough power say $v$ such that no set $S(a)$ has any number divisible by $2^v$. The answer is negative. That is for any large numberThe highest power of $2$ that will divide any number of this subset depends on $a$, in particular related to the power of $4$ that divides $a$.

The divisibility by $2$ of the sequence of natural numbers follows a very predictable pattern. Every second number is 
divisible by $2$. Out of those numbers, that are even, every second is divisible by 4 and so on. In fact, . On the other hand,  Obviously this set will have infinitely many numbers divisible by any high power of $2$.   For example, fixing  

This paper studies the basic question of divisibility by $2$ of the subsets of the set $S$ obtained by fixing one or more of the squares and the results are counterintutitive.
The highest power of 2 that divides a natural number $n$ is called valuation of $n$ with respect to 2, denoted by $\nu_2(n)$. 
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
* Hensel's lemma does not hold true for certain cases and the quadratic $x^2+a$ and $p=2$ precisely fits the criteria.
* The set of valuations of integer polynomials $\nu_2(x^2+a)$ is not bounded if and only if $a$ is of the form $4^m(8b+7)$.
* An integer $a$ can be written as sum of three or less squares if and only if $a$ is of the form $4^m(8b+7)$.


This analysis is deeply connected to the function $r_k(n)$, the number of ways to represent $n$ as sum of $k$ squares, that distinctly re-appears at many interesting places in number theory and combinatorics.


Divide blog into sections with headings
