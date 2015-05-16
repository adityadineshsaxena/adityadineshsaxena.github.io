---
layout: post
title: "Cleverly over-ride your Checkboxes and Radio buttons using CSS only!"
date: 2015-05-16
categories:
tags: "css3 html checkbox radio chrome"
---

With the advent of Web 3.0, HTML/CSS is a tricky game on most occasions. WYSIWYG editors have been making html/css easy much before I started to play around with this stuff. What they don't offer you, though, is creativity - which I must say, is in abundance at my workplace.

One of my oldest pet-peeves with fellow Designers has been their reluctance to learn more about what's possible to do on the Web. While I don't judge them for their lack of interest, I'm sure learning a little bit about the Web never hurt anybody. So, anyway, cutting to the chase, they gave me this wonderful piece of design with checkboxes and radio buttons that I knew were not possible just with plain css.

Here are some snapshots of the design.
![Checkboxes](/images/2015-05-16-checkboxes.png)
![Radio Buttons](/images/2015-05-16-radios.png)

Clearly, the designs are good. But, you'd have to say the checkboxes and radio buttons depicted aren't those that come out of the box in browsers.

Well, relax. There's no such thing as **impossible**, and it's the same here. The trick I learned to customize these boxes is while working with fellow developer at my workplace. Obviously I customized it to an extent to work for me, and so can you.

Before proceeding further, if you want to jump into the code right away and ignore my rest of the post, here is the [Gist](https://gist.github.com/adityadineshsaxena/654e00673f5ea5a40d3e). And here's the [JSBIN](http://jsbin.com/rekiqeqeqi/2/)

Let's dive into the code right away.

My HTML looks quite straightforward:

```html
<!-- custom radio button -->
<label>
    <input type="radio" name="sweet-radio" id="sweet-radio-1" value="Yes" checked>
    <span class="custom-radio-button">
    </span>
    <span>Sweet Radio 1</span>
</label>

<!-- custom checkbox -->
<label>
    <input type="checkbox" id="sweet-check-2" checked/>
    <span class="custom-checkbox-button">
    </span>
    <span>Sweet Check 2</span>
</label>
```

1. What we're trying to do here is replace the existing checkbox's and radio button's states: checked and unchecked.
2. We'll first hide the default radio buttons or checkboxes
3. Replace them (or, rather, their states) with a `background-image` or in this example's case, with a Font-Awesome Icon. Notice, that in the Gist, I've include font-awesome.css. Without it, this example wouldn't work. Font-Awesome basically allows me to replace the existing radio/checkboxes with some characters taken from Font-Awesome's Web Font, which is included in its CSS as `@font-face`

The label tag encloses everything that's got to do with one radio button or one checkbox and that's because even if you click on the label, the checkboxes and radio buttons get selected. (a handy trick that increases the UX of any form manifold)

The `input[type='radio']` & `input[type='checkbox']` have two siblings each. The 2nd sibling is a `<span>` tag that contains the text which needs to be displayed.

Most of the *magic* will happen, though, in these two places: `<span class="custom-checkbox-button"></span>` and `<span class="custom-radio-button"></span>`

*Note: I will be refer to customizing these in __Chrome browser__. With StackOverflow and Google, it's never too difficult to get these to work in other browsers as well, that is, if they're not already working there.*

My CSS goes like this:

```css
body {
  background-color: #eee;
}

/** CHECKBOX CSS **/

input[type="checkbox"] {
    display: none;
    position: relative;
}

input[type="checkbox"] + .custom-checkbox-button {
  margin-right: 11px;
  position: relative;
}

input[type="checkbox"] + .custom-checkbox-button:after {
  color: #cfdaed;
  display: inline-block;
  font-family: FontAwesome;
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: '\f096';
  font-size: 20px;
  cursor: pointer;
}

input[type="checkbox"]:checked + .custom-checkbox-button {
  margin-right: 10px;
  display: inline-block;
}

input[type="checkbox"]:checked + .custom-checkbox-button:after {
  content: '\f14a'; /* This comes from Font Awesome */
  color: #1569ad;
}

/** RADIO BUTTON CSS **/
input[type="radio"] {
  display: none;
  position: relative;
}

input[type="radio"][disabled] + .custom-radio-button:after {
  cursor: not-allowed;
}

input[type="radio"][disabled]:checked + .custom-radio-button:after {
  content: '\f111';
  color: #cfdaed;
}

input[type="radio"]:checked + .custom-radio-button:after {
  content: '\f058';
  color: #1569ad;
}

input[type="radio"] + .custom-radio-button:after {
  color: #cfdaed;
  display: inline-block;
  font-family: FontAwesome;
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: '\f10c';
  font-size: 18px;
  cursor: pointer;
}
```

Lets look at the CSS now, point by point

1. First, we hide the default states using `display: none;`
2. Then, using pseudo CSS for `:after` tag of the custom `<span>` implementation, I add some css that styles my custom checkbox or radio button.
3. Alongside these styles, is

    ```
    font-family: FontAwesome;
    content: '...'
    ```

4. For each icon, in Font-Awesome, which I want to use to replace the default behaviour of the checkboxes/radio buttons, I find out the character that the icon uses, and just pull it here.

5. Similarly, I add other icon characters to the `checked` or the `disabled` state of the Checkbox/Radio Button.
6. That's it!

Lets take a deep breath and look again what we did. It's not rocket science, and, once you get the hang of this, you'll want to do this again and again in your user interfaces just because this looks so neat.

Don't forget to hit me up on Twitter if you like what I do for a living. Cheers!