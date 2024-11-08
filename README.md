# Events

- [Setup](#setup)
- [Testing Your Code](#testing-your-code)
  - [Submitting On Time](#submitting-on-time)
  - [npm test](#npm-test)
- [Before You Start](#before-you-start)
- [Questions](#questions)
  - [Question 1: clickCounterHandler - modify.js](#question-1-clickcounterhandler---modifyjs)
  - [Question 2: handleKeydown - modify.js](#question-2-handlekeydown---modifyjs)
  - [Question 3: remove the inline event listener - modify.js](#question-3-remove-the-inline-event-listener---modifyjs)
  - [Question 4: handleDelegation - modify.js](#question-4-handledelegation---modifyjs)
  - [Question 5: addNewRandomNumber - modify.js](#question-5-addnewrandomnumber---modifyjs)
  - [Question 6: removing an event listener  - modify.js](#question-6-removing-an-event-listener----modifyjs)
  - [Question 7: Do it all from scratch - index.js](#question-7-do-it-all-from-scratch---indexjs)

## Setup

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

After cloning your repository, make sure to run the following commands:

```sh
npm i
git checkout -b draft
npm t
```

## Testing Your Code

### Submitting On Time

You have to understand that "grades" don't exist at Marcy. We only need performance data in order to know how you're doing, and make sure the people who need help get it as quickly as they can. It's ok if you didn't finish by the deadline! Just show us what you have. We'll have office hours and reviews, and we want to know what you are all struggling with so we can use those meetings effectively. **This is not about grades, its about seeing what you know, and where we can help!**

### npm test

Before submitting your code, make sure you got things right by running the provided automated tests.

You can do this using the commands:

```sh
npm test # run the automated tests
npm run test:w # run the automated tests and rerun them each time you save a change
```

You will know that you have "completed" an assignment once you have passed 75% or more of the automated tests!

## Before You Start

Now things are *really* getting interesting. You get to add interactivity to your pages! To try and set you on the right path, our `modify.js` has some existing code, but it's not enough! You'll still need to use the DOM manipulation skills in order to get everything to work.

So in problem one, we give you a simple empty function and a `main` function to run things in. But it's up to you to grab the button itself and then actually *add* the event listener to it. You must read the tests in order to understand fully what is being asked of you. Reading tests is a crucial skill on the job, so practice it now!

Really think about what the question is asking you to do. Don't be restrained by the code we give you, you are supposed to add more! Study the provided `modify.html` document as well, a lot of the questions make more sense when you see the scaffolding.

## Questions

### Question 1: clickCounterHandler - modify.js
As you can see in our `modify.html`, we have a `button#click-button` element with a `data-clicks` attribute (line 14). 

The functionality we want is that each time you click on the button, the `data-clicks` attribute should be incremented, and the button text should show the number of times it has been clicked.

1. Inside the `main` function, register a `click` event listener for the `#click-button` button that uses the function `clickCounterHandler`.
2. Inside of `clickCounterHandler`, it should...
    - increment the value of the `data-clicks` attribute on the clicked button (how can you get the element that was clicked without using `document.querySelector` again?)
    - update the text of the clicked button to tell us how many times it's been clicked (check out the tests to see exactly what we want the button to say)

<details><summary>Hints!</summary>
  
> **Notes about `data-` attributes**:
> 1. Remember that the value of a `data-` attribute will be a string so you may need to convert the string to a number before incrementing!
> 2. `data-` attributes can be accessed from a selected element using the `.dataset` property
> 3. `data-` attribute names are converted to camelCase. For example, the `data-my-name` attribute would be converted to `.dataset.myName` on the element.
> 
> **Use the `event` object**:
> * The `event.target` value can be used to tell you which element was clicked (or, more generally, which element triggered the event)
> 
> ```js
> const printTheTarget = (event) => {
>   // ▼ this is much better than querying for the clicked element
>   console.log(event.target);
>
>   // ▼ this is the same value as event.target but with much more code
>   const target = document.querySelector("#thingy");
>   console.log(target);
> }
> 
> document.querySelector("#thingy").addEventListener("click", printTheTarget);
> ```

</details>


### Question 2: handleKeydown - modify.js

Anytime the user presses a key on their keyboard, we want to tell them the key they pressed. 

Do the following:
* In the `main` function, add a `"keydown"` event listener to the `document.body` that triggers the `handleKeydown` function to be invoked.
* The `handleKeydown` function should:
   *  select the `p#keydown-tracker` element
   *  modify the `textContent` of that element to display the name of the key that was pressed.

Check the tests to see *exactly* what the text content of the tag should be. Investigate the `event` object to see where you can grab the needed information.

### Question 3: remove the inline event listener - modify.js
You many have noticed there's another button with a `data-clicks` attribute. However, it's using an inline `onclick` function to do this. You need to replace that inline event handler with one assigned using JavaScript.

* In `modify.html`, **edit just this section of the html** to remove the click handler. 
* In the `main` function of `modify.js`, add an event listener to the `button#inline-example` element using the `clickCounterHandler` from question 1. 
* Check the tests to see exactly what we're looking for.

### Question 4: handleDelegation - modify.js
In `modify.html`, we have a `div#delegation` element that contains a bunch of buttons, followed by a `p` with a `span#delegation-result` element.

The idea here is that whenever you click a `button` in the `div#delegation` container, the `span#delegation-result` element will update with the text of that button.

In the JS code, you'll see there's already the start of some delegation handling. However, if you click in the empty space around the buttons in the the `div#delegation` container, the span will update, not just when you click the buttons. We only want it to update when a button is clicked. So, update `handleDelegation` to only update the span's text content if a *button* is clicked.

> Do not just add click event listeners to each button.You have to add the listener to the delegation container! (This ability to remove and remake children without causing event issues is actually one of the best features of delegation. Remember that for your own projects...)

<details><summary>Hint</summary>

> Remember, `event.target` will be the element that triggered the event (that is, the actual element that was clicked on). See if you can use `event.target` to determine if a button was clicked or if the div container was clicked.
>
>If you need another hint, try googling "how to check if event.target is a button?"

</details>

### Question 5: addNewRandomNumber - modify.js
This is a fun one. 

* In the `main` function, add a `"click"` event listener to the `#add-random-num` button for the `addNewRandomNumber` handler
* In the handler, create a new `li` whose `textContent` is a random number greater than `0` (the range of the random numbers doesn't matter, just make it random and greater than `0`). 
* Append the new `li` to the `ul#random-numbers` element.

### Question 6: removing an event listener  - modify.js
Lastly, it is important to know how to remove listeners. 

There's a `button#remove` element. Attach a click event listener to this button that will remove the `handleDelegation` event handler from the `#delegation` container.

### Question 7: Do it all from scratch - index.js
Ok, you got it with some help, now can you do it on your own? We have a blank `index.html` and blank `index.js`. Your job is to:
- fill out the `index.html` with boilerplate code:
  - A `head` tag with a title of `Intro to events`
  - A `body` tag
  - An `h1` with text content of `More Events Practice`
  - A `button` with an id of `add-one` and text content of `Click me to increment!`
  - A `p` tag with an id of `results` and text content of `0` to start
- Link the `index.js` script to this page
- Add a click event listener to the button that increments the `results` counter by `1` with each click
  - Do not add an inline `onclick` function, use `addEventListener`.

Check the tests to make sure you're doing what we're asking for!

# BONUS: research more events
We barely scratched the *surface* of all the events you can use on your pages. If you finish this assignment (and the short answers), we strongly encourage you to look up all the different JS events. Create a new repo and just mess around with them! Remember, you can learn much more on your own through experimentation!
