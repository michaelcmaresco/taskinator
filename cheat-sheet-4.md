Module - 4 - Web API's
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