Tags: #cheatsheet 

Derived from the following:
- [`adam-p/markdown-here`](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) 
- [Markdown Guide's Obsidian page](https://www.markdownguide.org/tools/obsidian/)

# Images
No standard syntax for linking images.

[Random gist](https://gist.githubusercontent.com/jongalloway/2e473d902406589db213c6cc1cb82e99/raw/65e5b3bd9eeb66926fae13192600c27aa8d9f69c/markdown-image-with-link.md)

```markdown
![Link Text - Possibly Alt Text](https://test.link/somewhere)
```

# Links
References to a section within the current document are done like so:

`[Link Text](#section-name)`

Where `#section-name` is always lower-case and hyphenated, regardless of how the section heading was formatted (e.g. upper-case and spaced).  Note that punctuation appears to be dropped from section names (e.g. the section `# Foo.Bar` is referenced by `#foobar`). There is no distinction between the section heading (i.e. `#Section Name` vs `###Section Name`).

Unclear if this is part of the specification, though Github supports it and so it is de facto specification that other tools follow (e.g. Pandoc).

# Tables

| Item | Price | Number |
| --- | --- | --- |
| Apples | 1.99 | 7 |
| Bananas | 0.45 | 20 |

```markdown
| Item | Price | Number |
| --- | --- | --- |
| Apples | 1.99 | 7 |
| Bananas | 0.45 | 20 |
```

Bars to separate columns, though outer pipes are optional.  At least 3 dashes separating header cells. 

Colons (`:`) can can bookend header cell entries to specify the column's justification:

| Left justified | Centered | Right Justified |
| --- | :---: | ---: |
| L | C | R |

```markdown
| Left justified | Centered | Right Justified |
| --- | :---: | ---: |
| L | C | R |
```

**NOTE:** [[Obsidian]] doesn't render tables in Live Preview, just in Reading mode.