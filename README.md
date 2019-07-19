# GoodEatsFood
<h1> Good Eats Food Project </h1>
<p> Here at Good Eats we strive to provide the community with a source for healthy         food habits. We provide delicious breakfast, lunch and dinner recipes for you and      your family. Each search provides breakdowns the recipes and food nutritions. </p>
<h2>Technical Part </h2>
<h3>Back-End</h3>
<p>For the backend of the development we used two different API for our website. The first was Edaman and the developer used Ajax to call the API passing the main ingredient and returning 10 different recipes. The second was Zomato and the developer used getJSON to passing the location of the user and retrieving different restaurant locations within a 25-mile radius.</p>
```js
$.getJSON(settings, function(data) {
  data = data.restaurants;
  var html = "";
  $.each(data, function(index, value) {
  }
}
```
```js
$(document).on("click", "#search", function(event) {
    event.preventDefault();
    var searchInput = $("#recSec").val().trim();
    recSearch(searchInput)
    $("#recSec").val("")
});
function recSearch(inputVal) {
    $("#recipe-views").empty();
    var preSearch = "?q=";
    var search = inputVal;                      //pass main ingredient to edamam api
    var appId = "&app_id=54624b1b";                             //edamam app id
    var apiKey = "&app_key=b9d60172abd893b7a8e61caf2661b7d7";   //edamam app key
    var queryURL = "https://api.edamam.com/search" + preSearch + search + appId + apiKey;
    console.log(queryURL)
    $.ajax({                                            //ajax call
        url: queryURL,
        method: "GET",
        })
    .then(function (response) {                         //response from api and begin formatting
        var results = response.hits;
        console.log(results);
        for (i = 0; i < results.length; i++) {          //loops through main array returned by ajax call
            // Building the Div
            var subView = $("<div>");                   //create new element
            subView.addClass("recipe-views-" + i);      //add incrementing recipe-views class
            // Building the image
            var recImage = $("<img>");                      //create new recImage element
            recImage.attr("class", "recImg");               //add recImg class
            recImage.attr("src", results[i].recipe.image);  //add image
            subView.append(recImage);                       //append element to subview
            $(".recipe-views").append(subView)              //append to main view div
            var recN = results[i].recipe.label;                                             //grab recipe name
            $(".recipe-views").append("<div class='recName'><h2>" + recN + "</h2></div");   //append recipe name to main view div
            var newDiv1 = $("<ul>");                        //create new element
            newDiv1 = $("<div>").text("Recipe Info: ");     //add recipe info to heading
            newDiv1.addClass("recInfo");                    //add recInfo class
            var recC = "Calories: " + (Math.floor(results[i].recipe.calories));   //create new variable for calories 
            var p = $("<li>");                              //create new list item element
            p.append(recC);                                 //append element to new variable
            newDiv1.append(p);                              //append variable to newDiv1 element
            $(".recipe-views").append(newDiv1);             //append to newDiv1 to recipe-views div
            for (k = 0; k < results[i].recipe.dietLabels.length; k++) {     //loop through dietlabels array
                var recDLabel = results[i].recipe.dietLabels[k];            //new variable to hold dietlabels
                var p = $("<li>")                                           //new element to hold diet labels
                p.append(recDLabel);                                        //append diet labels to list items
                newDiv1.append(p);                                          //append diet label list items to newDiv1
                $(".recipe-views").append(newDiv1);                         //append to main recipe-views div
            }
            for (l = 0; l < results[i].recipe.healthLabels.length; l++) {   //loop through health labels array
                var recHLabel = results[i].recipe.healthLabels[l];          //new variable to hold health labels
                var p = $("<li>")                                           //new element to hold health labels
                p.append(recHLabel);                                        //append health labels to list items
                newDiv1.append(p);                                          //append health labels list item to newDiv1
                $(".recipe-views").append(newDiv1);                         //append to recipe-views div
            }
            var newDiv2 = $("<ul>");                                        //new newDiv2 variable
            newDiv2 = $("<div>").text("Ingredients:");                      //add Ingrediants text to newDiv2
            newDiv2.addClass("recIngreds");                                 //add recIngreds class to newDiv2 
            for (j = 0; j < results[i].recipe.ingredientLines.length; j++) {    //loop through ingredients array
                var recIngred = results[i].recipe.ingredientLines[j];           //new variable to hold ingredients
                var p = $("<li>")                                               //new list item to hold ingredients
                p.append(recIngred);                                            //append ingredients to div
                newDiv2.append(p);                                              //append list item to newDiv2
                $(".recipe-views").append(newDiv2);                             //append newDiv2 to main div
            }
        }
    });
}
```
<h3>Front-End</h3>
<p>The Good Eats site was designed and styled using Materialize and Bootstrap, with three of our html pages using solely Materialize and our Restaurant page using both Bootstrap and Materialize. With using the APIs, documentation states that we must visibly show that the website API is powering that page. </p>
```css 
nav.nav-extended ul {
  text-align: center;
}
nav.nav-extended ul li {
  display: inline;
  float: none;
}
nav.nav-extended ul li a {
  display: inline-block;
  text-align: center;
}
.jumbotron-billboard .img {
    margin-bottom: 0px;
    opacity: 0.7;
    color: #fff;
    background: #000 url("https://cdn.fstoppers.com/styles/full/s3/media/2017/09/11/autumn_food_photography_0.jpg") top center no-repeat;
    width: 100%;
    height: 100%;
    background-size: cover;
    overflow: hidden;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
  }
```