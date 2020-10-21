---
title: HOW TO RECREATE THE RIPPLE EFFECT OF MATERIAL DESIGN BUTTONS (BY BRET CAMERON)
description: When I first discovered Material Design, I was particularly inspired by its button component
layout: 'layouts/post.html'
---

When I first discovered Material Design, I was particularly inspired by its button component. It uses a ripple effect to give users feedback in a simple, elegant way.

How does this effect work? Material Design’s buttons don’t just sport a neat ripple animation, but the animation also changes position depending on where each button is clicked.

We can achieve the same result. We’ll start with a concise solution using ES6+ JavaScript, before looking at a few alternative approaches.

HTML
Our goal is to avoid any extraneous HTML markup. So we’ll go with the bare minimum:

<button>Find out more</button>

Styling the button
We’ll need to style a few elements of our ripple dynamically, using JavaScript. But everything else can be done in CSS. For our buttons, it’s only necessary to include two properties.

button {
  position: relative;
  overflow: hidden;
}

Using position: relative allows us to use position: absolute on our ripple element, which we need to control its position. Meanwhile, overflow: hidden prevents the ripple from exceeding the button’s edges. Everything else is optional. But right now, our button is looking a bit old school. Here’s a more modern starting point:

/* Roboto is Material's default font */
import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

button {
  position: relative;
  overflow: hidden;
  transition: background 400ms;
  color: #fff;
  background-color: #6200ee;
  padding: 1rem 2rem;
  font-family: 'Roboto', sans-serif;
  font-size: 1.5rem;
  outline: 0;
  border: 0;
  border-radius: 0.25rem;
  box-shadow: 0 0 0.5rem rgba(0, 0, 0, 0.3);
  cursor: pointer;
}

Styling the ripples
Later on, we’ll be using JavaScript to inject ripples into our HTML as spans with a .ripple class. But before turning to JavaScript, let’s define a style for those ripples in CSS so we have them at the ready:

span.ripple {
  position: absolute; /* The absolute position we mentioned earlier */
  border-radius: 50%;
  transform: scale(0);
  animation: ripple 600ms linear;
  background-color: rgba(255, 255, 255, 0.7);
}

To make our ripples circular, we’ve set the border-radius to 50%. And to ensure each ripple emerges from nothing, we’ve set the default scale to 0. Right now, we won’t be able to see anything because we don’t yet have a value for the top, left, width, or height properties; we’ll soon be injecting these properties with JavaScript.

As for our CSS, the last thing we need to add is an end state for the animation:

@keyframes ripple {
  to {
    transform: scale(4);
    opacity: 0;
  }
}

Notice that we’re not defining a starting state with the from keyword in the keyframes? We can omit from and CSS will construct the missing values based on those that apply to the animated element. This occurs if the relevant values are stated explicitly — as in transform: scale(0) — or if they’re the default, like opacity: 1.

Now for the JavaScript
Finally, we need JavaScript to dynamically set the position and size of our ripples. The size should be based on the size of the button, while the position should be based on both the position of the button and of the cursor.

We’ll start with an empty function that takes a click event as its argument:

function createRipple(event) {
  //
}

We’ll access our button by finding the currentTarget of the event.

const button = event.currentTarget;
Next, we’ll instantiate our span element, and calculate its diameter and radius based on the width and height of the button.

const circle = document.createElement("span");
const diameter = Math.max(button.clientWidth, button.clientHeight);
const radius = diameter / 2;
We can now define the remaining properties we need for our ripples: the left, top, width and height.

circle.style.width = circle.style.height = `${diameter}px`;
circle.style.left = `${event.clientX - (button.offsetLeft + radius)}px`;
circle.style.top = `${event.clientY - (button.offsetTop + radius)}px`;
circle.classList.add("ripple");
Before adding our span element to the DOM, it’s good practice to check for any existing ripples that might be leftover from previous clicks, and remove them before executing the next one.

const ripple = button.getElementsByClassName("ripple")[0];

if (ripple) {
  ripple.remove();
}

As a final step, we append the span as a child to the button element so it is injected inside the button.

button.appendChild(circle);
With our function complete, all that’s left is to call it. This could be done in a number of ways. If we want to add the ripple to every button on our page, we can use something like this:

const buttons = document.getElementsByTagName("button");
for (const button of buttons) {
  button.addEventListener("click", createRipple);
}

We now have a working ripple effect!

Taking it further
What if we want to go further and combine this effect with other changes to our button’s position or size? The ability to customize is, after all, one of the main advantages we have by choosing to recreate the effect ourselves. To test how easy it is to extend our function, I decided to add a “magnet” effect, which causes our button to move towards our cursor when the cursor’s within a certain area.

We need to rely on some of the same variables defined in the ripple function. Rather than repeating code unnecessarily, we should store them somewhere they’re accessible to both methods. But we should also keep the shared variables scoped to each individual button. One way to achieve this is by using classes, as in the example below:

Since the magnet effect needs to keep track of the cursor every time it moves, we no longer need to calculate the cursor position to create a ripple. Instead, we can rely on cursorX and cursorY.

Two important new variables are magneticPullX and magneticPullY. They control how strongly our magnet method pulls the button after the cursor. So, when we define the center of our ripple, we need to adjust for both the position of the new button (x and y) and the magnetic pull.

const offsetLeft = this.left + this.x * this.magneticPullX;
const offsetTop = this.top + this.y * this.magneticPullY;
To apply these combined effects to all our buttons, we need to instantiate a new instance of the class for each one:

const buttons = document.getElementsByTagName("button");
for (const button of buttons) {
  new Button(button);
}

Other techniques
Of course, this is only one way to achieve a ripple effect. On CodePen, there are lots of examples that show different implementations. Below are some of my favourites.
