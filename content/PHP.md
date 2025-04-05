
# 1. XAMPP server

XAMPP is a necessary software to run PHP on local machine. It helps integrating the local server, so that a PHP code can be seamlessly written (without need to deploy a website on the web). Everything could be run locally.

## Setting up XAMPP

Every time a computer is launched, we need to open a XAMPP software panel, from which we have to **check two boxes :**
* `Apache` - press "Start" button under *Actions* section
* `MySQL`- press "Start" button under *Actions* section

By checking above options, a XAMPP server is running, which can be accessed from by typing "localhost" in the browser searchbar (http://localhost). After accessing the site, there should be a view showcasing list of current PHP projects created by you. By clicking on a list entry, you can freely "travel to" and explore given PHP project.

## Creating project files

In case of PHP projects, there is a special directory, where a new PHP project can be created. Apache server is looking in a specific folder for your PHP projects. To access this directory:

1) Locate your `xampp` folder (obtained through XAMPP installation process). In most cases, it should be located in C:  Drive on your machine. 
2) Inside "xampp" directory, look for `htdocs` folder - then open it.
3) Inside "htdocs" you an create your new project, by simply adding a new folder. Each folder placed directly inside "htdocs" is treated as a new project.
4) Inside each project folder, you are free to create files that will be served by an Apache server and their content will be processed and finally displayed on the local server.

<br>
<br>

# 2. PHP basics

First of all, PHP code is a code that can be run only in files with special `.php` extension. That means, a casual ".html" or ".js" files will not accept PHP code. However, files with `.php` extension do accept HTML code inside them. With PHP You are still free to create HTML as a string, so technically good-old HTML is not mandatory!

## Initializing PHP code

In order to use PHP in the `.php` file, we need to inform complier about the occurence of it. For that purpose, there is a special tag, inside which a PHP code can be written:

```
<?php
  // Between the tags you are free to write PHP code
?>
```

## PHP inside HTML code
 
As mentioned before, `.php` file accepts standard HTML code syntax. In case you want to directly append or integrate PHP output with HTML structure, you can embbed PHP tag like so:

```
 <body>
	<p> PHP is fun! </p>
	<!-- Some other tags  -->
	<?php  ?>
	<p> This is all inside HTML code </p>
</body>
```

While above code is absolutely correct, it makes no sense to include a sole PHP tag with no code included. Let's fix that by adding an `echo` command, that will display some extra text in the website:

```
 <body>
	<p> PHP is fun! </p>
	<!-- Some other tags  -->
	<?php echo "This is real PHP code!!!"; ?>
	<p> This is all inside HTML code </p>
</body>
```

You are free to include PHP tag inside the other regular HTML tag, like paragraph for example:

```
<body>
	<p> A normal paragraph </p>
	<p> This is a <?php echo "PHP-included"; ?> paragraph! </p> 
</body>
```

Also, there is nothing wrong in declaring PHP tag more than just once :

```
 <body>
	<p> PHP is fun! </p>
	<!-- Some other tags  -->
	<?php echo "This is real PHP code!!!"; ?>
	<?php echo "Declaring 2nd PHP tag is valid"; ?>
	<p> This is all inside HTML code </p>
	<?php echo "Why not adding third tag?"; ?>
</body>
```

Just remember that each PHP tag should have a specified ending, that is the `?>` part for each PHP declaration respectively. 
## PHP inside PHP-only file

Sometimes, you may encounter a scenario, where you want to create a `.php` file that contains only PHP code and nothing else. In such cases *it is recommended to omit the closing ?> tag*. This bahavior makes it easier to understand that a given file is not meant to store anything but just PHP - so no HTML, CSS or JavaScript this time.

Here is the example of PHP-only file and the proper tag declaration:

```
<?php
	echo "This is PHP-only file";
	echo "It does not contain HTML, CSS, JS";
	echo "It is just PHP";
	echo "In PHP-only files we should not use the ending tag";
```

If we decide later, that the file will actually contain, let's say, some HTML code aswell, then the closing PHP tag should be added :

```
<body>
	<?php
	  echo "This is no longer a PHP-only file";
	  echo "That is why the closing PHP tag is included";
	?>
</body>
```

## PHP comments

Comments are useful to leave a note that describes what a given code fragment does. Their purpose is pretty much the same as in JavaScript :

```
<?php>
	// This is a one-line comment
	/*
		This is a multi-line comment. It works inside multiple lines
		Seriously...
	*/
?>
```

## PHP core syntax rules

In order for PHP code to work without any errors, some basic syntax rules have to be strictly abided.

### Semicolon = end of line

Use semicolons *ALWAYS* at the end of each statement. PHP does not have ASI (Automatic Semicolon Insertion) system built-in, so one have to set them manually. 

To be precise, if the ending php tag `?>`  is present, it automatically adds a semicolon to the very last statement only. That means, the following code is syntactically correct :

```
<?php
	echo "I need a semicolon at the end of line";
	echo "I am the last command in this PHP code - no semicolon needed!"
?>
```

However, as a best practice, you still should *ALWAYS* opt for semicolons! 

### Double quotes = wrap the string text

Every piece of PHP code that is supposed to be text (string of characters), it should be wrapped inside double quotes `"  "` .  Avoid using single quotes  `'  '` or backticks  `  `` ` . Example:

```
<?php
	echo "The string text is wrapped in double quotes. Good !";
?>
```

## Trick no. 1

PHP is able to produce not only string text, but also an HTML template. This is done for example by using the `echo` command, and storing the HTML content as a string. See the code snippet below:

```
<body>
	<?php
		echo "<p> I am the paragraph </p>";
	?>
</body>
```

The modern code editors will naturally treat the `echo` command value as a string. Even though the text inside is HTML, the code editor will not recognise it - resulting in no syntax highlighting nor syntax checking. This can negatively impact development experience, especially in case of more complex HTML templates.

However there is a workaround for this issue. In order to benefit from syntax checking & highlighting, a *PHP code tag should be written in following format*:

```
<body>
	<?php if(true) { ?>
		<p> I am the paragraph, both syntax checked & highlighted by VSCode !
	<?php } ?>
</body>
```

<br>
<br>

# 3. Data types & variables

What is common for most programming languages, is that they allow to represent data in different formats, based on what that data is. PHP is no exception here. It supports many different data types that are essential to understand.

## What is a variable? 

Variable under the hood is the memory location inside the project that stores some sort of data. You can think of it as a box *(memory location)*, that has it's own unique label *(memory address)* and inside that box some an item is stored *(data)*.  Whenever this box opened, the data within this box can be freely accessed. 

By referencing a variable, we can grab the data that is sotred in that variable, and based on such data, some further operations can be done.

## Defining & using a variable

To define a new variable in PHP, all you need to do is to add a preceding  "$"  sign just before the variable name (any of your choice) and use the "=" operator to assign newly created variable to a value:

```
<?php
	$name = "Joe Doe";
?>
```

Now with a variable already defined, we can now get access to the value underneath it, by using  "$"  followed by the variable name. In this example, the content of  `name` variable will be added to the webpage content by using `echo` command:

```
<body>
	$name = "Joe Doe";
	echo $name;
</body>
```

Variables can also be assigned to the other variables. In that situation, both variables store the same value:

```
$name = 'Kamil';
$myName = $name;

<?php echo $name ?> // Will output 'Kamil'
<?php echo $myName ?>  // Will alos output 'Kamil'
```
## Naming conventions

When naming variables, there are plenty of rules that you need to abide in order to avoid some lexical errors, and to follow the best practies:

* The variable name (apart from leading "$" sign) should start either with letter or underscore ( _ )
* After the first letter in variable name, other characters can be either letters, numbers, or underscoe ( _ )
* Follow _camelCase_ naming convention. First word in a variable name should be all written in lowercase, and every first letter of later words should be written in uppercase (eg. $myDogName)


## Base PHP data types

PHP includes many data types, that can be futher split into categories. Here are the most common ones:

### Scalar types

This type category means, that the variable contains just one value. This is the most common type category. Scalar type could be: **string**, **integers**, **floats**, **booleans** :

```
<?php
	// Scalar types
	$string = "Kamil"; // a word
	$int =  24441;  //  a number without decimal point
	$float = 1.43;  // a number with decimal points
	$boolean = true;  // either true or false
?>
```

### Array type

This type allows to contain multiple pieces of data inside the Array. As a good practice, each of the data included in a given array should be of the same type (like number Array / string Array).

Array can be defined in two ways:

```
// Old way of defining array - still working!
$namesArray = array('Ben', 'Joe', 'Adam');

// This way of defining array is only available in newer PHP versions
$namesArrayNew = ['Kate', 'Tom', 'Henry'];
```

### Unassigned type

PHP also allows to create a variable without attaching any value to it. If such variable is used, it **mimics the default type value depending on the context of where it is used** :

```
// Defining an unassigned variable (no value attached)
$empty;  

// "empty" will mimic the number type here, with default value 0
<?php 152 + $empty ?>

// "empty" will mimc the string type here, with default value ""
echo $empty;
```

Here is the list for default values for each specific data type:

```
<?php
	$string = "";
	$int = 0;
	$float = 0;
	boolean = false;

	$array = [];
	$object = {};
?>
```

**When it comes to declaring a variable, you should ALWAYS initialize it with a value (at least , default one for a desired type). Avoid using an unassigned type: **

```
// This is unassigned type - avoid using it
$unassigned;

// A better approach is to use default value for a desired variable type
$someName = "";
```