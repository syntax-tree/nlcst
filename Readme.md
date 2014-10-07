# ![NLCST](http://wooorm.com/nlcst.png)

Natural language for human and machine.

---

> Note: Several projects use this document. Do not make changes without consulting with [TextOM](https://github.com/wooorm/textom),  [parse-latin](https://github.com/wooorm/parse-latin), and [retext](https://github.com/wooorm/retext).

## CST

### Node

Node represents any unit in NLCST hierarchy.

```
interface Node {
    type: string;
    data: Data | null;
}
```

### Data

Data represents data associated with any node. Data is a scope for plug-ins to store any information. Its only limitation being that each property should by stringifyable: not throw when passed to `JSON.stringify()`.

```
interface Data { }
```

### Parent

Parent ([Node](#node)) represents a unit in NLCST hierarchy which can have zero or more children.

```
interface Parent <: Node {
    children: [];
}
```

### Text

Text ([Node](#node)) represents a unit in NLCST hierarchy which has value.

```
interface Text <: Node {
    value: string;
}
```

### RootNode

Root ([Parent](#parent)) represents a document.

```
interface RootNode < Parent {
    type: "RootNode";
}
```

### ParagraphNode

Paragraph ([Parent](#parent)) represents a self-contained unit of discourse in writing dealing with a particular point or idea.

```
interface ParagraphNode < Parent {
    type: "ParagraphNode";
}
```

### SentenceNode

Sentence ([Parent](#parent)) represents grouping of grammatically linked words, that in principle tells a complete thought, although it may make little sense taken in isolation out of context.

```
interface SentenceNode < Parent {
    type: "SentenceNode";
}
```

### WordNode

Word ([Parent](#parent)) represents the smallest element that may be uttered in isolation with semantic or pragmatic content.

```
interface WordNode < Parent {
    type: "WordNode";
}
```

### PunctuationNode

Punctuation ([Parent](#parent)) represents typographical devices which aids understanding and correct reading of other grammatical units.

```
interface PunctuationNode < Parent {
    type: "PunctuationNode";
}
```

### WhiteSpaceNode

White Space ([PunctuationNode](#punctuation)) represents typographical devices devoid of content, separating other grammatical units.

```
interface WhiteSpaceNode < PunctuationNode {
    type: "WhiteSpaceNode";
}
```

### SourceNode

Source ([Text](#text)) represents an external (ungrammatical) value embedded into a grammatical unit: a hyperlink, an emoticon, and such.

```
interface SourceNode < Text {
    type: "SourceNode";
}
```

### TextNode

Text ([Text](#text)) represents actual content in an NLCST document: one or more characters.

```
interface TextNode < Text {
    type: "TextNode";
}
```

## Related

- [retext](https://github.com/wooorm/retext) — Analyse and Manipulate natural language, 20+ plug-ins.
- [parse-latin](https://github.com/wooorm/parse-latin) — Transforms latin-script natural language into a CST;
- [TextOM](https://github.com/wooorm/textom) — Provides an object-oriented manipulation interface to NLCST;
- [nlcst-to-string](https://github.com/wooorm/nlcst-to-string) — Transforms a CST into a string;

## License

MIT © Titus Wormer
