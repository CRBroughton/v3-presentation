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
<div class="flex gap-10">
<div>
```mermaid {scale: 0.58}
graph TB
MU['User' Model]
MU --> UT
MU --> MM
MM['User' Model Migration]
MM --> DB
UT(('User' Type))
UT <--> UM
UM{'User' Mutation}
DB[(Database)]
DB <--> UT
FRNTUM([Front End Mutation])
UT2(('User' Type))
UM <--> UT2
UT2 <--> FRNTUM

style MU stroke:#fff;,stroke-width:2px
style MM stroke:#fff;,stroke-width:2px
style DB stroke:#fff;,stroke-width:2px
style UT stroke:#27609e;,stroke-width:2px
style UT2 stroke:#27609e;,stroke-width:2px
style FRNTUM stroke:#42b883;,stroke-width:2px
```
</div>

```ts {all|1|5|6|8-22|9|11-15|16-19|20|8-22}
import type { User } from '@prisma/client'
import { match } from 'ts-pattern'

export const store = () => {
  const { $client } = useNuxtApp()
  const user = ref<User>()

  const createUser = async (input: User) => {
    const { type, error, data } = await $client.user.createUser.mutate(input)

    match(type)
      .with(
        'error',
        () => { throw new Error(error?.message) },
      )
      .with(
        'ok',
        () => { user.value = data! },
      )
      .exhaustive()
  }

  return {
    user,
    createUser,
  }
}

```

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
- Mention the graph
- Import same User type from Prisma
- Destructuring the type-safe client from previous slide
- Create a User ref to store the user data
- 'createUser' function
- Access type-safe TRPC client
- Destructuring the backend responses
- Pattern matching against the type of response
- Exhaustively checking each possible response type
-->