# Go Code Conventions

## Modules

go mod init bitbucket.org/aanzeeonline/[yourprojectname]

Working with a local fork of a module, put an extra line in the go.mod:
// replace bitbucket.org/aanzeeonline/libgoaz => ../LibGOAZ
(and remove the comments)

Before pushing the final update to git, make sure that the fork isn't in use anymore

We need to investigate, if a vendor option (go mod vendor) is usable.
(The upcoming 1.13 will have the final module solution.)
"go mod vendor puts them in a vendor folder inside your project, running go build -mod vendor
uses the dependency put in the vendor folder. This further isolates the project from the
globally installed dependencies."

## Project structure for an API / Web application

Root folder
- Holds various files for building
main.go
- the bootstrap of the application
/config
/dist
- Where the binary is placed
/src
- the actual root of the software
	start.go (*optional; can be a folder too)
	- Bootstrap of the application
	- Only needed for an application (not for a library)
	- Holds the start/stop/init/config
    /web
	- holds the routing initialization
		/middlewares (if they exist in the project)
    /helpers
	- Project specific, can have subfolders
    /database
		/migrations
		/seeds
	/datamodels (*optional; can be a folder inside a domain too)
	/business (separation of concerns)
    	/domain(s)
            /handlers
            /queries (if you work with a database)
            /repositories
            /services
            /validators
			/datamodels (*optional; can be a /src folder too)

## Makefile

Every project must have a makefile.
(You can look at other projects for a universal working version.)

Depending on the project (Application / Library), there should be a makefile in the root directory
that shows help about the functions that are available.

with the following functions:
	install
	- installs tools needed for the project
  	update
	- update mod-file (and sometimes the vendor directory which is project based)
	check
	- linting
	check2
	- linting
	check3
	- linting
	test
	- run all tests
	test-c
	- run all tests with codecoverage
	test-v
	- run all tests verbose
	watch
	- starts a watcher
	doc
	- look at documentation
	migrate
	- database migration (only needed when a database is used)
	start
	- runs application 	(only needed when it's an application)
	build
	- compile application (only needed when it's an application)

Of course there can be more makefile functions, that are project specific.

## Package name

A package name represents the content it houses. Inside there will be 1 or more files with functions that
don't have the package name in front of it. Otherwise, when using a function, you get a stutter-effect,
like this: database.DatabaseOpener(), while database.Opener() is enough.

When importing an external library (from Aan Zee), make it clear by using an alias, like:
capilaErrors "bitbucket.org/aanzeeonline/capila/errors"
libgoazConv "bitbucket.org/aanzeeonline/libgoaz/conv"
libgoazCrypt "bitbucket.org/aanzeeonline/libgoaz/crypt"

Don't use a name that is meaningless, like: util, common, misc.
There is one exception to this: helpers.
We will use helpers to store various helper-functions and over time, we can decide to group them into
a package that is more suitable, of move them to Capila or Libgoaz.

## Imports

Order of imports:
- Internal go packages
- External packages (3rd party)
- Aan Zee library packages
- Aan Zee packages of current project

## Variable declaration

Top level order of declaration:
- Constants
- Types
- Variables

Global / package / function

No Global Variables. Use getters for that.

If a package variable or function is used in more than 1 file, put it in a base.go or a file starting with base.

Declare a function variable at the top of the function, or close to the first usage.

## Functions and methods

You can house more than 1 function inside a file (inside a package).
The file name represents the content it houses.

- Naming
	- Give the function a name it represent
	- Don't abbreviate
	- List / Get / Create / Update / Delete

- Return variables:
  - When returning an error, it is always the last value that returns

## Testing

- Code coverage (100%, unless it's a project decision not to do so)
- No '.' imports

- Fuzzy testing on high level
- Handlers should only test the basic working
- Services should test every scenario possible and should be tested with 100% codecoverage
  - If there are model validations, these should be tested too
- Repositories should test every scenario possible and should be tested with 100% codecoverage

## Comments

- Package
  - Doc
    - Describes why the package exists
    - It has the package format:
      - Package the_name the_rest_of_the_text
- Variable
  - Single line
    - Format of that:
    // Explain what it does and/or why it exists

- Function/method
  - Multi line / single line
    - Is written in third-person singular with minimal 4 words
     - Format of that:
	/*
	YourFunction does something spectacular.
	*/
	or:
	// YourFunction does something spectacular.

## Variable naming

A variable name is always named after the thing it contains.

In a loop, like in this example:
for userIndex,userRecord := range userRecords {
	println("userIndex:", userIndex)
	println("userRecord:", userRecord)
}

If it can hold a collection of things, name it plural, like "users".
If it can only hold one value, name it singular, like "user".
if it is a boolean var, start it with something like "has", "should", "would" ,"can", "could" or "is".

It's also common use, when a variable name holds an abbreviation, that the letters are all capitals, or all lowercase.
like "SQLStatement" or "sqlStatement"

## Linting

It is nice to start a linter now and then.
Make check, or make check2 will run the linters and will check your files for "mistakes".
Try to improve your code with the hints you get from them.

## Read
https://golang.org/doc/effective_go.html
https://github.com/golang/go/wiki/CodeReviewComments
