---
title:  "Extending GitHub Command Line Interface"
published: true
rubrica:
---

## gh create-repo

Using `gh api` and `gh alias --shell` add to `gh` 
an extension `gh create-repo` that creates the repo inside the given organization:

```
gh create-repo prueba-repo ULL-MII-SYTWS-2021
```

Use the GitHub REST API

## gh delete-repo

Lo mismo pero con delete:

```
gh delete-repo prueba-repo ULL-MII-SYTWS-2021
```

* GitHub API doc for [Delete repository](https://docs.github.com/es/rest/reference/repos#delete-a-repository)