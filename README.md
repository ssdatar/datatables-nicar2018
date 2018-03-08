# Interactive datatables in less than an hour
This is a simple tutorial to build an interactive data table that you can publish quickly. Quick link [bit.ly/nicar18-datatables](http://bit.ly/nicar18-datatables)

## What we will use
- **jQuery**: A JavaScript library used to manipulate web pages
- **[jQuery Datatables](https://datatables.net/)**: A JavaScript library built on top of jQuery to build interactive data tables

## What you need
- A computer
- A dataset
- A text editor
- An internet connection

### ***Step 1: Project setup***
- HTML: A document that the web browser reads and interprets the structure of the page (list, tables, headline, paragraphs). This is `index.html` in our case
- CSS: A file that tells the browser how to display the page (colors, fonts, margins, etc). For us, this is `main.css`.
- JavaScript: This is the language of the browser. It allows you to manipulate how elements of the page. This is the `main.js` file. 

### ***Step 2: Data -> Table***
So you have a spreadsheet that you want to display? Cool! Let's get started and convert our spreadsheet into an HTML table. Why? So that the browser can read it and display it as a table. 

We will use a tool called [Mr. Data Converter](https://shancarter.github.io/mr-data-converter).

Open your csv file in the text editor, copy its contents and paste it in the top text box of Mr Data Converter. (You could also have an Excel spreadsheet, in which case you can open the sheet in Excel, select all the cells you want to display as a table and paste it in)

### ***Step 3: Make it interactive!***
Time to fire up Datatables. Let's move over to `main.js` and write this code.
```javascript
$(document).ready(function() {
    $('#my-table').DataTable();
});
```

`example` is the ID of the table you want to make interactive. `$('#my-table')` is a way for jQuery to refer to the table. Whatever is the ID of the table, you add a `#` before it if you want to manipulate it using jQuery. (e.g. $(document) refers to the entire html)

The whole code basically means: once the document is ready to load, select `my-table` and apply the DataTable() function to it to turn it into an interactive table.

### ***Step 4: See your web page come alive*** 
You could put all of these files on a server and then see how it looks. But, your computer is capable of being a server, too. We have installed a software called `http-server`, which allows you to make your computer a local server.

```bash
cd path/to/folder
http-server
```
This will "serve" all the files from your current directory to port 8080. Open a browser and type `localhost:8080` and see your first interactive table!

### Table options
jQuery DataTables offers us several options to work with our interactive table. The way to access these options is by using a [JavaScript object](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics). This is how an object looks.

```
{
  'name': 'Bob Smith',
  'age': 32,
  'gender': 'male',
  'interests': ['music', 'skiing'],

}
```

We see that it's basically a collection of attributes. We will use this object to modify attributes of our DataTable. The library has certain defined attributes that we will access.

1. **Disable certain features**
```javascript
  'paging': false,
  'ordering': false
```


2. **Default to ordering by a particular column.**
```javascript
  "order": [[ 2, "desc" ]]

```

3. **Hide certain columns.**
```javascript
  "columnDefs": [
      {
          "targets": [ 2 ],
          "visible": false,
          "searchable": false
      }
  ]
```

4. **Language options: Change your thousand and decimal separators.**
```javascript
  "language": {
            "decimal": ",",
            "thousands": "."
        }
```

There are more examples in the [library documentation](https://datatables.net/examples/index).