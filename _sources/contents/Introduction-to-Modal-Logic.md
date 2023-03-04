$\newcommand{\sem}[1]{[\![#1]\!]}$
# Introduction to Modal Logic

(draft) 

## Motivation

Superficially, modal logic adds to the propositional connectives $\wedge$ (and), $\vee$ (or), $\neg$ (not) two new connectives that allow us to take any formula $\phi$ and form two new formulas 

$$
\Box\phi\quad\quad\Diamond\phi.
$$

One of the reasons modal logic has been so important is that there are so many possible interpretations for these connectives. For example,
- $\Box\phi$ means necessarily $\phi$ and $\Diamond\phi$ means possibly $\phi$,
- $\Box\phi$ means always $\phi$ and $\Diamond\phi$ means sometimes $\phi$,
- $\Box_i\phi$ means agent $i$ knows $\phi$ and $\Diamond_i\phi$ means agent $i$ thinks $\phi$ is possible.

**(Temporal and Epistemic Logic)** Each of these interpretations created their own field of research. The first one dominated modal logic in the first half of the 20th century. The second one is known as temporal logic and has been playing an important role in computer science (verificiation, model checking) since the 1980ies. The third one is known as epistemic logic and continues to be cutting edge in philosophy, economics, software engineering, AI and other areas.

Besides temporal logic and epistemic logic there is also ... (insert more examples) ...

**(Fragments of First-Order Logic)** Another reason modal logic has been important is as a fragment of first-order logic. As we can see from the examples above, $\Box\phi$ is a universal quantifier (eg always) and $\Diamond\phi$ is an existential quantifier (eg sometimes). Consequently, modal logic is a fragment of first-order logic. In fact, modal logic is a fragment of first-order logic in at least two different but interesting ways:
- Modal logic is a decidable fragment of first-order logic.
- Modal logic is the bisimulation invariant fragment of first-order logic.

The first point has given rise to various generalisations of modal logic, in particular in the area of automated theorem proving. Search for [guarded fragment](https://www.google.com/search?q=%22guarded+fragment%22&oq=%22guarded+fragment%22&aqs=chrome..69i57j0j0i22i30l2.3319j1j4&sourceid=chrome&ie=UTF-8) for references. 

In the second point bisimulation refers to a relation of observational or behavioural equivalence of dynamic systems, which are themselves considered as "black boxes". In fact, bisimulation is the natural notion of behavioural equivalence for non-determinstic transition systems in which the states themselves are not observable but choices are. This leads us to the next item.

**(Possible Worlds Semantics)** The idea that something is necessarily true if it is true in all possible worlds is an old one. The turning point for modal logic was the mathematical formalisation of possible world semantics by Kripke:
- Saul Kripke: [A Completeness Theorem in Modal Logic](http://www.naturalthinker.net/trl/texts/Kripke,Saul/Kripke%20S.%20-%20A%20Completeness%20Theorem%20in%20Modal%20Logic.pdf). 1959.
- Saul Kripke: [Semantical Analysis of Modal Logic I](http://fitelson.org/142/kripke_1.pdf). 1963. I recommend Section 2.1, which also contains the solution to one of the exercises below.
- Saul Kripke: [Semantical Analysis of Modal Logic II](http://fitelson.org/142/kripke_2.pdf). 1965. 

There is a lot to say here, but to present the main ideas as quickly as possible I would proceed as follows (see Chapters 3.1 and 3.2 of the book referenced below).

**Definition:** Let $Prop$ be a set of 'propositional variables'. The language of modal logic is the smallest set of 'formulas' containing $Prop$ and closed under $\wedge$ , $\vee$, $\neg$, $\Box$, $\Diamond$.

**Definition:** Let $W$ be a set of 'worlds' and $R\subseteq W\times W$. Let $\sem{-}:Prop\to 2^W$ be a function assigning sets of worlds to each atomic proposition. Define
\begin{align}
\sem{\phi\wedge\phi'} &= \sem{\phi}\cap\sem{\phi'}\\
\sem{\phi\vee\phi'} &= \sem{\phi}\cup\sem{\phi'}\\
\sem{\neg\phi} &= W\setminus \sem{\phi}\\
\sem{\Box\phi} &= \{w\in W\mid \forall v\in W\,.\, v\in\sem{\phi}\}\\
\sem{\Diamond\phi} &= \{w\in W\mid \exists v\in W\,.\, v\in\sem{\phi}\}\\
\end{align}
and  

$$
(W,R)\models \phi
$$ 

iff $\sem{\phi}=W$ for all choices of $\sem{-}:Prop\to 2^W$. 

It is convenient to write 

$$
w\Vdash \phi \quad \stackrel{\rm  def}{\Longleftrightarrow} \quad w\in\sem{\phi}.
$$

The following exercise is a straightforward unvraveling of definitions:

**Exercise:** If $R$ is reflexive, then $(W,R)\models \Box p\to p$. 

A crucial observation that lets us glimpse the power of Kripke's approach is that the converse is also true. 

**Prop:** If $(W,R)\models \Box p\to p$, then $R$ is reflexive.

The proof is short once you know the trick. Try to find it for yourself before looking at the footnote.[^proof]

[^proof]: *Proof:* Let $w\in W$. Let $\sem{p}=\{v \mid wRv\}$. We know $w\Vdash\Box p$ by definition of $\sem{\Box p}$ and $w\Vdash \Box p\to p$ by assumption. It follows $w\Vdash p$, which implies $wRw$ by definition of $\sem{p}$.

The proof can be generalised to a method applying to all so-called Sahlqvist formulas and the area of modal logic is known as correspondence theory. We just look at one other basic example:

**Exercise:** $(W,R)\models \Box p\to\Box\Box p$ iff $R$ is transitive.

**Remark:** In the early 20th century modal logics where developed by philosophers from a syntactic and proof theoretic point of view. Axioms such as $\Box p\to p$ and $\Box\phi\to\Box\Box\phi$ where discovered by reading them as "necessarily p implies p" and "necessarily p implies necessarily necessarily p" and modal logics where characterised by axioms and proof rules. As far as I know the history, it came as a surprise that these axioms had such a neat semantic characterisation. 

**Exercise:** Interpret $\Box p\to p$ and $\Box p\to\Box\Box p$ from the point of view of temporal and epistemic logic.

#### Further Reading

The paper
- Halpern, Vardi: [Model Checking v. Theorem Proving: A Manifesto](https://www.cs.cornell.edu/home/halpern/papers/manifesto.pdf). 1991.

illustrates many of the themes that make modal logic so important for computer science applications.

## The Basic Theory of Modal Logic

We have seen that modal logic comprises several independent areas (temporal logic, epistemic logic, etc) and has important overlaps with others (concurrency, multi-agent systems, automated reasoning, game theory, etc). My intention here is only to sketch out the basic theory that is important in all these fields.

Actually, instead of writing this out myself, I refer to the book "Modal Logic" by Blackburn, de Rijke, Venema.(The book treats also $n$-ary relations (the "general case", as opposed to binary relations). This generalisation is interesting for some applications but should be skipped on a first reading.)

Here is what I would consider essential for a first run through the basics of modal logic.

- 1.2: Modal Languages 
- 1.3: Models and Frames
- 1.5: Semantic Consequence
- 1.6: Normal Modal Logics
- 2.1: Invariance Results (Def 2.10 and Prop 2.14)
- 2.2: Bisimulations (up to Thm 2.20)
- 2.3: Finite Models (can be skipped on first reading)
- 2.4: The Standard Translation (up to Prop 2.47)
- 3.1: Frame Definability (Exle 3.6)
- 3.2: Frame Definability and Second-Order Logic (Exle 3.11)


## References

Blackburn, de Rijke, Venema: "Modal Logic".


