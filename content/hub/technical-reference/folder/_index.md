---
title: Reference
type: docs
url: "hub/technical-reference/folder"
---

## Introduction

Comprehensive reference for all Artbox branches. Each branch modifies specific files to implement features and functionality.

To get a full overview of all the C code changes, use this git command from the root of the Artbox repository:

```sh
GIT_PAGER=cat git diff --stat HEAD~1 HEAD -- . ':(exclude)plug-ins' ':(exclude)themes'
```

This compares the latest commit (HEAD) to the one before it (HEAD~1), excluding changes in the plug-ins/ and themes/ directories. The result is a concise summary of changes to core C source files.

## Branch Categories

{{< cards >}}
  {{< card link="Construction-Branches" title="Construction Branches" subtitle="All branches used in the Artbox staged construction pipeline" >}}
{{< /cards >}}

![technical](/images/gallery/at_the_seaside_tlined_final.webp)
