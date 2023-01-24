# Assignment 0: JQuery AJAX Field Autocomplete

Autocomplete automatically provides contextual completion suggestions during data input. In this assignment, you will complete a small application to provide autocomplete suggestions for a country input box.

To get this working:
* A key-up event must be attached to the field in order to make a JavaScript call when new data is input into the country input.
* This function will in turn use JQuery functions to make an AJAX call to a service that provides a list of values matching a provided keyword. In the AJAX call, we will also set a callback function to take action when the AJAX function received a response.
* The callback function will parse the response and make the suggestions be rendered in a div below the input box.

## Instructions

* If you have not done so in the past, create your GitHub account.
* Create a new GitHub repository for eCommerce Assignment 0.
* Invite your teacher (paquettm) as a contributor.
* Progressively implement and commit the requested application feature by feature.

### HTML

The HTML for this assignment contains the following elements:
* The JQuery 3.6.3 library is loaded from JQuery.com.
* There is a text input with the name and id "country".
* A div below the text input will receive completion suggestions.
Complete the code provided below.

```
<html>
<head>
<title>jQuery AJAX Country Autocomplete</title>
<script src="https://code.jquery.com/jquery-3.6.3.min.js" integrity="sha256-pvPw+upLPUjgMXY0G+8O0xUf+/Im1MZjXxxgOcBQBXU=" crossorigin="anonymous"></script>
<script>
// TODO: insert the later-detailed JavaScript
</script>
<style>
/* TODO: insert CSS to display things correctly */
</style>
</head>
<body>
    <div class="container">
        <h1>jQuery-AJAX Country Autocomplete</h1>
    
        <!-- TODO: insert a text input box with the name country and id country -->
        <!-- to give users instructions, the placeholder data should be "Country name" -->
        <!-- TODO: insert a div with id country-suggestion and class suggestion-box -->
        <p>Write the name of the country in the text input above to search for a country. Then when you see the country of your liking, click on it to automatically complete the input.</p>
    </div>
</body>
</html>
```

### CSS

To display autocomplete suggestions correctly, set the CSS for the suggestion-box class such that 
* positioning is absolute
* the background color is white
* there is a border with 1px width, #333333 color, solid line style, and 3px-radius rounded corner
* the space between the border and contents (padding) is 7px
* the div does not initially display

Later, we will insert HTML elements in the suggestion div and these will be of the suggestion class. Make sure that when this class is hovered
* the text is underlined
* the mouse cursor is of pointer type

## JavaScript

 **Instruction: You are provided below with partial code and you must compelete this code to fulfill the indications provided in comments.**

We use JQuery to set up event handlers once the page has completely loaded. Notice below that \$ symbol is a reference to the JQuery function. This function has the \$ alias. \$() takes as a parameter a JavaScript object or a CSS-style selector, for example, and returns a single object or a collection of objects that it has found to match. We then can call other JQuery methods on the returned objects according to their types.

Below we first set the function to run when the document will be ready, i.e., when the page will be fully loaded. The function in turn sets the keyup function for the HTML element with id=country.

The keyup function only gets called when a key is released while the input with id=country is in focus, i.e., when keypresses are input in the box.

Since the goal of this exercise is to propose options to the user to autocomplete their text input, we will make an HttpRequest to an external service that can return country names given partial input. This service is at the URL `https://instasham.cstutoring.ca/Country/search` and requires input to work correctly: the keyword key must be provided with data through the GET method, i.e., requests are made as follows
```
https://instasham.cstutoring.ca/Country/search?keyword=cana
```
In this example we would be searching for automcomplete suggestions for a country starting with "cana".

The data is returned in JSON format. The data is then parsed correctly by the JQuery functions and fed to the callback function set for the _success_ attribute below. Learn more about JSON [here](https://www.json.org/json-en.html).

```
$(document).ready(function(){
    //notice below that the #country selector denotes the element with id=country
    $("#country").keyup(function(){
        $.ajax({
        type: "GET",
        url: "https://instasham.cstutoring.ca/Country/search",
        data: {keyword: $(this).val()},
        dataType: 'json',
        success:
            function(data){
                if(data.length==0 || data.length == 1 && data[0].nicename == $("#country").val())
                {
                    removeSuggestions();
                    return;
                }
                //the variable newContent is there for you to write all required HTML
                var newContent = '';
                data.forEach(function(a){
                    newcontent += '<span class="suggestion" onClick="selectCountry(\'' + a.nicename +'\');">' + a.nicename + '</span><br>';
                });

                //TODO: set the contents div id=country-suggestion to the value of newContent using the html() method
                //TODO: display the div id=country-suggestion
            }
        });
    });
});

function selectCountry(val) {
    // TODO: set the input id=country value to the value of the val variable
    removeSuggestions();
}

function removeSuggestions(){
    // TODO: hide the div with id=country-suggestion
    // TODO: empty the div with id=country-suggestion
}

```

## Conclusion
The goal of this exercise is to ensure that you have good comprehension of frontend programming before starting backend programming. 

**For this purpose, you will add comments to the JavaScript/JQuery code, to explain each line.**

To summarize the instructions:
* Complete the above code where instructed.
* Put everything in a single HMTL file. Then test and debug the page.
* To the JavaScript/JQuery code, add comments to explain each line.
* Don't forget to commit to your GitHub repository and invite your teacher to see your work.