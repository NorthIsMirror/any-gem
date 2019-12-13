# `any-gem` Zsh package

| **Package source:** | Source Tarball | Binary | Git | Node | Gem |
|:-------------------:|:--------------:|:------:|:---:|:----:|:---:|
| **Status:**         |        -       |  -     |  -  |  –   |  + <br> (default)  |

## Introduction

[Zplugin](https://github.com/zdharma/zplugin) can use a `package.json`
(similar in construct to the one used in `npm` packages) to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
    - there can be multiple lists of ices,
    - the ice lists are stored in *profiles*; there's at least one profile, *default*,
    - the ices can be selectively overriden.

## The `any-gem` Package

This package is special – it is designed for easy installing of any Ruby Gems
locally inside the plugin directory, exposing their binaries via *shims* (i.e.:
forwarder scripts) created automatically by
[Bin-Gem-Node](https://github.com/zplugin/z-a-bin-gem-gem) annex.

The Ruby Gem(s) to install are specified by the `param'MOD → {gem1}; MOD2 →
{gem2}; …'` ice. The name of the plugin will be `{gem1}`, unless `id-as''` ice
will be provided, or the `IDAS` param will be set (i.e.: `param'IDAS →
my-plugin'; MOD → …`).

A few example invocations:

```zsh
# Install `chef' Gem and call the plugin with the same name
zplugin pack param='MOD → chef' for any-gem

# Install `rails' Gem and call the plugin: ruby-on-rails
zplugin id-as=ruby-on-rails pack param='MOD → remark-man; MOD2 → remark-cli' for any-gem

# Install `jekyll' Gem and call the plugin: jkl
zplugin pack param='IDAS → jkl; MOD → pen' for any-gem
```

## Default Profile

The only profile that does all the magic. It relies on the `%PARAM%` keywords,
which are substituted with the `value` from the ice `param'PARAM → value; …'`.

The Zplugin command executed will be equivalent to:

```zsh
zplugin lucid id-as="${${:-%IDAS%}:-%MOD%}" as=null \
    gem="%MOD%;%MOD2%;%MOD3%;%MOD4%;%MOD5%;%MOD6%;%MOD7%;%OTHER%" \
    sbin="n:bin/*" for \
        zdharma/null
```

The package is thus a simplifier of Zplugin commands.

<!-- vim:set ft=markdown tw=80 fo+=an1 autoindent: -->
