## BUILDING DJANGO ECOMMERCE 'FINESAUCES'

https://github.com/gurnitha/django-ecom-finesauces
https://github.com/Peter-Vought

## Table of Contents

### 1 Initial setup

	PASS

	1.1 Windows Subsystem for Linux (WSL 2)
	1.1.1 Checking requirements for running WSL 2
	1.1.2 Enabling the Windows Subsystem for Linux
	1.1.3 Enabling Virtual Machine feature
	1.1.4 Downloading the Linux kernel update package
	1.1.5 Setting WSL 2 as your default version
	1.1.6 Installing Ubuntu 20.04 LTS
	1.1.7 WSL 2 in VS Code
	1.2 PostgreSQL
	1.3 Git
	1.4 Virtual environment
	1.5 Github remote repository

### 2 Starting our e-commerce project

#### 2.1 Creating a Django project and run dev. server

	(venv3922) ing| django-admin startproject config .

	(venv3922) ing| tree config/
	config/
	├── __init__.py
	├── settings.py
	├── urls.py
	└── wsgi.py

#### 2.2 Updating project settings

	modified:   config/settings.py
	modified:   readme.md

#### 2.3 Initial migration

	(venv3922) ing| python manage.py makemigrations
	No changes detected
	(venv3922) ing| python manage.py migrate
	Operations to perform:
	  Apply all migrations: admin, auth, contenttypes, sessions
	Running migrations:
	  Applying contenttypes.0001_initial... OK
	  ...
	  Applying sessions.0001_initial... OK

	modified:   readme.md

#### 2.4 Local repository

	DONE

#### 2.5 Remote repository

	DONE

#### 3. Creating listings application

	(venv3922) ing| django-admin startapp listings

	(venv3922) ing| tree -L 1
	.
	├── _docs
	├── config
	├── db.sqlite3
	├── listings
	├── manage.py
	└── readme.md

#### 3.1 Activating listings application

	modified:   config/settings.py
	modified:   readme.md

#### 3.2 Designing listings models

	modified:   listings/models.py
	modified:   readme.md

#### 3.3 Creating and applying migrations

	(venv3922) ing| python3 manage.py makemigrations
	(venv3922) ing| python3 manage.py migrate

	BEGIN;
	--
	-- Create model Category
	--
	CREATE TABLE "listings_category" (
		"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, 
		"name" varchar(100) NOT NULL UNIQUE, 
		"slug" varchar(100) NOT NULL UNIQUE);
	--
	-- Create model Product
	--
	CREATE TABLE "listings_product" (
		"id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, 
		"name" varchar(100) NOT NULL UNIQUE, 
		"slug" varchar(100) NOT NULL UNIQUE, 
		"image" varchar(100) NOT NULL, 
		"description" text NOT NULL, 
		"shu" varchar(10) NOT NULL, 
		"price" decimal NOT NULL, 
		"available" bool NOT NULL,
		"category_id" bigint NOT NULL REFERENCES "listings_category" ("id") DEFERRABLE INITIALLY DEFERRED);
	CREATE INDEX "listings_product_category_id_5d2fa1ec" ON "listings_product" ("category_id");
	COMMIT;

	new file:   listings/migrations/0001_initial.py
	modified:   readme.md

#### 3.4 Creating administration site
	
	PASS

#### 3.4.1 Creating superuser

	PASS

#### 3.4.2 Accessing administration site

	PASS

#### 3.4.3 Adding models to the administration site

	modified:   listings/admin.py
	modified:   readme.md

#### 3.4.4.1 Customizing how models are displayed - Overiding naming conventions from Categorys to Categoris

	modified:   listings/models.py
	modified:   readme.md


#### 3.4.4.2 Customizing how models are displayed - Displaying actual name of the category

	modified:   listings/models.py
	modified:   readme.md

#### 3.4.4.3 Customizing how models are displayed

	modified:   listings/admin.py
	modified:   readme.md

#### 3.5 Displaying our categories and products
#### 3.5.1 Building our product list view
#### 3.5.2 Creating template for our product list
#### 3.5.3 Adding URL pattern for our view
#### 3.5.4 Filtering by category
#### 3.5.5 Product detail page

4. Adding reviews, starts and average reviews

4.1 Adding modal window form review
4.2 Adding data-toggle to form review
4.3 Create Review model
4.4 Create forms for user input
4.5 Modify product_detail in listngs/views.y
4.6 Modify detail page - Include review form modal
4.7 Modify detail page - Modify modal form (radio button vertical)
4.8 Modify detail page - Modify modal form (radio button horizontal)
4.9 Modify detail page - Modify modal form (replace button horizontal with codes)
4.10 Modify detail page - Add Review model to admin
4.11 Modify detail page - Modify ProductAdmin class in admin
4.12 Modify detail page - Modify modal in datail page
4.13 Adding average_review_score in Product model
4.14 Modify detail page - load average_review_score to detail page

5. Shopping cart

5.1 Sessions
5.2 Storing shopping cart in session
5.3 Shopping cart form and views
5.4 Displaying our cart
5.5 Adding products to the cart
5.6 Updating product quantities in cart
5.7 Shopping cart link
5.7.1 Setting our cart into the request context

6. Customers orders

6.1 Creating order models
6.2 Adding models to the administration site
6.3 Creating customer order
6.4 Integrating Stripe payment
6.4.1 Adding Stripe to our view
6.4.2 Using Stripe elements
6.4.3 Placing an order
6.5 Sending email notifications
6.6.1 Setting up Celery
6.6.2 Setting up RabbitMQ
6.6.3 Adding asynchronous tasks to our application
6.6.4 Simple Mail Transfer Protocol (SMTP) setup

6 Extending administration site

6.1 Adding custom actions to the administration site
6.1.1 Exporting data into .xlsx report
6.1.2 Changing order status
6.2 Generating PDF invoices
6.2.1 Installing WeasyPrint
6.2.2 Creating PDF invoice template
6.2.3 Rendering PDF invoices
6.2.4 Sending invoices by email
6.3 Admin site styling

8. Customer accounts

8.1 Login view
8.1.1 Messages framework
8.1.2 Django LoginView
8.2 Logout view
8.3 User registration
8.3.1 Updating product review functionality
8.4 Password change views
8.5 Password reset views
8.6 Extending User model
8.7 Creating user profile section
8.8 Linking orders to customers
8.9 Displaying customer orders

9. Deploying to DigitalOcean

9.1 VPS access and security
9.1.1 Creating Droplet
9.1.2 Creating SSH key
9.1.3 Logging into Droplet
9.1.4 Creating a new user and updating security settings
9.2 Installing software
9.2.1 Database setup
9.3 Virtual environment
9.3.1 Settings and migrations
9.4 Gunicorn setup
9.5 NGINX setup
9.6 Domain setup
9.7 Setting up an SSL certificate

Conclusion
References 


