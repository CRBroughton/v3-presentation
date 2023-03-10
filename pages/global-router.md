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
    <p>Global router</p>
```ts {all|2|4-6|8|0}
import { router } from './trpc'
import { userRouter } from './routers/user'

export const appRouter = router({
  user: userRouter,
})

export type AppRouter = typeof appRouter
```
  </div>

  <div>
    <p>TRPC client plugin</p>
```ts {0|all|3|6-7|16-20}
import { createTRPCNuxtClient, httpBatchLink } from 'trpc-nuxt/client'
import superjson from 'superjson'
import type { AppRouter } from '~~/server/api/router'

export default defineNuxtPlugin(() => {
  // Consumes the AppRouter type
  const client = createTRPCNuxtClient<AppRouter>({
    transformer: superjson,
    links: [
      httpBatchLink({
        url: '/api/trpc',
      }),
    ],
  })

  return {
    provide: {
      client, // provides a type-safe client for the front-end
    },
  }
})

```
</div>

</div>

<!--
- Global router
- Imports the routers and adds them to the exported
global router
- Exports a type to define the global router
- Import AppRouter type
- Pass type to client for type inference
- Return type-safe client to the front end
-->