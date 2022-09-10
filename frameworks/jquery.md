# JQuery

lightweight, "write less, do more", JavaScript library. Common tasks that require many lines of JS are wrapped into methods that are called with a single line:

* HTML/DOM manipulation
* CSS manipulation
* HTML event methods
* Effects and animations
* AJAX
* Utilities

***

## Adding JQuery to a project

* Download the jQuery library from jQuery.com
  * ```
    npm install jquery
    ```
  *
* Include jQuery from a Google CDN. This will lead to faster load time.
  *
* #### Functions In A Separate File
  * you can put your jQuery functions in a separate .js file:
  * ```js
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="my_jquery_functions.js"></script>
    ```

***

## JQuery Syntax

### $(selector).action( )

* _**$**_ - define/access jQuery
* _**(selector)**_ - uses CSS syntax to select elements. ("#id"), (".class") ("tag")
* _**action( )**_ - to be performed on the element(s)

***

## JQuery Selectors

* $("\*") - selects all elements
* $(this) - selects the current HTML element
*   $("p.intro") - selects all

    with class="intro"
*   $("p.first") - selects first

    element
* $("ul li:first") - Selects the first
*   element of the first

    * $("\[attribute]") - selects all elements with a attribute
    *   $("p\[target='\_blank']") - selects all

        with a specified target value
    * $("tr:even") - Selects all even elements
    * $("tr:odd") - Selects all odd elements

    [Reference](https://www.w3schools.com/jquERy/jquery\_selectors.asp)

    ***

    ### JQuery Events

    The term **"fires/fired"** is often used with events. ie. "The keypress event is fired, the moment you press a key". ie:

    ```js
    $("p").click( function() {
      // action goes here
    });
    ```

    _Mouse Events_:

    * **click** - when the user _clicks_ on the HTML element
    * **dblclick** - when the user _double-clicks_ on the HTML element
    * **mouseenter** - when the cursor enters \[_hover over_] the HTML element
    * **mouseleave** - when the cursor leaves \[_hover out_] the HTML element
    *   **hover** - combo of mouse-enter & mouse-leave. Requires 2 functions.

        ```js
        $("#p1").hover(function(){
          alert("enter");
        },
        function(){
          alert("leave");
        });
        ```

    _Keyboard Events_:

    * **keypress** - when a keypress event occurs.
    * **keydown** - when the key is pressed down.
    * **keyup** - when the key is released.

    _Form Events_:

    * **submit** - when a form is submitted (press of submit button)
    * **change** - when the value of an element has been changed (only for , ,  )
    * **focus** - when the form field gets _focus_ (input field is clicked on)
    * **blur** - when the form field _loses focus_

    _Document/Window Events_:

    * **load** - deprecated and removed. There's also an AJAX method named load().
    * **resize** - when the browser window _changes size_.
    * **scroll** - when the user _scrolls_ in the specified element.
    * **unload** - deprecated and removed.

    [More events](https://www.w3schools.com/jquERy/jquery\_ref\_events.asp)

    #### The on() Method - multiple events

    *   attaches one or more event handlers for the selected elements

        ```js
        $("p").on({
          mouseenter: function(){
            $(this).css("background-color", "lightgray");
          }, 
          mouseleave: function(){
            $(this).css("background-color", "lightblue");
          }, 
          click: function(){
            $(this).css("background-color", "yellow");
          } 
        });
        ```

    ***

    ### The Document Ready Event

    Most people put all jQuery methods inside a document ready event to prevent any jQuery code from running before the document is finished loading (is ready).

    ```js
    $(document).ready(function(){
    		// jQuery methods go here...
    });
    ```

    ***

    ### JQuery Effects

    #### Hide and Show

    * you can hide and show HTML elements with the `hide()` and `show()` methods.

    ```js
    // a button has id="hide", and another has id="show", when clicked, all <p> are either hiden or shown.
    $("#hide").click(function(){
      $("p").hide();
    });

    $("#show").click(function(){
      $("p").show();
    });
    ```

    *   #### Optional Speed Parameter

        The optional speed parameter specifies the speed of the hiding/showing, and can take the following values: _"slow"_, _"fast"_, or a value in ms (milliseconds):

        ```js
        // when a <button> is clicked, all <p> tags get hidden over 1000ms (1s)
        $("button").click(function(){
          $("p").hide(1000);
        });
        ```

    #### Fade

    you can fade elements in\&out of visibility. All of the below methods have an optional speed parameter as explained above.

    * **fadeIn( \[speed] )** - used to _fade in_ a hidden element.
    * **fadeOut( \[speed] )** - used to _fade out_ a hidden element.
    * **fadeToggle( \[speed] )** - toggles b/n fadeIn and fadeOut. If elements are faded out, fadeToggle will fade them in. vice verca.
    * **fadeTo( \[speed], opacity )** - allows fading to a given opacity (0 < x < 1 opaque)

    #### Sliding

    slide elements up and down

    * **slideDown( \[speed] )** - used to _slide down_ an element
    * **slideUp( \[speed] )** - used to _slide up_ an element
    * **slideToggle( \[speed] )** - toggles b/n slideDown and slideUp. If elements have been slid down, slideToggle will slide them up. vice verca.

    #### Animation - skipped, and the stop() method which stops animations.

    ***

    ### JQuery Callback Functions

    All of the above event functions also have a second '_callback function_' parameter, which is basically a function which is executed/called after the current effect is finished.

    With effects, the next line can be run even though the effect is not finished. This can create errors. To prevent this, use a callback function. A callback function is executed after the current effect is finished.

    ```js
    $("button").click(function(){
    		$("p").hide("slow", function(){
        	alert("The paragraph is now hidden");
      	});
    });
    ```

    ***

    ### JQuery Chaining

    you can chain together actions/methods. Chaining allows us to run multiple jQuery methods (on the same element) within a single statement. Basically method chaining.

    ie. chain together _**css() ,slideUp(), slideDown()**_ : the element first changes to red, then slides up, then slides down:

    ```js
    $("#p1").css("color", "red").slideUp(2000).slideDown(2000);

    // same thing as above, but cleaner syntax:
    $("#p1").css("color", "red")
      .slideUp(2000)
      .slideDown(2000);
    ```

    ***

    ### jQuery DOM Manipulation

    JQuery has methods for changing and manipulating HTML elements and attributes.

    ### JQuery Get

    #### Get Content

    * **element.text()** - sets/returns inner text of selected element.
    * **element.html()** - sets/returns inner html of selected element.
    * **element.val()**- sets/returns the value from form fields.

    ```js
    $("#id").text()
    ```

    #### Get Attributes

    * **element.attr("attributeName")** - gets the value of an attribute.

    ### JQuery Set

    #### Set Content

    ```js
    // .text/html/val("updated")
    $("#id").text("Updated Text");
    ```

    #### Set Attributes

    ```js
    // .attr(attrName, newValue)
    $("#link").attr("href", "https://www.google.com");

    // set multiple attributes at the same time
    $("#link").attr({
        "href" : "https://www.google.com",
        "title" : "Google"
    });
    ```

    ##

    ### JQuery Add

    With JQuery, it's easy to add new elements/content.

    #### Add New HTML Content

    * **`.append()`** - Inserts _at the end_ of the selected elements
    * **`.prepend()`** - Inserts _at the beginning_ of the selected elements
    * **`.after()`** - Inserts _after_ the selected elements
    * **`.before()`** - Inserts _before_ the selected elements

    ```js
    // adds new li at the end of the list
    $("ol").append("<li>Appended item</li>");

    // adds new li at the beginning of the list
    $("ol").prepend("<li>Prepended item</li>");
    ```

    ![Modifying the document](https://javascript.info/article/modifying-document/before-prepend-append-after.svg)

    #### Adding Multiple Elements

    *   All 4 methods can take an infinite number of new elements as parameters:

        ```js
        // create elements in 3 ways and append them all at once
        var txt1 = "<p>Text.</p>";               // Create element with HTML  
        var txt2 = $("<p></p>").text("Text.");   // Create with jQuery
        var txt3 = document.createElement("p");  // Create with DOM

        $("body").append(txt1, txt2, txt3);
        ```

    ### JQuery Remove

    * **`.remove( [selector] )`** - removes the selected element(s) and its child elements
    *   **`.empty()`** - removes the child elements of the selected element(s).

        ```js
        $("#div1").remove();
        $("#div1").empty();

        // removes all <p> elements with class="test"
        $("p").remove(".test");
        // removes all <p> elements with class="test" or class="demo"
        $("p").remove(".test, .demo");
        ```

    ***

    ### JQuery CSS Classes

    With jQuery, it is easy to manipulate the style of elements

    #### jQuery Manipulating CSS

    *   **`addClass()`** - Adds 1 or more classes to the selected elements' attributes.

        ```js
        // in css file--> .blue {color: blue}, .bold{font-weight: bold}

        // adds the 'blue' class to all h1, h2, and p, making their text color, blue.
        $("h1, h2, p").addClass("blue");

        // multiple classes as well as multiple elements
        $("h1, h2, p").addClass("blue bold");
        ```
    *   **`removeClass()`** - removes a specific class attribute from elemnt(s)

        ```js
        // h1, h2, and p elements no longer have a 'blue' class
        $("h1, h2, p").removeClass("blue");
        ```
    *   **`toggleClass()`** - adds a class if an element doesn't have it, removes a class if it does have it.

        ```js
        // if h1/h2/p have class="blue", it gets removed, otherwise added.
        $("h1, h2, p").toggleClass("blue");
        ```

    ### JQuery css()

    sets/returns 1 or more style properties for selected element(s).

    #### Return a CSS property

    *   **`.css("propertyName")`** - returns the value of the css property specified

        ```js
        // returns the background-color value of the FIRST <p>
        $("p").css("background-color");
        ```

    #### Set a CSS property

    *   **`css("propertyName", "value")`** - sets the value of the css property specified

        ```js
        // sets the background-color value for ALL <p>
        $("p").css("background-color", "yellow");
        ```
    *   Setting multiple properties:

        ```js
        $("p").css({
          "background-color": "yellow",
          "font-size": "200%"
        });
        ```

    ***

    ### JQuery Dimensions

    ![jQuery Dimensions](https://www.w3schools.com/jquERy/img\_jquerydim.gif)

    * **`.width()`** - sets/returns the width of the element (excl. padding/border/margin)
    * **`.height()`** - sets/returns the height of the element (excl. padding/border/margin)
    * **`.innerWidth()`** - returns the width of an element (including padding)
    * **`.innerHeight()`** - returns the height of an element (including padding)
    * **`.outerWidth()`** - returns the width of an element (includes padding+border).
    * **`.outerHeight()`** - returns the height of an element (includes padding+border).
    * **`.outerWidth(true)`** - returns the width of an element (includes padding, border, margin).
    * **`.outerHeight(true)`** - returns the height of an element (includes padding, border, margin).

    Misc:

    * `$(document).width/height()` returns the width/height of the document.
    *   `$(window).width/height()` returns the width/height of the window.

        ```js
        // sets the width and height of a specified <div> element. Parameter unit is px.
        $("#div1").width(500).height(500);
        ```

    ***

    ### JQuery AJAX

    _AJAX_ = Asynchronous JavaScript and XML.

    AJAX is about loading data in the background and displaying it on the webpage, without reloading the whole page.

    With the jQuery AJAX methods, you can request text, HTML, XML, or JSON from a remote server using both HTTP Get and HTTP Post - And you can load the external data directly into the selected HTML elements of your web page!

    #### JQuery load()

    rrrloads data from a server and puts the returned data into the selected element

    `$(selector).load(URL, [data], [callback]);`

    * _**URL**_ - URL you wish to load.
    * _**data**_ - optional parameter specifies a set of querystring key/value pairs to send along with the request.
    *   _**callback**_ - callback function. The callback has 3 parameters:

        * `responseTxt` - contains the resulting content if the call succeeds
        * `statusTxt` - contains the status of the call ('success'/'error')
        * `xhr` - contains the XMLHttpRequest object

        ```js
        // loads the content of an external file named 'demo_test.txt' into a specific div.
        $("#div1").load("demo_test.txt");

        // loads content of the element with id="p1", INSIDE the demo_test file, INTO a specific div.
        $("#div1").load("demo_test.txt #p1")

        // callback usage
        $("#div1").load("demo.txt", function(responseTxt, statusTxt, xhr) {
            if(statusTxt == "success")
            		alert("External content loaded successfully!");
            if(statusTxt == "error")
              	alert("Error: " + xhr.status + ": " + xhr.statusText);
        });
        ```

    #### get() and post()

    Two commonly used methods for a request-response between a client and server are: GET and POST:

    * **GET** - Requests data from a specified resource
    * **POST** - Submits data to be processed to a specified resource (can also act as GET)

    **`$.get(URL, [callback])`** - requests data from the server with an HTTP GET request.

    * URL - URL you wish to request.
    * callback - optional callback function.

    ```js
    // retrieve data from a file on the server
    $.get("demo_test.asp", function(data, status) {
        alert("Data: " + data + "\nStatus: " + status);
    });
    ```

    **`$.post(URL, data, [callback])`** - requests data from the server using an HTTP POST request.

    * URL - URL you wish to request.
    * data - optional parameter is some data to send along with the request.
    * callback - optional callback function.

    ```js
    // send some data along with the request
    $.post("demo_test_post.asp",
      {
        name: "Donald Duck",
        city: "Duckburg"
      },
      function(data, status){
        alert("Data: " + data + "\nStatus: " + status);
    });
    ```

    ***

    ### JQuery noConflict()

    jQuery uses the `$` sign as a shortcut for jQuery.

    What if you want to use another JavaScript framework along with JQuery. What if those frameworks also use the $ sign as a shortcut? One of the frameworks' shortcut might stop working.

    The **`noConflict()`** method releases the hold on the $ shortcut identifier, so that other scripts can use it.

    You can of course still use "jQuery", simply by writing the full name instead of the shortcut:

    ```js
    $.noConflict();

    jQuery(document).ready(function(){
      	jQuery("button").click(function(){
        		jQuery("p").text("jQuery is still working!");
      	});
    });
    ```

    #### Custom shortcut for $

    You can also create your own shortcut very easily:

    ```js
    // the $ shortcut is now jq
    var jq = $.noConflict();

    jQuery(document).ready(function(){
      	jQuery("button").click(function(){
        		jQuery("p").text("jQuery is still working!");
      	});
    });
    ```

    ***

    ### JQuery Filters

    Use jQuery to filter/search for specific elements.

    #### Filter Tables

    *   Perform a case-insensitive search for items in a table:

        ```js
        $(document).ready(function(){
          $("#myInput").on("keyup", function() {
            var value = $(this).val().toLowerCase();
            $("#myTable tr").filter(function() {
              $(this).toggle($(this).text().toLowerCase().indexOf(value) > -1)
            });
          });
        });
        ```

    ***

    ### JQuery Traversing DOM Tree

    #### Ancestors

    * An ancestor is a parent, grandparent, great-grandparent, and so on.
    * **`parent()`** - returns the direct parent element of the selected element.
