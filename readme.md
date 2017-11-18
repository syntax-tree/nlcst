# ![NLCST][logo]

**N**atural **L**anguage **C**oncrete **S**yntax **T**ree format.

* * *

Natural language for human and machine.

**NLCST** discloses the parts of natural language as a concrete syntax
tree.  Concrete means all information is stored in this tree and an
exact replica of the original document can be re-created.

**NLCST** is a subset of [**Unist**][unist], and implemented by
[**retext**][retext].

This document may not be released. See [releases][] for released
documents. The latest released version is [`1.0.0`][latest].

## Table of Contents

*   [List of Utilities](#list-of-utilities)
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
*   [Related](#related)
*   [Contribute](#contribute)
*   [Acknowledgments](#acknowledgments)
*   [License](#license)

## List of Utilities

*   [`nlcst-is-literal`](https://github.com/syntax-tree/nlcst-is-literal)
    — Check whether a node is meant literally
*   [`nlcst-normalize`](https://github.com/syntax-tree/nlcst-normalize)
    — Normalize a word for easier comparison
*   [`nlcst-search`](https://github.com/syntax-tree/nlcst-search)
    — Search for patterns in an NLCST tree
*   [`nlcst-to-string`](https://github.com/syntax-tree/nlcst-to-string)
    — Stringify a node
*   [`nlcst-test`](https://github.com/syntax-tree/nlcst-test)
    — Validate a NLCST node

In addition, see [**Unist**][unist] for other utilities which
work with **retext** nodes.

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

## Related

*   [retext][]
*   [unist][]
*   [vfile][]
*   [hast][]
*   [mdast][]

## Contribute

**nlcst** is built by people just like you!  Check out
[`contribute.md`][contribute] for ways to get started.

This project has a [Code of Conduct][coc].  By interacting with this repository,
organisation, or community you agree to abide by its terms.

Want to chat with the community and contributors?  Join us in [Gitter][chat]!

Have an idea for a cool new utility or tool?  That’s great!  If you want
feedback, help, or just to share it with the world you can do so by creating
an issue in the [`syntax-tree/ideas`][ideas] repository!

## Acknowledgments

The initial release of this project was authored by
[**@wooorm**](https://github.com/wooorm).

Thanks to [**@nwtn**](https://github.com/nwtn),
[**@tmcw**](https://github.com/tmcw),
[**@muraken720**](https://github.com/muraken720), and
[**@dozoisch**](https://github.com/dozoisch) for contributing commits since!

## License

MIT © Titus Wormer

<!--Definitions-->

[logo]: https://cdn.rawgit.com/syntax-tree/nlcst/d9fe388/logo.svg

[unist]: https://github.com/syntax-tree/unist

[retext]: https://github.com/wooorm/retext

[parent]: https://github.com/syntax-tree/unist#parent

[text]: https://github.com/syntax-tree/unist#text

[symbol]: #symbol

[releases]: https://github.com/syntax-tree/nlcst/releases

[latest]: https://github.com/syntax-tree/nlcst/releases/tag/1.0.0

[retext]: https://github.com/wooorm/retext

[vfile]: https://github.com/vfile/vfile

[unist]: https://github.com/syntax-tree/unist

[hast]: https://github.com/syntax-tree/hast

[mdast]: https://github.com/syntax-tree/mdast

[contribute]: contributing.md

[coc]: code-of-conduct.md

[ideas]: https://github.com/syntax-tree/ideas

[chat]: https://gitter.im/wooorm/retext
