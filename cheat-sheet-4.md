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

