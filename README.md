# Interactive datatables in an hour
#### Quick link [bit.ly/nicar18-datatables](http://bit.ly/nicar18-datatables)

***Saurabh Datar***
Find me on Twitter [@ssdatar](https://twitter.com/ssdatar) or email me
saurabhsdatar@gmail.com

This is a simple tutorial to build an interactive data table that you can publish quickly without having to write much code. 

## What we will use
- **jQuery**: A JavaScript library used to manipulate web pages
- **[jQuery Datatables](https://datatables.net/)**: A JavaScript library built on top of jQuery to build interactive data tables

## What you need
- A computer
- A dataset
- A text editor (Sublime Text 3, Atom, TextEdit or any other editor of your choosing)
- An internet connection

## Installation
1. Go to [this link](https://github.com/ssdatar/datatables-nicar2018). You should see a green "Clone or download" button towards the top right of the screen. Download the folder as zip, unpack the zip file and then open the folder using your text editor (Usually File -> Open Folder). 

2. [Served](http://enjalot.github.io/served/): This is a small piece of software allows you to turn your computer into a web server. Why would you do that? To see how your table will look on a website! It's a pretty simple installation for different operating systems. I promise this is the only thing you need to install.

### ***Step 1: Project setup***
Done installing? Great. Let's look at our project structure.

- HTML: A document that the web browser reads and interprets the structure of the page (list, tables, headline, paragraphs). This is `index.html` in our case
- CSS: A file that tells the browser how to display the page (colors, fonts, margins, etc). For us, this is `main.css`.
- JavaScript: This is the language of the browser. It allows you to manipulate how elements of the page. This is the `main.js` file.
- Libraries: Look at the `lib` folder. These contain the jquery, jquery Datatables and other supported files required for this to work.

#### What if I can't have these files on my computer?
No problem. Forget the `lib` folder. Open `index.html` in your text editor and follow these steps.
- At the top, you will see this link tag `<link rel="stylesheet" type="text/css" href="lib/DataTables/datatables.min.css"/>`. This is telling the browser to go to the lib, then to a subfolder called DataTables and download a file called `datatables.min.css`. Replace that with this `<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/v/dt/dt-1.10.16/datatables.min.css"/>`.

- Similarly, scroll all the way to the bottom of the index.html page and change the `src` links in the script tags for jquery and jquery DataTables to this.
```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script type="text/javascript" src="https://cdn.datatables.net/v/dt/dt-1.10.16/datatables.min.js"></script>
```

What we did is to tell our browser to download these files stored in some kind soul's server instead of having to store it locally somewhere on your newsroom server (which could also be an option if you talk to someone in IT or technology).

### ***Step 2: Data -> Table***
So you have a spreadsheet that you want to display? Cool! Let's get started and convert our spreadsheet into an HTML table. Why? So that the browser can display it as a table. 

We will use a tool called [Mr. Data Converter](https://shancarter.github.io/mr-data-converter). This tool allows you to drop in Excel or CSV data and conver it to an HTML table.

Open your csv file in the text editor, copy its contents and paste it in the top text box of Mr Data Converter. (You could also have an Excel spreadsheet, in which case you can open the sheet in Excel, select all the cells you want to display as a table and paste it in)

Then, click on the dropdown in the middle of the screen and choose HTML. Copy the entire generated HTML table, and paste it in `index.html` anywhere between the `<body>` and `</body>` tags. 

The browser reads your HTML page like humans do -- top to bottom. So paste the HTML table after whichever element you want it to appear on the page.

### ***Step 3: Name your table***
Often, there might be more than one table on your page. So we will give our table a special ID so that jQuery DataTables knows which table to make interactive. So scroll to the top of your table code i.e. where you can see `<table`>. Delete this tag and replace it with `<table id="my-table">`. An ID is a unique identifier in an HTML page; any element can have an ID but no two can have the same ID. So make sure to give it a unique name. Oh, you cannot use spaces in the ID. Try to use `-`, `_`, as a separator.

### ***Step 4: Make it interactive!***
Time to fire up Datatables. Let's move over to `main.js` and write this code.
```javascript
$(document).ready(function() {
    $('#my-table').DataTable();
});
```

`$('#my-table')` is a way for jQuery to refer to the table. Whatever is the ID of the table, you add a `#` before it if you want to manipulate it using jQuery. In human terms, this means: hey jQuery, select the element with the ID `my-table`. (Similarly, `$(document)` would pick the entire HTML document).

The whole code basically means: once the document is ready to load, select `my-table` and apply the DataTable() function to it to turn it into an interactive table.

### ***Step 4: See your web page come alive*** 
Launch Served and drag and drop your project folder in the application window. Served should give you the link on which you can view your website. Click on the link see your first interactive table in the browser!

### Table options
jQuery DataTables offers us several options to work with our interactive table. The way to access these options is by using a [JavaScript object](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics). This is how an object looks.

```
{
  'name': 'Bob Smith',
  'age': 32,
  'gender': 'male',
  'interests': ['music', 'skiing']
}
```

We see that it's basically a collection of attributes. We will use this object to modify attributes of our Datatable. The library has certain defined attributes that we will access. 

All we need to do is to pass a Javascript object to the function and what attribute we want to change. So enclosed within the two parentheses of `DataTable()` will be an object with properties we want to change. Something like this:

```javascript
$(document).ready(function(){
  $('#my-table').DataTable({
      'option1': true,
      'option2': false,
      'option3': somethingelse
    });
});
```

Here are a few examples. The first one includes the complete code you can copy-paste into your `script.js` file. The others just show the options available to you. All you need to do is include those options in the object you are passing to the DataTables function. Remember, each option-value pair is separated by a comma.

1. **Disable certain features**: Add these options to the object you pass to Datatables function to turn off ordering
```javascript
  $(document).ready(function(){
    $('#my-table').DataTable({
        'paging': false,
        'ordering': false
      });
  });
```


2. **Default to ordering by a particular column.**: 
```javascript
  "order": [[ 2, "desc" ]]

```

3. **Hide certain columns.**: This is DataTables' syntax for targeting certain columns and how you want it to behave. The code below basically means: Target the third column (counting in computers begins at 0!), hide it and also make the content in it not searchable.
```javascript
  "columnDefs": [
      {
          "targets": [ 2 ],
          "visible": false,
          "searchable": false
      }
  ]
```

3. **Change the number of elements per page**: This involves some more code. But it's pretty simple. Say you want to change the number of rows per page to 13. Here's what you do.
```javascript
$(document).ready(function(){
  var table = $('#my-table').DataTable();
  table.page.len(13).draw();
});
```

4. **Change your thousand and decimal separators.**
```javascript
  "language": {
      "decimal": ",",
      "thousands": "."
    }
```

There are more examples in the [library documentation](https://datatables.net/examples/index). If you have any questions, feel free to tweet to me or email me. I hope you found this useful.
