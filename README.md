# trapd00r/LS\_COLORS as a Zsh/NPM package

##### NPM link: [https://www.npmjs.com/package/zsh-ls\_colors](https://www.npmjs.com/package/zsh-ls_colors)

| **Package source:** | Tarball | Git | Node | Gem |
|---------------------|---------|-----|------|-----|
| **Status:**         |    -    |  +  |  –   |  –  |

[Zplugin](https://github.com/zdharma/zplugin) can use the NPM package registry
to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
    - there can be multiple lists of ices,
    - the ice lists are stored in *profiles*; there's at least one profile, *default*,
    - the ices can be selectively overriden.

Example invocations that'll install
[trapd00r/LS\_COLORS](https://github.com/trapd00r/LS_COLORS) from Git
repository in the most optimized way as described on the [Zplugin
Wiki](http://zdharma.org/zplugin/wiki/LS_COLORS-explanation/):

```zsh
# Download the default profile
zplugin pack for ls_colors

# Download the no-zsh-completion profile
zplugin pack"no-zsh-completion" for ls_colors

# Download the no-dir-color-swap profile
zplugin pack"no-dir-color-swap" for ls_colors
```

## Default Profile

Provides the LS\_COLORS definitions for GNU `ls`, `ogham/exa` and also setups
zsh-completion system to use the definitions. It also edits the color for the
directory (see the details in the `no-dir-color-swap` profile section).

The Zplugin command executed will be equivalent to:

```zsh
zplugin wait"0c" lucid reset \
 atclone"local P=${${(M)OSTYPE:#*darwin*}:+g}
    \${P}sed -i '/DIR/c\DIR 38;5;63;1' LS_COLORS; \
    \${P}dircolors -b LS_COLORS > c.zsh" \
 atpull'%atclone' pick"c.zsh" nocompile'!' \
 atload'zstyle ":completion:*:default" list-colors "${(s.:.)LS_COLORS}";' for \
    trapd00r/LS_COLORS
```

## `no-zsh-completion` Profile

Provides the LS\_COLORS definitions for GNU `ls`, `ogham/exa` but doesn't set up
the zsh-completion system to use them.

The Zplugin command executed will be equivalent to:

```zsh
zplugin wait"0c" lucid reset \
 atclone"local P=${${(M)OSTYPE:#*darwin*}:+g}
    \${P}sed -i '/DIR/c\DIR 38;5;63;1' LS_COLORS; \
    \${P}dircolors -b LS_COLORS > c.zsh" \
 atpull'%atclone' pick"c.zsh" nocompile'!' for \
    trapd00r/LS_COLORS
```

## `no-dir-color-swap` Profile

Provides the LS\_COLORS definitions like the `default` profile, however doesn't
edit the definitions file and doesn't change the color for directories. The
color is being edited in the default profile because the author found it to be
too dark.

The Zplugin command executed will be equivalent to:

```zsh
zplugin wait"0c" lucid \
 atclone"${${(M)OSTYPE:#*darwin*}:+g}dircolors -b LS_COLORS > c.zsh" \
 atpull'%atclone' pick"c.zsh" nocompile'!' \
 atload'zstyle ":completion:*:default" list-colors "${(s.:.)LS_COLORS}";' for \
    trapd00r/LS_COLORS
```

<!-- vim:set ft=markdown tw=80 fo+=an1 autoindent: -->
