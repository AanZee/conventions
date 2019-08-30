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

root folder
- holds various files for building
/config
main.go
/dist
- where the binary is placed
/src
	init.go
	- bootstrap of the application
	- only needed for an application (not for a library)
	- holds the start/stop/init/config
    /web holds the routing initialization
    /helpers
	- project specific
	/middlewares (if they exist in the project)
    /datamodels
	/business (separation of concerns)
    	/domain(s)
            /handlers
            /queries (if you work with a database)
            /repositories
            /services
            /validators

## 

Every project must have a makefile.
(You can look at other projects for a universal working version.)

Depending on the project (Application / Library), there should be a makefile in the root directory
with the following functions:
	update
	check
	check2
	start	(only needed when it's an application)
	migrate (only needed when a database is used)
	test
	test-s
	test-c
	test-v
	modd

## Package name

A package name represents the content it houses. Inside there will be 1 or more files with functions that
don't have the package name in front of it. Otherwise, when using a function, you get a stutter-effect,
like this: database.DatabaseOpener(), while database.Opener() is enough.

When importing an external library (from aan zee), make it clear by using an alias, like:
capilaErrors "bitbucket.org/aanzeeonline/capila/errors"
libgoazConv "bitbucket.org/aanzeeonline/libgoaz/conv"
libgoazCrypt "bitbucket.org/aanzeeonline/libgoaz/crypt"

Don't use a name that is meaningless, like: util, common, misc.
There is one exception to this: helpers.
We will use helpers to store various helper-functions and over time, we can decide to group them into
a package that is more suitable.

## Imports

order of imports

- internal go packages
- external packages (3rd party)
- aanzee library packages
- aanzee packages of current project

## Variable declaration

Top level order of declaration:
- constants
- types
- variables

Global / package / function

No Global Variables. Use getters for that.

If a package variable is used in more than 1 file, put it in a base.go

Declare a function variable at the top of the function, or close to the first usage.

## Functions and methods

You can house more than 1 function inside a file (inside a package).
The file name represents the content it houses.

- naming
	- give the function a name it represent.
	- Don't abbreviate.
	- Getters for retrieving data
    	- GetUsers, GetUser
- no getters (the fact it begins with a capital and returns value, makes it a getter)
- setters can be used
- if crud, follow crud order inside source? (thoughts about this?)
- global vs local
  - first all global functions and methods (they start with capitals)
  - local function below that (they start with lowercase)
- return variables:
  - when returning an error, it is always the last value that returns

## Testing

- code coverage (100%, unless it's a project decision not to do so)
- no '.' imports

- Fuzzy testing on high level.
- Handlers should only test the basic working.
- Services should test every scenario possible and should be tested with 100% codecoverage.
  - if there are model validations, these should be tested too.
- Repositories should test every scenario possible and should be tested with 100% codecoverage.

## Comments

- package
  - doc
    - Describes why the package exists
    - it has the package format:
      - Package the_name the_rest_of_the_text.
- variable
  - single line
    - format of that:
    // explain what it does and/or why it exists

- function/method
  - multi line
    - if the function/method is public:
      - first line is a complete sentence, starting with capital, ending with dot.
    - if it is private:
      - first line is a complete sentence, starting with lowercase, not ending with dot.
    - is written in third-person singular with minimal 4 words
     - format of that
	/*
	YourFunction does something spectacular.
	*/

## Variable naming

A variable name is always named after the thing it contains.

in a loop, like in this example:
for key,record := range records {
	println("key:", key)
	println("val:", record)
}

If it can hold a collection of things, name it plural, like "users".
If it can only hold one value, name it singular, like "user".
if it is a boolean var, start it with something like "has", or "is".
In some checks, you will find a boolean variable like "ok",
which is mostly used for checking if an element is present in a map.

It's also common use, when a variable name holds an abbreviation, that the letters are all capitals, or all lowercase.
like "SQLStatement" or "sqlStatement"

## linting

It is nice to start a linter now and then.
make check, or make check2 will run the linters and will check your files for "mistakes".
Try to improve your code with the hints you get from them.

## Code Quality

I wrote a lint tool, which also checks for cognitive complexity.
If code is "too complex" (which is mostly caused by conditions, loops etc.), I will advice
to refactor the code, because understandable code is easy to maintain in the future.

## read :
https://golang.org/doc/effective_go.html
https://github.com/golang/go/wiki/CodeReviewComments
