# ![NLCST][logo]

**N**atural **L**anguage **C**oncrete **S**yntax **T**ree format.

* * *

Natural language for human and machine.

**NLCST** discloses the parts of natural language as a concrete syntax
tree.  Concrete means all information is stored in this tree and an
exact replica of the original document can be re-created.

**NLCST** is a subset of [**Unist**][unist], and implemented by
[**retext**][retext].

This document describes version 1.0.0 of **NLCST**.
[Changelog »][changelog]

## Table of Contents

*   [CST](#cst)
    *   [Root](#root)
    *   [Paragraph](#paragraph)
    *   [Sentence](#sentence)
    *   [Word](#word)
    *   [Symbol](#symbol)
    *   [Punctuation](#punctuation)
    *   [WhiteSpace](#whitespace)
    *   [Source](#source)
    *   [TextNode](#textnode)
*   [List of Utilities](#list-of-utilities)
*   [License](#license)

## CST

### `Root`

`Root` ([`Parent`][parent]) houses all nodes.

```idl
interface Root <: Parent {
  type: "RootNode";
}
```

### `Paragraph`

`Paragraph` ([`Parent`][parent]) represents a self-contained unit of
discourse in writing dealing with a particular point or idea.

```idl
interface Paragraph <: Parent {
  type: "ParagraphNode";
}
```

### `Sentence`

`Sentence` ([`Parent`][parent]) represents grouping of grammatically
linked words, that in principle tells a complete thought, although it
may make little sense taken in isolation out of context.

```idl
interface Sentence <: Parent {
  type: "SentenceNode";
}
```

### `Word`

`Word` ([`Parent`][parent]) represents the smallest element that may
be uttered in isolation with semantic or pragmatic content.

```idl
interface Word <: Parent {
  type: "WordNode";
}
```

### `Symbol`

`Symbol` ([`Text`][text]) represents typographical devices like
white space, punctuation, signs, and more, different from characters
which represent sounds (like letters and numerals).

```idl
interface Symbol <: Text {
  type: "SymbolNode";
}
```

### `Punctuation`

`Punctuation` ([`Symbol`][symbol]) represents typographical devices
which aid understanding and correct reading of other grammatical
units.

```idl
interface Punctuation <: Symbol {
  type: "PunctuationNode";
}
```

### `WhiteSpace`

`WhiteSpace` ([`Symbol`][symbol]) represents typographical devices
devoid of content, separating other grammatical units.

```idl
interface WhiteSpace <: Symbol {
  type: "WhiteSpaceNode";
}
```

### `Source`

`Source` ([`Text`][text]) represents an external (ungrammatical) value
embedded into a grammatical unit: a hyperlink, a line, and such.

```idl
interface Source <: Symbol {
  type: "SourceNode";
}
```

### `TextNode`

`TextNode` ([`Text`][text]) represents actual content in an NLCST
document: one or more characters.  Note that its `type` property
is `TextNode`, but it is different from the asbtract [`Text`][text]
interface.

```idl
interface TextNode < Text {
    type: "TextNode";
}
```

## List of Utilities

*   [`nlcst-is-literal`](https://github.com/syntax-tree/nlcst-is-literal)
    — Check whether a node is meant literally;
*   [`nlcst-normalize`](https://github.com/syntax-tree/nlcst-normalize)
    — Normalize a word for easier comparison;
*   [`nlcst-search`](https://github.com/syntax-tree/nlcst-search)
    — Search for patterns in an NLCST tree;
*   [`nlcst-to-string`](https://github.com/syntax-tree/nlcst-to-string)
    — Stringify a node;
*   [`nlcst-test`](https://github.com/syntax-tree/nlcst-test)
    — Validate a NLCST node;

In addition, see [**Unist**][unist] for other utilities which
work with **retext** nodes.

## License

MIT © Titus Wormer

<!--Definitions-->

[logo]: https://cdn.rawgit.com/syntax-tree/nlcst/f677854/logo.svg

[unist]: https://github.com/syntax-tree/unist

[retext]: https://github.com/wooorm/retext

[parent]: https://github.com/syntax-tree/unist#parent

[text]: https://github.com/syntax-tree/unist#text

[symbol]: #symbol

[changelog]: https://github.com/syntax-tree/nlcst/releases
