# How NextJs works ?

Before we learn more advanced Next.js features, it would be helpful to understand the basics of how Next.js works. Let's see the journey of the Next.js applications.

Next.js provides a framework to structure your application, and optimizations that help make both the development process and final application faster. And to know how Next.js works, we’ll look at what happens to your application code during these different stages:

- The environment where your code runs: `Development vs. Production`
- When your code runs: `Build Time vs. Runtime`
- Where rendering happens: `Client vs. Server`

## Development and Production Environments

You can think of environments as the context in which your code is running.<br/><br/>
**_Development_** : building and running the application on your local machine.<br/>
**_Production_** : process of making your application ready to be deployed and consumed by users.<br/>

Next.js provides features for both the development and production stages of an application.

### Development

In the development stage, Next.js optimizes for the developer and their experience building the application. It comes with features that aim to improve the Developer Experience such the [TypeScript](https://nextjs.org/docs/pages/building-your-application/configuring/typescript) and [ESLint integration](https://nextjs.org/docs/pages/building-your-application/configuring/eslint), [Fast Refresh](https://nextjs.org/docs/architecture/fast-refresh), and more.

### Production

In the production stage, Next.js optimizes for the end-users, and their experience using the application. It aims to transform the code to make it `performant and accessible`.

but how Next.js implement this ?

Since each environment has different considerations and goals, there is a lot that needs to be done to move an application from development to production. For instance, the application code needs to be **_compiled, bundled, minified, and code split_**.

The Next.js Compiler handles much of these code transformations and underlying infrastructure to make it easier for your application to go to production.
This is made possible because Next.js has a compiler written in Rust, a low-level programming language, and [SWC](https://nextjs.org/docs/architecture/nextjs-compiler), a platform that can be used for [compilation](https://nextjs.org/learn/foundations/how-nextjs-works/compiling), [minification](https://nextjs.org/learn/foundations/how-nextjs-works/minifying), [bundling](https://nextjs.org/learn/foundations/how-nextjs-works/bundling), and more. also Next.js has [built-in support for code splitting](https://nextjs.org/learn/foundations/how-nextjs-works/code-splitting).
