> [!NOTE]
> For issue outlined in https://github.com/vercel/next.js/issues/94499

## To reproduce

1. Clone repo
2. Install packages `pnpm i`
3. Open [instrumentation.ts](/instrumentation.ts)

The code within `instrumentation.ts` is an exact copy of the sample within the [next.js docs](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#onrequesterror-optional). Despite the docs saying the following:
> Types: 
> ```typescript
> export function onRequestError(
>   error: { digest: string } & Error,
>   request: {
>     path: string // resource path, e.g. /blog?name=foo
>     method: string // request method. e.g. GET, POST, etc
>     headers: { [key: string]: string | string[] }
>   },
>   context: {
>     routerKind: 'Pages Router' | 'App Router' // the router type
>     routePath: string // the route file path, e.g. /app/blog/[dynamic]
>     routeType: 'render' | 'route' | 'action' | 'proxy' // the context in which the error occurred
>     renderSource:
>       | 'react-server-components'
>       | 'react-server-components-payload'
>       | 'server-rendering'
>     revalidateReason: 'on-demand' | 'stale' | undefined // undefined is a normal request without revalidation
>     renderType: 'dynamic' | 'dynamic-resume' // 'dynamic-resume' for PPR
>   }
> ): void | Promise<void>
> ```
> - **`error`: The caught error itself (type is always Error), and a digest property which is the unique ID of the error.**
> - `request`: Read-only request information associated with the error.
> - `context`: The context in which the error occurred. This can be the type of router (App or Pages Router), and/or (Server Components (`'render'`), Route Handlers (`'route'`), Server Actions (`'action'`), or Proxy (`'proxy'`)).


Type `err` shows up as `unknown`
![Screenshot of LSP highlighting 'err' is of type 'unknown'.](/public/typescript-error.png)