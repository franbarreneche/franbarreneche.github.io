---
layout: post
title:  Angular new control syntax
date:   2023-06-20 21:15:00
description: New ways to write your templates!
tags: angular  rfc
categories: code
---
A new RFC has been submitted in the GitHub discussions of the Angular project.

You can find it at the following link: [Link](https://github.com/angular/angular/discussions/50719)

The RFC introduces a proposal for a new control flow syntax, which represents a substantial change to how the framework handles control flow.

Below is the proposed syntax for an "if" block:

```
{#if cond.expr}
  Main case was true!
{:else if other.expr}
  Extra case was true!
{:else}
  False case!
{/if}
```

Proposed syntax for a "switch" block:

```
{#switch cond.kind}
  {:case x}
    X case
  {:case y}
    Y case
  {:case z}
    Z case
  {:default}
    No case matched
{/switch}
```

Finally, proposed syntax for a "for" block:

```
{#for item of items; track item.id}
  item
{:empty}
  There were no items in the list.
{/for}
```

Please note that the syntax provided is just an example based on the information given. For more details and a comprehensive understanding of the proposed syntax, it is recommended to refer to the RFC document itself on the GitHub discussion page.