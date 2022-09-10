# Next.js

* Framework for creating _**pre-rendered**_ React websites
* relatively unopinionated framework
* Next.js offers both
  * **SSR **_**(Server Side Rendering)**_ - app's ability to convert HTML files on server into fully rendered HTML pages for client.
  * **SSG **_**(Static Site Generation)**_ - tool that generates full static HTML website based on raw data and set of templates.
* Pre-rendering from SSR improves performance and better search engine optimization (SEO)

_**`>>> Development and Production Environments`**_

* During development, you’re building and running the application on your local machine. Going to production is the process of making your app ready to be deployed.
* Since each environment has different goals, there's a lot that needs to be done to move an application from development to production, including: _compiling_, _bundling_, _minifying_, and _code spliting_.
* _**`Compiling`**_ - process of taking code in one language (developer friendly ie. JSX) and outputting it in another language or another version of that language. _Web app code needs to be compiled into a version browsers can understand_.
* _**`Bundling`**_ - process of resolving the dependencies and merging (‘packaging’) the files ('modules') into optimized bundles for the browser. The goal is to reduce the # of requests for files when a user visits a web page.
* _**`Minifying`**_ - process of removing unnecessary code formatting (ie. comments, spaces, and indents) without changing the code’s functionality. The goal is to improve the app's performance by decreasing file sizes.
* _**`Code Splitting`**_ - process of splitting the app's bundle into smaller chunks required by each endpoint (different URL's). The goal is to improve the app's initial load time by only loading the code required to run that page.
  * The files inside the _**`pages/`**_ directory will be automatically code split by Next.js into its own JS bundle during the build step.

_**`>>> Rendering`**_

* process of converting the code you write in React into the HTML rep. of your UI.
* With Next.js, three types of rendering methods are available:
  1. **Server-Side Rendering** _(pre-rendering)_
     * the HTML of the page is generated on a server for **each** request
  2. **Static Site Generation** _(pre-rendering)_
     * the HTML is generated on the server, but unlike server-side rendering, there is no server at runtime. Instead, content is generated once, at build time, when the application is deployed, and the HTML is stored in a [CDN](https://nextjs.org/learn/foundations/how-nextjs-works/cdns-and-edge) and re-used for each request.
  3. **Client-Side Rendering** _(not pre-rendering)_
     * the browser receives an empty HTML shell from the server along with the JavaScript instructions to construct the UI

***

## > Getter Started

```bash
npx create-next-app@latest <my_app>
# or
yarn create next-app <my_app>

# if parsing error, go to eslintrc.json, and replace with:
# "extends": ["next/babel","next/core-web-vitals"]
```

After the installation is complete:

* To start a development server –– _`npm run dev`_ / _`yarn dev`_
* View application on –– _`http://localhost:3000`_
* Edit _`pages/index.js`_ and see the updated result in your browser

***

## > Pages & Routes

In Next.js, a _**`page`**_ is a React Component exported from a file in the `/pages` directory.

_Creating New Pages_

* To create new pages, add file endpoints to the `/pages` directory s.t. :
  * _**pages/index.js**_ is on endpoint **/**
  * _**pages/posts/first-post.js**_ is on endpoint **/posts/first-post.js**

Note: The page react component itself can have any name, but you must export it as a `default` export:

```jsx
export default function componentName() {
		return <h1>First Post</h1>
}
```

### Linking Pages (Components)

* _**`<Link>`**_ allows you to do _**Client-Side Navigation**_ which means that the page transition happens _using JavaScript_, which is faster than the default navigation done by the browser

1.  First, open _**`pages/index.js`**_, and import the _**`Link`**_ component from _**`next/link`**_ by adding this line at the top:

    ```js
    import Link from 'next/link'
    ```
2.  Then wrap the _**`<a>`**_ tag with a _**`<Link>`**_ tag whose href-property is the relative path of the page (component) being linked to.

    ```jsx
    // links the current <a> tag to pages/posts/first-post.js
    <Link href="/posts/first-post">
        <a>this page!</a>
    </Link>
    ```

Note:

* If you need to link to an _external_ page outside the Next.js app, just use an `<a>` tag without `Link`.
* If you need to add attributes like, for example, `className`, add it to the `a`tag, _not_ to the `Link` tag

***

#### Adding other components:

* If you want to make, say, a Navbar.js component for your app, make a new directory for those kind of components. Don't put them in any of the pre-existing directories.
* ie. put Navbar.js in _components/_

***

## Assets, Metadata, CSS

* Next.js has built-in support for CSS & SASS

### _\[ Assets ]_

* Next.js can serve **static assets**, ie. images, under the _**/public**_ directory.
* The _**/public**_ directory is also useful for **robots.txt**, **Google Site Verification**, and any other static assets.

### _\[  and Image Optimization ]_

* With the regular HTML  tag, you would have to manually handle:
  * Ensuring your image is responsive on different screen sizes
  * Optimizing your images with a third-party tool or library
  * Only loading images when they enter the viewport
*   Next.js'  component handles all the above for you.

    ```
    import Image from 'next/image'

    const YourComponent = () => (
      <Image
        src="/images/profile.jpg" // Route of the image file
    	  alt="Your Name"

        // Desired size with correct aspect ratio
        height={144}
        width={144}
      />
    )
    ```

### _\[ Head ]_

* _**`<Head>`**_ is a React Component that is built into Next.js. It allows you to modify the _**`<head>`**_ of a page.
*   You can import the `Head` component from the _**`next/head`**_ module:

    ```jsx
    import Head from 'next/head'

    export default function Home() {
      return (
      	<>
        <Head>
          <title>First Post</title>
          {/*other tags you would put in head, put here.*/}
        </Head>
        <div>
        	{/*etc...*/}
        </div>
      )
    }
    ```

### _\[3rd-Party JavaScript ]_

* **3rd-party JS** refers to any scripts that are added from a third-party source.
* In addition to metadata, scripts that need to load and execute as soon as possible are usually added within the _**`<head>`**_ of a page.
*   Instead of the HTML tag, use Next.js' tag:

    ```jsx
    // In the same file, add an import for Script from next/script 
    import Script from 'next/script'

    // ... ie. (w/ additional properties strategy, onLoad)
    <Head>
    	<title>First Post</title>
    </Head>

    <Script
    	src="https://connect.facebook.net/en_US/sdk.js"
    	strategy="lazyOnload"
      onLoad={() =>
         console.log("script loaded correctly")
      }
    />
    ```

### _\[ CSS Styling ]_

1.  You can use a library called _**styled-jsx**_ which is a "CSS-in-JS" library that lets you write CSS within a React component, and the CSS styles will be _**scoped**_ (other components won’t be affected).

    ```jsx
    <style jsx>{`
    	.container {
    			min-height: 100vh;
          padding: 0 0.5rem;
    	}

    	main {
    			padding: 5rem 0;
          align-items: center;
    	}
    `}</style>
    ```
2. If not 1), then you can just use the regular import-css styling method. Next.js has built-in support for **.css** and **.scss** files. Ie:
   *   To apply css styles for a **Layout.js** , you would create a **layout.module.css** and add the styles in there ie.

       ```css
       /* layout.module.css */
       .container {
       		min-height: 100vh;
           padding: 0 0.5rem;
       }
       ```
   *   Then, you would import the css file in the React Component file:

       ```jsx
       // Layout.js
       import styles from './layout.module.css
       ```
   *   The, to use the **.container** class in Layout.js, use **styles.container** as the **className** for the HTML to apply the styles:

       ```jsx
       // Layout.js
       export default function Layout({ children }) {
         return
         	<div className={styles.container}>
             {children}
         </div>
       }
       ```

### _\[ Global CSS Styling ]_

* Create a **styles/global.css** and add global styles in there.
*   To load this **global.css** styling to **every page**, create a file called _**pages/\_app.js**_ with the following content:

    ```jsx
    import '../styles/global.css'

    export default function App({ Component, pageProps }) {
      return <Component {...pageProps} />
    }
    ```
* The imported **global.css** will be applied to all pages since this **App** component is the top-level component which will be common across **all the hanimpages**.
* Note: You need to restart the dev. server when you add _**pages/\_app.js**_.

***

## Pre-Rendering

* By default, Next.js _**pre-renders**_ every page, meaning it **generates HTML for each page in advance**, instead of having it all done by client-side JS
* Results in better **performance** and **SEO**
* Pre-rendering also allows your app to work w/o JS.

_**Hydration**_ –– Each generated HTML is associated with minimal JavaScript code necessary for that page. When a page is loaded by the browser, its JavaScript code runs and makes the page fully interactive. This process is called **hydration**.

!\[Screen Shot 2022-04-12 at 6.34.58 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-12 at 6.34.58 PM.png)

!\[Screen Shot 2022-04-12 at 6.35.15 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-12 at 6.35.15 PM.png)

There are 2 Forms of Pre-Rendering, and the core difference b/n the two being **when** it generates the HTML for the page:

### 1. Static Site Generation - (SSG)

* pre-rendering method that generates the HTML at **build time**. The pre-rendered HTML is then _reused_ on each request

!\[Screen Shot 2022-04-12 at 6.38.09 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-12 at 6.38.09 PM.png)

### 2. Server-Side Rendering - (SSR)

* pre-rendering method that generates the HTML on **each request**.

!\[Screen Shot 2022-04-12 at 6.38.21 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-12 at 6.38.21 PM.png)

(Note: In dev. mode, pre-rendering occurs when you run **yarn dev**)

Next.js lets you **choose** which pre-rendering form to use for each page!!

You should ask yourself: "Can I pre-render this page **ahead** of a user's request?" If the answer is yes, then you should choose **SSG**.

### SSG with & w/o Data

Pages which **don't require fetching external data** will automatically be statically generated when the app is built for production.

!\[Screen Shot 2022-04-12 at 6.45.42 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-12 at 6.45.42 PM.png)

However, for some pages, you might not be able to render the HTML without first fetching some external data (file system, API, DB, ...)

!\[Screen Shot 2022-04-12 at 6.46.51 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-12 at 6.46.51 PM.png)

#### SSG with Data via getStaticProps

* In Next.js, when you export a page component, you can also export an _**async**_ function called _**getStaticProps**_.
* This way, inside the function, you can fetch external data and send it as props to the page.

```jsx
export async function getStaticProps() {
  // Get external data from, say, an API
  const res = await fetch('endpoint');
  const data = await res.json(); // JSON data in 'data'  

  // Value of 'props' key will be passed to Home comp.
  return {
    props: { users: data }
  }
}

// now you pick up the props from above function
export default function Home( {users} ) {
  return (
  	<div>
      <h1>All users</h1>
			{/*..handle data here..*/}
    </div>
  )
}
```

*   Essentially, _**getStaticProps**_ allows you to tell Next.js:

    _" Hey, this page has some data dependencies — so when you pre-render this page at build time, make sure to resolve them first! "_

***

#### _Gray-Matter (file system data parser)_

*   gray-matter is a npm package which lets us parse metadeta in .md files formatted a certain way:

    ```markdown
    ---
    title: 'Title'
    date: '04-12-2022'
    ---

    ContentContentContent
    ```

```bash
yarn install gray-matter
```

An example [implementation](https://nextjs.org/learn/basics/data-fetching/implement-getstaticprops).

***

#### SSR with Data

*   To use SSR, you need to export _**getServerSideProps**_ instead of _**getStaticProps**_ from your page:

    ```jsx
    export async function getServerSideProps(context) {
      return {
        props: {
          // props for your component
        }
      }
    }
    ```
* Since SSR is called at **request time**, its parameter _**context**_ contains request specific params.
* You should use getServerSideProps only if you need to pre-render a page whose data must be fetched at request time.

#### SWR

* The team behind Next.js has created a React hook for data fetching called **SWR**.
* It's highly recommended for when you're fetching data on the client side. It handles caching, revalidation, focus tracking, refetching on interval, and more.
* see more [here](https://swr.vercel.app)

***

## Custom 404 Page

* To make a custom 404 page, create a **404.js** file in the _**/pages**_ directory. This is a specially-named file which handles all invalid endpoints.

```jsx
import Link from 'next/link'

export default function NotFound() {
  return (
  	<div>
    	<h1>Oops...</h1>
      <h2>That page cannot be found.</h2>
      <p>Go back to the <Link href="/"><a>Homepage</a></Link></p>
    </div>
  )
}
```

***

## Redirecting Users

*   To automatically redirect users to a link, use the **useEffect** and **useRouter** hooks.

    * **useEffect** fires the useRouter once the user _mounts_
    * **useRouter** does the actual redirecting

    ie. A 404 Page which redirects user to homepage automatically after 3s

    ```jsx
    // 404.js

    import Link from 'next/link'
    import { useEffect } from 'react'
    import { useRouter } from 'next/router'

    export default function NotFound() {
      const router = useRouter();
      
      useEffect(() => {
        setTimeout(() => {
        		// router.go(-1) // Go -1 back in history
          router.push('/');	// redirect to homepage
        }, 3000)
      }, [])
      
      return (
      	<div>
        	<h1>Oops...</h1>
          <h2>That page cannot be found.</h2>
          <p>Go back to <Link href="/"><a>Homepage</a></Link></p>
        </div>
      )
    }
    ```

***

## Dynamic Routes

* Instead of making separate pages for: **/posts/1** and **/posts/2**, etc... , you can statically generate pages w/ _dynamic routes_: **/posts/\[id]**

We can do this by creating a page file: _**pages/posts/\[id].js**_

––> Pages that begin with **\[** and end with **]** are **dynamic routes** in Next.js!

!\[Screen Shot 2022-04-13 at 3.27.51 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-13 at 3.27.51 PM.png)

See implementation [here](https://nextjs.org/learn/basics/dynamic-routes/implement-getstaticpaths).

!\[Screen Shot 2022-04-13 at 3.49.05 PM]\(/Users/dev/Library/Application Support/typora-user-images/Screen Shot 2022-04-13 at 3.49.05 PM.png)

***
