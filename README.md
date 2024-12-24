# Frontend Mentor - Bento grid solution

This is a solution to the [Bento grid challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/bento-grid-RMydElrlOj). Frontend Mentor challenges help you improve your coding skills by building realistic projects. 

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


## Overview

### The challenge

Users should be able to:

- View the optimal layout for the interface depending on their device's screen size

### Screenshot

![](./assets/Screenshot%20of%20website.png)

### Links

- Solution URL: [Solution URL](https://www.frontendmentor.io/solutions/responsive-layout-using-css-grid-and-flexbox-zLrHRy5edQ)
- Live Site URL: [Live site URL](https://bentogridfrontend.netlify.app/)

## My process
  - I followed the mobile-first approach for this project: 
    Started coding considering a width of 375px and then modified the layout as the screen grew wider. When things started to get out of hand, I had to start from scratch following a different approach.

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- CSS Grid
- Mobile-first workflow

### What I learned

MOBILE-FIRST APPROACH:
Screen Width: 375px:
1- In order to include a variable font, I defined it in my styles.css file:
  ```css
  @font-face {
    font-family: 'DMSansItalic';
    src: url('assets/fonts/DMSans-VariableFont_opsz,wght.ttf') format('truetype');
    font-weight: 400 500;
    font-style: italic;
  }
  body {
    font-family: 'DMSansItalic', sans-serif;
    font-weight: 453;
  }
  ```
  ==> I learned a few differences between variable fonts and regular fonts:
        - A variable font is a single file that includes all variations of a font (e.g., weights, widths, slants). 
        - When using regular fonts (found in static folder), you're required to have separate files for each style or weight (e.g., regular.ttf, bold.ttf). 
        - A variable font supports fine-tuning of font styles, like adjusting weight from 100 to 900 dynamically.
        - A regular font is limited to predefined styles (e.g., bold or italic).
        - A variable font reduces the number of HTTP requests because only one font file is used.
        - Multiple font files increase HTTP requests and load time.

2- I faced some difficulties when trying to properly center some text and make it span two lines:
``` html
    <div class="platforms">
      <img src="assets/images/illustration-multiple-platforms.webp" 
          alt="an illustration of two accounts.">
      <div class="manage-accounts">
        <p>Manage multiple accounts and platforms.</p>
      </div>
    </div>
```
    - My approach consisted of wrapping the text in a div container on which I applied the following styles:
```css
    .platforms .manage-accounts {
    display: flex;
    justify-content: center;
    align-items: center;  
    width: 90%;
    }
    .platforms .manage-accounts p {
    word-wrap: break-word;
    font-size: large;
    color: var(--black);
    font-weight: 600;
    }
```
    - I know there's probably multiple other approaches that are far better than mine.

3- I tried to position the image of the third container (schedule) slightly below its container's bottom edge: 
    - I applied the following styling on "schedule":
```css
    .schedule {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: 15px;
      margin: 15px;
      padding: 15px;
      background-color: var(--yellow-500);
      border-radius: 5%;
      position: relative;
      overflow: hidden;
      height: 240px;
    }
    .schedule img {
    max-width: 70%;
    position: absolute;
    bottom: -12%;
    }
```
  - I applied `position: relative;` to the container to make it the reference for absolutely positioned child elements.
  - `overflow: hidden;` to hide any part of the image that's outside the container.
  - `position: absolute;` to position the image relative to its container (.schedule).

**UPDATED SCHEDULE STYLES**

- I modifiedd the styles of the schedule container to make it responsive, because the styles prior to these were not as responsive as I wanted. I ended up using a grid layout instead of flexbox.

```css
  .schedule {
    display: grid;
    grid-template-rows: auto 1fr;
    margin: 15px;
    padding: 20px;
    background-color: var(--yellow-500);
    border-radius: 5%;
    height: 240px;
    overflow: hidden;
  }
  .schedule h2 {
    width: 80%;
    font-size: x-large;
    color: var(--black);
    font-weight: 600;
  }

  .schedule img {
    width: 70%;
    justify-self: start;
    align-self: end;
    margin-bottom: -12%;
    max-width: 300px;
  }
```
- I added a grid layout to the container, with the image in the second row and the text in the first row.
- I used `justify-self: start;` and `align-self: end;` to position the image in the bottom left corner of the container.

Screen Width: 774px (min-width):
  - I applied the grid layout to the container: 
  ```css
    .container {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      grid-template-rows: repeat(2, 1fr);
      overflow-x: hidden;
    }
  ```
  - I struggled to properly position the child elements of the container in the grid. I looked up some approaches and found out that I could use the `grid-template-areas` property to position the child elements in the grid.
  ```css
    .container {
      display: grid;
      grid-auto-columns: 1fr;
      grid-auto-rows: 75px;
      margin: 1rem;
      gap: 2rem;
      grid-template-areas: 
      'box1 box2 box2 box3'
      'box1 box2 box2 box3'
      'box1 box2 box2 box3'
      'box1 box2 box2 box3'
      'box1 box5 box6 box3'
      'box4 box5 box6 box3'
      'box4 box5 box6 box3'
      'box4 box7 box8 box8'
      'box4 box7 box8 box8'
      'box4 box7 box8 box8';
    }
  ```
  - Once I added the grid-template-areas property, the initial mobile layout was unordered.

  **SECOND TRY**

  - Things started to get messy, elements were overlapping, an element disappeared altogether, so I decided to start from scratch, which is a painful process.

  - I decided to start differently with the help of online resources, I started with larger layouts and then moved to the mobile layout.

  - I simplified the index.html file: 
  ```html
    <div class="container">
      <div class="item">
        <div class="large-text">Create and schedule content <em>quicker.</em></div>
        <img src="assets/images/illustration-create-post.webp" alt="a create post image.">
      </div>

      <div class="item">
        <p class="x-large">Social Media <span class="emph">10x</span> <em>Faster</em> with AI</p>
        <img src="assets/images/illustration-five-stars.webp" alt="a five star image.">
        <p class="small-text">Over 4,000 5-star reviews</p>
      </div>
      ...
    </div>
  ```

  - I included a CSS rule at the beginning of the stylesheet to manage images effectively: 
  ```css
    img {
    max-width: 100%;
    display: block;
    }
  ``` 
  - This'll make sure that the image is responsive and doesn't overflow the container as it did before.

  - In my first approach, I overlooked the fact that I could have used the same class name for multiple elements to avoid repetition and apply the same styling to common elements. This is especially useful when dealing with text elements that need to be styled consistently.
  ```css
    .x-large {
    font-size: 4rem;
    font-weight: 500;
    }

    .large-text {
      font-size: 2.75rem;
      font-weight: 500;
    }

    .medium-text {
      font-size: 2.35rem;
      font-weight: 500;
    }

    .small-text {
      font-size: 1.5rem;
      font-weight: 400;
    }
  ```
  - I kept the same styling for the container except this time I specified the max-width: 
  ```css
    .container {
      max-width: 1400px;
      margin: 1rem;
      display: grid;
      grid-auto-columns: 1fr;
      grid-auto-rows: 75px;
      gap: 2rem;
      grid-template-areas: 
      'box1 box2 box2 box3'
      'box1 box2 box2 box3'
      'box1 box2 box2 box3'
      'box1 box2 box2 box3'
      'box1 box5 box6 box3'
      'box4 box5 box6 box3'
      'box4 box5 box6 box3'
      'box4 box7 box8 box8'
      'box4 box7 box8 box8'
      'box4 box7 box8 box8';
    }
  ```
  - I applied the following styling to the third item and its image: 
  ```css
    .container .item:nth-child(3) {
      grid-area: box3;
      padding: 2.75rem 2rem 2.5rem 2rem;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
    }

    .container .item:nth-child(3) img {
      position: absolute;
      height: 410px;
      object-fit: cover;
      object-position: left;
      top: 150px;
    }
  ```
  - this was so it follows the desktop layout.

  - I applied the following styling to the container, with max-width being 1024px: 
  ```css
    @media (max-width: 1024px) {
      .container {
        grid-auto-rows: initial;
        grid-template-areas: 
        'box1 box1 box2 box2'
        'box1 box1 box2 box2'
        'box3 box3 box4 box4'
        'box3 box3 box4 box4'
        'box5 box5 box6 box6'
        'box5 box5 box6 box6'
        'box7 box7 box8 box8'
        'box7 box7 box8 box8';
      }
  ```
  - I used `grid-auto-rows: initial;` because: I previously set grid-auto-rows to a specific value and now want to reset it for smaller screen sizes. This allows the grid to adjust its row heights dynamically based on the content within each grid item. And finished the project accordingly.

### Continued development

This project was immensely useful, I knew about grid layout beforehand but when it came to practice, I had to redefine my definition for learning, it's not only knowledge but also practice and continued development that contribute to your excellence, I still lack proper understanding of how to implement some of the techniques I learned building this project, for e.g., `grid-template-areas` and the `initial` value given to CSS properties, but I'm willing to develop myself further by building projects from the Frontend Mentor.

### Useful resources

- [edsHTML](https://www.youtube.com/watch?v=-muwduB2G1A) - Looking back at my initial approach and this guy's approach made me realize my oversight of simplicity. I learned a lot from this YouTube video and am planning to follow a similar approach moving forward.

## Author

- Frontend Mentor - [@ziad-rima](https://www.frontendmentor.io/profile/ziad-rima)
- LinkedIn - [Ziad Rima](https://www.linkedin.com/in/ziad-rima-97b6b72b2/)


