# Writing JavaScript
javaScript provides the logic that runs your pages. You can use JavaScript to control elements, respond to interactions, update, edit, and create new content, and more! 

Here you will use JavaScript to: 
- load data
- display the title of the flashcard set
- display the description of the flashcard set
- show the number of of the current question and the total number of questions

## Screate script.js
JavaScript is written in plain text files with the `.js` file extension. Create a new file in the same folder as your `index.html` file, and name it `script.js`.

Everything in `script.js` should be written in the JavaScript language. 

Make another new file, name this one `data.js`, save this to the same folder as `index.html`.

This new file will hold a list of questions and answers, along with some meta information describing the set of questions. 

Copy the text below and add it to `data.js`. 

```JS
const data = {
  "title":"Cats Flashcards",
  "description":"These Flashcardsask ask a series of questions to test your knowledge of cats!",
  "questions":[
    {"q":"The scientific name for cat is?", "a":"Felis catus"},
    {"q":"People who make cats their hobby are known as?", "a":"Cat fanciers"},
    {"q":"The latin word for cat?","a":"cattus"}
  ]
}

export default data
```

The first line defines a variable `data`, I used the keyword `const` to declare that this variable can't be reassigned, in other words, you won't be assigning a new value to `data` in the furture, and if you try you'll get an error. 

You might recognize value assigned to `data` as JSON, a Python Dictionary. Everything is arranged in name and value pairs. You can think of the data here as a tree structure! 

- tile - a string 
- description - a string
- questions - an array of questions. 
  - Each element in the array is an object with properties "q" and "a"

The last line, `export default data` allows this file to share `data` with any other files that migth need to use it. 

Open `index.html`, just above the closing body tag add this line: 

```HTML
      ...
      <script src="script.js" type="module"></script>
  </body>
  ...
```

The script tag allows you to load a script file. The attribute, `type="module"` allows that script to import other scripts. 

back in `script.js`, import `data` from `data.js`, like this.

```JS
import data from './data.js'
```

You can access any of the values in data using any of the key names. Try this:

```JS
console.log(data.title)
console.log(data.description)
console.log(data.questions)
```

The `console.log()` method prints a message to the console in the browser. Add the lines above to your `script.js` file and open your `index.html` in the browser. Open the web inspector and find the console. You should see something like: 

```
[Log] Cats Flashcards (script.js, line 4)
[Log] These Flashcardsask ask a series of questions to test your knowledge of cats! (script.js, line 5)
[Log] Array (4) (script.js, line 6)
0 {q: "The scientific name for cat is?", a: "Felis catus"}
1 {q: "People who make cats their hobby are known as?", a: "Cat fanciers"}
2 {q: "The latin word for cat?", a: "cattus"}
```

## JavaScript and the DOM
As mentioned previously, the Document Object Model is the structure of the page, described by teh HTML that you wrote! Each tag describes an object that is created. 

Objects have properties and methods you can access with JS. These properties an methods allow you to set the content or appearance of that element, and more. 

Sometimes you will need a "reference" to on object in the DOM so you can work with it. For example, imagine you want to set the title displayed to the title text in your data? 

```JS
const titleH1 = document.querySelector('#title')
```

Above you declared a new variable, as a constant, because it will not be changed in the future. The value assigned is a reference to the DOM element with the `id` name "title". 

Notice, that `querySelector('#title')` uses a selector string, in the same way you would write a selector in the CSS language! In this case it's an id name which begins with the `#`. 

The variable `titleH1` is a refernce to the element created by the html `<h1 id="title">The title</h1>` you wrote in `index.html`.

Try logging it to the console: 

```JS
console.log(titleH1)
```

To set the text that appears between the tags you can set the `innerHTML` property. Set it to the title in the data. 

```JS
titleH1.innerHTML = data.title
```

The `h1` should now display "Cats Flashcards". 

**Challenge:** You should try this on your own for practice! Define a new variable. Assign this new variable a refernce to the paragraph (p tag) with the id "description". 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

```JS
const descriptionP = document.querySelector('#description')
```

I used the name of the tag as part of the variable name to help clarify and remind me what this variable is storing. 

**Challenge:** Now set the `innerHTML` of this new variable to the value stored in `data` to the "description" key. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

```JS
descriptionP.innerHTML = data.description
```

This should display "These Flashcardsask ask a series of questions to test your knowledge of cats!" in the p under the title. 

**Challenge:** You need a refernce to the `p#score` to display the current question and the number of questions. Find this element in `<header>`. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

Here is what I used:

```JS
const scoreP = document.querySelector('#score')
```

Important! I used the name `scoreP`, future scripts will use this name, if you used a different name, you'll need to replace `scoreP` with the name you chose in the future!

**Challenge:** you need a reference to the element with the id "flip-card". You'll use this to "flip" the card over to reveal the answer card. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

Here is what used. 

```JS
const questionContainer = document.querySelector('#flip-card')
```

Important! I used the name `questionContainer` if you used a different name, you'll need replace this name with the name you used in the scripts that come later! 

**Challenge:** Each of the cards, these have the id names: "q-card" and "a-card", contain a p tag, and this is where you need to display the question and answer from each of the flashcards. 

To do this you can use `document.querySelector()` with a the descendant or child selector. Something like: `#q-card p` or `#q-card > p`. 

Read about these selectors here: https://www.w3schools.com/css/css_combinators.asp

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

```JS
const qCardP = document.querySelector('#q-card > p')
const aCardP = document.querySelector('#a-card > p')
```

Alternately you could use: 

```JS
const qCardP = document.querySelector('#q-card p')
const aCardP = document.querySelector('#a-card p')
```

Either of these should work. The first selects a p element that is a child of an element with the id name "q-card". The second selects the element that is a descendant of an element with the id name "q-card". A child is a descendant but not all descendants are children! 

## A function to show the next question
The process of showing a question will be used more than once, its best to put the code responsible for this in a function! 

To track the current question you will need a variable. The questions are stored in an array, and we access the elements of an array via their index. Index 0 is the first element of the array, index 1 is the second element, index 2 is the thrid element, etc. 

```JS
let questionIndex = -1
```

The initial value is -1, but the first element of the array is 0. We're going to add one to the index each time we show question, after adding 1 the -1 will be 0, so this will work for us. 

Define a function like this: 

```JS
const showNextQuestion = () => {

}
```

Here you defined a variable, `showNextQuestion`, and set the value to a function. 

The first thing your function needs to do is add 1 to `questionIndex`.

```JS
const showNextQuestion = () => {
  questionIndex += 1
}
```

Next check the length of the array to see if we have gotten to the last question. If we are at the last question we will loop back to the first. 

```JS
const showNextQuestion = () => {
  questionIndex += 1
  questionIndex = questionIndex % (questions.length - 1)
}
```

The `%` operator is modulo. Read about `%` here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder

In short, `%` returns the whole number remainder, for example `4 % 3` equals `1`. 3 divides into 4 once and leaves 1. Another example: `7 % 3` is 1, 3 divides into 7 twice for 6, the whole number remainder is `1`. 

Here we divide the `questionIndex` by `questions.length - 1` because the first index of an array is 0, and the last index of an array is the length - 1. 

Now get the current question and answer from the array. 

```JS
const showNextQuestion = () => {
  questionIndex += 1
  questionIndex = questionIndex % (questions.length - 1)
  qCardP.innerHTML = questions[questionIndex].q
  aCardP.innerHTML = questions[questionIndex].a
}
```

Here you getting the object in the `questions` array at the `questionIndex`. Then setting the `innerHTML` of `qCardP` to the value of the `q` property. Then doing the same for the `aCardP`.

Last, we need to display the question number and total number of questions. 

```JS
const showNextQuestion = () => {
  questionIndex += 1
  questionIndex = questionIndex % (questions.length - 1)
  qCardP.innerHTML = questions[questionIndex].q
  aCardP.innerHTML = questions[questionIndex].a

  scoreP.innerHTML = `Score ${questionIndex + 1}/${questions.length - 1}`
}
```

The last line sets the innerTML of `scoreP` to "Score 1/3". 

Important! Here you are using the back quotes `\`\``. This is the key in the upper left of your keyboard! These cahracters are used to create a "Template String". We use these to display variables in strings. Read about Template Strings here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals


To start your program you should call `showNextQuestion`. Calling a function invokes/executes/runs the code inside that function. So far you hae defined the function, but the code inside the block (`{}`) of the function hasn't run. 

To run the code in a function call the function by using it's variable name followed by `()`. 

```JS
const showNextQuestion = () => {
  questionIndex += 1
  questionIndex = questionIndex % (questions.length - 1)
  qCardP.innerHTML = questions[questionIndex].q
  aCardP.innerHTML = questions[questionIndex].a

  scoreP.innerHTML = `Score ${questionIndex + 1}/${questions.length - 1}`
}

showNextQuestion() // Run the function!
```

Testing your code now should show "Score 1/3" in the upper corner, and the first question in the `p#q-card`. The Answer was also displayed in the `p#a-card` but you can't see it because it is underneath the the question card!

## Conclusion
In this section you learned how to write JavaScript! You defined variables, imported values from another module (file), used `document.querySelector()` to get a reference to objects in the DOM, and set the `innerHTML` of those eleemnts. 
