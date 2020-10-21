---
title: COMPARING STYLING METHODS IN 2020 (BY CHRIS COYIER)
description: Over on Smashing, Adebiyi Adedotun Lukman covers all these styling methods. It’s in the context of Next.js, which is somewhat important as Next.js has some specific ways you work with these tools, is React and, thus, is a components-based architecture. But the styling methods talked about transcend Next.js, and can apply broadly to lots of websites.
date: 2020-09-10
layout: 'layouts/post.html'
---

![afbeeldingpost1](/img/cssstyle.jpg)

Over on Smashing, Adebiyi Adedotun Lukman covers all these styling methods. It’s in the context of Next.js, which is somewhat important as Next.js has some specific ways you work with these tools, is React and, thus, is a components-based architecture. But the styling methods talked about transcend Next.js, and can apply broadly to lots of websites.

Here are my hot takes on the whole table-of-contents of styling possibilities these days.


- Regular CSS. If you can, do. No build tooling is refreshing. It will age well. The only thing I really miss without any other tooling is nesting media queries within selector blocks.

- Sass. Sass has been around the block and is still a hugely popular CSS preprocessor. Sass is built into tons of other tools, so choosing Sass doesn’t always mean the same thing. A simple Sass integration might be as easy as a sass --watch src/style.scss dist/style.css npm script. Then, once you’ve come to terms with the fact that you have a build process, you can start concatenating files, minifying, busting cache, and all this stuff that you’re probably going to end up doing somehow anyway.

- Less & Stylus. I’m surprised they aren’t more popular since they’ve always been Node and work great with the proliferation of Node-powered build processes. Not to mention they are nice feature-rich preprocessors. I have nothing against either, but Sass is more ubiquitous, more actively developed, and canonical Sass now works fine in Node-land.

- PostCSS. I’m not compelled by PostCSS because I don’t love having to cobble together the processing features that I want. That also has the bad side effect of making the process of writing CSS different across projects. Plus, I don’t like the idea of preprocessing away modern features, some of which can’t really be preprocessed (e.g. custom properties cannot be preprocessed). But I did love Autoprefixer when we really needed that, which is built on PostCSS.

- CSS Modules. (Built on PostCSS). If you’re working with components in any technology, CSS modules give you the ability to scope CSS to that component, which is an incredibly great idea. I like this approach wherever I can get it. Your module CSS can be Sass too, so we can get the best of both worlds there.

- CSS-in-JS. Let’s be real, this means “CSS-in-React.” If you’re writing Vue, you’re writing styles the way Vue helps you do it. Same with Svelte. Same with Angular. React is the un-opinionated one, leaving you to choose between things like styled-components, styled-jsx, Emotion… there are a lot of them. I have projects in React and I just use Sass+CSS Modules and think that’s good but a lot of people like CSS-in-JS approaches too. I get it. You get the scoping automatically and can do fancy stuff like incorporate props into styling decisions. Could be awesome for a design system.

- All-in on utility styles: Big advantages: small CSS files, consistent yet flexible styles. Big disadvantage: you’ve got a zillion classes all commingled in your markup, making it cumbersome to read and refactor. I’m not compelled by it, but I get it, those advantages really hit for some folks.
