# Stretch goals 
If you got the end of the tutorial pat yourself on the back. This tutorial used some sophisticated CSS, medium complex JavaScript, and HTML. 

Here are some challenges you can try to review and test your understanding of this project.

## Change the cards: 
Edit the questions. Make a whole new list of questions and answers. The questions are all stored in an array under the key "questions" in this data object: 

```JS
...
  "questions":[
    {"q":"The scientific name for cat is?", "a":"Felis catus"},
    {"q":"People who make cats their hobby are known as?", "a":"Cat fanciers"},
    {"q":"The latin word for cat?","a":"cattus"}
  ]
...
```

Every question has two properties "q" which stores the question text, and "a" which stores the answer to the question. 

## Change the styles
Edit the styles. Change the color, background color, border, font family, and anything else you think might be an improvement. 

## Add another set of slides
Include a button at the top to load of the slide sets. Here is a rough idea of how to do this:

- You'll need to add some new keys, each with an array of new questions. 
- Add a button for question set. Listen for these button events in your event listenr. Load the corresponding list of questions for the button clicked. 
