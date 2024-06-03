
# Virtual DOM 

## What is DOM and its working ?
Imagine the content you see on a website is like a big, fancy castle. This castle is the real DOM (Document Object Model). It's built from many smaller parts, like bricks for walls, windows for viewing, and banners for announcements. Each of these parts is an element in the DOM.

The real DOM works behind the scenes in your browser. It takes the website's code (HTML) and turns it into the visual elements you see on the screen. It remembers how everything is arranged and connected, like where the walls meet and the windows are placed.

Here's how it works:

1. **Building the Castle:** When you visit a website, the browser reads the HTML code. This code tells the DOM what elements to create (bricks, windows, banners) and how to arrange them (walls connected, windows in specific spots).
2. **Making Changes:** If something on the website needs to update, like a news banner changing content, the browser goes back to the code and tells the DOM to adjust the specific element (update the banner text). The DOM then makes those changes in the castle, like replacing the old banner with a new one.

However, the real DOM has a weakness: it can be slow to update, especially with complex websites. Imagine constantly rebuilding sections of the castle for every little change!

That's where the virtual DOM comes in, but that's a story for another time. 

Basically real DOM repaints whole page from scratch at every update and this is time taken process, this is also known as reloading of page when DOM update.

## Now here's come Virtual DOM

Imagine you're building a Lego house. That house is like the real DOM (Document Object Model) - the actual building blocks that make up a web page. Changing these blocks around one by one can be slow and cumbersome.

The virtual DOM comes in as a blueprint for your Lego house. It's a lightweight copy in memory that reflects the actual house (real DOM). When you want to make changes to the house, you first update the blueprint (virtual DOM) with the new design. Then, React, the Lego builder in this case, compares the old and new blueprints and figures out the most efficient way to update the real house (DOM) with minimal changes. 

## createRoot
This is where the `createRoot` method comes in. In React 18 (the latest version as of May 2024), this method is like setting the foundation for your Lego house. It tells React where to put your virtual DOM blueprint (on a specific HTML element with an ID, for example). Once you have the foundation set, you can use React to create your components (like walls, doors, windows) and populate your virtual house. React will then efficiently update the real DOM (webpage) to match your blueprint.

Here's the benefit: Updating a lightweight blueprint in memory is much faster than constantly tinkering with the real house (DOM). This makes React apps fast and efficient, especially when dealing with complex UIs.

### fallback of Virtual DOM and introduction of Fiber Algorithm
The introduction of the Fiber core algorithm in React 16 (released in 2017) doesn't negate the need for the virtual DOM. They work together to enhance React's performance, but in different ways:

**Virtual DOM - Efficiency for Updates:**

* Introduced earlier than Fibers, the virtual DOM remains a core concept in React.
* It creates a lightweight copy of the real DOM in memory.
* React compares the old and new virtual DOM states to identify the minimal changes needed.
* This minimizes the number of manipulations required on the real DOM, improving performance.

**Fiber Core Algorithm - Prioritizing Updates:**

* Introduced in React 16, Fibers brought a new approach to how React handles updates.
* It breaks down UI updates into smaller, prioritized tasks (reconciliation) instead of one big update.
* This allows React to pause updates if needed (e.g., user scrolls rapidly) and prioritize rendering what's currently visible.
* This creates a smoother user experience, especially for complex UIs or slow devices.

Here's an analogy: Imagine you're redecorating a room (updating the DOM).

* **Virtual DOM:** You create a blueprint (virtual DOM) to plan the changes efficiently.
* **Fiber Algorithm:** You prioritize tasks (reconciliation) -  painting the walls first, then arranging furniture (important for user experience) - and pause if interrupted (user scrolls).

While the virtual DOM focuses on what needs changing, Fibers handle the scheduling and prioritization of those changes for a smoother update process.

In essence, they work together:

1. The virtual DOM identifies efficient updates.
2. The Fiber algorithm prioritizes those updates for a smooth user experience.

Basically, Fiber do the work of hydration like initially you have two button on UI but right now if you try to click on that buttons so you will see any change bcuz right javascript is not injected in your page but the moment at which javascript then your buttons become interactive and this process of injecting javascript is known as hydration.

## Difference Between reconciliation and hydration
No, reconciliation and hydration are not the same in React, although they are both related to updating the DOM. Here's a breakdown of their differences:

**Reconciliation:**

* Focuses on **updating** the real DOM efficiently based on changes in the virtual DOM.
* Happens throughout the lifecycle of a React application, whenever the component state or props change.
* Involves comparing the old virtual DOM with the new virtual DOM to determine the minimal changes needed in the real DOM.
* Aims for efficient updates, minimizing the number of DOM manipulations required.

**Hydration:**

* Focuses on the **initial rendering** of a React application on the client-side (in the browser).
* Occurs only once, right after the server-rendered HTML is received by the browser.
* Involves taking the server-rendered HTML (which represents the initial DOM state) and making it interactive by attaching React event listeners and state management.
* Essentially, it "hydrates" the static server-rendered HTML with React functionality.

**Here's an analogy:**

* **Reconciliation:** Imagine you have a well-maintained garden (real DOM) and a plan (virtual DOM) for minor adjustments (like planting new flowers). Reconciliation involves efficiently making those adjustments to the garden based on the plan.
* **Hydration:** Think of receiving a beautifully designed garden (server-rendered HTML) but without the flowers planted yet (no React interactivity). Hydration involves adding those flowers (React functionality) to bring the garden to life.

In short:

#### Reconciliation deals with updates throughout the React app's lifecycle,like reconciliation happens whenever the state of your component changes.
* Lifecycle methods: Imagine different checkpoints (mounting, updating, unmounting) on a train journey. You have specific actions (methods) you can perform at each station.
* Hooks: Think of versatile tools you can use throughout the train ride (useState for managing luggage, useEffect for buying snacks at stations). These tools are not tied to specific stations and offer more flexibility. 
#### Hydration is a one-time process for making the initial server-rendered HTML interactive with React.

[Must read this readme for understanding virtual DOM reconciliation and fibre primary goal in depth.](https://github.com/acdlite/react-fiber-architecture)