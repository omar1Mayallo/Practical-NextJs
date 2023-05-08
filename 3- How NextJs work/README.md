# How NextJs works ?

Before we learn more advanced Next.js features, it would be helpful to understand the basics of how Next.js works. Let's see the journey of the Next.js applications.

Next.js provides a framework to structure your application, and optimizations that help make both the development process and final application faster. And to know how Next.js works, we’ll look at what happens to your application code during these different stages:

- The environment where your code runs: `Development vs. Production`
- When your code runs: `Build Time vs. Runtime`
- Where rendering happens: `Client vs. Server`

## Development and Production Environments

You can think of environments as the context in which your code is running.<br/>
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

## Build Time and Runtime

**_Build Time_** : (or build step) is the name given to a series of steps that prepare your application code for production.<br/>
**_Runtime_** : (or request time) refers to the period of time when your application runs in response to a user’s request, after your application has been built and deployed.<br/>

When you build _(Build Time)_ your application, Next.js will transform your code into production-optimized files ready to be deployed to servers and consumed by users. These files include:

- HTML files for statically generated pages
- JavaScript code for rendering pages on the server
- JavaScript code for making pages interactive on the client
- CSS files

## Client, Server and Rendering

<!-- prettier-ignore -->
> I Will Discuss these in [4- Rendering folder](https://github.com/omar1Mayallo/Practical-NextJs/tree/main/4-%20Rendering%20(CSR%20vs%20Pre-rendering%20%5BSSR%2C%20SSG%2C%20ISG%5D%20))
