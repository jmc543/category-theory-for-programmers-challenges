# Category Theory for Programmers Challenges

## 3. Categories Great and Small

### 3.1. Generate a free category from:

#### 3.1.1. A graph with one node and no edges

Each node needs an edge to itself.

```dot
digraph G {
  singlenode -> singlenode [label="id"]
}
```

![A graph with one node and one id edge](https://rawgit.com/awalterschulze/category-theory-for-programmers-challenges/master/103-1-1.png "A graph with one node and one id edge")

#### 3.1.2. A graph with one node and one (directed) edge (hint: this edge can be composed with itself)

Each node needs an edge to itself that is the id edge.
If the existing edge is the id edge, then we don't need another edge, but otherwise we do.

```dot
digraph G {
  singlenode -> singlenode [label="id"]
  singlenode -> singlenode [label="existing"]
}
```

![A graph with one node and two edges](https://rawgit.com/awalterschulze/category-theory-for-programmers-challenges/master/103-1-2.png "A graph with one node and two edges")

#### 3.1.3. A graph with two nodes and a single arrow between them

Each node needs an id edge to itself.

```dot
digraph G {
  nodeone -> nodetwo [label="existing"]
  nodeone -> nodeone [label="id"]
  nodetwo -> nodetwo [label="id"]
}
```

![A graph with two nodes](https://rawgit.com/awalterschulze/category-theory-for-programmers-challenges/master/103-1-3.png "A graph with two nodes")

#### 3.1.4. A graph with a single node and 26 arrows marked with the letters of the alphabet: a, b, c ... z.

Each node needs an id edge to itself.

```dot
digraph G {
  singlenode -> singlenode [label="a"]
  singlenode -> singlenode [label="b"]
  singlenode -> singlenode [label="c"]
  singlenode -> singlenode [label="d"]
  singlenode -> singlenode [label="e"]
  singlenode -> singlenode [label="f"]
  singlenode -> singlenode [label="g"]
  singlenode -> singlenode [label="h"]
  singlenode -> singlenode [label="i"]
  singlenode -> singlenode [label="j"]
  singlenode -> singlenode [label="k"]
  singlenode -> singlenode [label="l"]
  singlenode -> singlenode [label="m"]
  singlenode -> singlenode [label="n"]
  singlenode -> singlenode [label="o"]
  singlenode -> singlenode [label="p"]
  singlenode -> singlenode [label="q"]
  singlenode -> singlenode [label="r"]
  singlenode -> singlenode [label="s"]
  singlenode -> singlenode [label="t"]
  singlenode -> singlenode [label="u"]
  singlenode -> singlenode [label="v"]
  singlenode -> singlenode [label="w"]
  singlenode -> singlenode [label="x"]
  singlenode -> singlenode [label="y"]
  singlenode -> singlenode [label="z"]
  singlenode -> singlenode [label="id"]
}
```

![A graph with 27 edges](https://rawgit.com/awalterschulze/category-theory-for-programmers-challenges/master/103-1-4.png "A graph with 27 edges")

### 3.2. What kind of order is this?

#### 3.2.1. A set of sets with the inclusion relation: A is included in B if every element of A is also an element of B.

Our morphisms are subset relations. Every set includes itself, A ⊆ A. Inclusion is also composable.
A ⊆ B and B ⊆ C implies A ⊆ C.  This means that we at least have a preorder.
If A ⊆ B and B ⊆ A then A = B, which means that we at least have a partial order.
Not all objects are a subset of each other though. For example {1} and {2,3} are not subsets of each other.
This means we don't have a total order and only a partial order.

#### 3.2.2. C++ types with the following subtyping relation: T1 is a subtype of T2 if a pointer to T1 can be passed to a function that expects a pointer to T2 without triggering a compilation error.

Our morphisms are subtypes. Every type includes itself as a subtype. Subtypes are also composable.
This means that we at least have a preorder.
I am not sure, since I am not familiar with C++, but I assume that if A can be passed to a function expecting a B and B can be passed to a function expecting an A then A = B, which means that we at least have a partial order.
Not all types are subtypes of each other.  So we don't have a total order, only a partial order.

### 3.3. Considering that Bool is a set of two values True and False, show that it forms two (set-theoretical) monoids with respect to, respectively, operator && (AND) and || (OR).

A monoid is a binary relation that needs to be associative and have a special element that behaves like unit.
Boolean operators AND and OR are both associative:

  a && (b && c) = (a && b) && c
  a || (b || c) = (a || b) || c

AND has the special element TRUE:

  a && true = a
  true && a = a

OR has the special element FALSE:

  a || false = a
  false || a = a

### 3.4. Represent the Bool monoid with the AND operator as a category: List the morphisms and their rules of composition.

```dot
digraph G {
  TRUE -> TRUE [label="AND TRUE (id)"]
  TRUE -> FALSE [label="AND FALSE"]
  FALSE -> FALSE [label="AND TRUE (id)"]
  FALSE:nw -> FALSE:nw [label="AND FALSE"]
}
```

![And category](https://rawgit.com/awalterschulze/category-theory-for-programmers-challenges/master/103-4.png "And category")

### 3.5. Represent addition modulo 3 as a monoid category.

```dot
digraph G {
  0 -> 0 [label="(_ + 0) % 3 => id"]
  0 -> 1 [label="(_ + 1) % 3"]
  0 -> 2 [label="(_ + 2) % 3"]
  1 -> 1 [label="(_ + 0) % 3 => id"]
  1 -> 2 [label="(_ + 1) % 3"]
  1 -> 0 [label="(_ + 2) % 3"]
  2 -> 2 [label="(_ + 0) % 3 => id"]
  2 -> 0 [label="(_ + 1) % 3"]
  2 -> 1 [label="(_ + 2) % 3"]
}
```

![Modulo 3](https://rawgit.com/awalterschulze/category-theory-for-programmers-challenges/master/103-5.png "Modulo 3")