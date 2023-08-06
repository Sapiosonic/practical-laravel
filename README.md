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

### Creating app.blade.php (commit 381c6e5)

1. Create a folder called layouts under the
resources/views directory.
2. In resources/views/layouts , create a new file    `app.blade.php` 
3. code is based on the Bootstrap starter template code and the Bootstrap Navbar (https://getbootstrap.com/docs/5.1/components/navbar/). We modified the base code, including links in the header ( Home and About ). The starter template includes a Bootstrap CSS file ( bootstrap.min.css ), and a Bootstrap JS file ( bootstrap.bundle.min.js ). We included three @yield Blade directives.

@yield is used as a marker. We will inject code in those markers from child Blade views (using the @section directive). @yield uses two parameters, the first is the marker identifier. The second is a default value that will be injected if a child view does not inject code for that marker.

 

