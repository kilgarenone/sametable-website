---
layout: post.njk
title: How I Built My First SaaS
---

# How I Built My First SaaS

_From first principles_

I switched my career to web development back in 2013. I did it for two reasons. First, I noticed I could get lost in building customer-facing products amongst all the colors and endless possibilities of interactivity; so while being reminded by the trite "_Find a job you enjoy doing, and you will never have to work a day in your life._", I thought "_Hey, why not make this a job, huh???_". And second, I wanted to make something for myself having spent my teenage years inspired by the Web 2.0(The Digg.com circa 2005 opened the world for me). My plan was to work on the latter while working in the former.

Turns out though, the job and the 'Javascript fatigue' ensued to wholly consume me. It also didn't help that I was reckless in my pursue of my ambition having been influenced by my perception of successes from the 'Silicon Valley'. I read Paul Graham's _Hackers & Painters_ and Peter Thiel's _Zero to One_. I'm properly fired up! I'm hustling. I can do this too! But nope, I can't. At least not alone. I always was beat after work. I couldn't gather a team who would buy into dreams. So meanwhile, I rinse and repeat less than half-baked projects. I start to mellow out as years go by. And I begin to cultivate a personal philosophy on entrepreneurship and technology that align with my personality and life circumstances- Until September 2019.

The fog in the path ahead finally cleared up. I got pretty good at it; the job became less taxing; I'd reined in on my 'Javascript fatigue'. For the longest time, I had the mental resources, time, and the mindset that allowed me to see through a side project. And this time, I start simple.

But, I was totally lost.

Having been a front-end developer for my entire career, I could only go as far as naming the things that I imagined I would need&mdash;a 'server', a 'database', an 'authentication' system, a 'host', a 'domain name', but _how_... _where_... and _what_..._I..I don..I don't even_... :sob:

Now, I knew my life would have been easier if I'd decided to use those abstract tools like 'create-react-app', 'firebase SDK', 'ORM', and 'one-click-deployment' services; the ode of '_Don't reinvent the wheel. Iterate fast_'. But there were a few things I wanted my decisions to meet:

- No vendor lock-in &mdash; This ruled out using the Firebase SDK all over my codebase. Including the 'create-react-app', because ejecting it forces me to inherit and maintain its massive tooling infrastructure.
- Simplicity & Minimalistic &mdash; Cut having to learn new opinionated syntax and pattern. This ruled out 1) Project generators that output complex architecture and layers of boilerplate codes, 2) Using third-party libraries such as 'knex.js' or 'sequalize' ORM.
- Pay-as-you-need &mdash; I wanted to keep my operating cost proportional to the usage level. This ruled out many services such as 'one-click-deployment'.

To be fair though, I got the following things going for me:

- I was building a simple SaaS.
- I was not anxious to scale, dominate, disrupt etc.
- I was still [holding](https://aeon.co/essays/dont-quit-your-day-job-the-benefits-of-being-a-bifurcator) my day job.
- I had accepted my odds of failure. :skull:

Also keep in mind that:

- It's a one-man show&mdash;design, development, maintenance, marketing etc.
- I'm not a 10x rockstar full-stack programmer.

**Most importantly**, I wanted to follow through with a guiding principle: Building things [_responsibly_](https://alistapart.com/article/responsible-javascript-part-1/). Although, unsurprisingly, doing so had had a significant impact on my development speed, it had forced me to delineate my motivations:

- If I had to ship something the soonest possible, unless it's a matter of life and death, then I probably wasn't solving a unique and hard problem, in which case&mdash;assuming I was still on my day job and had zero debt took on&mdash;What is the rush?
- And second-guessing from an ethical perspective: Was it even a problem needs solving? What will be the second-order consequences if I solved it? Could my good intentions have been better directed elsewhere?

## Finding ideas

I used to lose sleep thinking and remixing thoughts, hoping for an eureka - Until I started to look inward:

- Build things that solve problems that you encounter and piss you off frequently.
- Solving the so-called 'pain points' or 'frictions'. Go outside, don't stop listening to people and learn from them.
- Be an expert in your own domain. Feel its pain. Seems to me lots of founders founded company related to their domain on which they have built their career and social capital.

## The Stack

How your stack looks like will depend on how you will render your application. Here is a [comprehensive](https://developers.google.com/web/updates/2019/02/rendering-on-the-web#wrapup) discussion about that, but in a nutshell:

- **Client-side rendering(CSR); SPA; APIs with JSON**
  This is currently the most common approach in the modern web. It's great for building interactive web applications. But [be aware](https://macwright.org/2020/05/10/spa-fatigue.html) of its downsides and steps to mitigate them. This is the approach I took, so we will talk more about this in details.

- **Hybrid CSR; Both client-side and server-side rendering(SSR)**
  With this approach, you still build your SPA. But when a user requests your app, for example, the homepage, you would first render the homepage's component into the corresponding static HTML **in your server** before serving it to the user. Then once the user's browser parse the HTML, [hydration](https://reactjs.org/docs/react-dom.html#hydrate) will happen so the whole thing becomes a SPA.

  The main benefits of this approach are that you get good SEO and users can see your stuff sooner(faster 'First Meaningful Paint'). But there are downsides too. Apart from the extra maintainance costs, we have to download the same payload twice- First, the HTML, and second, its Javascript counterpart for 'hydration'.

  The technologies that are adopted for this approach are [NextJs](https://nextjs.org/), [NuxtJs](https://nuxtjs.org/), and [GatsbyJs](https://www.gatsbyjs.org/).

- **Server-side rendering and sprinkle :sparkles: it with Javascript**
  This was the old-school way of building on the web!- Render your templates in PHP, then bind events handlers with jQuery. This approach might be ill-suited to build the increasingly complex app that businesses have asked for on the web, but some technologies have emerged to elevate this approach:

  - [https://stimulusjs.org/](https://stimulusjs.org/)
  - [https://github.com/turbolinks/turbolinks](https://github.com/turbolinks/turbolinks)
  - [https://github.com/phoenixframework/phoenix_live_view](https://github.com/phoenixframework/phoenix_live_view)
  - For more, check out this [twitter thread](https://mobile.twitter.com/nateberkopec/status/1260602209475198976)

  To be honest, if I could have been more patient with myself, I would have gone down this path. This approach is making a comeback in light of the wretched excess of Javascript in this modern web.

Bottom line is, pick any approach you are already proficient with. Be mindful of the associated downsides, and try to mitigate them before shipping it to your users.

With that, here is my boring stack:

### Front-end

- Webpack, Babel
- **Preact**

### Back-end

- **Node** &mdash; API web server with ExpressJS
- **Postgresql** &mdash; Database
- **Redis** &mdash; Store users' session data and cache queries' results.

### Hosting

- **Google Cloud Platform** &mdash; GAE for hosting Nodejs, GCE for hosting Redis.
- **Firebase** &mdash; For hosting my SPA.

<img loading="lazy" src="https://i.imgur.com/CA88ijh.png" alt="Sametable architecture" />

## Repo

[https://github.com/kilgarenone/boileroom](https://github.com/kilgarenone/boileroom)

This repo contains the structure I'm using to develop my SaaS. We have one folder for the **client** stuff, and one folder for the **server** stuff:

```json
- client
    - src
      - components
      - index.html
      - index.js
    - package.json
    - webpack.config.js
    -.env
    -.env.development
- server
    - server.js
    - package.json
    - .env
- package.json
- .gitignore
- .eslintrc.js
- .prettierrc.js
- .stylelintrc.js

```

The file structure aims to be flat, cohesive, and as linear to navigate as possible. Each 'component' is self-contained; it contains all the constituent files(html|css|js). For example, in a 'Login' route folder:

```
- client
   - src
     - routes
       - Login
         - Login.js
         - Login.scss
         - Login.redux.js
```

I learned this from the [Angular2 style guide](https://angular.io/guide/styleguide#angular-coding-style-guide).

### Local development

The `package.json` at the root has a **npm script** that I will run to start both of my client and server **to begin my local development**:

```json
"scripts": {
    "client": "cd client && npm run dev",
    "server": "cd server && npm run dev",
    "dev": "npm-run-all --parallel server client"
}
```

Run the following in a terminal at your project's root:

```json
npm run dev
```

## Client

```json
- client
    - src
      - components
      - index.html
      - index.js
    - package.json
    - webpack.config.js
    -.env
    -.env.development
```

The folder structure of 'client' is quite like that of the 'create-react-app'. The meat of your application code is inside the `src` folder: A `components` folder contains your functional React components; `index.html` is your [custom template](https://github.com/kilgarenone/boileroom/blob/master/client/config/webpack.development.js#L41-L43) provided to the [`html-webpack-plugin` ](https://github.com/jantimon/html-webpack-plugin#options); [`index.js`](https://github.com/kilgarenone/boileroom/blob/master/client/src/index.js) is your [entry point](https://github.com/kilgarenone/boileroom/blob/master/client/config/webpack.common.js#L12-L15) for Webpack bundling.

#### npm script

The client's `package.json` file contains two npm scripts: 1) `dev` to start development, 2) `build` to bundle for production.

```json
"scripts": {
    "dev": "cross-env NODE_ENV=development webpack-dev-server",
    "build": "cross-env NODE_ENV=production node_modules/.bin/webpack"
}
```

#### Environment variables

It's a good practice to have a `.env` file where you define your sensitive values such as API keys and database credentials:

```
SQL_PASSWORD=admin
STRIPE_API_KEY=1234567890
```

A library called [dotenv](https://www.npmjs.com/package/dotenv) is usually used to load these variables for our application code to consume. However, in the context of Webpack, we will use [dotenv_webpack](https://www.npmjs.com/package/dotenv-webpack) to load them during compile or build time [as shown here](https://github.com/kilgarenone/boileroom/blob/master/config/webpack.common.js#L33-L37). The variables will then be accessible in `process.env` across your application code:

```js
// payment.jsx

if (process.env.STRIPE_API_KEY) {
  // do stuff
}
```

#### Webpack & Babel

Webpack is used to bundle all my UI components and its dependencies(npm libraries, files like images, fonts, SVG) into `.js` files. During the bundling, Webpack will run through my [babel config](https://github.com/kilgarenone/boileroom/blob/master/client/config/webpack.production.js#L19-L57), and, if necessary, transpiles the Javascript I have written to an older version(e.g. es5) to support my [targeted browsers](https://github.com/kilgarenone/boileroom/blob/master/client/package.json#L13-L27).

Here is roughly how it goes down: When webpack has done its job, it will have generated one(or [several](https://webpack.js.org/concepts/entry-points/#multi-page-application)) `.js` and `.css` files. What commonly happens next is, by [utilizing](https://github.com/kilgarenone/boileroom/blob/master/client/config/webpack.production.js#L189-L202) a webpack plugin called ['html-webpack-plugin'](https://github.com/jantimon/html-webpack-plugin), the Javascript files are _automatically_(default behaviour) injected as [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script) in your `index.html`. Then when a user requests your app in a browser, the 'index.html' is fetched and parsed. When a browser sees the `<script>`'s `.js` files inside, it will fetch and execute them, and finally your app is [rendered](https://preactjs.com/guide/v10/api-reference/#render)(i.e. client-side rendering) in all its glories to the users.

I have written about minimally configuring Webpack and Babel:

##### Webpack

https://medium.com/@kilgarenone/minimal-webpack-setup-a5f32c5f8960

[Here is](https://github.com/nystudio107/annotated-webpack-4-config) an accessible reference about configuring Webpack that I kept going back to in the beginning.

##### Babel

https://medium.com/@kilgarenone/minimal-babel-setup-b12b563ee2ca

### Performance

A web app that performs well is good for your [users and business](https://developers.google.com/web/fundamentals/performance/why-performance-matters).

Although web perf is a huge subject that's been [well documented](https://web.dev/fast/), I would like to highlight below few of the most impactful things I do for web perf, apart from [optimizing the images](https://images.guide/) which can account for over 50% of a page's weight.

#### Critical rendering path

We mentioned before that 'html-webpack-plugin' automatically injects all Webpack-generated `.js` and `.css` files for us in our `index.html`. But we don't want to do that now to have full control over resources ordering, and setting resource hints. So let's disable the auto-injection:

```javascript
// webpack.production.js
plugins: [
  new HtmlWebpackPlugin({
    template: settings.templatePath,
    filename: "index.html",
    inject: false, // we will inject ourselves
    mode: process.env.NODE_ENV,
  }),
];
```

And knowing that we can grab Webpack-generated assets from the [`htmlWebpackPlugin.files`](https://github.com/jantimon/html-webpack-plugin#writing-your-own-templates) object inside our `index.html`:

```json
// example of what you would see if you
// console.log(htmlWebpackPlugin.files)

{
  "publicPath": "/",
  "js": [
    "/js/runtime.a201e1a.js",
    "/vendors~app.d8e8c.js",
    "/app.f8fb511.js",
    "/components.3811eb.js"
  ],
  "css": ["/app.5597.css", "/components.b49d382.css"]
}
```

We will inject our assets ourselves in `index.html`:

```html
<% if (htmlWebpackPlugin.options.mode === 'production') { %>

<script
  defer
  src="<%= htmlWebpackPlugin.files.js.filter(e => /^\/vendors/.test(e))[0] %>"
></script>
<script
  defer
  src="<%= htmlWebpackPlugin.files.js.filter(e => /^\/app/.test(e))[0] %>"
></script>
<link
  rel="stylesheet"
  href="<%= htmlWebpackPlugin.files.css.filter(e => /app/.test(e))[0] %>"
/>

<% } %>
```

Note:

- We only do this when building for production; we let `webpack-dev-server` injects for us during local development.
- We use the `defer` attribute on our JS files so that browser will fetch them _while_ parsing our HTML, and only execute the fetched JS once the HTML is parsed.

  <figure>
  <img src="https://i.imgur.com/cF7jPjB.png" alt="defer diagram" loading="lazy"/>
  <figcaption><a href="https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/">source</a></figcaption>
  </figure>

#### Inlining CSS and JS

If you [managed](https://web.dev/extract-critical-css/#overview-of-tools) to separate your _critical_ CSS or you have a tiny JS script, you might want to consider inlining them in `<style>` and `<script>` respectively. Inlining saves network trips, although not being able to cache the inlined is a concern worth factoring in.

Let's inline the `runtime.js` generated by Webpack as suggested [here](https://developers.google.com/web/fundamentals/performance/webpack/use-long-term-caching#inline_webpack_runtime_to_save_an_extra_http_request). Back in the `index.html` above, add this snippet:

```html
<!-- more link and script -->

<script>
  <%= compilation.assets[htmlWebpackPlugin.files.js.filter(e => /runtime/.test(e))[0].substr(htmlWebpackPlugin.files.publicPath.length)].source() %>
</script>
```

The key is the `compilation.assets[<ASSET_FILE_NAME>].source()`:

> - compilation: the webpack [compilation object](https://webpack.js.org/api/compilation-object/). This can be used, for example, to get the contents of processed assets and inline them directly in the page, through `compilation.assets[...].source()` (see [the inline template example](https://github.com/jantimon/html-webpack-plugin/blob/master/examples/inline/template.pug)). ([source](https://github.com/jantimon/html-webpack-plugin#writing-your-own-templates))

You can use this method to inline your critical CSS asset too:

```
<style>
  <%= compilation.assets[htmlwebpackplugin.files.css.filter(e => /app/.test(e)) [0].substr(htmlWebpackPlugin.files.publicPath.length) ].source() %>
</style>
```

For non-critical CSS, you can consider 'preload' them.

#### Preload non-critical CSS

In short:

```html
<link
  rel="stylesheet"
  href="/path/to/my.css"
  media="print"
  onload="this.media='all'"
/>
```

[source](https://timkadlec.com/remembers/2020-02-13-when-css-blocks/)

Let's see how to do this with Webpack.

So I have my non-critical CSS contained in a CSS file, which I specify as its own entry point in Webpack:

```javascript
// webpack.config.js
module.exports = {
  entry: {
    app: "index.js",
    // final asset name will be like '/components.[hash].css'
    components: path.resolve(__dirname, "../src/css/components.scss"),
  },
};
```

Finally, I inject it below my critical CSS:

```html
<!-- Inlined critical CSS -->
<style>
  <%= compilation.assets[htmlwebpackplugin.files.css.filter(e => /app/.test(e)) [0].substr(htmlWebpackPlugin.files.publicPath.length) ].source() %>
</style>

<!-- Preloading non-critical CSS -->
<link
  rel="stylesheet"
  href="<%= htmlWebpackPlugin.files.css.filter(e => /components/.test(e))[0] %>"
  media="print"
  onload="this.media='all'"
/>
```

Let's **measure** if, after all this, we have actually done anything good on the [signup page](https://web.sametable.app/signup):

**BEFORE**
<img src="https://i.imgur.com/rfy7og8.png" loading="lazy"/>

**AFTER**
<img src="https://i.imgur.com/n5llJWx.png" loading="lazy"/>

Looks like we have improved almost all of the important user-centric metrics(not sure about the First Input Delay..)! 🎉

Here is a [good video tutorial](https://www.youtube.com/watch?v=j9LW94EN7n4) about measuring web performance in Chrome Dev tool.

#### Code splitting

Rather than bundle all your app's components, routes and third-party libraries into a single `.js` file, you should 'split' and load them on-demand based on a particular user's action. This will **dramatically** reduce the bundle size of your SPA and reduces initial Javascript processing costs, hence improving metrics like 'First interactive time' and 'First meaningful paint'.

Do code splitting in Webpack with the ['dynamic imports'](https://webpack.js.org/guides/code-splitting/#dynamic-imports):

```javascript
// editor.jsx

// LAZY-LOAD A MASSIVE THIRD-PARTY LIBRARY
componentDidMount() {
  const { default: MarkdownIt } = await import(
    /* webpackChunkName: "markdown-it" */
    "markdown-it"
  );
  new MarkdownIt({ html: true }).render(/* stuff */);
}

// OR LAZY-LOAD ONE OF YOUR COMPONENTS
checkout = () => {
  const { default: CheckoutModal } = await import(
    /* webpackChunkName: "checkoutModal" */
    "../routes/CheckoutModal"
  );
}
```

##### Guide

https://medium.com/@kilgarenone/pragmatic-code-splitting-with-preact-and-webpack-a3d3b19f86a3

### Fonts

Font files can be costly too. Take my favorite font [Inter](https://rsms.me/inter/) for an example: If I used 3 of its font styles, the total size could get up to 300KB, incurring costs such as network request and the accompanied FOUT and FOIT situations, particularly in low-end devices. Thus, I'm usually happy with the 'system fonts' that come with the machines:

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
}

code {
  font-family: SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono",
    "Courier New";
}
```

But if you must use custom web fonts, consider doing it right:

- You should [host](https://kevq.uk/how-to-self-host-your-web-fonts/) them [yourself](https://www.tunetheweb.com/blog/should-you-self-host-google-fonts/).
- ['Font-subsetting'](https://medium.com/@kilgarenone/subsetting-your-fonts-in-windows-10-using-wsl-bae4fafa35fc) to dramatically reduce the size of the font file.
- Go through this [checklist](https://www.zachleat.com/web/font-checklist/).

### Icons with SVG sprites

Icons in Sametable use SVG. There are different ways that I could have done it:

- Copy and paste the markup of an SVG icon wherever I need it. The downside is it would bloat the HTML and incur parsing costs particularly in mobile.
- Network request for a particular SVG file. Unless an SVG is huge (> 5KB), making a request for every SVG icon seems a bit much.
- Make an icon reusable in the form of a [React component](https://medium.com/@david.gilbertson/icons-as-react-components-de3e33cb8792). The downside is it unnecessarily introduces Javascript and its associated costs.

Instead, the solution I opted for my icons was '**SVG sprites**' which is more closer to the nature of SVG itself( [`<use>`](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/use) and [`<symbol>`](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/symbol)).

Let's see how.

Say there are many places that will use two of our SVG icons. In your `index.html`:

```html
<body>
  <svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
    <symbol id="pin-it" viewBox="0 0 96 96">
      <title>Give it a title</title>
      <desc>Give it a description for accessibility</desc>
      <path d="M67.7 40.3c-.3 2.7-2" />
    </symbol>
    <symbol id="unpin-it" viewBox="0 0 96 96">
      <title>Un-pin this entity</title>
      <desc>Click to un-pin this entity</desc>
      <path d="M67.7 40.3c-.3 2.7-2" />
    </symbol>
  </svg>
</body>
```

1. Hide the parent SVG element `style="display: none"`.
2. Give each SVG symbol an unique id `<symbol id="unique-id"`.
3. Make sure to define the `viewBox`(usually is already provided), but skip the `width` and `height`.
4. Give it `title` and `desc` for accessibility.
5. And most importantly, the `path` data of an icon.

And finally, here is how you use them in your components:

```javascript
// example.jsx

render() {
  <svg
    xmlns="http://www.w3.org/2000/svg"
    xmlnsXlink="http://www.w3.org/1999/xlink"
    width="24"
    height="24"
  >
    <use xlinkHref="#pin-it" />
  </svg>

}
```

1. Define the `width` and `height` as desired.
2. Specify the `id` of one of the `<symbol>` in the 'index.html' above: `<use xlinkHref="#pin-it" />`.

#### Lazy load SVG sprites

Or to putting your SVG symbols in the `index.html`, you could put them in a `.svg` file:

```html
<svg xmlns="http://www.w3.org/2000/svg">
  <symbol id="header-1" viewBox="0 0 26 24">
    <title>Header 1</title>
    <desc>Toggle a h1 header</desc>
    <text x="0" y="20" font-weight="600">H1</text>
  </symbol>
  <symbol id="header-2" viewBox="0 0 26 24">
    <title>Header 2</title>
    <desc>Toggle a h2 header</desc>
    <text x="0" y="20" font-weight="600">H2</text>
  </symbol>
</svg>
```

And I put that file in `client/src/assets`:

```
- client
  - src
    - assets
      - svg-sprites.svg
```

Finally, to use one of the symbols in the file:

```javascript
// Editor.js

import svgSprites from "../../assets/svg-sprites.svg";

/* component stuff */

render() {
  return (
    <button type="button">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlnsXlink="http://www.w3.org/1999/xlink"
        width="24"
        height="24"
      >
        <use xlinkHref={`${svgSprites}#header-1`} />
      </svg>
    </button>
  )
}
```

And browser will, during runtime, fetch the `.svg` file if it hadn't already.

And there you have it! No more plastering those lengthy `path` data all over the place.

#### Sources of icons

- https://material.io/resources/icons/?style=baseline
- https://logomakr.com/
- https://github.com/wmira/react-icons-kit#bundled-icon-sets (has a nice list of sources)

#### References

https://css-tricks.com/mega-list-svg-information/#svg-icons

### Favicon

If I hadn't disabled the `inject` option of 'html-webpack-plugin', I would have used a plugin called ['favicons-webpack-plugin'](https://github.com/jantimon/favicons-webpack-plugin) that automatically generates all types of favicons, and inject them in my `index.html`:

```javascript
// webpack.config.js

plugins: [
  new HtmlWebpackPlugin(), // 'inject' is true by default
  // must come after html-webpack-plugin
  new FaviconsWebpackPlugin({
    logo: path.resolve(__dirname, "../src/assets/logo.svg"),
    prefix: "icons-[hash]/",
    persistentCache: true,
    inject: true,
    favicons: {
      appName: "Sametable",
      appDescription: "Manage your tasks in spreadsheets",
      developerName: "Kheoh Yee Wei",
      developerURL: "https://kheohyeewei.com", // prevent retrieving from the nearest package.json
      theme_color: "#fcbdaa",
      // specify the vendors that you want favicon for
      icons: {
        coast: false,
        yandex: false,
      },
    },
  }),
];
```

Since I had disabled the auto-injection, here is how I handled my favicon:

1. Go to https://realfavicongenerator.net/

   - Provide your logo in SVG format.
   - Select the 'Version/Refresh' option to enable cache-busting your favicon asset in your users' browser.
   - Complete the instructions at the end. You can store your favicons in any folder in your project.

2. Use ['copy-webpack-plugin'](https://webpack.js.org/plugins/copy-webpack-plugin/) to copy all your favicon assets generated from Step-1, from the folder you store them(in my case, `src/assets/favicon`) to my Webpack's output's [path](https://github.com/kilgarenone/boileroom/blob/master/client/config/webpack.production.js#L140) ([default behaviour](https://github.com/webpack-contrib/copy-webpack-plugin#to)), so that they will be accessible from the root(i.e. https://example.com/favicon.ico).

   ```javascript
   // webpack.config.js
   const CopyWebpackPlugin = require("copy-webpack-plugin");

   plugins: [new CopyWebpackPlugin([{ from: "src/assets/favicon" }])];
   ```

And that's it!

### Security

Consider adding the [CSP](https://developers.google.com/web/fundamentals/security/csp/) security headers.

To add headers in firebase: https://firebase.google.com/docs/hosting/full-config#headers

Sample of CSP headers in your `firebase.json`:

```json
{
  "source": "**",
  "headers": [
    {
      "key": "Strict-Transport-Security",
      "value": "max-age=63072000; includeSubdomains; preload"
    },
    {
      "key": "Content-Security-Policy",
      "value": "default-src 'none'; img-src 'self'; script-src 'self'; style-src 'self'; object-src 'none'"
    },
    { "key": "X-Content-Type-Options", "value": "nosniff" },
    { "key": "X-Frame-Options", "value": "DENY" },
    { "key": "X-XSS-Protection", "value": "1; mode=block" },
    { "key": "Referrer-Policy", "value": "same-origin" }
  ]
}
```

If you use Stripe, make sure you add their CSP directives too:
https://stripe.com/docs/security/guide#content-security-policy

Finally, make sure you get an **A** [here](https://observatory.mozilla.org/) and pat yourself on the back!

## Design

We will explore a few concepts that help structure your design to be coherent.

### Modular scale

Your design will demand less efforts from your users to make sense of when it flows as enforced by a 'modular scale', which specifies a scale of spaces or sizes that each increments with a certain ratio.

One way to create a scale is with CSS ['Custom Properties'](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)(credits to [every-layout.dev](https://every-layout.dev/)):

```css
:root {
  --ratio: 1.414;
  --s-3: calc(var(--s0) / var(--ratio) / var(--ratio) / var(--ratio));
  --s-2: calc(var(--s0) / var(--ratio) / var(--ratio));
  --s-1: calc(var(--s0) / var(--ratio));
  --s0: 1rem;
  --s1: calc(var(--s0) * var(--ratio));
  --s2: calc(var(--s0) * var(--ratio) * var(--ratio));
  --s3: calc(var(--s0) * var(--ratio) * var(--ratio) * var(--ratio));
}
```

If you don't know what scale to use, just [pick a scale](https://www.modularscale.com/) that fits closest to your design and stick to it.

Then I create a bunch of utility classes, each associated with a scale, in a file call `spacing.scss`. I will use them to space my UI elements across a project:

```css
.mb-1 {
  margin-bottom: var(--s1);
}
.mb-2 {
  margin-bottom: var(--s2);
}
.mr-1 {
  margin-right: var(--s1);
}
.mr--1 {
  margin-right: var(--s-1);
}
```

Notice that I try to define the spacing only in the `right` and `bottom` direction as [suggested here](https://csswizardry.com/2012/06/single-direction-margin-declarations/).

In my experience, it's better to not bake in any spacing definitions in your UI components:

**DON'T**

```javascript
// Button.scss
.btn {
  margin: 10px; // a default spacing; annoying to have in most cases
  font-style: normal;
  border: 0;
  background-color: transparent;
}

// Button.jsx
import s from './Button.scss';

export function Button({children, ...props}) {
  return (
    <button class={s.btn} {...props}>{children}</button>
  )
}

// Usage
<Button />
```

**DO**

```javascript
// Button.scss
.btn {
  font-style: normal;
  border: 0;
  background-color: transparent;
}

// Button.jsx
import s from './Button.scss';

export function Button({children, className, ...props}) {
  return (
    <button class={`${s.btn} ${className}`} {...props}>{children}</button>
  )
}

// Usage
// Pass your spacing utility classes when building your pages
<Button className="mr-1 pb-1">Sign Up</Button>
```

### Colors

There are many color palette tools out there. But the one from [Material](https://material.io/design/color/the-color-system.html#tools-for-picking-colors) is where I always go to for my colors.

Then I will define them as CSS Custom Properties again:

```css
:root {
  --black-100: #0b0c0c;
  --black-80: #424242;
  --black-60: #555759;
  --black-50: #626a6e;

  font-size: 105%;
  color: var(--black-100);
}
```

### CSS Reset

Very simple:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
  overflow-wrap: break-word;
  margin: 0;
  padding: 0;
  border: 0 solid;
  background-color: inherit;
  font-family: inherit;
  color: inherit;
}

/* Set core body defaults */
body {
  scroll-behavior: smooth;
  text-rendering: optimizeLegibility;
}

/* Make images easier to work with */
img {
  max-width: 100%;
}

/* Inherit fonts for inputs and buttons */
button,
input,
textarea,
select {
  color: inherit;
  font: inherit;
}
```

### A Styling Practice

I always try to style at the **tag**-level first before bringing out the big gun if necessary, in my case, 'CSS Modules', for encapsulating styles per component:

```
- src
  - routes
    - SignIn
      - SignIn.js
      - SignIn.scss
```

The `SignIn.scss` contains CSS that pertains only to the `<SignIn />` component.

Furthermore, I don't use any CSS libraries popular in the React ecosystem like 'styled-components' and 'emotion'. I try to **use pure HTML and CSS whenever I can, and only let Preact handle the DOM and state updates** for me.

For example, for the `input` element:

```css
// index.scss

label {
  display: block;
  color: var(--black-100);
  font-weight: 600;
}

input {
  width: 100%;
  font-weight: 400;
  font-style: normal;
  border: 2px solid var(--black-100);
  box-shadow: none;
  outline: none;
  appearance: none;
}

input:focus {
  box-shadow: inset 0 0 0 2px;
  outline: 3px solid #fd0;
  outline-offset: 0;
}
```

Then using it in a JSX file:

```javascript
// SignIn.js

render() {
  return (
    <div class="form-control">
      <label htmlFor="email">
        Email&nbsp;
        <strong>
          <abbr title="This field is required">*</abbr>
        </strong>
      </label>
      <input
        required
        value={this.email}
        type="email"
        id="email"
        name="email"
        placeholder="e.g. sara@widgetco.com"
      />
    </div>
  )
}
```

### Layout

I use **CSS Flexbox** for layout works in Sametable. There was no need for any CSS frameworks at all. Learn CSS Flexbox from its first principles to do more with less code. Plus, in many cases, the result is already responsive thanks to the layout algorithms, saving those `@media` queries.

Let's see how to build a common layout in Flexbox with a minimal amount of CSS:

<img src="https://i.imgur.com/PTCrd0K.png" alt="sidebar and content layout" loading="lazy"/>

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="html,result" data-user="kilgarenone" data-slug-hash="mdeLwvx" data-preview="true" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Sidebar/Content layout">
  <span>See the Pen <a href="https://codepen.io/kilgarenone/pen/mdeLwvx">
  Sidebar/Content layout</a> by Ahwei (<a href="https://codepen.io/kilgarenone">@kilgarenone</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

#### Resources

- https://flexboxfroggy.com/
- https://www.freecodecamp.org/news/understanding-flexbox-everything-you-need-to-know-b4013d4dc9af/

### API Calls

A client needs to communicate with a server to do the works of 'CRUD'- Create, Read, Update, and Delete:

<img src="https://i.imgur.com/VjAWItp.png" alt="client and server communication diagram" loading="lazy"/>

Here is my hopefully easy to understand `api.js`:

<details>
  <summary>API wrapper</summary>

```javascript
import { route } from "preact-router";

function checkStatus(response) {
  const responseCode = response.status;

  if (responseCode >= 200 && responseCode < 300) {
    return response;
  }

  // handle user not authorized scenario
  if (responseCode === 401) {
    response
      .json()
      .then((json) =>
        route(`/signin${json.refererUri ? `?dest=${json.refererUri}` : ""}`)
      );
    return;
  }

  // pass along error response to the 'catch' block of your await/async try & catch block
  return response.json().then((json) => {
    return Promise.reject({
      status: responseCode,
      ok: false,
      statusText: response.statusText,
      body: json,
    });
  });
}

function handleError(error) {
  error.response = {
    status: 0,
    statusText:
      "Cannot connect. Please make sure you are connected to internet.",
  };
  throw error;
}

function parseJSON(response) {
  if (response.status === 204 || response.status === 205) {
    return null;
  }
  return response.json();
}

function request(url, options) {
  return fetch(url, options)
    .catch(handleError) // handle network issues
    .then(checkStatus)
    .then(parseJSON)
    .catch((e) => {
      throw e;
    });
}

export function api(endPoint, userOptions = {}) {
  const url = process.env.API_BASE_URL + endPoint;

  // to pass along our auth cookie to server
  userOptions.credentials = "include";

  const defaultHeaders = {
    "Content-Type": "application/json",
    Accept: "application/json",
  };

  if (userOptions.body instanceof File) {
    const formData = new FormData();
    formData.append("file", userOptions.body);
    userOptions.body = formData;
    // let browser set content-type to multipart/etc.
    delete defaultHeaders["Content-Type"];
  }

  if (userOptions.body instanceof FormData) {
    // let browser set content-type to multipart/etc.
    delete defaultHeaders["Content-Type"];
  }

  const options = {
    ...userOptions,
    headers: {
      ...defaultHeaders,
      ...userOptions.headers,
    },
  };

  return request(url, options);
}
```

</details>

There is almost nothing new to learn to start using this api module if you have used the native [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) before.

#### Usage

```javascript
// Home.jsx
import { api } from "../lib/api";

async componentDidMount() {
  try {
    // POST-ing data
    const response = await api(
      '/projects/save/121212121',
      {
        method: 'PUT',
        body: JSON.stringify(dataObject)
      }
    )

    // or GET-ting data
    const { myWorkspaces } = await api('/users/home');

  } catch (err) {
    // handle Promise.reject passed from api.js
  }
}
```

But if you preferred to use a library to handle your http calls, I'd recommend ['redaxios'](https://github.com/developit/redaxios) which not only shares API with the popular [axios](https://www.npmjs.com/package/axios), but also it's much more lightweight.

## Server

```json
- server
  - server.js
  - package.json
  - .env

```

The [server](https://github.com/kilgarenone/boileroom/tree/master/server) is run on NodeJS(ExpressJS framework) to serve all my **API** endpoints.

```javascript
// Example endpoint: https://example.com/api/tasks/save/12345
router.put("/save/:taskId", (req, res, next) => {});
```

The [`server.js`](https://github.com/kilgarenone/boileroom/blob/master/server/server.js) contains the [familiar](https://expressjs.com/en/starter/hello-world.html) codes to start a Nodejs server.

#### Project structure

I'm grateful for this digestible [guide](https://node-postgres.com/guides/project-structure) about project structure, allowing me to hunker down quickly to build out my API.

#### npm script

In the server's `package.json`, there is a npm script that will start your server for you:

```json
"scripts": {
  "dev": "nodemon -r dotenv/config server.js",
  "start": "node server.js"
}
```

- The `dev` script ['preload'](https://www.npmjs.com/package/dotenv#preload) dotenv as suggested [here](https://medium.com/the-node-js-collection/making-your-node-js-work-everywhere-with-environment-variables-2da8cdf6e786#b1af). And that's it&mdash; You will have access to the env variables defined in the `.env` file from the `process.env` object.

- The `start` script, as we will see later, is used to start our Nodejs server in production.

### Database

Database is used to store and persist users' data.

I use **Postgresql** for my database. And I use ['node-postgres'](https://node-postgres.com/)(a.k.a `pg`) library to connect my Nodejs to the database. Once that's done, I can do CRUD works between my API endpoints and the database.

#### Setup

For local development:

### 1.

Download the [software here](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads). Get the latest version. Leave everything as it is. Remember the password you set. Then,

- Open 'pgAdmin'. It's a browser application.
- Create a database for you app, :

<img src="https://i.imgur.com/trcAaSi.png" loading="lazy"/>

### 2.

Define a set of environment variables in the `.env` file:

```
DB_HOST='localhost'
DB_USER=postgres
DB_NAME=<YOUR_CUSTOM_DATABASE_NAME_HERE>
DB_PASSWORD=<YOUR_MASTER_PASSWORD>
DB_PORT=5432
```

### 3. [#](#db-wrapper)

Then we will [connect](https://node-postgres.com/features/connecting) a new client through a [connection pool](https://node-postgres.com/features/pooling) to our Postgresql database from our Nodejs. I do it in `server/db/index.js`:

```javascript
const { Pool } = require("pg");

const pool = new Pool({
  user: process.env.DB_USER,
  host: process.env.DB_HOST,
  port: process.env.DB_PORT,
  database: process.env.DB_NAME,
  password: process.env.DB_PASSWORD,
});

// TRANSACTION
// https://github.com/brianc/node-postgres/issues/1252#issuecomment-293899088
const tx = async (callback, errCallback) => {
  const client = await pool.connect();
  try {
    await client.query("BEGIN");
    await callback(client);
    await client.query("COMMIT");
  } catch (err) {
    console.log(("DB ERROR:", err));
    await client.query("ROLLBACK");
    errCallback && errCallback(err);
  } finally {
    client.release();
  }
};
// the pool will emit an error on behalf of any idle clients
// it contains if a backend error or network partition happens
pool.on("error", (err) => {
  process.exit(-1);
});

pool.on("connect", () => {
  console.log("❤️ Connected to the Database ❤️");
});

module.exports = {
  query: (text, params, callback) => pool.query(text, params, callback),
  tx,
  pool,
};
```

- I will use the `tx` function if I have to call **many** queries that depends on each other in an API.
- If I'm making a **single** query, I will use the `query` function.

And that's it! Now you have got a database to work with for your local development :rocket:

#### Usage

I will confess: I **hand-craft** all the queries for Sametable.

In my opinion, SQL itself is already a declarative language that needs no further abstraction-it's easy to read, understand, and write. It can be maintainable if you separated well your API endpoints. But, if you knew you were building a facebook-scale app, perhaps it would be wise to use an ORM. But I'm just a [everyday normal guy](https://www.youtube.com/watch?v=5PsnxDQvQpw) building a very narrow-scoped SaaS all by myself. So I needed to avoid overhead and complexity while considering factors such as ease of onboarding, performance, ease of reiteration, and the potential lifespan of the knowledge. It's like the advice that urges us to learn vanilla Javascript before jumping on the bandwagon of a popular front-end framework. Because you just might realize: That's all you need for what you have set out to accomplish.

To be fair though, when I decided to go down this path, I'd had modest experiences in writing MySQL. So if you knew nothing about SQL and you were anxious to ship it, then you might want to consider a library like [knex.js](http://knexjs.org/).

##### Example

```javascript
// server/routes/projects.js

const express = require("express");
const asyncHandler = require("express-async-handler");
const db = require("../db");

const router = express.Router();

module.exports = router;

// [POST] api/projects/create
router.post(
  "/create",
  express.json(),
  asyncHandler(async (req, res, next) => {
    const { title, project_id } = req.body;

    db.tx(async (client) => {
      const {
        rows,
      } = await client.query(
        `INSERT INTO tasks (title) VALUES ($1) RETURNING mask_id(task_id) as masked_task_id, task_id`,
        [title]
      );

      res.json({ id: rows[0].masked_task_id });
    }, next);
  })
);
```

- With [`express-async-handler`](https://github.com/Abazhenov/express-async-handler/blob/master/index.js), I can write my route handlers with the 'async/await' pattern and handling the async errors. It will be obsolete when Express 5 drops.

* Import the `db` module to use the `tx` method. Pass your hand-crafted SQL queries and [parameters](https://node-postgres.com/features/queries).

That's it!

#### Creating table schemas

Before you can start quering a database, you need to create tables. Each table contains information about an entity or relationships. Before that can happen, you need to decide which information goes to which table. And what has helped me in that exercise is a concept called [**denormalization**](https://firebase.google.com/docs/database/web/structure-data). Essentially, you don't want to store everything about an entity in the same table. For example, say, we have a `users` table storing `fullname`, `password` and `email`. It wouldn't be advisable to also store the ids of all the projects assigned to a particular user. Instead, I would break them up into separate tables:

1. Create the `users` table. Notice that it's not storing any data related to 'projects':

   ```sql
   CREATE TABLE users(
     user_id BIGSERIAL PRIMARY KEY,
     fullname TEXT NOT NULL,
     pwd TEXT NOT NULL,
     email TEXT UNIQUE NOT NULL,
   );
   ```

2. Create a `projects` table to store data solely about a project's details:

   ```sql
   CREATE TABLE projects(
     project_id BIGSERIAL PRIMARY KEY,
     title TEXT,
     content TEXT,
     due_date TIMESTAMPTZ,
     status SMALLINT,
     created_on TIMESTAMPTZ NOT NULL DEFAULT now()
   );
   ```

3. Create a 'bridge' table about projects' ownerships by connecting a user's 'id' to an id of a project that she owns. This table is just a bunch of ids from different tables, in this case, the `users` and `projects` tables:

   ```sql
   CREATE TABLE project_ownerships(
     project_id BIGINT REFERENCES projects ON DELETE CASCADE,
     user_id BIGINT REFERENCES users ON DELETE CASCADE,
     PRIMARY KEY (project_id, user_id),
     CONSTRAINT project_user_unique UNIQUE (user_id, project_id)
   );
   ```

4. Finally, to get all the projects that are assigned to a particular user, we will do what relational database do best: [`join`](https://www.postgresqltutorial.com/postgresql-joins/).

Now the way I create and maintain my tables' schema is, to say the least, lackluster.

I put all my schemas in a file:

```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

CREATE TABLE users(
  user_id BIGSERIAL PRIMARY KEY,
  fullname TEXT NOT NULL,
  pwd TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL,
  created_on TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

Then, I would copy the schemas from the file, paste and run them in pgAdmin:

<img src="https://i.imgur.com/gm9YFZF.png" alt="create table schemas in pgadmin" loading="lazy" />

No doubt there are more advanced ways of doing this, so it's up to you if you want to spend more time exploring them to see which suits you.

##### Dropping a database

Deleting an entire database to start with a new set of schemas was something I had to do very often at the beginning.

The trick is, well: Copy, paste, and run it in the database's query editor as accessed from above:

```sql
DROP SCHEMA public CASCADE;
CREATE SCHEMA public;
GRANT ALL ON SCHEMA public TO postgres;
GRANT ALL ON SCHEMA public TO public;
COMMENT ON SCHEMA public IS 'standard public schema';
```

#### Building SQL queries

I craft my SQL queries in **pgAdmin** to get the data I want out of an API endpoint.

Hopefully this annotated image sums that up:

<img src="https://i.imgur.com/54tIRzc.png" alt="writing sql queries in pgadmin editor" loading="lazy" />

##### Writing queries with Common Table Expressions(CTEs)

I stumbled upon a pattern called [**CTEs**](https://www.postgresql.org/docs/9.1/queries-with.html) when I was exploring how I am going to get the data that I want from disparate tables, and structure them as desired, without doing lots of separate database queries and for-loops.

The way CTE works is simple enough: You write your queries. Each is given an alias name (`q`, `q1`, `q3`). And a next query can access any previous query's results by their alias name(`q1.workspace_id`):

```sql
WITH q AS (SELECT * FROM projects_tasks WHERE task_id=$1)
, q1 AS (SELECT wp.workspace_id, wp.project_id, q.task_id FROM workspaces_projects wp, q WHERE wp.project_id = q.project_id)
, q3 AS (SELECT q1.workspace_id AS workspace_id, wp.name AS workspace_title, mask_id(q1.project_id) AS project_id, p.title AS project_title, mask_id(t.task_id) AS task_id, t.title, t.content, t.due_date, t.priority, t.status)

SELECT * FROM q3;
```

### Redis

Redis is a NoSQL database that stores data in memory which makes it fast. In Sametable, I used Redis for two purposes:

1. Store a user's session data.
2. Cache the results of some of my Postgresql's queries, saving us from having to query the database if the cache is still fresh.

#### Installation

I'm on a Windows 10 machine with Windows Subsystem Linux(WSL) installed. This was the only guide I followed:

https://redislabs.com/blog/redis-on-windows-10/

Follow the guide to install WSL if you don't have it already.

Then I will start my local Redis server in WSL bash:

1. Press `Win` + `R`.
2. Type `bash` and enter.
3. In the terminal, run `sudo service redis-server start`

Now install the [`redis`](https://www.npmjs.com/package/redis) npm package:

```
cd server

npm i redis
```

Make sure to install it in the `server`'s `package.json`, hence the `cd server`.

Then I create a file named `redis.js` under `server/db`:

```javascript
// server/db/redis.js

const redis = require("redis");
const { promisify } = require("util");

const redisClient = redis.createClient(
  NODE_ENV === "production"
    ? {
        host: process.env.REDISHOST,
        no_ready_check: true,
        auth_pass: process.env.REDIS_PASSWORD,
      }
    : {}
);

redisClient.on("error", (err) => console.error("ERR:REDIS:", err));

const redisGetAsync = promisify(redisClient.get).bind(redisClient);
const redisSetExAsync = promisify(redisClient.setex).bind(redisClient);
const redisDelAsync = promisify(redisClient.del).bind(redisClient);

// 1 day expiry
const REDIS_EXPIRATION = 7 * 86400; // seconds

module.exports = {
  redisGetAsync,
  redisSetExAsync,
  redisDelAsync,
  REDIS_EXPIRATION,
  redisClient,
};
```

- By [default](https://www.npmjs.com/package/redis#options-object-properties), `node-redis` will connect to `localhost` at port `6379`. But that might not be the case in production particularly when you host your Redis in a VM. So I provide this object when it's 'production':

  ```
  {
     host: process.env.REDISHOST,
     no_ready_check: true,
     auth_pass: process.env.REDIS_PASSWORD,
   }
  ```

  - TBH, I'm not entirely sure about the `no_ready_check`. I got it from this official [tutorial](https://docs.redislabs.com/latest/rs/references/client_references/client_nodejs/).
  - The `auth_pass` and `host` are provided as custom since I host my Redis in a GCE VM where I have also set a password on my Redis.

* I [promisfy](https://www.npmjs.com/package/redis#promises) the Redis methods that I will use to make them async to avoid blocking NodeJS's single-thread.

And now you have the Redis for your local development!

### Error handling & Logging

#### Error handling

Error handling in Nodejs has a paradigm which we will explore in 3 different contexts.

To set the stage, we need two things in place first:

1. An npm package called [http-errors](https://www.npmjs.com/package/http-errors) that will give us a standard error data structure to work with.

   ```
   npm install http-errors
   ```

2. Our custom error handler at the global level to capture **all** propagated errors(i.e. `next(err)`) from the routes or the `catch` blocks.

   ```javascript
   // app.js
   const express = require("express");
   const app = express();
   const createError = require("http-errors");

   // our central custom error handler
   // NOTE: DON"T REMOVE THE 'next' even though eslint complains it's not being used!!!
   app.use(function (err, req, res, next) {
     // errors wrapped by http-errors will have 'status' property defined. Otherwise, it's a generic unexpected error
     const error = err.status
       ? err
       : createError(500, "Something went wrong. Notified dev.");

     res.status(error.status).json(error);
   });
   ```

   As you will see, the general pattern of error handling in Nodejs revolves around the 'middleware' chain and the `next` parameter:

   > Calls to next() and next(err) indicate that the current handler is complete and in what state. next(err) will skip all remaining handlers in the chain except for those that are set up to handle errors . . . [source](https://expressjs.com/en/guide/error-handling.html)

   Note that although this is a common pattern of handling error in Express, you might want to consider an [alternative way](https://github.com/goldbergyoni/nodebestpractices/blob/master/sections/errorhandling/centralizedhandling.md) that's, however, more complicated.

##### Input validation

It's a [good practise](https://github.com/goldbergyoni/nodebestpractices#-610-validate-incoming-json-schemas) to validate a user's inputs both in the client and server side. At the server side, I use a library called ['express-validator'](https://express-validator.github.io/docs/) to do the job. If any input is invalid, we will handle it by responding with a http code and an error message to inform the user about it.

For example, when an email provided by a user is invalid, we will exit early by creating an error object with the 'http-errors' library, and then pass it to the `next` function:

```javascript
const { body, validationResult } = require("express-validator");

router.post(
  "/login",
  upload.none(),
  [body("email", "Invalid email format").isEmail()],
  asyncHandler(async (req, res, next) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return next(createError(422, errors.mapped()));
    }

    res.json({});
  })
);
```

The following response will be sent to the client:

```json
{
  "message": "Unprocessable Entity",
  "email": {
    "value": "hello@mail.com232",
    "msg": "Invalid email format",
    "param": "email",
    "location": "body"
  }
}
```

Then it's up to you what you want to do with it. For example, you can access the `email.msg` property to display the error message below the email input field.

##### Errors from business logic

Let's say we have a situation where a user entered an email that doesn't exist in the database. In that case, we need to tell the user to try again.

```javascript
router.post(
  "/login",
  upload.none(),
  asyncHandler(async (req, res, next) => {
    const { email, password } = req.body;

    const {
      rowCount,
    } = await db.query(`SELECT * FROM users WHERE email=($1)`, [email]);

    if (rowCount === 0) {
      // issue an error with generic message
      return next(
        createError(422, "Please enter a correct email and password")
      );
    }

    res.json({});
```

Remember, any error object passed to 'next'- `next(err)`- will be captured by the custom error handler as we have set above.

##### Unexpected errors from database

I pass the route handler's `next` to my db's <a href="db-wrapper">transaction</a> wrapper function to handle any unexpected erorrs.

```javascript
router.post(
  "/invite",
  async (req, res, next) => {
    db.tx(async (client) => {
          const {
            rows,
            rowCount,
          } = await client.query(
            `SELECT mask_id(user_id) AS user_id, status FROM users WHERE users.email=$1`,
            [email]
          );
    }, next)
)
```

#### Logging

When a particular error occurs, it's a common practise to 1) Log it to a system for records, and 2) Automatically send you a notification about it.

As expected, there are many tools out there in this area. But I ended up with [**Sentry**](https://sentry.io/welcome/) for storing details(e.g. stack traces) of my errors, and [**pino**](https://github.com/pinojs/pino) to enable logging in my Nodejs.

**Why Sentry**? Well it was recommended by lots of solo devs and small startups. It offers 5000 errors you can send per month for free. For perspective, if you are operating a small side project and careful about it, I would say that'd last you until you can afford a more luxurous vendor or plan. Another option worth exploring is [honeybadger.io](https://www.honeybadger.io/) with more generous free-tier but without a [pino transport](https://getpino.io/#/docs/transports).

**Why Pino**- Why not the official SDK provided by Sentry? Because Pino has ['low overhead'](https://github.com/pinojs/pino#low-overhead), whereas, Sentry SDK, although it gives you a more complete picture of an error, it seemeed to have a complex [memory issue](https://github.com/getsentry/sentry-javascript/issues/1762) that I couldn't see myself being able to circumvent.

With that, here is how the logging system works in Sametable:

```javascript
// server/lib/logger.js

// install missing packages
const pino = require("pino");
const { createWriteStream } = require("pino-sentry");
const expressPino = require("express-pino-logger");

const options = { name: "sametable", level: "error" };

// SENTRY_DSN is provided by Sentry. Store it as env var in the .env file.
const stream = createWriteStream({ dsn: process.env.SENTRY_DSN });

const logger = pino(options, stream);
const expressLogger = expressPino({ logger });

module.exports = {
  expressLogger, // use it like app.use(expressLogger) -> req.log.info('haha)
  logger,
};
```

Rather than attaching the logger(`expressLogger`) as a middleware at the top of the chain(`app.use(expressLogger)`), I use the `logger` object whenever I need to log an error.

For example, the custom global error handler uses the `logger`:

```javascript
app.use(function (err, req, res, next) {
  const error = err.status
    ? err
    : createError(500, "Something went wrong. Notified dev.");

  if (isProduction) {
    // LOG THIS ERROR IN MY SENTRY ACCOUNT
    logger.error(error);
  } else {
    console.log("Custom error handler:", error);
  }

  res.status(error.status).json(error);
});
```

That's it! And don't forget to enable email **notification** in your Sentry dashboard to get an alert when your Sentry receives an error! :heart:

## User authentication system

A user authentication system can get very complicated when you need to support things like SSO and third-party OAuth providers. That's why we have third-party tools such as Auth0, Okta, and PassportJS to abstract that out for us. But those tools cost: vendor lock-in, more Javascript payload, and cognitive overhead.

I would argue that if you are starting out and just need _some_ _kind of_ authentication system so you can move on to other parts of your app, and at the same time, overwhelmed by all the dated tutorials and heavy-handed tools out there, well, chances are all you need is the good old way of doing authentication: **Session cookie** with **email** and **password**! And we are not talking about 'JWT' either! None of that.

### Guide

https://medium.com/@kilgarenone/easily-implements-user-authentication-in-nodejs-b22bdb6f15bc

## Email

Currently, in Sametable, the only emails it sends are of 'transactional' type like sending a reset password email when users reset their password.

There are two ways to send emails in Nodejs:

1. **Roll your own** with [Nodemailer](https://nodemailer.com/about/).

   I wouldn't go down this path because although sending one email might seem a trivial task, doing it 'at scale' is hard; every email must be sent successfully; and they must not end up in a user's spam folder; and other things I haven't even realized yet.

2. Choose one of the **email service providers**.

   There are many email services who offer a free-tier plan offering a limited number of emails you can send per month/day for free. When I started exploring this space for Sametable in October 2019, Mailgun stood out to be a no-brainer- It offers 10,000 emails for free per month! But, sadly, as I was researching for this section write-up, I learned that it no longer offers that. Despite that though, I would still stick to Mailgun, on their [pay-as-you-go](https://www.mailgun.com/pricing) plan: 1000 emails sent will cost you 80 cents. If you would rather not pay a cent for whatever reason, here are two options for you that I could find:

   - https://www.mailjet.com/pricing/
   - https://www.sendinblue.com/pricing/

   But do go down this path while being aware there's no guarantee that all free-tier plans will stay that way forever as was the case with Mailgun.

### Implementation

#### Wrapper file

```javascript
// server/lib/email.js

// Run 'npm install mailgun-js' in your 'server' folder
const mailgun = require("mailgun-js");

const DOMAIN = "mail.sametable.app";

const mg = mailgun({
  apiKey: process.env.MAILGUN_API_KEY,
  domain: DOMAIN,
});

function send(data) {
  mg.messages().send(data, function (error) {
    if (!error) return;
    console.log("Email send error:", error);
  });
}

module.exports = {
  send,
};
```

#### Usage

```javascript
const mailer = require("../lib/email");

// Simplified for only email-related stuff
router.post(
  "/resetPassword",
  upload.none(),
  (req, res, next) => {
    const { email } = req.body;
    const data = {
      from: "Sametable <feedback@sametable.app>",
      to: email,
      subject: "Reset your password",
      text: `Click this link to reset your password: https://example.com?token=1234`,
    };
    mailer.send(data);
    res.json({});
  })
);
```

### Email templates

An email template contains a particular email's contents with some optional dynamic values.

#### Tool

[**mjml**](https://mjml.io/) - The tool I use to build my email templates.

It's easy to [get started](https://mjml.io/getting-started/1). It's quite similar to React: You compose a template with a bunch of reusable components with props.

Here are the places where I would write my templates:

- This [VSCode extension](https://marketplace.visualstudio.com/items?itemName=attilabuti.vscode-mjml)
- [Live code editor](https://mjml.io/try-it-live)

#### Example template

<details>
  <summary>Template</summary>

```html
<mjml>
  <mj-head>
    <mj-attributes>
      <mj-class
        name="font-family"
        font-family="-apple-system,system-ui,BlinkMacSystemFont,'Segoe UI',sans-serif"
      />
      <mj-class name="fw-600" font-weight="600" />
    </mj-attributes>
  </mj-head>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-image
          width="150px"
          src="https://www.dl.dropboxusercontent.com/s/pgtwrnfa3lqkf5r/sametable_logo_with_text.png"
        />
      </mj-column>
    </mj-section>
    <mj-section>
      <mj-column>
        <mj-text align="center" font-size="20px" mj-class="font-family"
          >{{assigner_name}} assigned a project to you</mj-text
        >
        <mj-spacer height="10px" />
        <mj-text align="center" font-size="25px" mj-class="font-family fw-600"
          >{{project_title}}</mj-text
        >
        <mj-spacer height="25px" />
        <mj-button
          font-size="16px"
          mj-class="font-family fw-600"
          background-color="#000"
          color="white"
          href="{{invite_link}}"
          >View the project</mj-button
        >
      </mj-column>
    </mj-section>
    <mj-spacer height="55px" />
    <mj-section background-color="#EEEBE7" padding="25px 40px">
      <mj-column>
        <mj-text
          align="center"
          color="#45495d"
          font-size="15px"
          line-height="14px"
        >
          Problems or questions? Feel free to reply to this email.
        </mj-text>
        <mj-text padding="30px 0 0 0" align="center" font-size="16px">
          Made with ❤️ by
          <a href="https://twitter.com/kheohyeewei">@kheohyeewei</a>
        </mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

</details>

##### Result

<img width="400px" src="https://i.imgur.com/JnaSDYJ.png" loading="lazy" />

Notice the placeholder names that are wrapped in double curly brackets: `{{project_title}}`. They will eventually be replaced by their corresponding value.

#### Integration with Mailgun

First, generate HTML from your mjml templates. You are able to do that with the vscode extension and the code editor:

<img src="https://i.imgur.com/O9mnBvN.png" alt="generate html in mjml online code editor" loading="lazy" />

Then create a new template on Mailgun:

<img src="https://i.imgur.com/OkvLxiT.png" alt="create message template on mailgun dashboard" loading="lazy" />

#### Send email with a template in Express

Inside a route:

```javascript
const data = {
  from: "Sametable <feedback@sametable.app>",
  to: email,
  subject: `Hello`,
  template: "invite_project", // the template's name you gave when you created it in mailgun
  "v:invite_link": inviteLink,
  "v:assigner_name": fullname,
  "v:project_title": title,
};

mailer.send(data);
```

Notice that, to associate a dynamic value with a placeholder name in a template: `"v:project_title" : 'Project Mario'`.

## Tenancy

When an organization, say, Acme Inc., signs up on your SaaS, it's considered a 'tenant'- They 'occupy' a space on your service.

While I'd heard of the 'multi-tenancy' term being associated with a SaaS before, I never had the slightest idea about implementing it. I always thought that it'd involve some cryptic computer-sciency maneuvering that I couldn't possibly have figured it all out by myself.

Fortunately, there is an easy way to do 'multi-tenancy':

> Single database; all clients share the same tables; each client has a `tenant_id`; queries the database as per an API request by `WHERE tenant_id = $ID`.

So don't worry: If you know basic SQL, you should have a clear picture on the steps required to implement this.

Here are three instrumental resources about 'multi-tenancy' I have bookmarked:

- https://stackoverflow.com/a/47783180/73323
- https://stackoverflow.com/a/44530588/73323
- https://blog.checklyhq.com/building-a-multi-tenant-saas-data-model/

## Domain name

Sametable.app domain and all its DNS records are hosted in [**NameCheap**](https://www.namecheap.com/). I was on [hover](https://www.hover.com/) before(it still hosts my personal website's domain). But I hit a limitation there when I tried to enter my Mailgun's DKIM value. Namecheap also has more competitive prices in my experience.

At which stage in your SaaS development should you get a domain name? Well, I would say not until when the lack of a DNS registrar is blocking your development. In my case, I deferred it until I had to integrate Mailgun which requires creating DNS records in a domain.

## Deployment

Ugh. This was a stage where I struggled for the longest time :persevere:. It was one hell of a journey where I found myself doubling down on a cloud platform but end up bailing out as I realized their downsides while optimizing for developer experience, costs, quota, and performance(latency).

The journey started with me jumping head-first(bad idea) into Digital Ocean, since I saw it recommended a lot in the IndieHackers forum. And sure enough, I managed to get my Nodejs up and running in a VM by following [closely](https://coderrocketfuel.com/article/create-and-deploy-an-express-rest-api-to-a-digitalocean-server#configure-and-deploy-your-node-js-app) the [tutorials](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-18-04). Then I found out that the [DO Space](https://www.digitalocean.com/products/spaces/) wasn't exactly AWS S3-It [can't](https://ideas.digitalocean.com/ideas/DO-I-318) host my SPA. Although I [could have](https://coderrocketfuel.com/article/deploy-a-create-react-app-website-to-digitalocean) hosted it in my droplet and [hook up](https://www.youtube.com/watch?v=2X_Tp_G7aTs) a third-party CDN like CloudFlare to the droplet, I wanted something more seamless and well-trodden setup like the S3+Cloudfront. I was also using a DO's Managed Database(Postgresql) because I didn't want to manage my DB and tweak in the `*.config` files myself. That costs a fixed \$15/month.

Then I learnt about [AWS Lightsail](https://aws.amazon.com/lightsail/) which is a mirror image of DO, but, to my surprise, with more competitive [quota](https://aws.amazon.com/lightsail/pricing/) at a given price point:

#### VM at \$5/month

| AWS Lightsail      | Digital Ocean    |
| ------------------ | ---------------- |
| 1 GB Memory        | 1 GB Memory      |
| 1 Core Processor   | 1 Core Processor |
| **40 GB** SSD Disk | 25 GB SSD Disk   |
| **2 TB** transfer  | 1 TB transfer    |

#### Managed database at \$15/month

| AWS Lightsail      | Digital Ocean    |
| ------------------ | ---------------- |
| 1 GB Memory        | 1 GB Memory      |
| 1 Core Processor   | 1 Core Processor |
| **40 GB** SSD Disk | 10 GB SSD Disk   |

This was when I started betting on Lightsail instead. But, the \$15/month for a managed database in Lightsail got to me at one point. I didn't want to have to pay that money when I wasn't even sure that I would ever have any paying customers.

At this point, I supposed that I had to get my hands dirty to optimize for the cost factor. So I started looking into wiring AWS EC2, RDS, etc. But it was just too many of AWS-specific things I had to pick up, and the AWS doc wasn't exactly helping either-It's just one rabbit hole after another to do one thing; I just needed something to host my SPA and Nodejs for goodness sake!

Then I checked back in IndieHacker for a sanity check, and came across [render.com](https://render.com/). It seemed perfect! It's one of those tools that are on a mission 'so you can focus on building your app'. The tutorials were short and got you up and running in no time. But, it was [expensive](https://render.com/pricing):

#### Comparison of Lightsail and Render at their lowest price point

| AWS Lightsail(\$3.50/mo) | Render(\$7/mo)                               |
| ------------------------ | -------------------------------------------- |
| 512 GB Memory            | 512 MB Memory                                |
| 1 Core Processor         | Shared Processor                             |
| 20 GB SSD Disk           | $0.25/GB/mo SSD Disk(20GB = $5/mo)           |
| 1 TB transfer            | 100 GB/mo. $0.10/GB above that(1TB = $90/mo) |

And that's just for hosting my Nodejs!

So what now?! Do I just say f\*\*\* it and do whatever it takes to 'ship it'?

But I held my ground. I revisit AWS again. I still believed AWS was the answer because everyone else is singing its song. I must be missing something. I considered their higher level tools like AWS AppSync and Amplify. But I couldn't overlook the fact that both of them force me to completely work by their standards. So at this point, I'd had it with AWS, and turned to another...platform: **Google Cloud Platform(GCP)**.

**Sametable's Nodejs, Redis, and Postgresql are hosted on GCP**. The thing that drew me to GCP was its documentation-It's much more linear; code snippets for Nodejs; step-by-step guides about the common things you would do for a web app. Plus, it's serverless! Which means your cost is proportional to your usage.

### NodeJS on GCP

The GAE ['standard environment'](https://cloud.google.com/appengine/docs/the-appengine-environments) hosts my Nodejs.

#### Cost

GAE's stardard environment has [free quota](https://cloud.google.com/free/docs/gcp-free-tier#always-free-usage-limits) unlike the 'flexible environment'. Beyond that, you will pay only if somebody is using your SaaS :blush:.

#### Guide

This was the _only_ guide I relied on. It was my north star. It covers Nodejs, Postgresql, Redis, file storage, and more:

> https://cloud.google.com/appengine/docs/standard/nodejs

Start with the ['Quick Start'](https://cloud.google.com/appengine/docs/standard/nodejs/quickstart) tutorial because it will set you up with the `gcloud cli` which you are going to need when following the rest of the guides, where you will find commands you can run to follow along. If you aren't comfortable with CLI environment, the guides will provide alternative steps to achieve the same thing on the GCP dashboard too. I love it.

I noticed that while going through GCP doc, I never had to open more than 4 tabs in my browser. It's the complete opposite with AWS doc- My browser would be packed with it.

#### CORS

To stop your browser from complaining about CORS issues, it's [all about](https://medium.com/@kilgarenone/deploy-your-nodejs-app-to-digital-ocean-1de40797666f#4aa4) getting your backend to send those `Access-Control-Allow-*` headers back per request. (Apologies for oversimplification is in order)

But, correct me if I'm wrong, there's [no way](https://stackoverflow.com/a/60502433/73323) to configure CORS in GAE itself. So I had to do it with the [cors](https://www.npmjs.com/package/cors) npm package:

```js
const express = require("express");
const app = express();
const cors = require("cors");

const ALLOWED_ORIGINS = [
  "http://localhost:8008",
  "https://web.sametable.app", // your SPA's domain
];

app.use(
  cors({
    credentials: true, // include Access-Control-Allow-Credentials: true. remember set xhr.withCredentials = true;
    origin(origin, callback) {
      // allow requests with no origin
      // (like mobile apps or curl requests)
      if (!origin) return callback(null, true);
      if (ALLOWED_ORIGINS.indexOf(origin) === -1) {
        const msg =
          "The CORS policy for this site does not " +
          "allow access from the specified Origin.";
        return callback(new Error(msg), false);
      }
      return callback(null, true);
    },
  })
);
```

### Postgresql on GCP

#### Guide

https://cloud.google.com/sql/docs/postgres/connect-app-engine-standard

#### Cost

It's pay-as-you-use as opposed to the fixed \$15/mo in Lightsail and DO.

https://cloud.google.com/products/calculator/#id=dd6b78da-1215-4366-b7b4-afefe5472ee6

### Redis on GCP

If you were following the main guide about Nodejs, you can't miss [this guide](https://cloud.google.com/appengine/docs/standard/nodejs/using-memorystore) to setting up your Redis in MemoryStore. But I figured it would be more cost effective to **host my Redis in a Google Compute Engine**(GCE) which has, unlike MemoryStore, free quota. ([See this](https://github.com/ripienaar/free-for-dev#major-cloud-providers) for comparison of free quota across different cloud platforms)

#### Guide

1. Setup Redis in a VM:
   https://cloud.google.com/community/tutorials/setting-up-redis

2. Setup VPC:

   > Serverless VPC Access enables you to connect from your App Engine app directly to your VPC network, **allowing access to Compute Engine VM instances**, Memorystore instances, and any other resources with an internal IP address.

   https://cloud.google.com/appengine/docs/standard/python/connecting-vpc

3. In your `app.yaml` file:

   ```yaml
   vpc_access_connector:
     name: "<YOURS_HERE>"

   env_variables:
     REDIS_PASSWORD: "<PASSWORD_YOU_SET_IN_A_GUIDE_ABOVE>"
     REDISHOST: "<INTERNAL_IP_OF_YOUR_VM>"
     REDISPORT: "6379" # default port when install redis
   ```

   <figure>
    <img src="https://i.imgur.com/N4bqhcT.png" alt="internal ip of a GCE vm" loading="lazy" />
    <figcaption>
        <small>Internal IP of a GCE</small>
    </figcaption>
   </figure>

4. Finally, in `lib/redis.js`:

   ```js
   const redis = require("redis");

   const redisClient = redis.createClient(
     NODE_ENV === "production"
       ? {
           host: process.env.REDISHOST,
           port: process.env.REDISPORT, // default to 6379 if wasn't set
           no_ready_check: true,
           auth_pass: process.env.REDIS_PASSWORD,
         }
       : {} // just use the default: localhost and ports
   );

   module.exports = {
     redisClient,
   };
   ```

### Storing files

[Cloud Storage](https://cloud.google.com/storage/docs) is what you need for your users to upload their files such as images which they will need to retrieve and display later.

#### Cost

There is a [free tier](https://cloud.google.com/free/docs/gcp-free-tier#always-free-usage-limits) for Cloud Storage too.

#### Guide

You will be fine:
https://cloud.google.com/appengine/docs/standard/nodejs/using-cloud-storage

## Hosting your SPA

When I was still on Lightsail, my SPA was [hosted](https://medium.com/@kilgarenone/deploy-spa-to-aws-9302796acd88) on S3+Cloudfront because I assumed it's better to keep them under the same platform for better latency. Then I found GCP. As a beat refugee from AWS landing in GCP, I first explored the 'Cloud Storage' to host my SPA, and turns out it wasn't ideal for SPA. It requires a lot of works too. So you can skip that.

Then I tried hosting my SPA in [**Firebase**](https://firebase.google.com/docs/hosting/quickstart), and I was happily ever after.

Another option you can consider is [Netlify](https://netlify.com) which is super easy to get started too.

## Payment & Subscription

A SaaS usually allows users to pay and subscribe to access the paid features you have designated.

To enable that possibility in Sametable, I use **Stripe** to handle both the payment and subscription flows.

### Guide

There are two ways to implement them:

1. [Very hands-on](https://stripe.com/docs/billing/subscriptions/fixed-price) that's great for customization in UI.
2. [**Checkout**](https://stripe.com/docs/payments/checkout/set-up-a-subscription). Fastest to implement. This was what I went for.

#### Webhook

The last key component I needed was a 'webhook' which is just a typical endpoint from your Nodejs that can be called by third-party such as Stripe.

In my case, I created a webhook that will be called when a payment has been charged successfully to signify in the user record that corresponds to the payee as a PRO user in Sametable from there onwards:

```javascript
router.post(
  "/webhook/payment_success",
  bodyParser.raw({ type: "application/json" }),
  asyncHandler(async (req, res, next) => {
    const sig = req.headers["stripe-signature"];

    let event;

    try {
      event = stripe.webhooks.constructEvent(req.body, sig, webhookSecret);
    } catch (err) {
      return res.status(400).send(`Webhook Error: ${err.message}`);
    }

    // Handle the checkout.session.completed event
    if (event.type === "checkout.session.completed") {
      // 'session' doc: https://stripe.com/docs/api/checkout/sessions/object
      const session = event.data.object;

      // here you can query your database to, for example,
      // update a particular user/tenant's record

      // Return a res to acknowledge receipt of the event
      res.json({ received: true });
    } else {
      res.status(400);
    }
  })
);
```

##### Reference

Here is a code snippet of a webhook:
https://stripe.com/docs/webhooks/signatures#verify-official-libraries

##### Guide

https://stripe.com/docs/webhooks

## Landing page

### Building

I use [**Eleventy**](https://www.11ty.dev/) to build the landing page of Sametable. I [wouldn't](https://twitter.com/devongovett/status/1222953655722110981) recommend Gatsby or Nextjs. They are an overkill for this job.

I started off with one of the [starter projects](https://www.11ty.dev/docs/starter/) as I was impatient to get my page off the ground. But I struggled working in them. Although Eleventy claims to be a simple SSG, there are actually quite a few concepts to grasp. Coupled with the tools introduced by the starter kits, things can get complex. So I decided to start from zero and take my time reading the doc from start to finish, slowly building up. And also write my blog posts with Markdown. Quiet and easy. :pray:

#### Guides

- **Long version**
  - https://tatianamac.com/posts/beginner-eleventy-tutorial-parti/
  - https://www.11ty.dev/docs/
- **Short version**: https://github.com/kilgarenone/personal-website (the first website I built for my personal site while learning 11ty. It has a homepage and blog posts. Very few concepts introduced here. You could start with this 'starter project')

### Hosting

I use [**Netlify**](https://www.netlify.com/) to host the landing page. There are also [surge.sh](https://surge.sh/) and [Vercel](https://vercel.com).

## Terms and Conditions

T&C makes your SaaS legit. As far as I know, here are your options to come up with it:

1. Write your own https://pinboard.in/tos/ .
2. Copy and paste others'. Change accordingly.
3. Lawyer up.
4. Generate them https://getterms.io/ .

## Marketing

There is no shortage of marketing posts saying "_Let the product speaks for itself_" was a bad idea. Well, in my view- Not if you are trying to 'hack growth'.

The following is the trajectory of existence I have in mind for Sametable:

1. Build something that purportedly solves a problem.
2. Do your SEO. Write the blog posts. Anyone who has the problem that you solve for will search for it or know about it by word of mouth.
3. If it still didn't take off, well, chances are you weren't solving a huge real problem, or enough people have solved it. In that case, be grateful for whatever success that comes to you over the long haul. Or, you know, just move on.

### Resources

- https://stripe.com/en-my/atlas/guides/starting-sales
- https://github.com/LisaDziuba/Marketing-for-Engineers
- https://www.coryzue.com/writing/seo-for-developers/

## Well-being

It's easy to sit and get lost in our contemporary works. And we do that by accumulating debts from the future. One of the debts, in this case, is our personal **health**.

Here is how I try to stay out of health debt:

- **Install** [**Workrave**](https://workrave.org/)
  You can set it to lock your screen after an interval has passed. Most importantly, it can show some exercises that you can perform behind your computer!
- Get an adjustable **standing desk** if you can afford it. I got mine from IKEA.
- Do [burpees](https://www.youtube.com/watch?v=Kjhl-8yU6hI). Stretch those joints. Maintain good posture. Planking helps.
- Meditate to stay sane. I'm using https://meditofoundation.org/