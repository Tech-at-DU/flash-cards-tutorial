# Flipping the Card
To get the card to flip we can use CSS. The `div#q-card` and `div#a-card` have a parent element `div#flip-card`. It's this parent element that will rotate. Since the question and answer cards are children of `#flip-card` they move with it when we transform it. 

Imagine a line drawn through the center of the card from top to bottom. This is y axis, you will rotate the card on this axis. 

## Add some styles to div#flip-card
Open `styles.css` and add this new rule. 

```CSS
#flip-card {
  width: 100%;
  height: 100%;
  transition: transform 400ms;
  transform-style: preserve-3d;
}
```

This rules sets the height and width of this element to 100% of it's container. 

The last property `transform-style: preserve-3d` cause the element to be drawn as if it were in 3d space. This will give the rotation a 3d look. 

The `transition` property will animate this element when its properties change. Instead of changing instantly, the properties will take `400ms` (400 milliseconds) to change. Since the proprty `transform` is listed changes to this property will be animated over `400ms`. 

You may have noticed that there is no `transform` property! That's because we haven't added it yet! 

Add another new rule: 

```CSS
#flip-card.flip {
  transform: rotateY(180deg);
}
```

This rule uses an interesting selector `#flip-card.flip`. This selector describes an element that has the id name "flip-card" and the class name `flip`. In HTML that would look like this: 

```HTML
<div id="flip-card" class="flip">
  ...
</div>
```

We don't have this but, we do have: 

```HTML
<div id="flip-card">
  ...
</div>
```

The class name is missing. What you are going to do is add the class name when the "Answer" button is clicked, and remove it when the "Question" button is clicked. 

When the class name is added, the new rule applies, `#flip-card` now has `transform: rotatey(180deg)`, which applies the `transition: transform 400ms`, and card animates its rotation over 400 milliseconds. 

**Experiment:** I can tell you're sceptical that this will work. You can test it for yourself. With your page open in the browser, open `index.html`. Add the class "flip" to `div#flip-card`. It should look like this: 

```HTML
<div id="flip-card" class="flip">
  ...
</div>
```

Save your file, the answer card should appear. You will not see the animation since the card started with the value and the value wasn't changed. 

Remove `class="flip"` before continuing. 

## Event Listeners and Event Delegation
Event listeners are how we handle interaction with webpages. Events are things that happen in your app. Listener reacts to events when an event occurs. 

A listener has two parts, an event name, and a handler function. Event names can be things like "click", "input", "load", etc. A handler is a function that contains code that is run when the event occurs. 

### Event Delegation
Event delegation is a method of handling events that is a an industry best practice. Read about event delegation here: https://www.youtube.com/watch?v=aZ3JWv0ofuA

In short event delegation allows us to handle events from a parent element. It is used to avoid potential problems. 

Open `script.js`. 

```JS
document.body.addEventListener('click', e => {

} )
```

Here you added a new event listener, with `addEventListener()`. This takes two parameters: event name, and handle function. 

The event name is "click". 

The function is an anonymous function, it doesn't have a name. This function receives one argument, so we have defined a single parameter variable `e`. This is event object, which will be important! 

Notice that the event listener was assigned to the body, `document.body` is an alias for the `<body>` element. You could have used: `document.querySelector('body')` instead!

### Event Object
When an event occurs, if there is a listener the handler function is called and passed an event object. This object has properties that "describe" the event that just occured. 

For example with a "click" event properties include: `pageX` and `pageY` which tell us where the click occured onthe page. 

Another property that all events include is `target`. The target of the event is the element where the event originated. Read about the target here: https://developer.mozilla.org/en-US/docs/Web/API/Event/target

### Flipping the card
To flip the card you are going to check the event target, if it's `#answer-button` you'll add the class "flip", if its the `#question-button` you will remove the class "flip", if its the `#next-button` you will call the `showNextQuestion()` function to show the next question. 

```JS
document.body.addEventListener('click', e => {
  console.log(e)
  if (e.target.matches('#answer-button')) {
    questionContainer.classList.add('flip')
  } else if (e.target.matches('#question-button')) {
    questionContainer.classList.remove('flip')
  } else if (e.target.matches('#next-button')) {
    questionContainer.classList.remove('flip')
    showNextQuestion()
  }
})
```

Here `questionContainer.classList.remove('flip')` should remove the class name "flip" from the element `questionContainer`, while `questionContainer.classList.add('flip')` will add the class name "flip" to `questionContainer`.

Test your work. Observe these things and work through testing each of the features. 
- load the page. 
  - The title should appear
  - The description should appear
  - The score should show 1/3
  - The question card should show the first question
- Click the "Answer" button in the lowerright. 
  - The card should flip over
  - The answer card should show the answer to the question
- Click the "Question" button in the lower right. 
  - The card should flip and show the question card. 
- Flip back to the answer. Click the Next button. 
  - The card should flip and show the next question
  - The score should update to display 2/3
- Click through all of the questions
  - After the last question we should loop around to the first question. 

## Debugging your work
If something is not working here are some steps you can follow to solve those problems. These steps can be used n any project! Even if things are working you should consider these. 

The first step to solving a problem is identifying the problem. This often comes from examining actions and expectations. An action is something you do or set in motion. This could be clicking a button or loading the page. before you take the action, clarify in your mind what you expect to happen. Think of something concrete and quantifiable. Now take the action and compare the result to your expectation. 

If things are not what you expect, ask yourself what could be going wrong? 

Follow these steps: 
- Check for error messages. Open the web inspector in the browser and look for errors in the console. If there is an error it will come with a description, a file name, and a line number. Usually on the right side. Use this to identify in your code where the computer thinks the error is occuring. 
- Idenitfy the element where the problems is occuring. Often problems will occur at en element, for example clicking a button causes no effect, text that should be displayed in a h1 is not showing. Think about where your code is referencing the element and where it might be handling the click or setting the `innerHTML` or whatever else it might be doing. Examine the code closely looking for problems. 
- Use `console.log()`. Much of what is happening in the code we write is invisible to us. Making values visible can often go very far explaining why something isn't working. A variable might have a value of `0` when we thought it should have a value of `1`, or a number could be a string `"42"`. 
  - Identify the area in your code where you think the problem is occurring, look for a value that you can log to the console.
  - You may have a function, that never being called, or an event that is not being handled. You can log any message to let you know that this is function is being called. If you don't see the message then look for the location where the function should be invoked for the problem. 

## Comclusion 
This was a look at using HTML, CSS, and JavaScript to create a web app. 

Important concepts covered were HTML and attributes. HTML defines the structure of your pages. HTML defines the Object/Elements that are created by the browser. Attributes further define those objects, and add important information to them like id names and class names. 

CSS is written in rules, which include a selector, followed by properties, and values. You used Flex Box to arrange elements along an axis, horizontal or vertical. You also used position with relative and absolute values to arrange elements outside the default browser positioning. 

You wrote JavaScript that got references to the object/elements created by your HTML so your code could change the content of those elements. You did this with `document.querySelector()` along with a CSS selector string. You also used an array to store the list of questions, and object to structure data a collection of data. You also defined a function, and wrote some JS logic to display questions. 

You also used event delegation to handle events from an ancestor element. This is a highlevel concepts that appears on coding interviews! 
