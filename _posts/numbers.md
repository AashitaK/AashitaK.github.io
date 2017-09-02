The divisibility by 2 of the sequence of natural numbers follows a very *regular* pattern. Every second number is odd, 
that is, it is not divisible by 2. Out of the remainining numbers, that are even numbers, every second is not divisible by 4. 
Then again among all the numbers divisible by 4, every second is not divisible by 8 and so on. The highest power of 2 that divides a natural number $n$ is called valuation of $n$ with respect to 2, denoted by $\nu_2(n)$. For example, $\nu_2(12)=2$ since $4$ divides $12$ but not $8$. The divisiblity pattern described above can be summarized as a valuation tree, pasted here:

So this valuation tree is completely figured out. We know that at any level, the left branch will terminates and the right 
one continues. The valuation trees can be used to represent the valuations of any integer sequence. Often times, such a clear picture is not available.

Lagrange's four-square theorem says every natural number can be written as a sum of four squares or less. For a natural number, say $n$, this representation is not unique. Infact, there is a well-known function called $r_4(n)$ that counts the number of ways $n$ can be represented as sums of four squares, not necessarily non-zero. So, if we considered a set of numbers S that is obtained by ......., the question I studied was very basic: what can we say about the valuation wrt $2$ of numbers in this set. As we know in case of the set of natural numbers, a fourth of them are divisible by $4$ but not $8$. What proportion of numbers in this set are divisible by $4$ but not $8$. It turns out that the answer is not the same as for the natural numbers but it is also very *regular* in the sense defined later. 

Moreover, the same analysis is done for the subsets of the above set S obtained by fixing one of the squares, we again get a pattern. The same is also true for even smaller subsets obtaining by fixing two or three squares. 
So, one might think whats so interesting about such sets having terms divisible by higher powers of $2$, it is but natural. But, no that is not the case. There is something special about $p=2$ and the sum of four squares. Consider the set $A = \{ n^2 + 1 + 0 + 0\}$ with $n$ taking all the integer values. This set has no term divisible by 3. Similarly, the set $B = \{ n^2 + 4 + 1 + 1\}$ has terms divisible by $3$ but not by $9$.

So what happens when we take five or more squares. It so haapens that we might end up with a huge set with no numbers divisible by certain high enough powers of 2, give example for $8$........


This special relation between sums of squares and prime $p=2$ happens for a reason. The valuations of all our above sets can be linked to the valuation of the polynomial $x^2+a$ where $a$ is a constant number and $x$ varies over natural numbers. There are certain facts:
* Hensel's lemma does not hold true for certain cases and the quadratic $x^2+a$ and $p=2$ precisely fits the criteria.
* The set of valuations of integer polynomials $\nu_2(x^2+a)$ is not bounded if and only if $a$ is of the form $4^m(8b+7)$.
* An integer $a$ can be written as sum of three or less squares if and only if $a$ is of the form $4^m(8b+7)$.


This analysis is deeply connected to the function $r_k(n)$, the number of ways to represent $n$ as sum of $k$ squares, that distinctly re-appears at many interesting places in number theory and combinatorics.


Divide blog into sections with headings
