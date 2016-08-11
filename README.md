# ASP.NET-Web-API
Follow a tutorial creating a ProductsApp

# [Creating a Web API Tutorial](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* ASP.NET Web Application
* 

## 1) Create Web API


## 2) Call the `Web API` with `JQuery` and `JavaScript`
* Add an `HTML` page that uses `AJAX` to call the web API. 
* We'll use `jQuery` to make the `AJAX` calls and also to update the page with the results.
```go
<div>
    <h2>Search by ID</h2>
    <input type="text" id="prodId" size="5" />
    <input type="button" value="Search" onclick="find();" />
    <p id="product" />
  </div>
<script src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js"></script>
  <script>
    var uri = 'api/products';
    //getting a list of products
    $(document).ready(function () {
      // Send an AJAX request
      $.getJSON(uri) //getJSON() is a JQuery function that sends AJAX request.
          .done(function (data) {
            // On success, 'data' contains a list of products.
            $.each(data, function (key, item) {
              // Add a list item for the product.
              $('<li>', { text: formatItem(item) }).appendTo($('#products')); //#products is the id of element <ul>
            });
          });
    });

    function formatItem(item) {
      return item.Name + ': $' + item.Price;
    }

    //Getting a Product By ID
    function find() {
      var id = $('#prodId').val(); //save the input text
      $.getJSON(uri + '/' + id) //Send an HTTP GET request to "/api/products/id"
          .done(function (data) {
            $('#product').text(formatItem(data)); //if success, display the content in element <p>(#product is the id of element p)
          })
          .fail(function (jqXHR, textStatus, err) {
            $('#product').text('Error: ' + err); //id fail, dispaly the error message
          });
    }
  </script>
```
