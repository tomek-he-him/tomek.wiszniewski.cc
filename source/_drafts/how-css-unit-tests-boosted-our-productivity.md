---
title: How CSS unit tests boosted our productivity
author: Tomek Wiszniewski
author_url: https://github.com/tomekwi
cover: /img/machinery
---

The way you manage styles can make or break a long-running web project. Keeping things modular helps a great deal, but that’s only part of the solution.

Six months ago we had a go at setting up CSS unit tests for our components. Brilliant decision, as it turns out! Since then, our job is a lot nicer. The speed of development is fast and steady. Each of us on the team is now coding with confidence, without the fear that things might unexpectedly break.

And here’s how we did it:

<!-- more -->

## A step back

Before we see solution, let’s take a broader look at the problem itself. CSS was originally designed to power simple websites – and it’s a wonderful tool for that. It’s amazing how quickly you can get up and running creating beautiful UI nuggets, which work across all platforms and devices. Just a few lines of CSS make a pretty decent-looking button:

<iframe src="https://jsfiddle.net/27eb7a01/embedded/css,html,result" style="border: none; width: 100%; height: 13em"></iframe>

But since CSS appeared in 1996, the web has changed beyond recognition. We’re now delivering full-blown apps with beautiful, immersive user experiences. Like never before, we’re living the “write once, run anywhere” dream. Web apps [run without installation][step-back.A1] on any device and adapt to the size of the screen, network availability, user permissions, pointing device, viewing mode, browser support and other factors.

{% pullquote %}
A modern web frontend  
has zillions of moving parts
{% endpullquote %}

The price for all this awesomeness is complexity. Countless moving parts which we have to wire up and keep synchronized. And let’s face it – despite web standards moving forward at breakneck speed today, the building blocks that power our apps are still good old HTML, CSS and JavaScript. Technologies designed for simple websites in the mid-nineties.

Let’s focus on CSS. We all know the [problems with CSS at scale][step-back.B1]. We know the feeling when you discover a visual bug caused by that line of CSS changed weeks ago at the other end of your app. We know how much harder it gets with every new member on the team.

<p class="text-center"><figure><img class="img-responsive"
  src="/post-images/simpsons-jenga.gif"
  alt="CSS at scale is like Bart Simpson playing Jenga"
  style="width: 100%"
/><figcaption>Source: giphy.com</figcaption></figure></p>

Brilliant folks keep coming up with [loads][step-back.B2] [of][step-back.B3] [brilliant][step-back.B4] [solutions][step-back.B5] to many of these problems. We are learning to [write our styles in a modular way][step-back.B6]. We don’t need to worry about the global namespace anymore. But that’s just part of the solution. Just as the arrival of modules to JavaScript didn’t magically make our apps well-organized and bug-free, modular CSS isn’t a cure for everything.

[step-back.A1]: /good-quotes/#/web-best-app-delivery-platform "The web as an app delivery platform"

[step-back.B1]: https://speakerdeck.com/vjeux/react-css-in-js?slide=2 "CSS in JS — by Christopher Chedeau"
[step-back.B2]: https://github.com/jsstyles/jss "jsstyles/jss"
[step-back.B3]: https://github.com/krasimir/cssx "krasimir/cssx"
[step-back.B4]: https://github.com/css-modules/css-modules "css-modules/css-modules"
[step-back.B5]: https://github.com/rtfeldman/elm-css "rtfeldman/elm-css"
[step-back.B6]: http://chrispearce.co/elephants-the-three-code-ilities-two-months-with-css-modules/ "Elephants, The Three Code Ilities, & Two Months With CSS Modules — by Chris Pearce"




## Moving fast

The key to moving fast is to embrace change – or even [drive change][moving-fast.A]. Move forward with confidence, without looking back.

[moving-fast.A]: https://vimeo.com/91537336 "Bringing Change to Life — by Bill Scott"

{% blockquote Eric Elliott https://medium.com/javascript-scene/how-to-build-a-high-velocity-development-team-4b2360d34021 How to build a high-velocity development team %}
Eradicate your team’s fear of change.  
This should be **priority number one** until nobody  
worries about changing a line of code again.
{% endblockquote %}

Facebook [used to say “move fast and break things”][moving-fast.C] – but a couple of years ago they announced in a famous keynote: “Breaking things wasn’t helping us to move faster, because we had to slow down to fix these bugs and it wasn't improving our speed”. Following this conclusion, they changed their motto to “move fast with stable infra”.

[moving-fast.C]: http://mashable.com/2014/04/30/facebooks-new-mantra-move-fast-with-stability/#BryYX_gAQsqq "Facebook Changes Its ‘Move Fast and Break Things’ Motto — at Mashable"

<p class="text-center"><figure><img class="img-responsive"
  src="/post-images/move-fast-with-stable-infra.jpg"
  alt="Mark Zuckerberg saying “move fast with stable infra”"
/><figcaption>Source: facebook</figcaption></figure></p>

But what exactly does it mean to “not look back”? What exactly does “stable infra” mean? How to make sure nobody worries about changing code? Eric Elliott gives us another hint in his [series of][moving-fast.B2] [thought-provoking articles][moving-fast.B1]:

[moving-fast.B1]: https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d "5 Questions Every Unit Test Must Answer"
[moving-fast.B2]: https://medium.com/javascript-scene/how-to-build-a-high-velocity-development-team-4b2360d34021 "How to build a high-velocity development team"

{% blockquote Eric Elliott https://medium.com/javascript-scene/how-to-build-a-high-velocity-development-team-4b2360d34021 How to build a high-velocity development team %}
**Write automated tests**  
for every feature  
and every bug fix.
{% endblockquote %}

We definitely found this to be true with libraries doing business logic.

Heavy refactoring. Taking new people on the team. A major rebase. Swapping out a dependency. Getting rid of dead code. Resurrecting code months after the last commit. Handing projects over. These things happen day to day in an environment of constant change. Without unit tests, you might be facing days, weeks or even months of tedious work. But when a good suite of unit tests has your back, each of these is a breeze.

But what about CSS? Is it possible to keep a similar pace of development there?




## Our story



<!-- TRASH

From a network of articles it’s growing into an app delivery platform.

Hold on… doesn’t that sound familiar?

Most of us remember the day modular JS arrived to town ([RequireJS](http://requirejs.org/), then [browserify](http://browserify.org/), [webpack](http://webpack.github.io/), [rollup](http://rollupjs.org/) – all while we’re waiting for native ECMAscript modules). This helped a great deal


If you’ve worked on a project bigger than a simple website (which CSS was originally designed for), you probably know much better

(A bit better)

Writing any non-trivial web app, you’re bound to face the question “How do I manage styles in a sustainable way”. The bigger your team and the more sophisticated the app, the more relevant the question gets.

(Still bad – maybe useful for the body)

 The same shift happened to JS a few years back.

(Very bad)

We all remember how easy it was to get started with CSS on that first small pet project. But with anything larger than a pet landing page stylesheets get notoriously difficult to write and manage. Writing a full-blown progressive web app, you’ll definitely face the problem …
-->