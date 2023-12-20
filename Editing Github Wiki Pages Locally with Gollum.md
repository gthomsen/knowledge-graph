[Gollum](https://github.com/gollum/gollum) is useful for editing a local, Markdown-based wiki and is *mostly* compatible with Github's Wiki.  Below are lessons learned about the differences between the two to avoid headaches when local edits in Gollum don't produce the desired effect in Github Wiki.  

***TL;DR*** In general, there are inconsistencies between the two and one must target Github Wiki's features even if they don't work in Gollum if you don't want to restrict yourself to a compatible subset of the two.

***NOTE:*** This has been derived from a private, Github Enterprise instance rather than the public Github instance.  In theory that should not affect things...

Github's [Wiki documentation](https://docs.github.com/en/communities/documenting-your-project-with-wikis/editing-wiki-content) explains that both WikiLink syntax (`[[Text]]`) and Markdown syntax (`[Text](link)`) is supported.

This [Github gist](https://gist.github.com/plokta/b5c5a4e2d435650dd2820354a90067c6) looks useful, though is several years old.

# Link Rendering
The WikiLinks syntax (`[[Text|link]]`) is supported in both Gollum and Github Wiki pages for internal pages.  `link` should not have a `.md` suffix.  External links use the Markdown syntax of `[Text](link)` and `link` should have a suffix.

Note that this is different than Github's Markdown rendering within a repository, where the Markdown link syntax is used.

One discrepancy between the two is where an internal link is used within a table and the vertical bar (`|`) must be escaped within the link, otherwise it will be misparsed as a table cell delimiter.  That is, links must look like `[[Text\|link]]` inside of table cells.  

***NOTE:*** Gollum v5.3.0 will render `Text\` as the link's text, while Github Wiki will render it as `Text`.

# Local Internal Link Anchors
Gollum and Github Wiki do not render local, internal link anchors the same way.  That is `[[Text|#anchor]]` works fine on Gollum, but creates a link to `#anchor#anchor` in Github Wiki.  Explicitly referencing the current page (which makes the link more brittle as it is now page-specific) seems to work in both, like so `[[Text|Current Page#anchor]]`.

# Anchor Normalization
Gollum and Github Wiki normalize local, internal link anchor names the same way.

Gollum will normalize `Ubuntu 22.04` to `#ubuntu-22-04` while Github Wiki will use `#ubuntu-2204`.
