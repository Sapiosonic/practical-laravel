# Practical Laravel: Develop clean MVC web Applications.

**Authors:** *Daniel Correa* and *Paola Vallejo* - 2022

I will use this **README** file as a notebook in order to store the Terminal commands and quotations important to understand concepts and techniques taugh throughout the book, divided by chapters.

## Preface

- **Who is this book for?** This book is for *web developers* or *programmers* who want to learn Laravel and improve their code skills.

## Chapter 02 – Online Store Running Example

- A running example is an example where we
visit repeatedly throughout the book.
- Let’s define the *application scope* for the app:
  - **Home page** will display a welcome message and some images.
  - **About page** will display information about the online store and developers.
  -  **Products page** will display the available products information. In addition, you can click on a specific product and see its information.
  -   **Cart page** will display the products added to the cart and the total price to be paid. In addition, a user can remove products from the cart and make purchases.
  - **Login page** will display a form to allow users to log in to the application.
  - **Register page** will display a form to allow users to sign up for accounts.
  - **My orders page** will display the orders placed by the logged in user.
  - **Admin panel** will contain sections to manage the store’s products (create, update, delete, and list them).
- The Online Store will be implemented with **Laravel (PHP)**, **MySQL** database, **Bootstrap** (a CSS framework), and **Blade** (a Laravel templating system).
- Below is a class diagram illustrating the application scope and design:
![UML Diagram](/public/img/readme/uml_diagram.jpg)
- Designing a class diagram before starting to code helps us understand the application’s scope and identify important data.

## Chapter 03 – Introduction to Laravel and Installation

### Introduction to Laravel

Laravel is a free and open-source PHP framework that provides a set of tools and resources to build modern PHP web applications (https://laravel.com/).

Laravel aims to make the development process a pleasing one for the developer without sacrificing application functionality.

### **Checking PHP version in cmd**
     php --version

### **Composer**

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on, and it will manage (install/update) them for you. 

If you don’t have Composer installed, go to (https://getcomposer.org/download/). Download and install it.

Once Composer is installed, go to the Terminal, and execute the following command: 
  
    composer --version

### Create a new Laravel Project (using Composer)

    cd C:\laragon\www\

    composer create-project laravel/laravel onlineStore "9.*" --prefer-dist

### Run the application

    cd onlineStore

### What's Artisan?

Artisan is the command line interface included with Laravel. Artisan exists at the root of your application as the artisan script and provides helpful commands to assist you while you build your application. More information about Laravel Artisan can be found here: (https://laravel.com/docs/9.x/artisan).

#### Running Laravel
    php artisan serve


### Laravel Project Structure

-  **app/Http/Controllers/*:** we will place the app controllers here.
-  **app/Models/*:** we will place the app models here.
-  **database/migrations/*:** we will define the app migrations (the app's database schema definition) here.
- **public/*:** we will store our CSS, JavaScript, and images files here. The public folder also contains the index.php file, which is the entry point to the application.
-  **resources/views/*:** we will place the app views here.
- **routes/web.php:** the web.php file will contain all the route definitions for the web application.
- **storage/app/public/*:** here, we will store the user-generated files, such as product images, that should be publicly accessible.
- **vendor/*:** The /vendor folder contains all libraries downloaded from Composer. The libraries/dependencies are listed in the composer.json file.
- **.env:** contains some common configuration values that may differ based on whether your application is running locally or on a production web server. It includes information such as database name, database username, and database password, among others.
- **composer.json:** holds metadata relevant to the project and manages the project’s dependencies, scripts, version, and many more.

### NOTE: 

Laravel is an **opinionated framework.** It means that it comes with most of the parts you need to build an application. It defines a project structure, defines an architecture, contains a lot of libraries and helpers to deal with database management authentication, web session, and so on. The advantage is that a developer can implement web applications very quickly. However, performance could not be the best, and you can have a significant number of folders and files which can be overwhelming to understand.

On the other side, you have **unopinionated frameworks** (such as Express). Express (a Node.js framework) comes with limited functionalities, and even it does not define a project structure and an architecture. The advantage is that performance is increased.

However, a web developer should take many critical
decisions (such as defining the application architecture) and deal with the inclusion of third-party libraries (such as a library to connect and manage the database).

## Chapter 04 – Introduction to MVC applications

There are different ways of designing and implementing web applications.

As you can see, structuring your code is not an easy task. That is the reason why developers and computer scientists have developed what are called software architectural patterns. **Software architectural patterns** are structural layouts used to solve commonly faced software design problems.

There are many architectural patterns, such as model-view-controller, layers, service-oriented, and micro-services. Each one has its advantages and disadvantages. Many are widely adopted. Still, one of the most used is the model-view-controller pattern.

**Model-view-controller (MVC)** is a software architectural pattern commonly used to develop web applications containing user interfaces. This pattern divides the application into three interconnected elements.

- **Model** contains the business logic of the application. For example, the Online Store application product data and its functions.
- **View** contains the application’s user interface. For example, a view to register products or users.
- **Controller** acts as an interface between model and view elements. For example, a product controller collects information from a “create product” view and passes it to the product model to be stored in the database.

Laravel provides support for the MVC pattern thanks to the integration of the Blade templating engine. 
 
 The MVC pattern provides some advantages: better code separation, multiple team members can work and collaborate simultaneously, finding an error is easier, and maintainability is improved.

 ![UML Diagram](/public/img/readme/mvc_schema.jpg)

Let’s have a quick analysis of this architecture:

-  On the left, we have clients (users of our application e.g., browsers in mobile/desktop devices). Clients connect to the application through the Hypertext Transfer Protocol (HTTP). HTTP gives users a way to interact with our web application.
- On the right, we have the server where we place our application code.
- All client interactions first pass for a route file called `web.php`.
-  The `web.php` file passes the interaction to a controller.
-  Controllers communicate with models and pass information to the views which are finally delivered to the clients as HTML, CSS, and JavaScript code.

We highlight the Model, View, and Controller layers in grey. We have four models (entities) corresponding to the classes defined in our class diagram (in Fig. 2-1). As mentioned, there are different approaches to implement web applications with Laravel. There are even different versions of MVC used in a Laravel application.  

## Chapter 05 – Layout View

### Introducing Blade

Blade is a powerful templating engine that is included with Laravel. Blade template files use the .blade.php file extension and are typically stored in the resources/views directory. In your blade files, you will have a mix of HTML code with Blade directives and Blade elements. Blade directives are convenient shortcuts for common PHP control structures, such as conditional statements and loops.

### Quick Discussion

why do PHP frameworks use templating engines? The main reason is to avoid using PHP syntax or PHP tag inside your view files. Instead, you should use the templating engine directives or helpers. What is the advantage? The template engines limit the number of available functionalities implemented in views (to provide a proper code separation). 

if you don’t find a directive or helper for a functionality you need to implement in a view file, it is because that functionality should not be implemented in the view (maybe it should be implemented in a controller or in another file).
  
### Tip

Do not use plain PHP code in your views. Blade contains a @php directive that will enable you to inject plain PHP code. However, only use it as your last resort. 

### Introducing Blade Layouts

Most web applications maintain the same general layout across various pages (common header navigation bar, and footer).

we can define this layout as a single Blade file and use it throughout our application.

### Creating app.blade.php [commit 381c6e5](https://github.com/Sapiosonic/practical-laravel/commit/381c6e57c4824180c44cbcec6e123cad485695cb)

1. Create a folder called layouts under the
resources/views directory.
2. In resources/views/layouts , create a new file    `app.blade.php` 
3. code is based on the Bootstrap starter template code and the Bootstrap Navbar (https://getbootstrap.com/docs/5.1/components/navbar/). We modified the base code, including links in the header ( Home and About ). The starter template includes a Bootstrap CSS file ( bootstrap.min.css ), and a Bootstrap JS file ( bootstrap.bundle.min.js ). We included three @yield Blade directives.

@yield is used as a marker. We will inject code in those markers from child Blade views (using the @section directive). @yield uses two parameters, the first is the marker identifier. The second is a default value that will be injected if a child view does not inject code for that marker.

### Modifying *welcome.blade.php* [commit 1e7a5b7](https://github.com/Sapiosonic/practical-laravel/commit/1e7a5b7f8ef7a4ee53bb9435dab58240e34701b3)

- Delete all the existing code in `resources/views/welcome.blade.php`

The welcome view extends the layouts.app view. This view injects the 'Home Page - Online Store' message in the @yield('title') of the layouts.app and injects an HTML div with a welcome message inside the @yield('content') of the layouts.app .

### Adding custom CSS styles and a Footer 

#### Custom style (app.css) [commit 38b762c](https://github.com/Sapiosonic/practical-laravel/commit/38b762cf7ec329d7ae6494ea1402995f325b4aae)

- Create a folder css under the `public/` directory.
- in `public/css ` create a new file `app.css`

#### Modifying app.blade.php [commit 99dafc0](https://github.com/Sapiosonic/practical-laravel/commit/99dafc0a519851f66e27775c0e14481e2e6cebfa)

- in `resources/views/layouts/app.blade.php` , make changes to include the previous CSS file and create the footer section.

Laravel includes a variety of global helper PHP functions. For example, the asset function generates a URL for an asset using the current scheme of the request (HTTP or HTTPS). Since our css/app.css file is inside the public folder, it will be automatically deployed over our server link (i.e., http://127.0.0.1:8000/css/app.css). We used curly braces {{ }} to invoke the asset function. Curly braces are used in Blade files to display data passed to the view or invoke Laravel helpers.

The currently design was inspired by a free Bootstrap template called Freelancer. You can find more information about this template here: https://startbootstrap.com/theme/freelancer. 

## Chapter 06 – Index and About Pages

### Index view [commit 4896d21](https://github.com/Sapiosonic/practical-laravel/commit/4896d219dfe390a828fa73f8a75870af728e70c5)

Let’s create a new index view. In `resources/views/`,create a subfolder `home`. In `resources/views/home`, create a new file `index.blade.php` and fill it with the code.

The first @section injects the content of the viewData["title"] variable. That variable will be defined in the web route file (presented later in this chapter) and passed to this view. 

in the public folder, create a subfolder `img`, download the following three images and store them inside the `public/img` folder.

### About view [commit ecb4b9d](https://github.com/Sapiosonic/practical-laravel/commit/ecb4b9d9b05fe12710700a266413f6e12a10f741)
 

Let’s create the About view. In `resources/views/home` , create a new file `about.blade.php` and fill it with the code.

**Remember that Blade allows curly braces to display data passed to the view.**

### Introducing Laravel Routing [commit a4670e9](https://github.com/Sapiosonic/practical-laravel/commit/a4670e950fdfd64a058a19595f2c65d0d405294c)

Laravel routes accept a URI (Uniform Resource Identifier) along with a closure. Closures are PHP’s version of anonymous functions. A closure is a function you can pass around as an object, assign to a variable, or pass as a parameter to other functions and methods.

Laravel routes are defined in your route files (located in the routes directory).

- The `routes/web.php` file defines routes for your web interface. These are the routes that we will use in this book.
- The `routes/api.php` file defines routes for your API (if you have one). These are routes used in service-oriented architectures or REST APIs (which is out of the scope of this book).

we presented two ways of defining Laravel routes.

- The first route connects the “/” URI with a closure that returns a view, `view()` is a Laravel helper which retrieves a view instance.
- The second route connects the “/about” URI with the HomeController about method, we define a custom route name by chaining the name method onto the route definition. 

### Introducing Laravel Controllers [commit fc18a98](https://github.com/Sapiosonic/practical-laravel/commit/fc18a983ace3ccb2dfb3d04d4827f76f617a8c73)

Controllers can group related request handling logic into a single class. For example, a UserController class might handle all incoming requests related to users, including showing, creating, updating, and deleting users.

In `app/Http/Controllers` , create a new file `HomeController.php` and fill it with the code.

We have the HomeController which extends the Laravel Controller class. We have the index, then we have the about method connected to the (“/about”) route in the `routes/web.php` file. This method defines a set of variables and passes them to the home.about view.

Recap, when a user goes to the `(“/”)` route, the `home.index` view will be displayed (delivered in the `routes/web.php` file). Likewise, when a user goes to the `(“/about”)` route, the `home.about` view will be displayed (delivered in the HomeController about method).

**We have also purposely introduced some serious mistakes when defining the previous elements. Why? It is because we want to illustrate the concept of clean code.**

## Chapter 07 – Refactoring Index and About Pages

The code in the previous chapter can be further cleaned and improved. We will provide general tips for handling routes, controllers, and views.

### Refactoring routes [commit fb26b50](https://github.com/Sapiosonic/practical-laravel/commit/fb26b506f4b4718dd686424f7e1d0df19cd1143b)

Our route is now connected to a controller method. We also put a name on that route. We recommend a combination of the controller’s name plus the controller’s method name to define the route name. 

**As a software developer, a good strategy is to create a document with architectural rules and share that document with your team**

### Refactoring controllers [commit ad44300](https://github.com/Sapiosonic/practical-laravel/commit/ad44300ba6a49d38f56b3fed76c2496da81565f9)

Here we have three problems:

-  Variable naming is a mess.
-   We have many with methods chained.
-    we have a blank line before the ending of the curly bracket. 

let’s analyze the index method we only define one variable called viewData which contains all the data sent to the view. This variable is an associative array.

### New controller

**Now that we use the single variable strategy, both methods are consistent. we create a subfolder with the controller’s name inside the `resources/views` folder. In this case, the subfolder is called home . And if a controller method displays data, we create a file with the controller’s method name inside the view controller subfolder. So, we have the about.blade.php file stored inside the `resources/views/home` subfolder. It makes easier to find specific views for specific controller methods.**

### Refactoring views [commit 3a04fa2](https://github.com/Sapiosonic/practical-laravel/commit/3a04fa29e047520ca213aaf63a0efb05170af127)

The previous chapter showed two views that display data a little differently. The `home/index` view won’t be changed since it displays the data using the viewData strategy. However, we will need to modify the `home/about` view to match the single variable strategy previously defined.

### Updating links in Header

Now that we have the proper routes, controller, and views, let’s include the links in the header. We use the route helper method in the previous layout, which generates a URL for a given named route. We used the names of the routes defined for the (“/”) route ( home.index ) and the (“/about”) route ( home.about ).


## Chapter 08 – Use of a Coding Standard

A coding standard is a set of rules and agreements used when writing source code in a particular programming language. One of the most used PHP coding standards is PSR-2 .

PHP_CodeSniffer is a set of two PHP scripts. The phpcs script tokenizes PHP, JavaScript, and CSS files to detect violations based on a defined coding standard. The phpcbf script automatically corrects coding standard violations.
PHP_CodeSniffer is an essential development tool that ensures your code remains clean and consistent. More information about PHP_CodeSniffer can be found [here](https://github.com/squizlabs/PHP_CodeSniffer)

### Installing and configuring PHP_CodeSniffer

    composer require --dev squizlabs/php_codesniffer

We will apply a quick configuration of PHP_CodeSniffer. In the project root directory, create a new file phpcs.xml and fill it with the code. [commit e9c86a9](https://github.com/Sapiosonic/practical-laravel/commit/e9c86a9cfcd7bbc6fbe83e0e814f5eeae1b2d3cd)

This file establishes that PHP_CodeSniffer will use PSR-2 as the coding style standard. It also defines that when we run PHP_CodeSniffer, it will find errors in the app/* , config/* , database/* , and routes/* folders. We exclude locations that include a migrations folder.

 ### Running PHP_CodeSniffer

 In the Terminal, go to the project directory, and execute the following:

    ./vendor/bin/phpcs

The previous command executes PHP_CodeSniffer based on the custom configuration defined in the phpcs.xml file Our case showed 17 errors, all with an “X” mark, which means that PHP_CodeSniffer can handle them and fix them (if you want). Some of those errors are related to spaces, indentation, and rules defined in the PSR2 coding style guide. For example, there was an annoying blank line at the end of the about method of the HomeController (before the curly brace closing). So, PHP_CodeSniffer marked it as an error.

To automatically fix it, we need to execute the PHP_CodeSniffer phpcbf file with the following command:

    ./vendor/bin/phpcbf

After that, it shows the errors fixed. [commit d9259fa](https://github.com/Sapiosonic/practical-laravel/commit/d9259faa1b044f9d6a1404f57d69b5480f70884d)


### Final remarks

- There are other tools that you can use to extend the PHP_CodeSniffer capabilities. For example, [Larastan](https://github.com/nunomaduro/larastan).
- PHP_CodeSniffer does not work well with blade files. A formatting Visual Studio Code plugin called Format HTML in PHP can help you to format your Blade views.
- PHP_CodeSniffer does not automatically fix all errors.

**Don’t leave “broken windows” (e.g., bad designs, wrong decisions, or poor code) unrepaired. Fix each one as soon as it is discovered.**

**Always use a coding standard tool, formatter, static code analysis tool, or even a combination of them in your projects. It will save you much time and improve the code quality.**

## Chapter 09 – List Products with Dummy Data

In this chapter, we will implement functionality to list all products and to be able to click those products and display their data in a separate section.

### Modifying routes [commit 96e2e0d](https://github.com/Sapiosonic/practical-laravel/commit/96e2e0db983946e64c6d5711fe8f5af480dcfb92)

We will list all the application products in the first route (“/products”). The second route will be used to show the data of a single product. “/products/{id}” takes a parameter called id. This parameter is the product id to identify
which product data to show. For example, if we access “/products/1”, the application will display the data of the product with id=1.

If you noticed, both routes are connected to the ProductController . So, let’s implement it.

### ProductController [commit 30bb213](https://github.com/Sapiosonic/practical-laravel/commit/30bb213121ed6a58dd0cb76411fe7f668ecdbf26)

$products is an array that contains a set of products with its data. In the array index 0, we have the product with id=1 (the “TV”). We have four dummy products. Currently, they are stored as a static attribute of the ProductController class. We will later retrieve product data from a MySQL database.

The index method gets the array of products and sends them to the product.index view to be displayed.

The show method gets an ``$id`` as a parameter the id is collected from the URL. We extract the product data with that id check the bold line. We subtract one unit since we stored the product with id=1 in the `ProductController::$products` array index 0, the product with id=2 in the ProductController::$products array index 1, and so on. We then send the product data to the product.show view.

### Product views

Let’s first implement the product.index view, and then, the product.show view.

### Product index view [commit e5ea657](https://github.com/Sapiosonic/practical-laravel/commit/e5ea6573721bc2e297b25e752e451b6a76da1615)

In `resources/views/` , create a subfolder product . Then, in `resources/views/product` , create a new `file index.blade.php`

The important part of the previous code is the [@foreach](https://laravel.com/docs/9.x/blade#blade-directives) . @foreach is a Blade directive which allows us to iterate over a list. 

Finally, we put a link to the product name. The link will route to the product.show route (defined previously in `routes/web.php`) and it requires a parameter to be sent. In this case, we send the product id of the current iterated product.

### Product show view [commit ba745d7](https://github.com/Sapiosonic/practical-laravel/commit/ba745d707335cde74c1ded88efbc8544fdc927f2)

In `resources/views/product` , create a new file `show.blade.php`.

We show the product image, name, and description in the above code. Remember, we are using dummy products. This will change in upcoming chapters.

In the last examples, we have defined a structure to store our controllers, controllers’ methods, routes’ names, and views. For example, the product.show route is linked to the ProductController show method, which displays the product/show view. Try to use this strategy across the entire project as it facilitates finding the views of the corresponding controllers’ methods and vice versa.

### Updating links in Header [commit 43a320f](https://github.com/Sapiosonic/practical-laravel/commit/43a320fec5cc6fd0f41c741c8121d33bb483cfdf)

Now, let’s include the products link in the header. In `resources/views/layouts/app.blade.php`

## Chapter 10 – Configuration of MySQL Database

### Introduction to MySQL

- **MySQL is a database management system.** A database is a structured collection of data. It may be anything from a simple shopping list to a picture gallery or the vast amounts of information in a corporate network. To add, access, and process data stored in a computer database, you need a database management system such as **MySQL.**
- **MySQL databases are relational.** A relational database stores data in separate tables rather than putting all the data in one big storeroom. The database structures are organized into physical files optimized for speed. MySQL provides a logical model with objects such as databases, tables, views, rows, and columns, which offers a flexible programming environment.

### MySQL tables

A table is used to organize data in rows and columns. It is used for both storing and displaying records in a structured format. The **columns** specify the data type, whereas the **rows** contain the actual data. Below is how you could imagine a MySQL table.

### Introduction to Laravel databases

Almost every modern web application interacts with a database. Laravel makes interacting with databases straightforward across a variety of supported databases. Laravel provides support for four databases:

- MySQL 5.7+
- PostgreSQL 9.6+
- SQLite 3.8.8+
- SQL Server 2017+

















