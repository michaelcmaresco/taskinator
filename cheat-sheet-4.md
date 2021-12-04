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


           4.2.6 Capture Form Field Values:

           At this point, the same canned tasks keep getting added to the page when we submit the form. Let's outline what we'll need to do for the event handler to retrieve the form's values upon submission:

                1. Target the HTML elements with the pertinent data.

                2. Read and store the content that those elements hold.

                3. Use that content to create a new task.

            We'll start off simple and only worry about reading the task's name first, then we'll retrieve the task's type when we know we're heading in the right direction.

            In createTaskHandler(), add the following code below the event.preventDefault();:


            PAUSE: 
            
                In the following selector, why do single quotes wrap the attribute's value and double quotes wrap the entire selector?

                document.querySelector("input[name='task-name']");
                If we used another set of double quotes to wrap the attribute's value, the entire string would fail because it would assume that we ended the string at "[name="; anything after would break the query selector.

            

            Get the Task to Display:

                Now that we've pinpointed the data we care about, we can grab it and put it on the page. We selected the right element, so we just need to retrieve its value property to access the submitted text in the input form. Let's delete the console.dir(taskNameInput); from createTaskHandler() and update the query selector to look like the following code:

                'var taskNameInput = document.querySelector("input[name='task-name']").value; ' 

                Previously, we selected and stored the entire HTML element for the task name form input. We don't need to worry about any of that element's other properties—just the value property. We can get to that property by adding a .value to the end. Now the value of the taskNameInput variable will be the text we entered in the <input> element.

                    NERD NOTE: The common verb that's used for retrieving or reading data from an object's property is getting. When we provide and store data in an object's property, it's called setting. These two terms are used often in web development.

                Next we want to get the task name we just stored in taskNameInput and add it to the listItemEl variable. Let's update the listItemEl.textContent property to look like the following code:


        Add Name and Type to a task:

            At this point, the task list looks like the following image:

            The mock-up, however, shows that the task type should appear below each task name, as shown in this image:

            To do this, first we'll have to get the value of the <select> dropdown's picked <option> element, then we'll have to create more HTML to go inside the <li> element that we created for a task item.

            Let's start by getting the value of the <select> dropdown. To do this, we can use the same code that we used to get the task name's value and update the selector to find the <select> element instead.

            Add the following code below the variable declaration for taskNameInput:

                'var taskTypeInput = document.querySelector("select[name='task-type']").value;' 


            Test it by using console.log(taskTypeInput); below the taskTypeInput variable declaration to see what the value is. It will display whatever <option> element was picked in the <select> dropdown.

            Great! We can use that value and add it to the task item, but first we'll need to refactor the code a little bit to make the HTML easier to style and maintain.

            Let's update the code in createTaskHandler() below the taskNameInput and taskTypeInput declarations to look like the following code:

                '// create list item
                var listItemEl = document.createElement("li");
                listItemEl.className = "task-item";

                // create div to hold task info and add to list item
                var taskInfoEl = document.createElement("div");
                // give it a class name
                taskInfoEl.className = "task-info";
                // add HTML content to div
                taskInfoEl.innerHTML = "<h3 class='task-name'>" + taskNameInput + "</h3><span class='task-type'>" + taskTypeInput + "</span>";

                listItemEl.appendChild(taskInfoEl);

                // add entire list item to list
                tasksToDoEl.appendChild(listItemEl);'



                We can now create a new task item with the content submitted through the form. We could've organized this content in a number of ways, but as we've discussed, wrapping content in a container <div> element will sync and bundle all that content together.

                Take a minute to select the Elements tab in Chrome DevTools and expand the <li> elements in the <ul>. In each <li>, observe each nested <div> with <h3> and <span> elements, and then look back at our JavaScript to see how the code created them.

                We still created the <li> element to hold the whole task (listItemEl), but instead of writing the task's content right to it, we created a <div> to hold the content (taskInfoEl).

                    'var listItemEl = document.createElement("li");
                    listItemEl.className = "task-item";

                    var taskInfoEl = document.createElement("div");
                    taskInfoEl.className = "task-info";

                Once we'd set the data into the <div>, we appended it to the <li>.

                    'taskInfoEl.innerHTML = "<h3 class='task-name'>" + taskDataObj.name + "</h3><span class='task-type'>" + taskDataObj.type + "</span>";

                listItemEl.appendChild(taskInfoEl);'

                Lastly, we appended the entire <li> to the parent <ul> (i.e., tasksToDoEl).

                    'tasksToDoEl.appendChild(listItemEl);'

                Notice how we can add a child HTML element to another HTML element in JavaScript before it even gets to the page? We can append the taskInfoEl to the listItemEl, meaning that all of the taskInfoEl content is set inside listItemEl as a child HTML element before we add listItemEl to the page. We can visualize this in the console by once again using console.dir() to print out the data in listItemEl. Add console.dir(listItemEl); as the last statement at the end of the createTaskHandler() function and save script.js. Refresh the browser and submit a new task. We should be able to see the nested element in the children property, like in the following image:

                That's not all, though. We also used a new DOM element property called innerHTML that works a lot like the textContent property, but with one big difference. The textContent property only accepts text content values. If it saw an HTML tag written in as a value, it would literally display the markup characters for that HTML tag without interpreting it as the HTML tag.

                The innerHTML property allows us to write HTML tags inside the string value we're giving it. When it loads, it reads the content as HTML and renders it to the DOM. So, an <h3> tag here will be rendered as an <h3> element in the DOM. (Notice here our difference in language: we write tags in our HTML in order to create corresponding elements in the DOM.)

                For textContent, it would display something like "<h3 class='task-name'>" and not infer that we wanted to use that actual HTML element.

                Let's change innerHTML to textContent for a second and see what displays. It should look something like the following image:

                Obviously that's not what we want, so innerHTML is the better fit here. Be sure to change it back to innerHTML, and we can move on!

                    IMPORTANT: We didn't have to use the innerHTML property here. Instead, we could have created HTML elements for the title and type separately and then appended them to the container element. While both approaches work, innerHTML lets us create fewer variables, but with less readable code.

                    Remember, there's usually more than one way to complete a task. It's up to you to decide which way to go.

                When to Refactor:

                    Right now, the createTaskHandler() function does a lot. It reads the form elements on submission, then creates quite a bit of HTML content and adds it to the page.

                    This works for our needs at the moment, but leaving it like this may lead to a headache when we add more features to the application. This may be a good time to separate createTaskHandler() into the following two different functions:

                        One function to handle the form submission, get the form values, and pass those values to another function as arguments

                        One function to accept the form values as arguments and use them to create the new task item's HTML

                    We'll tackle this type of refactor next. But first, let's do a quick safety check. The current state of your JavaScript should match this code:



4.2.7 Refactor the code to organize functionality. 

    The application works like we want it to. But with the current createTaskHandler() function, we'd struggle to add more content to a task item or the form for new features. In this step, we'll split up the tasks that each function is performing.

    Sometimes it's better to have many functions that each perform one task than to have one function that performs many tasks. We might want to do this for many reasons, such as one of the following:

    Functions with a lot of code performing separate tasks could become difficult to read and understand.

    Setting up a function to do multiple tasks, like getting the form values and then printing them to the page, lowers the potential to reuse the function for another part of the application.

    Both of these reasons can be hard to diagnose in the moment. That will get easier as you become more adept at predicting what the application may need in the future.

    Let's take a moment and outline what we'll do to refactor the code:

Rename the handler function to be a little more specific to the event it's handling.

Create a new function to take in the task's name and title as arguments and create the HTML elements that get added to the page.

Move the code that creates and adds HTML elements from the handler function into the newly created function.

Update the handler function to send the task name and type values from the form to the newly created function.

We're mostly just reorganizing code that we've already written, so a lot of work has already been done. We just need to get the code to its proper place.

We'll start by updating the name of the handler function. In script.js, change the createTaskHandler function name to taskFormHandler wherever the name is used: in the function's variable declaration and in the addEventListener() method at the bottom of the file.

If we update the name in both places, the application should still work, but we should test it before we move on, just in case. Save script.js and test the code by submitting the form.

If it still works, great! If it doesn't, double-check that nothing was spelled incorrectly. If the name of the handler function was all that changed before it stopped working, then there may be a typo or misspelling somewhere.

HINT:
    Don't forget to use the Chrome DevTools console tab to see if any errors show up.


Next we'll create a new function. We'll add the following code right below the taskFormHandler() function and above the addEventListener() method:

'var createTaskEl = function(taskDataObj) {

}'

We just created a new function called createTaskEl. As the name indicates, it will hold the code that creates a new task HTML element. But if we're going to provide this function with both the task's title and type, why is there only one parameter, called taskDataObj?

We could set up the function to have two parameters, one for each piece of data. That may limit us in the future, though, as we may end up using more information for each task. So instead of having to add another parameter to the function every time we want to use more data, we can just set up the function to accept an object as an argument.

This way, when we send the task's name and type to the createTaskEl() function, it'll look like the following code:

    '// taskDataObj
{
  name: "Task's name",
  type: "Task's type"
}'

Before we worry about passing the argument object, let's get the code for createTaskEl() in place. We could rewrite all of the code by hand, but it's already in the taskFormHandler() function, so we can just copy and paste it into createTaskEl().

Copy the following code from taskFormHandler() and paste it into createTaskEl():

' 
// create list item
var listItemEl = document.createElement("li");
listItemEl.className = "task-item";

// create div to hold task info and add to list item
var taskInfoEl = document.createElement("div");
taskInfoEl.className = "task-info";
taskInfoEl.innerHTML = "<h3 class='task-name'>" + taskNameInput + "</h3><span class='task-type'>" + taskTypeInput + "</span>";

listItemEl.appendChild(taskInfoEl);

// add entire list item to list
tasksToDoEl.appendChild(listItemEl);

Once it's pasted into createTaskEl(), make sure to remove that code from taskFormHandler().

Unfortunately we can't test the code yet, because we haven't updated taskFormHandler() to pass the data as arguments. Let's do that now by adding the following code to that function, to look like this:

' var taskFormHandler = function(event) {
  event.preventDefault();
  var taskNameInput = document.querySelector("input[name='task-name']").value;
  var taskTypeInput = document.querySelector("select[name='task-type']").value;

  // package up data as an object
  var taskDataObj = {
    name: taskNameInput,
    type: taskTypeInput
  };

  // send it as an argument to createTaskEl
  createTaskEl(taskDataObj);
}'

We gathered the form's values and placed them into an object with a name and title property. Then we inserted it as an argument when we called createTaskEl() at the bottom of taskFormHandler(). Doing this makes taskFormHandler() a lot easier to read, as it shows that it's collecting data and sending it elsewhere.

Lastly, we need to update the code in createTaskEl() to stop looking for the taskNameInput and taskTypeInput variables and start looking for the taskDataObj argument's properties instead. If we kept the two variable names there, the application would break when we attempted to submit a form.

The error would look something like the following image shows:

~image~

The error states that taskNameInput isn't defined. How could this be if it was clearly created in the taskFormHandler() function? Remember that any variables created within the curly braces of a function only exist within that function's braces. Any reference to it outside of the function will cause the program to break because it can't find a variable with that name. In this case, since the initialization of taskNameInput and taskTypeInput are now in taskFormHandler(), we don't have access to them in createTaskEl except by way of the object we've passed into it.

    NERD NOTE: This is known as lexical scoping. 

Let's fix the problem and update one line in the createTaskEl() function to look like the following code:

'
var formEl = document.querySelector("#task-form");
var tasksToDoEl = document.querySelector("#tasks-to-do");

var taskFormHandler = function(event) {
  event.preventDefault();
  var taskNameInput = document.querySelector("input[name='task-name']").value;
  var taskTypeInput = document.querySelector("select[name='task-type']").value;

  // package up data as an object
  var taskDataObj = {
      name: taskNameInput,
      type: taskTypeInput
  };

  // send it as an argument to createTaskEl
  createTaskEl(taskDataObj);
};

var createTaskEl = function (taskDataObj) {
  // create list item
  var listItemEl = document.createElement("li");
  listItemEl.className = "task-item";

  // create div to hold task info and add to list item
  var taskInfoEl = document.createElement("div");
  taskInfoEl.className = "task-info";
  taskInfoEl.innerHTML = "<h3 class='task-name'>" + taskDataObj.name + "</h3><span class='task-type'>" + taskDataObj.type + "</span>";
  listItemEl.appendChild(taskInfoEl);

  // add entire list item to list
  tasksToDoEl.appendChild(listItemEl);
};

formEl.addEventListener("submit", taskFormHandler);'



Again, learning to refactor code takes time. It feels unnatural at first: who wants to second-guess code they just wrote and got working? Over time, it will feel not like second-guessing but rather like a personal challenge to be a better developer.

The Taskinator application is taking shape, but as cautious developers, we have to ask ourselves, "How can this break?" We'll tackle that in the next and final step of this lesson, but first take a minute to celebrate future-proofing some of the code. It's not an easy task to perform or appreciate so early in a development career, and you've really set up the code to be reusable for any future features.

Don't forget to add, commit, and push the code to GitHub before moving on to the next step!



4.2.8: Address Usability Concerns:

    The end of the last lesson may have gotten you on the edge of your seat wondering how the code could possibly be broken. What happens if we submit the form without filling it out? What happens if we put in a task name but forget to pick a task type? Try doing it. You should get the result shown in the following image:

    ~img~

    As the preceding image shows, the task item was created just fine, but it's missing content! We can't delete a task (yet), but removing empty tasks would be cumbersome even with that ability. We should validate the form fields before completing the submission.

    Validation comes in a lot of different flavors, but it typically means checking that the required form fields have content and the content fits our needs. Think about creating a password: an application usually won't permit the creation of a short password without a number or uppercase letter.

    Luckily we don't have to test for that here. We just need to check whether the form fields have content. If they do, let the function continue and create the task item. If either field doesn't, stop the function and let the user know that something is missing.

    Let's do this right now and update taskFormHandler(), to have this code right before we create the taskDataObj variable:

    '
        // check if input values are empty strings
        if (!taskNameInput || !taskTypeInput) {
            alert("You need to fill out the task form!");
            return false;
        }'

    REWIND: 
        When used in a condition, empty strings and the number 0 are evaluated as falsy values. When we use the syntax !taskNameInput, we're checking to see if the taskNameInput variable is empty by asking if it's a falsy value.

        That's what the "not" operator ! is doing here. Because the default is to check for a true value, the ! is used to check for the opposite (false) value.


    If we save the script.js file and try to submit a task with an empty field now, we'll receive an alert that tells us we need to fill out the form, and then the function will stop when it reads return false. But if we include data in the form fields, the taskFormHandler() will work as intended and send the data to createTaskEl() to be printed to the page.

    This is a basic version of form input validation; we simply check to see if any value is read from the form inputs. By using the condition shown in the following code, we're seeing if either taskNameInput or taskTitleInput is empty, or if both are empty:

    '(!taskNameInput || !taskTypeInput)'

    Putting an exclamation point (!) in front of the variable name will make the condition return true if the value evaluates to false. So, this code literally says, "if either one or both of the variables are not true, then proceed," which is the same as "if either one or both of the variables are false, then proceed."

    That seems confusing at first, but think of it this way: we're checking to see if a false value is in fact false, which would result in the condition being true. Let's explore some examples of this in the following code before moving on:

                if (true) {
            // this will run because true is true
            console.log("Is true true? Yes.");
            }

            if (false) {
            // this will not run because false is not true
            console.log("Is false true? No.");
            }

            if (3 === 10 || "a" === "a") {
            // this will run because at least one of the conditions is true
            console.log("Does 3 equal 10? No.");
            console.log("Does the letter 'a' equal the letter 'a'? Yes.");
            }

            if (3 === 10 && "a" === "a") {
            // this will not run because both conditions have to be true to run
            console.log("Does 3 equal 10? No.");
            console.log("Does the letter 'a' equal the letter 'a'? Yes.");
            }
    
        We've now fixed a fairly large issue that this application could have, and we did it with only a few lines of code! We've made the application more user-friendly by making sure those two variables aren't empty strings and by giving feedback if users make a mistake.

    Reset the Form:

        We have one more thing to fix, however, and it's not so much an issue as a usability enhancement.

        Let's say we're adding multiple tasks at once. Every time we fill out the form and submit a new task, we have to erase the previous task's content and start over again. While this isn't a breaking bug or issue, it adds a little frustration for the user. Luckily, we can fix this frustration with one line of code.

        Let's add the following one last line of code to taskFormHandler(), underneath the validation if statement we just added:

        'formEl.reset();'

    Save script.js and try to submit a task. Note in the following animation that the form resets itself to its default values when you successfully submit a task. Before, it retained the task name and task type after you submitted the form.

    The browser-provided DOM element interface has the reset() method, which is designed specifically for the <form> element and won't work on any other element. We could use other methods, namely by targeting each form element and resetting their values manually, but that could be cumbersome when resetting a larger form.

    We're all set! We covered a lot of important ground in this lesson, and it shows. The Taskinator application not only accepts custom values from form elements but also validates the form as well. This is a big step in building this application, so let's close this feature branch's issue and merge it into the develop branch.

event.preventDefault() : tells the browser to not refresh ( which is it's default behavior) when we're using things like JavaScript to handle browser events like form submissions, etc. 

submit : allows us to use both a button and the enter key. 

How do we use JavaScript to get the information entered into a form’s input field?
        - We can select the form’s input element and use the value property to read its data.


Congratulations! You just learned a process that's used in all modern web development: using JavaScript to listen for browser events in the HTML, read data from the HTML page, and write data to the HTML page. You'll use these three actions often throughout your career as a web developer.

Let's recap what we accomplished in this lesson:

Added a form to the HTML document and learned a new HTML element, the <select> dropdown element.

Submitted forms using the submit event listener.

Overrode default browser behavior by introducing event.preventDefault();

Retrieved data from a form element using its value property.

Used a new DOM element property, innerHTML, to write HTML code instead of simple text.
        
Refactored the code to be reusable.

Used simple form validation with if statements to prevent user errors in the application.

Reset the form to its default state by using the reset() method on a form element.

This could be a shippable application at this point, as it has a lot of what we need for a task-tracking application. But we can still add some features, such as removing or editing a task and keeping track of the task's status.

We'll take this on in the next lesson, and because of the refactor we did in this lesson, it will be much less complicated than it could be!




4.3.1 Introduction:
4.3.2 We need to make a "tasks in progress" column and a "tasks completed" column. 
4.3.3 Develop branch - feature/updating branch. 
4.3.4 Kanban board. 

    As we introduced earlier, a Kanban board is a tool often used in productivity apps to visually convey the current stage of all tasks in a project. This is done by defining columns that tasks can move through from left to right. Some projects may define columns for To Do, In Progress, Code Review, Testing, Completed, and Blocked. We'll keep our app simple by only using three columns: Tasks To Do, Tasks In Progress, and Tasks Completed.

    ON THE JOB
    There are many Kanban-style project management apps that you'll come across in your career. Some of the more popular ones that companies use are Trello (Links to an external site.) and Jira (Links to an external site.).

    End of text box.
    We already have HTML in place for the first column, Tasks To Do, represented by a <section> element with class task-list-wrapper. Let's revisit the HTML in index.html and add two more <section> elements below the first one for the other columns:    

    Note that the <section> elements all have the same class, but the inner <h2> text and id attributes on the <ul> elements are different.

    Save the index.html file and refresh the browser. The page should now look like the following image:

    Flexbox, CSS grid, or even the float property.

    As a quick CSS refresher, use the Chrome DevTools to inspect the columns and verify which CSS properties are being used. You'll notice that the <main> element has the declaration display: flex, allowing it to control the distribution of its content. In turn, each <section> element has a flex: 1 declaration to specify that they should share space evenly.

    If you haven't already, try toggling the device toolbar from the DevTools by clicking on the following icon:

    An icon of two mobile devices standing upright.

    The browser should then mimic what the webpage looks like on a mobile device:

    In the CSS media query, the <section> elements' flex-basis is set to 100%, which defines a new width that takes up all available space. Thus, the elements become stacked.

Rewind:
    A media query defines a set of CSS rules that won't be applied unless a certain condition is met. For example, @media screen and (max-width: 900px) is applied when the screen size is equal to or less than 900 pixels wide.

    Fortunately, all of this CSS was provided ahead of time in the project files, but it's always helpful to understand what's happening, regardless of whether you wrote the code yourself or not.

Before we can implement the JavaScript logic to update tasks, we need to formalize a way to uniquely identify each task that's created. Consider the example in the following image:

Two tasks sit in the To Do column.

If you were to click the Delete button under "Learn JavaScript," how would you programmatically know which task the button was referring to? Assigning an id to each task will help keep track of what's what.

CONNECT THE DOTS
Later on in your web development journey, you'll start using databases, such as MySQL, to store information. In database design, a unique id is crucial to ensure that the correct data is being updated or deleted. Databases can be set up to create that id for you, but understanding their value now will better prepare you for the future.

End of text box.
There are a few ways we could generate this id:

Use Math.random() to (hopefully) create a unique id each time we use it.

Get the current time in milliseconds and call that an id.

Create a counter that increments by one each time a task is created.

The third option more closely matches what a MySQL database would do, and it doesn't require any new JavaScript methods, so we'll use that.

At the top of script.js, declare a new variable by adding the following code:

var taskIdCounter = 0;
In the createTaskEl() function, we'll use this taskIdCounter variable to assign an id to the current task being created. How would we attach the id to an HTML element, though? There's always the id attribute, but we should be mindful that this attribute already serves a different purpose. The browser uses id to keep track of elements for CSS selectors, links, event listeners, and so on. It wouldn't be appropriate to use it for a counter value.

That's where data-* attributes come in. Also known as custom data attributes, these allow developers to store extra information about an HTML element without conflicting with any of the built-in attributes.

Watch the following video for an example of how to use data-* attributes:


For Taskinator, we'll add a data-task-id attribute to each <li> element. In the createTaskEl() function, update the code as follows:

var createTaskEl = function(taskDataObj) {
  var listItemEl = document.createElement("li");
  listItemEl.className = "task-item";

  // add task id as a custom attribute
  listItemEl.setAttribute("data-task-id", taskIdCounter);

  var taskInfoEl = document.createElement("div");
  taskInfoEl.className = "task-info";
  taskInfoEl.innerHTML = "<h3 class='task-name'>" + taskDataObj.name + "</h3><span class='task-type'>" + taskDataObj.type + "</span>";
  listItemEl.appendChild(taskInfoEl);

  tasksToDoEl.appendChild(listItemEl);

  // increase task counter for next unique id
  taskIdCounter++;
};
Because we're making HTML elements in JavaScript, we needed to use the DOM method setAttribute() to add our task id. The setAttribute() method can be used to add or update any attribute on an HTML element, but the only attribute we need for now is data-task-id, which we set to the current value of taskIdCounter.

PAUSE
When the first task is created, what will the value of its data-task-id attribute be?

Answer
At the bottom of the createTaskEl() function, we then increment the counter by one (i.e., by using taskIdCounter++) to keep each id unique.

Save script.js and refresh the browser. Make a few tasks, then use Chrome DevTools to inspect the DOM. You'll know everything's working correctly if you can see data-task-id attributes in the Elements panel, as shown in the following image:

Chrome DevTools show two <li> elements with data-task-id attributes.
Next, we'll add buttons and dropdowns that can reference a task's id.

Now that we have an id for each task, we can start adding buttons and dropdowns that reference each id. Remember, each task will have its own set of form elements that perform different actions, as shown in the following image:

A task element shows an Edit button, Delete button, and status dropdown.

Because the tasks themselves are dynamically created in JavaScript, these form elements will also need to be dynamically created. It will take several lines of code to make all of these elements, so let's offset that logic into its own function.

Add the following function below createTaskEl():

var createTaskActions = function(taskId) {

};
Note the parameter called taskId. This is how we can pass a different id into the function each time to keep track of which elements we're creating for which task.

In the createTaskActions() function, add the following lines of code to create a new <div> element with the class name "task-actions":

var actionContainerEl = document.createElement("div");
actionContainerEl.className = "task-actions";
This <div> will act as a container for the other elements.

After these lines, create two new <button> elements and append them to the <div> by adding the following code:

// create edit button
var editButtonEl = document.createElement("button");
editButtonEl.textContent = "Edit";
editButtonEl.className = "btn edit-btn";
editButtonEl.setAttribute("data-task-id", taskId);

actionContainerEl.appendChild(editButtonEl);

// create delete button
var deleteButtonEl = document.createElement("button");
deleteButtonEl.textContent = "Delete";
deleteButtonEl.className = "btn delete-btn";
deleteButtonEl.setAttribute("data-task-id", taskId);

actionContainerEl.appendChild(deleteButtonEl);
Note that textContent, className, and setAttribute() are properties and methods of the <button> elements. The appendChild() method will then add this <button> to the <div>.

These elements still only exist in memory, though, so nothing has changed on the page yet. It might seem like it's too soon to be able to test if this function is working, but we can at least verify that it returns the correct data.

Add a return statement to the bottom of the createTaskActions() function:

return actionContainerEl;
Here's the fun part: we're going to run this function directly in the browser to test it out. Open Chrome DevTools and navigate to the Console tab. In the console, type createTaskActions(5) and press Enter. The results should look like the following image:

DevTools Console shows a div element with two buttons inside.

In this example, we ran our function, passing in the number 5 to act as a fake id. The function did what it was supposed to, however, and returned a <div> element with two <button> elements inside. The buttons also have the correct class and data-task-id attributes. Looks like everything is good to go!

PRO TIP
The last thing we're missing in createTaskActions() is the dropdown, or to be exact, the <select> element. After the delete button is appended but before the return statement, add the following block of code:

var statusSelectEl = document.createElement("select");
statusSelectEl.className = "select-status";
statusSelectEl.setAttribute("name", "status-change");
statusSelectEl.setAttribute("data-task-id", taskId);

actionContainerEl.appendChild(statusSelectEl);
This will add an empty <select> element to the <div> container. But looking at our HTML file again, we know that <select> elements are made up of child <option> elements. We'll need to add three options to this dropdown: To Do, In Progress, and Completed. We could create and add these one after the other, but we'd end up with some very similar-looking code.

PAUSE
What JavaScript feature could you use to execute a block of code a certain number of times?

Answer
While a for loop isn't required to make these <option> elements, any chance to make the code more DRY is always welcome! To facilitate this looping, create the following array after the statusSelectEl expressions:

var statusChoices = ["To Do", "In Progress", "Completed"];
Using an array also provides the benefit of being able to easily add new options later on without changing much code. Another win for the DRY principle!

After the array declaration, write the following for loop logic:

for (var i = 0; i < statusChoices.length; i++) {
  // create option element
  var statusOptionEl = document.createElement("option");
  statusOptionEl.textContent = statusChoices[i];
  statusOptionEl.setAttribute("value", statusChoices[i]);

  // append to select
  statusSelectEl.appendChild(statusOptionEl);
}
REWIND
There are several pieces in that for loop that might warrant a refresher. Let's break it down:

var i = 0 defines an initial counter, or iterator, variable
i < statusChoices.length keeps the for loop running by checking the iterator against the number of items in the array (length being the property that returns the number of items)
i++ increments the counter by one after each loop iteration
statusChoices[i] returns the value of the array at the given index (for example, when i = 0, or statusChoices[0], we get the first item)
Try running the createTaskActions() function in the console again to verify that the <select> element is being created correctly:

DevTools console shows a div element with two buttons and a select list inside.

Now that we've verified that the function works, add the following lines to the createTaskEl() function, right before the tasksToDoEl.appendChild() method:

var taskActionsEl = createTaskActions(taskIdCounter);
console.log(taskActionsEl);
Note that we're using taskIdCounter as the argument now to create buttons that correspond to the current task id. Because createTaskActions() returns a DOM element, we can store that element in a variable (taskActionsEl). Console-logging the variable is another way to quickly verify that the function is working in this new context. Save your work and refresh the browser, then run the program to see if the element is logged to the console when you submit the form.

If the console.log() statement looks good, we can remove it and finalize our function by appending taskActionsEl to listItemEl before listItemEl is appended to the page:

var taskActionsEl = createTaskActions(taskIdCounter);
listItemEl.appendChild(taskActionsEl);

tasksToDoEl.appendChild(listItemEl);
Save script.js, refresh the browser, and make a few tasks. The tasks should now look like the following image:

A task element shows an Edit button, Delete button, and status dropdown.

If not, check the Chrome DevTools console for errors or use the script debugger to verify that functions and methods are being called in the right order. When you're happy with the results, save your progress with Git!




    4.3.7
Now we're ready to add interactivity to the buttons we just created, and we'll start with the Delete button. This won't be as straightforward as adding an event listener to the formEl.

In an ideal world, we could do something like what's shown in the following code:

var allButtonEls = document.querySelector(".delete-btn");
allButtonEls.addEventListener("click", myFunction);
However, the Delete buttons don't exist when the page first loads, so this would give us an error. Also, document.querySelector() returns the first element it finds on the page, meaning only the first Delete button would work.

One solution would be to add individual event listeners to the Delete buttons as we make them, as the following code demonstrates:

var deleteButtonEl = document.createElement("button");
deleteButtonEl.addEventListener("click", myFunction);
This might make our code harder to follow, though, and the number of event listeners we'd be creating could lead to memory leaks and performance issues down the road.

Fortunately, with event delegation, we can set up the click event listener on a parent element and then, through that single event listener, determine which child elements were clicked.

Clicks in JavaScript are a funny thing. If an element that has parent elements is clicked, the click event bubbles, or travels, upwards to its parents. Watch the following video to further explore this idea of event bubbling:


We'll eventually have Delete buttons in three different columns, so the most appropriate parent element to delegate this click responsibility to would be the <main> element. It currently has a class="page-content" attribute, which is used by our CSS to style the page. Let's add a new id="page-content" attribute to the main element, so that it has both class and id attributes with values of page-content, by adding the following code:

Start of code snippet<main class="page-content" id="page-content">End of code snippet
In script.js, add a reference to the page-content element at the top and then an event listener on it at the bottom of the file:

var pageContentEl = document.querySelector("#page-content");

// other logic...

pageContentEl.addEventListener("click", taskButtonHandler);
The addEventListener() method references a function that doesn't exist yet, so let's create that now. Add the following taskButtonHandler() function before the pageContentEl.addEventListener() call:

var taskButtonHandler = function(event) {
  console.log(event.target);
};
Notice that we're using a familiar friend, the event object. In this case, we're console-logging event.target. event.target reports the element on which the event occurs, in this case, the click event. Test the app in the browser and click on different elements inside page-content to see what event.target is each time, as shown in the following animation:

DevTools shows four different HTML elements logged in the console.

The event listener triggers not only when page-content itself is clicked but any element inside it (the <ul> lists, the <button> elements, etc.). Thanks to event.target, though, we can know exactly which element triggered the listener.

Test the app again and click on an Edit button, then click on a Delete button. You'll see that event.target is different in both cases:

Start of code snippet<button class="btn edit-btn" data-task-id="0">Edit</button>
<button class="btn delete-btn" data-task-id="0">Delete</button>End of code snippet
What uniquely identifies the Delete versus the Edit button? The Delete button has a class called .delete-btn on it. While it's easy to see that distinction in the console, how can we translate that into code? How could we check the class name on the element that was clicked?

We could use a property that we've used in the past, className, or there's a catch-all method called matches() that was created specifically for checking if an element matches certain criteria. The matches() method is similar to using the querySelector() method, but it doesn't find and return an element. Instead, it returns true if the element would be returned by a querySelector() with the same argument, and it returns false if it wouldn't.

Revise taskButtonHandler() to include the if statement shown in the following code:

var taskButtonHandler = function(event) {
  console.log(event.target);

  if (event.target.matches(".delete-btn")) {
    console.log("you clicked a delete button!");
  }
};
Save script.js and refresh the browser. Click on different elements again and verify that the second console.log() only happens if a Delete button is clicked, shown in the following image:

The console logged an Edit button, then a Delete button, then the message "you clicked delete".

Remember, the click event is always firing regardless of which elements are clicked, so it's up to us to capture the element that we actually care about. With the if statement in place, we now know exactly when a Delete button is clicked. The next problem to solve is knowing which task the Delete button belongs to. There could be tens or hundreds of Delete buttons on the page, but think about what we set up earlier that helps us uniquely identify them.

PAUSE
What HTML attribute holds the task's id?

Answer
Previously when we created these <button> elements, we used the setAttribute() method to set the data-task-id. Now we want to get that attribute. It's no coincidence that the method we'll use is getAttribute(). The getAttribute() method is available on any DOM element. Since event.target is a reference to a DOM element, we can use the method there as well.

Update taskButtonHandler() to console-log what this method returns, as shown in the following code:

var taskButtonHandler = function(event) {
  console.log(event.target);

  if (event.target.matches(".delete-btn")) {
    // get the element's task id
    var taskId = event.target.getAttribute("data-task-id");
    console.log(taskId);
  }
};
Test the app in the browser again and notice that the second console.log() returns a number that corresponds to the data-task-id attribute on the HTML element itself. The following image shows this:

The console shows two delete buttons logged, followed by each task id.

Now that we have the id, we can use it to remove the entire task from the DOM. While we could do that right here in the taskButtonHandler() function, it's good practice to follow the separation of concerns and do the actual deletion in its own function. It might seem like we're creating too many functions, but this does make the code easier to maintain and test.

Add a Delete Task Function
In script.js, create the following new function that uses taskId as a parameter:

var deleteTask = function(taskId) {
  console.log(taskId);
};
Then call this function from taskButtonHandler() by adding the following code:

if (event.target.matches(".delete-btn")) {
  var taskId = event.target.getAttribute("data-task-id");
  deleteTask(taskId);
}
Save script.js and try running this in the browser again by clicking the Delete button on a task. We should see a similar result as before, but now the console.log() printing our task item's id is coming from the deleteTask() function instead of our handler function.

PRO TIP
Now that we've captured the id of the task we want to delete, how do we go about actually deleting it? Luckily for us, the data-task-id attribute wasn't only applied to the Delete button; it's on the task's <li> element as well.

Update the deleteTask() function to include the following code:

var deleteTask = function(taskId) {
  var taskSelected = document.querySelector(".task-item[data-task-id='" + taskId + "']");
  console.log(taskSelected);
};
See that we're selecting a list item using .task-item and further narrowing the search by looking for a .task-item that has a data-task-id equal to the argument we've passed into the function. Also notice that there's no space between the .task-item and the [data-task-id] attribute, which means that both properties must be on the same element; a space would look for a element with the [data-task-id] attribute somewhere inside a .task-item element.

Now save script.js and run the code in the browser by clicking on a task item's Delete button. The following image shows how this looks in the console:

DevTools console shows an li element with multiple child elements.

Using querySelector() with a selector like .task-item[data-task-id='0'] allowed us to find a different element with the same data-task-id attribute. We used a similar method earlier when we wanted to get the values from our form elements. With the form, we selected the element type (input) and then specified what attribute we were looking to match (input[name='task-name']). Here, we are selecting the element by its class name, and then checking to see if it also has the specific data attribute value.

Now that we have the correct element, let's update deleteTask() one more time to actually remove it from the page. Add the following code to do that:

var deleteTask = function(taskId) {
  var taskSelected = document.querySelector(".task-item[data-task-id='" + taskId + "']");
  taskSelected.remove();
};
Again, save script.js and run this code in the browser to test the functionality. When a Delete button is clicked, the corresponding task item should be removed from the page entirely thanks to the aptly named remove() method.

Now that we've handled the functionality for capturing button clicks in our task list and deleting them, we can move on to editing a task.




4.3.8
    It's time to add the ability to edit an existing task. Let's take a step back and look at the big picture. Editing a task involves the following two actions:

            Loading the task's current information into the form.

            On form submit, updating the task element's content.

            Visualizing the problem as two separate issues can help keep it from feeling overwhelming. For now, we're only concerned with putting an existing task's data into the form. This happens any time an Edit button is clicked. However, Edit buttons present the same dilemma that Delete buttons did—there are too many of them.

            PAUSE
            How can you know when an Edit button is clicked?

            Answer
            Fortunately, we can leverage the work we did with deleting a task to facilitate this process. Edit buttons already have a data-task-id attribute, after all. Editing can also use the same taskButtonHandler() handler function as a starting point.

            Update taskButtonHandler() to accommodate both button clicks so that it resembles the following code:

            var taskButtonHandler = function(event) {
            // get target element from event
            var targetEl = event.target;

            // edit button was clicked
            if (targetEl.matches(".edit-btn")) {
                var taskId = targetEl.getAttribute("data-task-id");
                editTask(taskId);
            } 
            // delete button was clicked
            else if (targetEl.matches(".delete-btn")) {
                var taskId = targetEl.getAttribute("data-task-id");
                deleteTask(taskId);
            }
            };
            Add an Edit Task Function
            Similar to what you did with deleteTask(), add a new function for editing that creates its own taskSelected variables based on the provided taskId. The function should look like the following code:

            var editTask = function(taskId) {
            console.log("editing task #" + taskId);

            // get task list item element
            var taskSelected = document.querySelector(".task-item[data-task-id='" + taskId + "']");
            };
            If you haven't already, save and test the app in the browser. Clicking an Edit button should console-log the appropriate task id.

            We've also defined a taskSelected variable that references the entire <li> element. We don't need everything from this element, though. The only pieces of information we care about are the task's name and type. In the DOM, these are an <h3> element and a <span> element respectively:

            Start of code snippet<h3 class="task-name">Sample Task</h3>
            <span class="task-type">Mobile</span>End of code snippet
            We didn't add data-task-id attributes to these elements, so how do we find them? We already have the parent <li> element, so we can use that as a querySelector() starting point.

            Update the editTask() function to look like the following code:

            // get task list item element
            var taskSelected = document.querySelector(".task-item[data-task-id='" + taskId + "']");

            // get content from task name and type
            var taskName = taskSelected.querySelector("h3.task-name").textContent;
            console.log(taskName);

            var taskType = taskSelected.querySelector("span.task-type").textContent;
            console.log(taskType);
            In the past, we've used querySelector() with the document object, but any DOM element can use this method. document.querySelector() searches within the document element, which is the entire page, while taskSelected.querySelector() only searches within the tastSelected element. Thus, we can narrow our search to the task item at hand to find its name (h3.task-name) and type (span.task-type).

            Test the app in the browser to verify if the console.log() statements display the correct data.

            Now that we have the information we want, we can reuse the selectors from before to update the form. Delete the console.log() statements in the function, and then add the following lines of code after the var taskType expression:

            document.querySelector("input[name='task-name']").value = taskName;
            document.querySelector("select[name='task-type']").value = taskType;
            Save the script.js file again and refresh the browser. After creating a task, click the Edit button. If all is well, the task's name and type should appear in the form inputs, which is shown in the following image:

            The form inputs and task list item have the same content.

            To make it clear to the user that the form is now in "edit mode," we should also update the text of the submit button to say "Save Task".

            Add the following line to editTask():

            document.querySelector("#save-task").textContent = "Save Task";
            In the browser, the button text will change after an Edit button has been clicked. The following image shows the "Save Task" button:

            The form button says Save Task.

            This is a nice UI improvement for the user, but we also need some way for us, the developer, to know which task is currently being edited. So far, we've only added the task's name and type to the form. The id is lost, meaning when the user presses Save Task, where does that information go?

            Let's make one more addition to the editTask() function. Add the following code to include the task's id:

            formEl.setAttribute("data-task-id", taskId);
            This will add the taskId to a data-task-id attribute on the form itself. It's a new attribute that users won't see but that we can use later on to save the correct task.

            Test out the app again to ensure this works. To do that, refresh the form, create a task, then click edit. If you then examine the <form> element in the DOM display, it should contain the "data-task-id" and attribute corresponding to the task being edited, which is shown in the following image:

            DevTools highlighting the form element having a data-task-id attribute.

            Congratulations, we're almost done adding this new feature! We haven't finished adding the ability to edit a task, of course, but this is a good milestone that's worth committing with Git.


4.3.9

                    On our journey to update (i.e., edit) a task, we first had to load the task's information into the form. The next bit of logic will involve saving the task and changing the necessary DOM elements.

                PAUSE
                Because we're using the same form, how do we know when a new task is being created versus an old task being updated?

                Answer
                The data-task-id attribute that we added to the form will serve two purposes. One, it keeps track of which task we're editing. Two, its existence lets us know that, yes, a task is being edited in the first place. A handy way of knowing if an element has a certain attribute or not is to use the hasAttribute() method.

                Add the following lines to your existing taskFormHandler() function above the declaration for var taskDataObj at the end:

                var isEdit = formEl.hasAttribute("data-task-id");
                console.log(isEdit);
                With the DevTools console open, first create a new task, then edit a task and click the Submit button. (Remember, every time we submit, we run the taskFormHandler function.) When we submit the form to create a new task, isEdit will be false, and false will display in the console. When we submit after editing, isEdit will be true, and true will display in the console. Awesome—this means we can use the same form handler for new and old tasks!

                Let's now do two things. First, delete the console.log() beneath isEdit. Then, replace createTaskEl(taskDataObj); with the following block of code, which wraps the createTaskEl() call and taskDataObj variable in an if/else statement (make sure that it follows the isEdit variable initialization):

                // PUT THIS BELOW `var isEdit = ...` in `taskFormHandler()`

                // has data attribute, so get task id and call function to complete edit process
                if (isEdit) {
                var taskId = formEl.getAttribute("data-task-id");
                completeEditTask(taskNameInput, taskTypeInput, taskId);
                } 
                // no data attribute, so create object as normal and pass to createTaskEl function
                else {
                var taskDataObj = {
                    name: taskNameInput,
                    type: taskTypeInput
                };

                createTaskEl(taskDataObj);
                }
                This way, createTaskEl() will only get called if isEdit is false. If it's true, we'll call a new function, completeEditTask(), passing it three arguments: the name input value, type input value, and task id.

                Let's create the completeEditTask() function now. Write the following function in the main body of the JavaScript file:

                var completeEditTask = function(taskName, taskType, taskId) {
                console.log(taskName, taskType, taskId);
                };
                At this point, the function logs the parameters to the console so we can verify that it is working and getting the data it needs. To check this, restart the app, create a task, select edit to bring it into the form fields, then submit. If all went well, the taskNameInput, taskTypeInput, and taskId will be logged to the console.

                We'll use taskId to find the correct <li> element and use taskName and taskType to update the <li> element's children accordingly.

                Replace the console.log() in completeEditTask() with the following code:

                // find the matching task list item
                var taskSelected = document.querySelector(".task-item[data-task-id='" + taskId + "']");

                // set new values
                taskSelected.querySelector("h3.task-name").textContent = taskName;
                taskSelected.querySelector("span.task-type").textContent = taskType;

                alert("Task Updated!");
                Also reset the form by removing the task id and changing the button text back to normal by adding the following code below the alert():

                formEl.removeAttribute("data-task-id");
                document.querySelector("#save-task").textContent = "Add Task";
                By removing the data-task-id attribute, we ensure that users are able to create new tasks again. Try it out in the browser, switching between making tasks and editing existing tasks. If anything seems off, check the console for errors. An error like Uncaught TypeError: Cannot set property 'textContent' of null, for instance, suggests one of the selectors is wrong.

                One opportunity for a bug lies in the querySelector in the code above, if you were to make a minor typo. h3.task-name isn't the same as h3 .task-name: the former looks for <h3> elements with a class of task-name, whereas the latter looks for elements with a class of task-name that are descendent elements of an <h3> element. The latter would return null, and because there is no textContent property on null, the browser itself would report an error message in the console.






                            4.3.9.

                            There's still one last method in which a task can be updated. Tasks have a status—To Do, In Progress, Completed—that isn't updated through the main form but rather through individual <select> elements. Changing the value of the <select> element should automatically move the task from one column to another, as you can see in the following image:

A To Do, In Progress, and Completed column sit side by side.

Because we'll be interacting with the remaining two columns, add the following two new variables at the top of script.js to reference them:

var tasksInProgressEl = document.querySelector("#tasks-in-progress");
var tasksCompletedEl = document.querySelector("#tasks-completed");
We technically already have a click event listener set up for the tasks' <select> elements thanks to the event delegation of taskButtonHandler(), which listens to events on the entire <main> element of the document. This click event doesn't really help us here, though, because a <select> click only fires on the initial click. Depending on the browser, the second click to choose an option fires on the <option> element instead of the <select> element. That sounds like a bigger headache to sort out than it's worth.

Thankfully, there are more events besides click and submit that we can tap into. There's also a change event that triggers, as the name implies, any time a form element's value changes. Like our Delete and Edit clicks, though, we'll need to delegate this event because it applies to multiple elements.

At the bottom of script.js, add a new event listener:

pageContentEl.addEventListener("change", taskStatusChangeHandler);
Alongside your other functions, define the following new function to handle this event:

var taskStatusChangeHandler = function(event) {

};
PAUSE
On the event object, how do you get the element that triggered the event?

Answer
In the taskStatusChangeHandler() function, console-log event.target and event.target.getAttribute("data-task-id"). When you click on and change the value of the <select> element in a task item, you should see the following in the DevTools:

DevTools console shows a select element and an id of zero.

event.target is a reference to a <select> element, meaning we can use additional DOM methods to get this element's properties. We'll want the id so we can find the overall task item, and we'll want the value of the <select> element to know which other column to move it to.

Update the function to create the following variables:

var taskStatusChangeHandler = function(event) {
  // get the task item's id
  var taskId = event.target.getAttribute("data-task-id");

  // get the currently selected option's value and convert to lowercase
  var statusValue = event.target.value.toLowerCase();

  // find the parent task item element based on the id
  var taskSelected = document.querySelector(".task-item[data-task-id='" + taskId + "']");
};
Converting the value to lowercase might seem unnecessary, but it helps future-proof the app in case we ever changed how the status text is displayed. Code-wise, we know we'll always check against the lowercase version. Based on whatever the value is, we can move the taskSelected element from one column to another.

Add the following if statements to the end of the taskStatusChangeHandler() function:

if (statusValue === "to do") {
  tasksToDoEl.appendChild(taskSelected);
} 
else if (statusValue === "in progress") {
  tasksInProgressEl.appendChild(taskSelected);
} 
else if (statusValue === "completed") {
  tasksCompletedEl.appendChild(taskSelected);
}
Remember that tasksToDoEl, tasksInProgressEl, and tasksCompletedEl are references to the <ul> elements created earlier. Thus, if the user selects "In Progress" from the dropdown, it will append the current task item to the <ul id="tasks-in-progress"> element with the tasksInProgressEl.appendChild(taskSelected) method.

The interesting thing about the use of appendChild() here is that it didn't create a copy of the task. It actually moved the task item from its original location in the DOM into the other <ul>. It's important to note that the variable taskSelected didn't create a second <li>. That would only be the case if we used document.createElement(). Instead, it's a reference to an existing DOM element, and we simply appended that existing element somewhere else.

Save and test the app in the browser to make sure the tasks move to the correct column when the dropdown changes. If it does, take a moment to appreciate what you've accomplished.


4.4.1
            - intro
            .2
            - preview
            -  Adding persistence with localStorage will enable us to keep tasks in their corresponding status lists after refreshing the page. The following animation shows the tasks persisting through a page refresh:

            Cursor clicks the page refresh icon to reload Taskinator, and the tasks remain in their lists.

            The UI and core functionality won't change, but this new feature will make Taskinator more usable. To make this possible, we'll need to restructure the app's data to make it easier to save and retrieve from localStorage.

            Let's consider the best approach to accomplishing this goal:

            Create a feature branch. We'll create a feature branch that corresponds to the GitHub issue we're addressing in this lesson.

            Save tasks to an array. We'll organize all the elements that correspond to a task into an object, and save those objects into an array.

            Save tasks to localStorage. We'll implement the ability to save our tasks to localStorage so that they can be retrieved later.

            Load tasks from localStorage. We'll add the ability to retrieve saved tasks from localStorage.

            Optimize the code. We'll reduce our technical debt by refactoring the code. This is a best practice and a good habit to develop.

            Save our progress with Git. We'll merge the feature branch into the develop branch and push our changes to GitHub.

            Deploy to GitHub Pages. We'll deploy our finished application to GitHub Pages so we can show it off to the world and use it anywhere!

            In the first part of the lesson, we'll set up the localStorage functionality. During that process, we'll be creating similar functionality to code we've written earlier. At that point, we could leave the code as it is, but that would be missing a good opportunity to refactor it so that we can reuse the existing functionality. Therefore, the latter part of the lesson will be devoted to refactoring the code and deploying the app to GitHub Pages.

            Let's get started by creating a feature branch for the issue.

        .3 : creating a new branch

            Let's review the GitHub issue pertaining to this feature one more time, and then create the feature branch. The following image shows the issue we're working on:

            GitHub issue for persistence.

            Because this issue is about persistence, let's call the feature branch feature/task-persistence. We'll create it now from the command line by following these steps:

            Use git branch to ensure that we're in the develop branch, as we want to build on that branch's code.

            Create a new branch for this feature by using the following command:

            git checkout -b feature/task-persistence
            As we know, this command creates the branch and moves us into it, but we can use git branch one more time just to double-check.

            Now that we've confirmed that we're in the correct branch, let's get started!

        .4 : save tasks to an array. 

            Currently, all the data associated with a task is kept with its respective DOM element on the page. This means that if we were to try to save this data to localStorage, we'd have to find every task item and pull the important data from it. We can't use a querySelector() method to save the entire task item element to localStorage because localStorage can only save data as a string, and it is difficult to convert DOM elements to strings.

            This all indicates that the task data is set up in a way that's difficult to organize and store, so we'll need a different storage solution. This solution should package each task's id, name, type, and status together, as shown in the following code:

            var taskDataObj = {
            id: 1,
            name: "Add localStorage persistence",
            type: "Web",
            status: "in progress"
            }
            The good news is that we started the process of organizing task data into an object in a previous lesson when we sent the task's data from taskFormHandler() to createTaskEl() as an argument. Now we just need to update that object to hold more information.

            We'll have more than one task to store, obviously, so creating a variable for each task isn't maintainable or practical.

            PAUSE
            How might we keep a list of the task objects in one variable?

            Answer
            Our solution will be to create a new variable in script.js to hold an array of task objects, as shown in the following code example:

            var tasks = [
            {
                id: 1,
                name: "Add localStorage persistence",
                type: "Web",
                status: "in progress"
            },
            {
                id: 2,
                name: "Learn JavaScript",
                type: "Web",
                status: "in progress"
            },
            {
                id: 3,
                name: "Refactor code",
                type: "Web",
                status: "to do"
            }
            ];
            Create a Tasks Array Variable
            The tasks array will look like the preceding code only after we start adding tasks to it. To get there, let's start by creating an empty array variable. Add the following code towards the top of the script.js file where you declared other variables:

            var tasks = [];
            We've created an empty tasks array. Now when we create a new task, the object holding all of its data can be added to the array. We just need to update the object that holds the task's data to also include its id and status, both of which are only written to the associated DOM element.

            In the taskFormHandler() function, let's update the taskDataObj variable to include a status property. Because this data gets sent to createTaskEl(), we can safely assume that the status will always have a value of to do. This is because a task that has just been created cannot possibly be in progress or complete yet.

            Update the taskDataObj variable to look like the following code:

            var taskDataObj = {
            name: taskNameInput,
            type: taskTypeInput,
            status: "to do"
            }
            Let's test this and add a console.log() into the createTaskEl() function. This will help us ensure that the new property gets to the function via the taskDataObj parameter that we set up.

            In createTaskEl(), add the following code anywhere in the function:

            console.log(taskDataObj);
            console.log(taskDataObj.status);
            Save script.js, refresh the app in the browser, and submit a new task. The following image shows what these two console.log() functions look like in the console:

            Console showing the Task object passed into function.

            As we can see, createTaskEl() now receives this new status property in its taskDataObj parameter.

            The only thing missing from the task's object now is its id. Luckily, we already have the value of the id in the taskIdCounter variable and are using it in the createTaskEl() function. We need to add that value as a property to the taskDataObj argument variable and add the entire object to the tasks array.

            After listItemEl.appendChild(taskInfoEl); and before taskIdCounter++;, update createTaskEl() with the following code:

            taskDataObj.id = taskIdCounter;

            tasks.push(taskDataObj);
            Syncing the Object Array with the GUI/DOM
            Remember, we're now managing two task lists: one in the visible GUI that's represented in the DOM, and one only found in our code in the form of an array of objects. So when we edit or delete a task in the GUI/DOM, we need to do the same to the object that represents it in our array. This syncs the array data that we'll be putting in localStorage with the GUI/DOM data.

            We did this by adding an id property to the taskDataObj argument and giving it the value of whatever taskIdCounter is at that moment. This way, the id of the newly created DOM element gets added to the task's object as well. We can use that id later to identify which task has changed for both the DOM and the tasks array.

            IMPORTANT
            Just as we can reassign the value of an object property, we can also create new properties as needed.

            Once we gave the task its id value, we had to get that object into the tasks array, so we used an array method called push(). This method adds any content between the parentheses to the end of the specified array.

            Developers use this method a lot, so let's look at the following examples of how it could be used in Taskinator:

            var pushedArr = [1, 2, 3];

            pushedArr.push(4); 
            // pushedArr is now [1,2,3,4]

            pushedArr.push("Taskinator"); 
            // pushedArr is now [1,2,3,4,"Taskinator"]

            pushedArr.push(10, "push", false); 
            // pushedArr is now [1,2,3,4,"Taskinator",10,"push",false]
            DEEP DIVE
            This update won't yield any visible differences on the page, but we can still test to make sure it works.

            Save script.js, refresh the page, and create a task or two. Then, in the Chrome DevTools console, type console.log(tasks). Pressing Enter to run the log function should return a printed list of the tasks in an array of objects, as shown in the following image:

            Tasks array in the console.

            Now the tasks array stores any tasks we add to the page, along with all their important information.

            So we've added the ability to save a task not only to the page but in the array as well. Because we also update and remove tasks as well as add them, we'll have to update the completeEditTask(), taskStatusChangeHandler(), and deleteTask() functions too.

            Find and Edit Array Data
            To sync the data presented by the DOM with the data stored in the tasks array, we’ll change the functions for updating and deleting tasks in the DOM so that they also update and delete tasks in the tasks array.

            We'll do this by looking up the task in the array by its id value. Then we'll update its object properties or remove it from the task array entirely. How do we find an element in an array by its id? We'll have to check each task in the array for an id property equal to the updated id of the task.

            In the completeEditTask() function, add the following for loop after the two querySelector() methods so that it looks like the following code:

            // THIS CODE IS ALREADY IN PLACE
            taskSelected.querySelector("h3.task-name").textContent = taskName;
            taskSelected.querySelector("span.task-type").textContent = taskType;

            // loop through tasks array and task object with new content
            for (var i = 0; i < tasks.length; i++) {
            if (tasks[i].id === parseInt(taskId)) {
                tasks[i].name = taskName;
                tasks[i].type = taskType;
            }
            };
            At each iteration of this for loop, we are checking to see if that individual task's id property matches the taskId argument that we passed into completeEditTask(). There is one problem: taskId is a string and tasks[i].id is a number, and when we compare the two, we need to make sure that we are comparing a number to a number. This is why we wrap the taskId with a parseInt() function and convert it to a number for the comparison.

            If the two id values match, then we've confirmed that the task at that iteration of the for loop is the one we want to update, and we've reassigned that task's name and type property to the new content submitted by the form when we finished editing it.

            PRO TIP
            Now that we've gotten the completeEditTask() function to update the task array, let's turn our attention to the other functions that deal with updating tasks, starting with taskStatusChangeHandler(). In completeEditTask(), we focused on updating a task's name or type. Here, we only need to worry about updating a task's status. Let's use a for loop again, but with a different property to reassign.

            At the bottom of the taskStatusChangeHandler() function, add the following code:

            // update task's in tasks array
            for (var i = 0; i < tasks.length; i++) {
            if (tasks[i].id === parseInt(taskId)) {
                tasks[i].status = statusValue;
            }
            }
            Add another console.log(tasks); after the for loop so we can verify that it's working. Save script.js, create a task, and update its status through the task's <select> dropdown. After this, the console should display an updated tasks array reflecting that task's new status.

            That wraps it up for taking care of updating tasks! Next, we'll delete them from the tasks array.

            Delete a Task from the Array
            Just as we used a for loop to identify and update a task's information, we'll use a for loop to identify a task that we want to remove. Because we're removing a task, however, we'll need to take a couple of extra steps to get there.

            Find the deleteTask() function and add the following code to the bottom of it:

            // create new array to hold updated list of tasks
            var updatedTaskArr = [];

            // loop through current tasks
            for (var i = 0; i < tasks.length; i++) {
            // if tasks[i].id doesn't match the value of taskId, let's keep that task and push it into the new array
            if (tasks[i].id !== parseInt(taskId)) {
                updatedTaskArr.push(tasks[i]);
            }
            }

            // reassign tasks array to be the same as updatedTaskArr
            tasks = updatedTaskArr;
            Let's back up and explore what we're doing here. When we updated a task's information, all we had to do was overwrite its data. We didn't have to worry about creating something new, because were just modifying something that already existed. When we delete a task, however, we essentially have to create a new array of tasks that is identical to our current one, except it won't receive the task we're deleting.

            Here, we created a new empty array variable called updatedTaskArr. When we iterate through the current tasks array, we check to see if the current task in the loop (for example, tasks[i]) does not have the same id value as the task we want to delete. If it's not the same task, then we know we should keep it, so we use the .push() method to add that task to the updatedTaskArr array.

            When we're done with the for loop, our updatedTasksArr will be almost the same as the tasks array, except it won't have the task we want removed. Because we need to keep the tasks array variable up-to-date at all times, we reassign the tasks variable to updatedTasksArr so that they are now the same and do not contain the deleted task.

            We just learned a lot of code for functionality that doesn't affect the page, but remember our end goal: storing all of the task's data as a JavaScript array will make it easier to save that data to localStorage.

            This is a good time to add, commit, and push your code to the GitHub feature branch before moving on.
