Module - 4 - Web API's

    4.1:
    Application Programming Interfaces 

    Pull Request:
    - proposing changes
    
    - you want someone to look at your changes and merge them into the main branch. 


    DOM : Document Object Module

        Callback Function: when you introduce a function to pass into another function.

        Data representation of the objects that comprise the structure and content of a document on the web.

        representation of what we see in the browser
            - since this is represented in data, we can edit this in javascript. 
                - Examples:
                    - document.getElementByid
                        document.getElementByid("text-header")  
                            lets us use javascript to search the DOM for an element on the page by passing in an ID.
                                This code looks for a element that has text editor as an id 

                                EXAMPLE:

                                document.getElementByid("text-header")

                                <h1 id="text-header">This is a header</h1>
                    - document.createElement
                        lets us create a new element to insert into the page. 
                            For example, executing this new javacript statement will create a new <div> element. 

                                EXAMPLE:

                                document.createElement("div")

                                    <div></div>

                    - element.appendChild
                        lets us insert a newly created element into the DOM 

                        This code designs a new paragraph element and then appends it to the body of the document. OR inserts it into the DOM. 

                        THE HTML ISNT THE DOM

                        HTML IS A STRUCTURED TEXT LANGUAGE

                            DOM IS A PARSED VERSION OF HTML THAT REPRESENTS A HIERARCHICAL STRUCTURE AND HTML ELEMENTS AS NODES AND OBJECTS THAT CAN BE MANIPULATED USING JAVASCRIPT. 

                    DOM IS HARD TO UNDERSTAND:
                        the only thing we need to remember now is that the DOM is representation of the html on the page and that it can be maniuplated by a scripting language like javaceript 

    4.2: Adding functionality to create custom tasks by entering the task name and type in HTML format fields. 

        Steps:

            1. Create a new feature branch. We'll create a new feature branch where we will build the form.

                'gitcheckout -b feature/form-submit'

            2. Add a task form to HTML. We'll add an HTML form that will allow the user to enter the task name and type.

                In the <header> element, replace the existing <button> code with a <form> element.

                    In order to do this we must add the following code.

                        '<form id="task-form">
                            <div class="form-group">
                                <button class="btn" id="save-task" type="submit">Add Task</button>
                            </div>
                            </form>

                    REVIEW of what we just did:

                We added a <form> element with an id attribute. Considering what we learned in the previous lesson, we can assume that we'll use this attribute in the JavaScript code.

                We also wrapped the <button> element in a <div> with a class of form-group. We'll wrap all of our form elements with this <div> to make styling it easier.

            **** REMEMBER: Remember that it can be hard to control the layout of HTML elements designed for content, such as <p>, <a>, <button>, and <input>. To make things a bit easier, wrap HTML elements in container elements whose sole purpose is to handle where they go on the page.

            Adding a Task Name Input:
                - Even though we enclosed the <button> element in <form> and <div> elements, the header still looks the same. But now it's set up for us to add more content, so let's add an <input> element to capture our task's name.

            Add the following code after the opening <form> tag:

            <div class="form-group">
                 <input type="text" name="task-name" placeholder="Enter Task Name" />
            </div>


            Add Task Type Dropdown

                Now we can enter a task name, but we still need another element that lets us set what type of task it is. We'll use an HTML element called <select>.

                Between the <div> elements that hold the text input and the button, add the following HTML:     

                Save index.html and refresh the browser. We now have a form element that allows us to select from a predetermined list of options. We've never come across this type of form element before, so let's review a few points:

                 We use <select> to tell the browser we're about to create this type of dropdown list, but we use <option> elements between the <select> tags to create the choices for that dropdown.

                We use the name attribute to help identify the form input. As we'll discover soon, we'll use it to select the element with the querySelector() method in our JavaScript.

                A value attribute should accompany every option, as this value will be used in the JavaScript later to read the option we've picked.

                For the option that merely describes the list, we need to ensure it appears first and also prevent the user from selecting it. To do that, we've added the selected property, which makes it appear first, and the disabled property, which prevents it from being chosen by the user.

                We used the options of Print, Web, and Mobile, but this is a personal project so feel free to customize these to fit your needs.

                This new element doesn't look so great, does it? The following image shows that pretty clearly:  


                
                    Click event listeners can lack usability features that may seem trivial but make forms feel more intuitive for some users, such as allowing both the submit <button> element and the Enter key to submit the form. Changing this type of behavior doesn't take too much work on our end, so let's do that to improve the Taskinator user experience.

                    To begin, we'll move the event listener from the <button> element that we added in the last lesson and apply it to the <form> element itself. Now the browser will be able to listen to an event happening on the entire form rather than just the button.

                    We need to change the code in the following two places:

                        At the top of script.js, delete the variable declaration for buttonEl and add the following code in its place:

                        var formEl = document.querySelector("#task-form");

                        At the bottom of script.js, remove the code to add an event listener to buttonEl and add the following code in its place:

                        formEl.addEventListener("submit", createTaskHandler);

                        Now the script.js file finds the <form> element in the page and saves it to the variable formEl, so that we can interact with the form and access some of its child HTML elements.

                        Because we're targeting the entire form instead of only the button, we can't use the click event listener anymore. If we kept a click event listener, then every time we clicked on the form it would run the createTaskHandler() function, which isn't what we want. Instead, we'll use a form-specific event called submit (also called onsubmit in certain documentation).

                        This particular listener listens for the following two events within the form:

                            When a user clicks a <button> element with a type attribute that has a value of "submit", like the button we currently have in the form

                            When a user presses Enter on their keyboard


                        What's happening here? Why would the code run, put something on the page, and then do nothing? If we add a console.log() statement to createTaskHandler() and monitor the Chrome DevTools console here, we'll notice that the log shows up for a second and then disappears as well.

                    Depending on how fast your computer is, you might notice that the browser actually reloads the page every time you submit the form! So the code works just fine here, but the browser is causing problems. This legacy browser behavior used to help webpages communicate with servers, but now JavaScript does most of that work.

                    Now that we use JavaScript to handle these types of actions, we no longer need to rely on this default browser behavior to complete the task. But the browser doesn't know that, and it still wants to do what it was designed to do. It's up to us to explicitly tell the browser to not do that.

                    Let's fix the issue right now by making the createTaskHandler() function look like the following code:
                

                    By adding the event argument to the createTaskHandler() function, we can use the data and functionality that object holds. We did that when we added event.preventDefault(); to the handler function's code. What might that method's name mean?

                    Think about what happened before we added it: the page refreshed every time we submitted the form. That was due to the browser's default behavior when handling a form submission. So if we execute a method named event.preventDefault(); in the handler, we're instructing the browser to not carry out its default behavior.

                    We won't need event.preventDefault(); for all event handlers, but we'll have to use it a few more times for Taskinator. After all, the click handler worked without it this whole time.

                    There's one more thing before we move on. Let's explore the event object a little bit by logging it to the console. Add the following code to the createTaskHandler() function:


                    As we learned when implementing the click event, the event object holds a fair amount of data. A lot of it is unimportant at the moment, but over time we'll learn how to use some of the properties in our applications.

                    So the form submission works, and the event handler can work as intended, but we're still creating a task item with preset values. Let's focus on the form's input values and see how we can retrieve the content we enter.

                    Before you move on, remove the console.log(event) call you added to createTaskHandler(). Your work should match this code:


            3. Handle form submission. We'll use JavaScript to add a task to the list when the "Add Task" button is clicked.

            4. Capture form field values. We'll use JavaScript to capture the unique information the user enters (the task name and type).

            5. Organize functionality. We'll refactor the code to make it more maintainable.

            6. Address usability concerns. We'll improve the user experience by validating form input and resetting the form after the user clicks the "Add Task" button.

            7. Save our progress with Git. We'll commit and push our changes up to GitHub
