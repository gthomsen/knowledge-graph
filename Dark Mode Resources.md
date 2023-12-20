Tags: #macos #firefox 

The following are resources for configuring dark mode across a variety of applications.  Useful when working in a low light environment or on a HDR display that has *really* bright whites.
# MacOS
In the Settings application, under `Appearance` set the theme to `Dark`.  For newer versions of OS X (at least 14.x), this does not change the top menu bar.  That is changed to a dark menu bar in `Accessibility -> Display` and toggling `Reduce transparency`.
# Firefox
Set `Settings -> General -> Language and Appearance -> Website Appearance` to `Dark`.
# Firefox Extensions
## Stylus
Provides custom CSS for specific sites.  Each style added to Stylus provides CSS for one site, so multiple styles are required. 

`userstyles.org` (typically referred to as USO) has long been under-maintained (unmaintained?) but still has a number of styles available.  A working mirror is hosted at [https://uso.kkx.one](https://uso.kkx.one).

The following table has a collection of useful styles.

| Name | Sites Affected | Style Page |
| --- | --- | --- |
| Amazon - Dark Slate | `amazon.com` and country-specific sites | https://userstyles.world/style/90/amazon-dark-slate |
| Dark-GitHub | `github.com`, `docs.github.com`, `gist.github.com`, `render.githubusercontent.com`, `viewscreen.githubusercontent.com` | https://userstyles.world/style/2/dark-github |
| Dark Gmail | `mail.google.com` | https://dark-by-dm-website.vercel.app/# |
| GNU Manuals - dark theme | `www.gnu.org/software/manual` | https://userstyles.world/style/10710/gnu-manuals-dark-theme |
| Stack Overflow Dark | Most every Stack Exchange site | https://userstyles.world/style/22/stack-overflow-dark |
| Wikipedia Dark | `wikipedia.org`, `m.wikidata.org`, `query.wikidata.org` | https://userstyles.world/style/17/wikipedia-dark |
| Reddit Old Redesigned Dark | `www.reddit.com`, `old.reddit.com` | https://userstyles.world/style/355/reddit-old-redesigned-dark |

## Dark Reader
Configure brightness and contrast on a per-site basis.  This sets a default for any page that isn't otherwise styled and appears to be complementary to [[#Stylus]] extensions.

[Firefox add-on page](https://addons.mozilla.org/en-US/firefox/addon/darkreader/). [Project home page](https://darkreader.org/).

# Freeplane
Freeplane doesn't have a native dark mode, but provides different dark templates for new files.  To set one, go to `Preferences -> Environment -> Files -> Standard Template File` and select a `.mm` that specifies the template.  Several dark mode templates are named `dark_*.mm`.  Once selected, one does not have to restart Freeplane for this update to take affect with new files.

Alternatively, one can simply make updates to the `standard-1.6-noEdgeColor.mm` file found in the user directory's `template/` subdirectory.  Go to `Tools -> Open user directory`, navigate to `template/` and open `standard-1.6-noEdgeColor.mm`.  Change the file's style as desired and then save it.  All newly created files will inherit the configured style.  A minimal update to get dark mode is to change the map's background color to gray via `Format -> Map background -> Background color`.
# Jupyter Notebooks
Notebooks can be themed on a per environment basis (one the desired theme is found, add it to the `base` Anaconda environment so clones pick it up).  Install the `jupyterthemes` package to get a set of themes:
```
conda install -c conda-forge jupyterthemes
```

Available themes can be listed with:
```
jt -l
```

Available dark themes as of 2023/12/20:
- `chesterish`
- `gruvboxd`
- `monokai`
- `oceans16`
- `onedork`
- `solarized`

Install a theme via:
```
jt -t <theme>
```

Open (or reload) a notebook for the style to be applied.