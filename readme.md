# ![nlcst][logo]

**N**atural **L**anguage **C**oncrete **S**yntax **T**ree format.

***

**nlcst** is a specification for representing natural language in a [syntax
tree][syntax-tree].
It implements the **[unist][]** spec.

This document may not be released.
See [releases][] for released documents.
The latest released version is [`1.0.2`][latest].

## Table of Contents

*   [Introduction](#introduction)
    *   [Where this specification fits](#where-this-specification-fits)
*   [Nodes](#nodes)
    *   [`Parent`](#parent)
    *   [`Literal`](#literal)
    *   [`Root`](#root)
    *   [`Paragraph`](#paragraph)
    *   [`Sentence`](#sentence)
    *   [`Word`](#word)
    *   [`Symbol`](#symbol)
    *   [`Punctuation`](#punctuation)
    *   [`WhiteSpace`](#whitespace)
    *   [`Source`](#source)
    *   [`Text`](#text)
*   [Glossary](#glossary)
*   [List of utilities](#list-of-utilities)
*   [Related](#related)
*   [References](#references)
*   [Contribute](#contribute)
*   [Acknowledgments](#acknowledgments)
*   [License](#license)

## Introduction

This document defines a format for representing natural language as a [concrete
syntax tree][syntax-tree].
Development of nlcst started in May 2014, in the now deprecated [textom][]
project for [retext][], before [unist][] existed.
This specification is written in a [Web IDL][webidl]-like grammar.

### Where this specification fits

nlcst extends [unist][], a format for syntax trees, to benefit from its
[ecosystem of utilities][utilities].

nlcst relates to [JavaScript][] in that it has an [ecosystem of
utilities][list-of-utilities] for working with compliant syntax trees in
JavaScript.
However, nlcst is not limited to JavaScript and can be used in other programming
languages.

nlcst relates to the [unified][] and [retext][] projects in that nlcst syntax
trees are used throughout their ecosystems.

## Nodes

### `Parent`

```idl
interface Parent <: UnistParent {
  children: [Paragraph | Sentence | Word | Symbol | Punctuation | WhiteSpace | Source]
}
```

**Parent** ([**UnistParent**][dfn-unist-parent]) represents a node in nlcst
containing other nodes (said to be [*children*][term-child]).

Its content is limited to only other nlcst content.

### `Literal`

```idl
interface Literal <: UnistLiteral {
  value: string
}
```

**Literal** ([**UnistLiteral**][dfn-unist-literal]) represents a node in nlcst
containing a value.

Its `value` field is a `string`.

### `Root`

```idl
interface Root <: Parent {
  type: "RootNode"
}
```

**Root** ([**Parent**][dfn-parent]) represents a document.

**Root** can be used as the [*root*][term-root] of a [*tree*][term-tree], never
as a [*child*][term-child].
Its content model is not limited, it can contain any nlcst content, with the
restriction that all content must be of the same category.

### `Paragraph`

```idl
interface Paragraph <: Parent {
  type: "ParagraphNode"
  children: [Sentence | WhiteSpace | Source]
}
```

**Paragraph** ([**Parent**][dfn-parent]) represents a unit of discourse dealing
with a particular point or idea.

**Paragraph** can be used in a [**root**][dfn-root] node.
It can contain [**sentence**][dfn-sentence], [**whitespace**][dfn-whitespace],
and [**source**][dfn-source] nodes.

### `Sentence`

```idl
interface Sentence <: Parent {
  type: "SentenceNode"
  children: [Word | Symbol | Punctuation | WhiteSpace | Source]
}
```

**Sentence** ([**Parent**][dfn-parent]) represents grouping of grammatically
linked words, that in principle tells a complete thought, although it may make
little sense taken in isolation out of context.

**Sentence** can be used in a [**paragraph**][dfn-paragraph] node.
It can contain [**word**][dfn-word], [**symbol**][dfn-symbol],
[**punctuation**][dfn-punctuation], [**whitespace**][dfn-whitespace], and
[**source**][dfn-source] nodes.

### `Word`

```idl
interface Word <: Parent {
  type: "WordNode"
  children: [Text | Symbol | Punctuation | Source]
}
```

**Word** ([**Parent**][dfn-parent]) represents the smallest element that may be
uttered in isolation with semantic or pragmatic content.

**Word** can be used in a [**sentence**][dfn-sentence] node.
It can contain [**text**][dfn-text], [**symbol**][dfn-symbol],
[**punctuation**][dfn-punctuation], and [**source**][dfn-source] nodes.

### `Symbol`

```idl
interface Symbol <: Literal {
  type: "SymbolNode"
}
```

**Symbol** ([**Literal**][dfn-literal]) represents typographical devices
different from characters which represent sounds (like letters and numerals),
white space, or punctuation.

**Symbol** can be used in [**sentence**][dfn-sentence] or [**word**][dfn-word]
nodes.

### `Punctuation`

```idl
interface Punctuation <: Literal {
  type: "PunctuationNode"
}
```

**Punctuation** ([**Literal**][dfn-literal]) represents typographical devices
which aid understanding and correct reading of other grammatical units.

**Punctuation** can be used in [**sentence**][dfn-sentence] or
[**word**][dfn-word] nodes.

### `WhiteSpace`

```idl
interface WhiteSpace <: Literal {
  type: "WhiteSpaceNode"
}
```

**WhiteSpace** ([**Literal**][dfn-literal]) represents typographical devices
devoid of content, separating other units.

**WhiteSpace** can be used in [**root**][dfn-root],
[**paragraph**][dfn-paragraph], or [**sentence**][dfn-sentence] nodes.

### `Source`

```idl
interface Source <: Literal {
  type: "SourceNode"
}
```

**Source** ([**Literal**][dfn-literal]) represents an external (ungrammatical)
value embedded into a grammatical unit: a hyperlink, code, and such.

**Source** can be used in [**root**][dfn-root], [**paragraph**][dfn-paragraph],
[**sentence**][dfn-sentence], or [**word**][dfn-word] nodes.

### `Text`

```idl
interface Text <: Literal {
  type: "TextNode"
}
```

**Text** ([**Literal**][dfn-literal]) represents actual content in nlcst
documents: one or more characters.

**Text** can be used in [**word**][dfn-word] nodes.

## Glossary

See the [unist glossary][glossary].

## List of utilities

See the [unist list of utilities][utilities] for more utilities.

*   [`nlcst-affix-emoticon-modifier`](https://github.com/syntax-tree/nlcst-affix-emoticon-modifier)
    — merge affix emoticons into the previous sentence
*   [`nlcst-emoji-modifier`](https://github.com/syntax-tree/nlcst-emoji-modifier)
    — support emoji
*   [`nlcst-emoticon-modifier`](https://github.com/syntax-tree/nlcst-emoticon-modifier)
    — support emoticons
*   [`nlcst-is-literal`](https://github.com/syntax-tree/nlcst-is-literal)
    — check whether a node is meant literally
*   [`nlcst-normalize`](https://github.com/syntax-tree/nlcst-normalize)
    — normalize a word for easier comparison
*   [`nlcst-search`](https://github.com/syntax-tree/nlcst-search)
    — search for patterns
*   [`nlcst-to-string`](https://github.com/syntax-tree/nlcst-to-string)
    — serialize a node
*   [`nlcst-test`](https://github.com/syntax-tree/nlcst-test)
    — validate a node
*   [`mdast-util-to-nlcst`](https://github.com/syntax-tree/mdast-util-to-nlcst)
    — transform mdast to nlcst
*   [`hast-util-to-nlcst`](https://github.com/syntax-tree/hast-util-to-nlcst)
    — transform hast to nlcst

## Related

*   [mdast](https://github.com/syntax-tree/mdast)
    — Markdown Abstract Syntax Tree format
*   [hast](https://github.com/syntax-tree/hast)
    — Hypertext Abstract Syntax Tree format
*   [xast](https://github.com/syntax-tree/xast)
    — Extensible Abstract Syntax Tree

## References

*   **unist**:
    [Universal Syntax Tree][unist].
    T. Wormer; et al.
*   **JavaScript**:
    [ECMAScript Language Specification][javascript].
    Ecma International.
*   **Web IDL**:
    [Web IDL][webidl],
    C. McCormack.
    W3C.

## Contribute

See [`contributing.md`][contributing] in [`syntax-tree/.github`][health] for
ways to get started.
See [`support.md`][support] for ways to get help.
Ideas for new utilities and tools can be posted in [`syntax-tree/ideas`][ideas].

A curated list of awesome syntax-tree, unist, mdast, hast, xast, and nlcst
resources can be found in [awesome syntax-tree][awesome].

This project has a [code of conduct][coc].
By interacting with this repository, organization, or community you agree to
abide by its terms.

## Acknowledgments

The initial release of this project was authored by
[**@wooorm**](https://github.com/wooorm).

Thanks to
[**@nwtn**](https://github.com/nwtn),
[**@tmcw**](https://github.com/tmcw),
[**@muraken720**](https://github.com/muraken720), and
[**@dozoisch**](https://github.com/dozoisch)
for contributing to nlcst and related projects!

## License

[CC-BY-4.0][license] © [Titus Wormer][author]

<!--Definitions-->

[license]: https://creativecommons.org/licenses/by/4.0/

[author]: https://wooorm.com

[logo]: https://raw.githubusercontent.com/syntax-tree/nlcst/0f9cce5/logo.svg?sanitize=true

[health]: https://github.com/syntax-tree/.github

[contributing]: https://github.com/syntax-tree/.github/blob/master/contributing.md

[support]: https://github.com/syntax-tree/.github/blob/master/support.md

[coc]: https://github.com/syntax-tree/.github/blob/master/code-of-conduct.md

[awesome]: https://github.com/syntax-tree/awesome-syntax-tree

[ideas]: https://github.com/syntax-tree/ideas

[releases]: https://github.com/syntax-tree/nlcst/releases

[latest]: https://github.com/syntax-tree/nlcst/releases/tag/1.0.2

[list-of-utilities]: #list-of-utilities

[dfn-unist-parent]: https://github.com/syntax-tree/unist#parent

[dfn-unist-literal]: https://github.com/syntax-tree/unist#literal

[dfn-parent]: #parent

[dfn-literal]: #literal

[dfn-root]: #root

[dfn-paragraph]: #paragraph

[dfn-sentence]: #sentence

[dfn-word]: #word

[dfn-symbol]: #symbol

[dfn-punctuation]: #punctuation

[dfn-whitespace]: #whitespace

[dfn-text]: #text

[dfn-source]: #source

[term-tree]: https://github.com/syntax-tree/unist#tree

[term-child]: https://github.com/syntax-tree/unist#child

[term-root]: https://github.com/syntax-tree/unist#root

[unist]: https://github.com/syntax-tree/unist

[syntax-tree]: https://github.com/syntax-tree/unist#syntax-tree

[javascript]: https://www.ecma-international.org/ecma-262/9.0/index.html

[webidl]: https://heycam.github.io/webidl/

[glossary]: https://github.com/syntax-tree/unist#glossary

[utilities]: https://github.com/syntax-tree/unist#list-of-utilities

[unified]: https://github.com/unifiedjs/unified

[retext]: https://github.com/retextjs/retext

[textom]: https://github.com/wooorm/textom
