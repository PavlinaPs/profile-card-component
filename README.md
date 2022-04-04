# Frontend Mentor - Profile card component solution

This is a solution to the [Profile card component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/profile-card-component-cfArpWshJ). Frontend Mentor challenges help you improve your coding skills by building realistic projects. 

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

- Build out the project to the designs provided

### Screenshot

| Desktop layout |
|:--:|
![Desktop layout](./screenshots/screenshot-desktop.jpg)

| Mobile layout |
|:--:|
![Mobile layout](./screenshots/screenshot-mobile.jpg)

- Solution URL: https://github.com/PavlinaPs/profile-card-component
- Live Site URL: https://pavlinaps.github.io/profile-card-component/

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- Pseudo-elements
- Mobile-first workflow

### What I learned

I really learned a lot solving this challenge. This is going to be a long README. 
There were two issues I had to adress:

**1. The profile image didn't fit exactly in its border:**
![](./screenshots/border-gap.jpg)

I thought I did something wrong. After I researched it I think I I did the border correctly and solved this issue by adding white background to its parent \<div>. 

```css
.card__profile-image {
    ..
    background-color: var(--clr-white);
}
```
Here is the link to Stack Overflow on this issue [Gap between border and image when border radius is added](https://stackoverflow.com/questions/23490320/gap-between-border-and-image-when-border-radius-is-added). I am a little bit surprised that a 7 year old article is still needed.

**2. The background bubbles troubles:**
The issue was to make the bubble illustrations stay in the same place behind the card when the window changes size or zoom. I keep each attempt as a git branch for reference.
I tried:
- Adding bubble illustrations to the body as *multiple backgrounds*. I learned a lot here. I didn't know there is such a feature. I explored it thouroughly.
Link to MDN: [Using multiple backgrounds](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Backgrounds_and_Borders/Using_multiple_backgrounds/).
The background did not behave as intended though.
```css
   body {
    ...
    background-color: var(--clr-dark-cyan);
    background-image: 
        url(./images/bg-pattern-top.svg), 
        url(./images/bg-pattern-bottom.svg);
    background-size: cover, cover;
    background-position:
        -21.4rem -22.6rem,
        14.3rem 20.5rem;
    background-attachment: fixed, fixed;
    background-repeat: no-repeat, no-repeat;
    }
```
- to *position* the bubble illustrations \<img>s wrapped in a \<div> *absolutly* to the \<body> element.
The background also did not behave as intended.
```html
    <body>
        <div class="card__bacground-bubbles">
            <img class="card__background-bubble__top" src="./images/bg-pattern-top.svg" alt="">
            <img class="card__background-bubble__bottom" src="./images/bg-pattern-bottom.svg" alt="">
        </div>
        ..
    </body>
```
```css
    .card__bacground-bubbles {
        position: absolute;
    }

    .card__background-bubble__top {
        position: relative;
        top: -3.5em;
        left: -15.5em;
    }

    .card__background-bubble__bottom {
        position: relative;
        top: 1.3em;
        left: 15.2em;
    }
```

- *Position fixed* also didn't work as intended.

- Then I realized that if I want the background scaled with the card and not change position, it needs to be *positioned absolutely to the card*, not to the body. I decided to learn how to use pseudo-elements ::before & ::after and used it.
Kevin Powell's 3-part tutorial was a great help, as always: [Before and After pseudo elements explained - part one: how they work](https://youtu.be/zGiirUiWslI)
Background scales with card and stays in place on a big screen. but on mobile screens there is a big vertical overflow and the card is not centered. I haven't figured why.

```css
.card::before {
    content: url(./images/bg-pattern-top.svg);
    display: block;
    position: absolute;
    z-index: -5;
    bottom: 9em;
    right: 6.2em;
}

.card::after {
    content: url(./images/bg-pattern-bottom.svg);
    display: block;
    position: absolute;
    z-index: -10;
    top: 9.7em;
    left: 4em;
}
```

### Continued development

I need to code a lot to get more experience and solve challenges faster.

### Useful resources

This time I added the links in the text of [What I learned](#what-i-learned), respectively to the topic.


## Author

- GitHub - [PavlinaPs](https://github.com/PavlinaPs)
- Frontend Mentor - [@PavlinaPs](https://www.frontendmentor.io/profile/PavlinaPs)

## Acknowledgments

It is great that I can solve Frontend Mentor's challenges. They are all very useful for me. As are Kevin Powell's tutorials.Thank you!