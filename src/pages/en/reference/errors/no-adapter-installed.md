---
# NOTE: This file is auto-generated from 'scripts/error-docgen.mjs'
# Do not make edits to it directly, they will be overwritten.
# Instead, change this file: https://github.com/withastro/astro/blob/main/packages/astro/src/core/errors/errors-data.ts
# Translators, please remove this note and the <DontEditWarning/> component.

layout: ~/layouts/MainLayout.astro
title: Cannot use Server-side Rendering without an adapter.
i18nReady: true
githubURL: https://github.com/withastro/astro/blob/main/packages/astro/src/core/errors/errors-data.ts
setup: |
  import DontEditWarning from '../../../../components/DontEditWarning.astro';
---

<DontEditWarning />


> **NoAdapterInstalled**: Cannot use `output: 'server'` without an adapter. Please install and configure the appropriate server adapter for your final deployment. (E03017)

## What went wrong?
To use server-side rendering, an adapter needs to be installed so Astro knows how to generate the proper output for your targetted deployment platform.

**See Also:**
-  [Server-side Rendering](/en/guides/server-side-rendering/)
-  [Adding an Adapter](/en/guides/server-side-rendering/#adding-an-adapter)


