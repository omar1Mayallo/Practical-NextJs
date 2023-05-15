# Rendering (CSR vs Pre-rendering [SSR, SSG, ISG] )

As developers, we are often faced with decisions that will affect the entire architecture of our applications. One of the core decisions web developers must make is where to implement logic and rendering in their application. This can be difficult, since there are a number of different ways to build a website.

In order to better understand the architectures we’re choosing from when we make this decision, we need to have a solid understanding of each approach and consistent terminology to use when speaking about them. The differences between these approaches help illustrate the trade-offs of rendering on the web through the lens of performance.

Let's see every rendering techniques : 

## CSR (Client Side Rendering)
**_Client-side rendering (CSR)_** is a web development approach where the **_web browser is responsible for rendering_** the web page's content.<br/>
In this approach, the server sends the client a bare-bones HTML file that includes a minimal amount of content, such as the document's title and basic structure. The JavaScript code on the page then fetches the remaining data from a server API and dynamically populates the page with the content.

### How it works:
- Build process ⇒ The HTML file is sent to the server
- When the user requests, the server will send the HTML file, then the client (browser) requests the data to the API server

> Note: In Next 13, you need to add [`‘use client’`](https://www.js-craft.io/blog/client-components-use-client-directive-nextjs-13/) at the top of your jsx/tsx file to let Next.js know it’s rendered on the client side.

- At the time the client is requesting data from the API server, the browser will display the _loading-state_ (in most cases)
- After the data is fetched from the API server, then the _loading-state_ will be turned off and the screen will be updated with the data from the API

<div align="center"><img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*9upv_6-qmVIoBdt4JYy_sg.png" width="700" height="400"/></div>


### Use Cases
- If your site’s data is updated frequently
- SEO is not an essential factor

Ex: Dashboards, Social Media (like facebook, instagram), Tasks Managment websites

### Pros
- Real-time data
- The burden is not too big for the server
- Scalability ⇒ CSR can be scalable since the server's primary role is to provide the data, while the browser is responsible for rendering the content. that's mean there's **_NO_** server load and reduced performance as the number of users increases.

### Cons
- There will be a loading-state
- Not good for SEO ⇒ Since the HTML built from the server is not including the data from the API
- Slower initial loading times ⇒ Because the browser first will render a blank page, and user wait js code to execute and get data from server to see the page content. This can lead to a poor user experience, especially for users with slower internet connections or lower-end devices.

<hr/>

## SSR (Server Side Rendering)
**_Server-side rendering (SSR))_** is a web development approach where the **_server generates the HTML for the web page_** and sends it to the client's browser.<br/>
In this approach, the server is responsible for rendering the content, which means that the user must wait for the server to generate and send the HTML before being able to interact with the page.


### How it works:
- The JS file is sent to the server
- When the user (browser) requests, the server will run the `getServerSideProps()` function (Next 12) or `fetch(‘https://...', { cache: ‘no-store’ });` (Next 13)
- After the data is fetched, it will be built on the server _(including the data from the API)_
- The server will send the HTML to the user’s browser

<div align="center"><img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*vqhwJbAmYIOQ20Va8RI6zg.png" width="700" height="400"/></div>


### Use Cases
- If your site data is updated frequently and need a fresh data every rendering
- While at the same time, SEO is an essential factor as well

Ex: News, Blogs, Banks, Stock exchange websites

### Pros
- No loading-state
- Real-time data
- Good for SEO
- Improved security ⇒ SSR can be more secure since the server has full control over the content that is rendered on the page, reducing the risk of client-side attacks such as cross-site scripting (XSS).

### Cons
- The user needs to wait for the HTML to be built on the server-side
- Too much burden on the server ⇒ every user’s request, the server needs to rebuild
- Slower initial loading times ⇒ Since the user must wait for the server to generate and send the HTML. This can lead to a poor user experience, especially for users with slower internet connections or lower-end devices.
- Scalability ⇒ SSR can be less scalable since the server is responsible for rendering the content, which can result in increased server load and reduced performance as the number of users increases.



