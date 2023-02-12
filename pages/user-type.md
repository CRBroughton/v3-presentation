---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
title: Why V3?
---
<div class="grid grid-cols-2">
<div>
```mermaid {scale: 0.7}
graph TB
MU['User' Model]
MU --> UT
MU --> MM
MM['User' Model Migration]
MM --> DB
UT(('User' Type))
DB[(Database)]
style MU stroke:#fff;,stroke-width:2px
style MM stroke:#fff;,stroke-width:2px
style DB stroke:#fff;,stroke-width:2px
style UT stroke:#27609e;,stroke-width:2px
```
</div>

<div>
Prisma Schema
```prisma
model User {
  id String @id @default(uuid())
  name String
  email String
  tasks Task[]
}
```
Generated 'User' Type
```ts
export type User = {
  id: string
  name: string
  email: string
}
```
</div>

<style>
.footnotes-sep {
  @apply mt-20 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>
</div>

<!--
- User type generated, matches model
-->