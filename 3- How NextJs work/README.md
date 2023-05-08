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

<hr/>

## Network(where your application code is stored)

It’s helpful to know _where your application code is stored and run once it’s deployed to the network._ You can think of the network as linked computers (or servers) capable of sharing resources. In a Next.js application, various components of your code can be distributed across different types of servers to `optimize performance`, `ensure scalability`, and `minimize latency`. Your application code can be distributed to **_origin servers_**, **_Content Delivery Networks (CDNs)_**, and the **_Edge_**. Let’s see what each of these are:

### Origin servers

As we discussed earlier, the server refers to the main computer that stores and runs the _original_ version of your application code.<br/>
We use the term _origin_ to distinguish this server from the other places application code can be distributed to, such as **_CDN servers_** and **_Edge servers_**.

Origin servers in the context of a Next.js application refer to the _primary servers that host your application code_, _handle server-side rendering_, and _process API requests_. These servers are responsible for **_managing `dynamic` content_**, **_running server-side logic_**, and **_generating server-side rendered (SSR)_** content when necessary. They can be either a single server or a cluster of servers, depending on the application's requirements and infrastructure setup.

In a Next.js application, the origin servers handle:

- **_Server-Side Rendering (SSR):_** When a Next.js page uses server-side rendering, the origin server generates the HTML for the page on each request. This approach is useful for handling dynamic content, SEO, and content that depends on user-specific data.
- **_API Routes:_** Next.js supports the creation of API routes, which allow you to build server-side APIs within your application. The origin server processes these API routes, executing the server-side logic and serving the data in response to client requests.
- **_Server-side logic:_** Any custom server-side logic or middleware needed by your application is executed on the origin server. This can include tasks like data manipulation, authentication, or integration with external services.
- **_Fallback pages:_** In cases where a static page generated using Incremental Static Regeneration (ISR) is not yet available or needs to be regenerated, the origin server can generate and serve a fallback version of the page.

While origin servers handle the `dynamic` aspects of a Next.js application, the `static` content (JavaScript, CSS, images, and static HTML pages) and cacheable ISR pages are served by Content Delivery Networks (CDNs) and edge servers, which `improve performance` and `minimize latency for users worldwide`.

### CDNs

CDNs store `static` content (such as HTML and image files) in multiple locations around the world and are placed between the client and the origin server. When a new request comes in, the closest CDN location to the user can respond with the cached result.

<div align="center"><img src="https://nextjs.org/static/images/learn/foundations/cdn.png" width="600" height="400"/></div>

This reduces the load on the origin because the computation doesn’t have to happen on each request. It also makes it faster for the user because the response comes from a location geographically closer to them.

In Next.js, since pre-rendering can be done ahead of time, CDNs are well suited to store the `static` result of the work - making content delivery faster.

When building a Next.js application, the framework optimizes assets like JavaScript, CSS, and images during the build process. Once your application is built, you can deploy it to a hosting provider or platform like Vercel, Netlify, or any other hosting service that supports edge caching and CDN integration.

Here's how Next.js works with CDNs:

- **_Static assets:_** During the build process, Next.js generates static assets, such as JavaScript, CSS, and images. These assets are given unique names based on their content, which enables efficient caching on CDN edge servers. When a user requests a page, the CDN serves these static assets from the nearest edge server, reducing latency and improving load times.
- **_Static site generation (SSG):_** Next.js can pre-render pages as static HTML during the build process. These pre-rendered pages can be cached and served directly from the CDN, ensuring fast response times and reducing the load on the origin server.
- **_Incremental Static Regeneration (ISR):_** Next.js also supports ISR, which allows you to regenerate static pages on-demand after they have expired or when new data is available. ISR pages can be cached and served by the CDN, ensuring that users receive the latest content while maintaining the performance benefits of static site generation.
- **_Image optimization:_** Next.js includes a built-in Image component that automatically optimizes images for better performance. When used in combination with a CDN, your images can be served from the nearest edge server, ensuring faster load times and improved user experience. You can also use third-party image optimization services like Cloudinary, Imgix, or Akamai, which integrate seamlessly with Next.js.

By leveraging CDNs, Next.js applications can `achieve optimal performance` and `provide users with a fast and smooth browsing experience, regardless of their geographic location`.

### The Edge

The Edge is a generalized concept for the fringe (or edge) of the network, _closest to the user_.

CDNs could be considered part of "the Edge" because they store `static` content at the fringe (edge) of the network.

Similar to CDNs, Edge servers are distributed to multiple locations around the world. But unlike CDNs, which store static content, some Edge servers `can run small snippets of code`.

This means both **_caching_** and **_code execution_** can be done at the Edge closer to the user.

#### Edge caching

Edge caching is a technique used in Content Delivery Networks (CDNs) to store and serve content from servers located at the "edge" of the network, which are geographically closer to the end users. This approach helps `reduce latency`, `increase content delivery speed`, and `improve the overall performance of web applications and websites`.

When a user requests content such as images, videos, JavaScript, or CSS files, edge caching serves the content from the "nearest" edge server instead of fetching it from the origin server. `This reduces the time taken for the content to travel from the server to the user, known as network latency, and ensures a better user experience.`

Here's how edge caching works:

- A user requests content from a website or web application.
- The request is routed to the nearest edge server in the CDN network based on the user's geographic location.
- If the requested content is available in the edge server's cache, it is served directly to the user. This results in faster load times and improved performance.
- If the content is not available in the cache, the edge server fetches the content from the origin server, caches it, and serves it to the user. Future requests for the same content will be served from the cache, ensuring faster delivery.
- Edge servers periodically update their caches by fetching new content from the origin server or by removing content that is no longer needed. This ensures that users always receive up-to-date content while still benefiting from the performance advantages of edge caching.

Edge caching is an essential component of modern CDN architectures and plays a crucial role in delivering web content quickly and efficiently to users around the world.
