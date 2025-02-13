<div class="alert alert-info">
<p>
We are currently updating the Lean community website to describe working with Lean 4,
but most of the information you will find here today still describes Lean 3.
</p>
<p>
Pull requests updating this page for Lean 4 are very welcome.
There is a link at the bottom of this page.
</p>
<p>
Please visit <a href="https://leanprover.zulipchat.com">the leanprover zulip</a>
and ask for whatever help you need during this transitional period!
</p>
<p>
The website for Lean 3 has been <a href="https://leanprover-community.github.io/lean3/">archived</a>.
If you need to link to Lean 3 specific resources please link there.
</p>
</div>

# Mathlib naming conventions

Author: [Jeremy Avigad](http://www.andrew.cmu.edu/user/avigad)

This guide is written for Lean 3.

### Names of symbols

When translating the statements of theorems into words, this dictionary is often used:

#### Logic

| symbol | shortcut | name                      | notes                                                               |
|--------|----------|---------------------------|---------------------------------------------------------------------|
| `∨`    | `\or`    | `or`                      |                                                                     |
| `∧`    | `\and`   | `and`                     |                                                                     |
| `→`    | `\r`     | `of`                      | the conclusion is stated first and the hypotheses are often omitted |
| `↔`    | `\iff`   | `iff`                     | sometimes omitted along with the right hand side of the iff         |
| `¬`    | `\n`     | `not`                     |                                                                     |
| `∃`    | `\ex`    | `exists` / `bex`          | `bex` stands for "bounded exists"                                   |
| `∀`    | `\fo`    | `all` / `forall` / `ball` | `ball` stands for "bounded forall"                                  |
| `=`    |          | `eq`                      | often omitted                                                       |
| `≠`    | `\ne`    | `ne`                      |                                                                     |
| `∘`    | `\o`     | `comp`                    |                                                                     |

#### Set

| symbol      | shortcut  | name               | notes |
|-------------|-----------|--------------------|-------|
| `∈`         | `\in`     | `mem`              |       |
| `∪`         | `\cup`    | `union`            |       |
| `∩`         | `\cap`    | `inter`            |       |
| `⋃`         | `\bigcup` | `Union` / `bUnion` |       |
| `⋂`         | `\bigcap` | `Inter` / `bInter` |       |
| `\`         | `\\`      | `sdiff`            |       |
| `ᶜ`         | `\^c`     | `compl`            |       |
| <code>{x &#124; p x}</code> |           | `set_of`           |       |
| `{x}`       |           | `singleton`        |       |
| `{x, y}`    |           | `pair`             |       |

#### Algebra

| symbol | shortcut              | name          | notes                                                       |
| ------ | --------------------- | ------------- | ----------------------------------------------------------- |
| `0`    |                       | `zero`        |                                                             |
| `+`    |                       | `add`         |                                                             |
| `-`    |                       | `neg` / `sub` | `neg` for the unary function, `sub` for the binary function |
| `1`    |                       | `one`         |                                                             |
| `*`    |                       | `mul`         |                                                             |
| `^`    |                       | `pow`         |                                                             |
| `/`    |                       | `div`         |                                                             |
| `•`    | `\bu`                 | `smul`        |                                                             |
| `⁻¹`   | `\-1`                 | `inv`         |                                                             |
| `⅟`    | `\frac1`              | `inv_of`      |                                                             |
| `∣`    | <code>\\&#124;</code> | `dvd`         |                                                             |
| `∑`    | `\sum`                | `sum`         |                                                             |
| `∏`    | `\prod`               | `prod`        |                                                             |

#### Lattices

| symbol | shortcut | name             | notes |
|--------|----------|------------------|-------|
| `<`    |          | `lt`             |       |
| `≤`    | `\le`    | `le`             |       |
| `⊔`    | `\sup`   | `sup`            |       |
| `⊓`    | `\inf`   | `inf`            |       |
| `⨆`    | `\supr`  | `supr` / `bsupr` |       |
| `⨅`    | `\infi`  | `infi` / `binfi` |       |
| `⊥`    | `\bot`   | `bot`            |       |
| `⊤`    | `\top`   | `top`            |       |

### General conventions

Identifiers are generally lower case with underscores. For the most
part, we rely on descriptive names. Often the name of theorem simply
describes the conclusion:

- `succ_ne_zero`
- `mul_zero`
- `mul_one`
- `sub_add_eq_add_sub`
- `le_iff_lt_or_eq`

If only a prefix of the description is enough to convey the meaning,
the name may be made even shorter:

- `neg_neg`
- `pred_succ`

Sometimes, to disambiguate the name of theorem or better convey the
intended reference, it is necessary to describe some of the
hypotheses. The word "of" is used to separate these hypotheses:

- `lt_of_succ_le`
- `lt_of_not_ge`
- `lt_of_le_of_ne`
- `add_lt_add_of_lt_of_le`

Sometimes abbreviations or alternative descriptions are easier to work
with. For example, we use `pos`, `neg`, `nonpos`, `nonneg` rather than
`zero_lt`, `lt_zero`, `le_zero`, and `zero_le`.

- `mul_pos`
- `mul_nonpos_of_nonneg_of_nonpos`
- `add_lt_of_lt_of_nonpos`
- `add_lt_of_nonpos_of_lt`

Sometimes the word "left" or "right" is helpful to describe variants
of a theorem.

- `add_le_add_left`
- `add_le_add_right`
- `le_of_mul_le_mul_left`
- `le_of_mul_le_mul_right`

An injectivity lemma that uses "left" or "right" should refer to the
argument that "changes". For example, a lemma with the statement
`a - b = a - c ↔ b = c` could be called `sub_right_inj`.

We can also use the word "self" to indicate a repeated argument:

- `mul_inv_self`
- `neg_add_self`

### Dots

Dots are used for namespaces, and also for automatically generated names
like recursors, eliminators and structure projections. They can also be
introduced manually, for example, where projector notation is
useful. Thus they are used in all of the following situations.

Intro, elim, and destruct rules for logical connectives, whether they
are automatically generated or not:

- `and.intro`
- `and.elim`
- `and.left`
- `and.right`
- `or.inl`
- `or.inr`
- `or.intro_left`
- `or.intro_right`
- `iff.intro`
- `iff.elim`
- `iff.mp`
- `iff.mpr`
- `not.intro`
- `not.elim`
- `eq.refl`
- `eq.rec`
- `eq.subst`
- `heq.refl`
- `heq.rec`
- `heq.subst`
- `exists.intro`
- `exists.elim`
- `true.intro`
- `false.elim`

Places where projection notation is useful, for example:

- `and.symm`
- `or.symm`
- `or.resolve_left`
- `or.resolve_right`
- `eq.symm`
- `eq.trans`
- `heq.symm`
- `heq.trans`
- `iff.symm`
- `iff.refl`

It is useful to use dot notation even for types which are not
inductive types. For instance, we use:

- `le.trans`
- `lt.trans_le`
- `le.trans_lt`

### Axiomatic descriptions

Some theorems are described using axiomatic names, rather than
describing their conclusions.

- `def`  (for unfolding a definition)
- `refl`
- `irrefl`
- `symm`
- `trans`
- `antisymm`
- `asymm`
- `congr`
- `comm`
- `assoc`
- `left_comm`
- `right_comm`
- `mul_left_cancel`
- `mul_right_cancel`
- `inj`  (injective)

### Variable conventions

- `u`, `v`, `w`, ... for universes
- `α`, `β`, `γ`, ... for generic types
- `a`, `b`, `c`, ... for propositions
- `x`, `y`, `z`, ... for elements of a generic type
- `h`, `h₁`, ...     for assumptions
- `p`, `q`, `r`, ... for predicates and relations
- `s`, `t`, ...      for lists
- `s`, `t`, ...      for sets
- `m`, `n`, `k`, ... for natural numbers
- `i`, `j`, `k`, ... for integers

Types with a mathematical content are expressed with the usual
mathematical notation, often with an upper case letter
(`G` for a group, `R` for a ring, `K` or `𝕜` for a field, `E` for a vector space, ...).
This convention is not followed in older files, where greek letters are used
for all types. Pull requests renaming type variables in these files are welcome.

### Names for symbols

- `imp`: implication
- `forall`
- `exists`
- `ball`: bounded forall
- `bex`: bounded exists

## Identifiers and theorem names

We generally use lower case with underscores for theorem names and
definitions. Sometimes upper case is used for bundled structures, such
as `Group`. In that case, use CamelCase for compound names, such as
`AbelianGroup`.

We adopt the following naming guidelines to make it easier for users
to guess the name of a theorem or find it using tab completion. Common
"axiomatic" properties of an operation like conjunction or
disjunction are put in a namespace that begins with the name of the
operation:

```lean
import logic.basic

#check and.comm
#check or.comm
#check and.assoc
#check or.assoc
```

In particular, this includes `intro` and `elim` operations for logical
connectives, and properties of relations:

```lean
import logic.basic

#check and.intro
#check and.elim
#check or.intro_left
#check or.intro_right
#check or.elim

#check eq.refl
#check eq.symm
#check eq.trans
```

Note however we do not do this for axiomatic arithmetic operations

```lean
import algebra.group.basic

#check mul_comm
#check mul_assoc
#check @mul_left_cancel  -- multiplication is left cancelative
```

For the most part, however, we rely on descriptive names. Often the
name of theorem simply describes the conclusion:

```lean
import algebra.ring.basic
open nat
#check succ_ne_zero
#check mul_zero
#check mul_one
#check @sub_add_eq_add_sub
#check @le_iff_lt_or_eq
```

If only a prefix of the description is enough to convey the meaning,
the name may be made even shorter:

```lean
import algebra.ordered_ring

#check @neg_neg
#check nat.pred_succ
```

When an operation is written as infix, the theorem names follow
suit. For example, we write `neg_mul_neg` rather than `mul_neg_neg` to
describe the patter `-a * -b`.

Sometimes, to disambiguate the name of theorem or better convey the
intended reference, it is necessary to describe some of the
hypotheses. The word "of" is used to separate these hypotheses:

```lean
import algebra.ordered_ring
open nat
#check lt_of_succ_le
#check lt_of_not_ge
#check lt_of_le_of_ne
#check add_lt_add_of_lt_of_le
```

The hypotheses are listed in the order they appear, _not_ reverse
order. For example, the theorem `A → B → C` would be named
`C_of_A_of_B`.

Sometimes abbreviations or alternative descriptions are easier to work
with. For example, we use `pos`, `neg`, `nonpos`, `nonneg` rather than
`zero_lt`, `lt_zero`, `le_zero`, and `zero_le`.

```lean
import algebra.ordered_ring
open nat
#check mul_pos
#check mul_nonpos_of_nonneg_of_nonpos
#check add_lt_of_lt_of_nonpos
#check add_lt_of_nonpos_of_lt
```

These conventions are not perfect. They cannot distinguish compound
expressions up to associativity, or repeated occurrences in a
pattern. For that, we make do as best we can. For example, `a + b - b = a`
could be named either `add_sub_self` or `add_sub_cancel`.

Sometimes the word "left" or "right" is helpful to describe variants
of a theorem.

```lean
import algebra.ordered_ring

#check add_le_add_left
#check add_le_add_right
#check le_of_mul_le_mul_left
#check le_of_mul_le_mul_right
```

## Naming of structural lemmas

We are trying to standardize certain naming patterns for structural lemmas.
At present these are not uniform across mathlib.

### Extensionality

A lemma of the form `(∀ x, f x = g x) → f = g` should be named `.ext`,
and labelled with the `@[ext]` attribute.
Often this type of lemma can be generated automatically by putting the
`@[ext]` attribute on a structure.
(However an automatically generated lemma will always be written in terms
of the structure projections, and often there is a better statement,
e.g. using coercions, that should be written by hand then marked with `@[ext]`.)

A lemma of the form `f = g ↔ ∀ x, f x = g x` should be named `.ext_iff`.

### Injectivity

Where possible, injectivity lemmas should be written in terms of an
`injective f` conclusion which use the full word `injective`, typically as `f_injective`.
The form `injective_f` still appears often in mathlib.

In addition to these, a variant should usually be provided as a bidirectional implication,
e.g. as `f x = f y ↔ x = y`, which can be obtained from `function.injective.eq_iff`.
Such lemmas should be named `f_inj`
(although if they are in an appropriate namespace `.inj` is good too).
Bidirectional injectivity lemmas are often good candidates for `@[simp]`.
There are still many unidirectional implications named `inj` in mathlib,
and it is reasonable to update and replace these as you come across them.

Note however that constructors for inductive types have
automatically generated unidirectional implications, named `.inj`,
and there is no intention to change this.
When such an automatically generated lemma already exists,
and a bidirectional lemma is needed, it may be named `.inj_iff`.

------
Copyright (c) 2016 Jeremy Avigad. All rights reserved.
Released under Apache 2.0 license as described in the file LICENSE.
Authors: Jeremy Avigad
