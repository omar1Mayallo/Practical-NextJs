# Why modern javaScript frameworks (like React, Angular and Vue) exist and What is the problem that try to solve ?

Before React.js, We as web developers had to do things manually and add watchers for every DOM element and bind it with the help of JavaScript or jQuery.
It was fine for managing applications that are not very interactive, but what is the problem that will occur if we build a very interactive application ?

Let's see this example : [https://codepen.io/gimenete/embed/vRZLrq?](https://codepen.io/gimenete/embed/vRZLrq?)

The code illustrates very well the amount of work needed to make a somewhat complex UI with vanilla JavaScript _*(using classic libraries such as jQuery would have been similar)*_.

Let's discuss the problems :

- In the example the static structure is created in the HTML, whereas the dynamic stuff is created in JavaScript (with `document.createElement`). This is the first problem: the JavaScript code that builds the UI is not very readable and we are defining the UI in two different parts. We could have used `innerHTML` and it could have been more readable but it has more issues .. see [https://www.geeksforgeeks.org/what-is-the-disadvantage-of-using-innerhtml-in-javascript/](https://www.geeksforgeeks.org/what-is-the-disadvantage-of-using-innerhtml-in-javascript/).

- The main problem is **_always updating the UI on every state change_**. Every time the state is updated there is a lot of code required to update the UI. When adding an email address in the example it takes 2 lines of code to update the state, but 13 lines to update the UI. And we made the UI as simple as possible!!

<div align="center"><img src="assets/state-change.webp"/></div>
<br/>

So, These frameworks provide lots of interesting things, but usually people miss the point about the deepest reason of their existence, which is not:

- They are based on components.
- They have a strong community.
- They have useful third party components.
- They have browser extensions that help debugging things.
- They are good for doing single page applications.

No, **_The main problem these frameworks try to solve is_** :

<div align="center"><i><b>"Keeping The UI In Sync With State Is HARD"</b></i></div>

<br/>

**_Thus .. The biggest, by far, improvement these frameworks provide is having the ability to implement UIs that are guaranteed to be in sync with the internal state of the application._**

## How Js frameworks solve this problem ?

DOM operations tend to be quite expensive in terms of performance, and any app which has lot's of DOM operations in the background is going to run slow.<br/>
So, React was built by Facebook to solve this very problem for them because they needed to manage 1000s of DOM objects and their updates. (likes, posts, comments ... etc).
The main solution to this problem is using a concept of **_Virtual DOM_**.

### Virtual DOM

React uses Virtual DOM exists which is like a lightweight copy of the actual DOM(a virtual representation of the DOM). So for every object that exists in the original DOM, there is an object for that in React Virtual DOM. It is exactly the same, but it does not have the power to directly change the layout of the document. Manipulating DOM is slow, but manipulating Virtual DOM is fast as nothing gets drawn on the screen. So each time there is a change in the state of our application, the virtual DOM gets updated first instead of the real DOM.

You may still wonder, _*“Aren’t we doing the same thing again and doubling our work? How can this be faster?” Read below to understand how things will be faster using virtual DOM.*_

When anything new is added to the application, a virtual DOM is created and it is represented as a tree. Each element in the application is a node in this tree. So, whenever there is a change in the state of any element, a new Virtual DOM tree is created. This new Virtual DOM tree is then compared with the previous Virtual DOM tree and make a note of the changes. After this, it finds the best possible ways to make these changes to the real DOM. **_Now only the updated elements will get rendered on the page again. In this way, lots of DOM operations/refreshes are minimized, improving performance significantly._**

<div align="center"><img src="https://miro.medium.com/v2/resize:fit:1400/1*eDpgmIW3vBGj6m64GGlFVw.gif" width="400" height="400"/></div>

<hr />

#### Resources

- [https://www.quora.com/What-does-react-js-try-to-solve-Can-you-provide-a-practical-example](https://www.quora.com/What-does-react-js-try-to-solve-Can-you-provide-a-practical-example)
- [https://medium.com/@aankit35/what-problem-does-react-js-solve-for-software-developers-a06cf50be28a](https://medium.com/@aankit35/what-problem-does-react-js-solve-for-software-developers-a06cf50be28a)
- [https://medium.com/dailyjs/the-deepest-reason-why-modern-javascript-frameworks-exist-933b86ebc445](https://medium.com/dailyjs/the-deepest-reason-why-modern-javascript-frameworks-exist-933b86ebc445)
- [https://www.reddit.com/r/webdev/comments/y42mq5/what_problems_does_react_solve/](https://www.reddit.com/r/webdev/comments/y42mq5/what_problems_does_react_solve/)
- [https://blog.eduonix.com/web-programming-tutorials/learn-react-framework-problems-solves/](https://blog.eduonix.com/web-programming-tutorials/learn-react-framework-problems-solves/)
- [https://www.geeksforgeeks.org/reactjs-virtual-dom/](https://www.geeksforgeeks.org/reactjs-virtual-dom/)
- [https://www.geeksforgeeks.org/reactjs-reconciliation/](https://www.geeksforgeeks.org/reactjs-reconciliation/)
