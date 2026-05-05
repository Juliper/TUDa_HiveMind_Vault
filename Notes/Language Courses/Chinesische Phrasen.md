---
title: Concept Name
aliases:
  - Alternative Name
tags:
  - topic-tag
description: "One-sentence summary of the concept."
draft: false
---

Main explanation goes here. Keep it focused on a single concept.

## Section

Content...

## Related Concepts

- [[Other Note]]: brief reason for the link

---
# Syntax
Full syntax docs: [https://quartz.jzhao.xyz/features/](https://quartz.jzhao.xyz/features/)

## Cool shit

### Comments
<!-- SYNTAX REFERENCE — delete everything below when using this template -->

---
### Callouts

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

---
### LaTeX

$$z = \sum_{i=1}^{n} w_i x_i + b = \mathbf{w}^\top \mathbf{x} + b$$

---
### Mermaid

```mermaid
graph LR
    A[Start] --> B{Decision}
    B -->|Yes| C[Result A]
    B -->|No| D[Result B]
```

```mermaid
sequenceDiagram
    Alice ->> Bob: Hello Bob, how are you?
    Bob-->> Alice: I am good thanks!
```

```mermaid
pie title NETFLIX
         "Time spent looking for movie" : 90
         "Time spent watching it" : 10

```

```mermaid
gitGraph:
    commit "Ashish"
    branch newbranch
    checkout newbranch
    commit id:"1111"
    commit tag:"test"
    checkout main
    commit type: HIGHLIGHT
    commit
    merge newbranch
    commit
    branch b2
    commit

```