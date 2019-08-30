# Go Code Conventions

## Tooling

- Visual Studio Code
- delve
- golangci-lint
- staticcheck
- modd

## Modules

go mod init bitbucket.org/aanzeeonline/[yourprojectname]

Working with a local fork of a module, put an extra line in the go.mod:
// replace bitbucket.org/aanzeeonline/libgoaz => ../LibGOAZ
(and remove the comments)

Before pushing the final update to git, make sure that the fork isn't in use anymore

## project structure for an API / Web application

main
- start (explain why)
- web
- helpers
- datamodels
- business (separation of concerns)
  - domains (if you have more than one)
    - handlers
    - queries (if you work with a database)
    - repositories
    - services
    - validators

## Makefile

Every project must have a makefile.
(You can look at other projects for an universal working version)

## Package name

A package name represents the content it houses. Inside there will be 1 or more files with functions that
don't have the package name in front of it. Otherwise, when using a function, you get a stutter-effect,
like this: database.DatabaseOpener(), while database.Opener() is enough.

You can simplify a package name when it's a common abbreviation. database could be db, so db.Opener() can be used.

When importing an external library (from aan zee), make it clear by using an alias, like:
capErrors "bitbucket.org/aanzeeonline/capila/errors"
libConv "bitbucket.org/aanzeeonline/libgoaz/conv"
libCrypt "bitbucket.org/aanzeeonline/libgoaz/crypt"

Don't use a name that it meaningless, like: util, common, misc.
There is one exception to this: helpers.
We will use helpers to store various helper-functions and over time, we can decide to group them into
a package that is more suitable.

## Imports

order of imports

- packages of current module
- packages of aan zee lib's
- the rest

## Variable declaration

Top level order of declaration:
- constants
- types
- variables

Global / package / function

Don't use many Global var's.

If a package var is used in more than 1 file, put it in a base.go

Declare function var's mostly at the top of the function, or close to the first usage.

## Functions and methods

You can house more than 1 function inside a file (inside a package).
The file name represents the content it houses.

- naming
	- give the function a name it represent.
	- You can simplify a function name when it's a common abbreviation.
		db.Initialize() could be db.Init()
- no getters (the fact it begins with a capital and returns value, makes it a getter)
- setters can be used
- if crud, follow crud order inside source? (thoughts about this?)
- global vs local
  - first all global functions and methods (they start with capitals)
  - local function below that (they start with lowercase)
- return var's:
  - when returning an error, it is always the last value that returns

## Testing

- code coverage (100% of relevant)
- no . imports

- Handlers should only test the basic working.
- Services should test every scenario possible and should be tested with 100% codecoverage.
  - if there are model validations, these should be tested too.
- Repositories should test every scenario possible and should be tested with 100% codecoverage.
- 

## Comments

- package
  - doc
    - Describes why the package exists
    - it has the package format:
      - Package the_name the_rest_of_the_text.
- section
  - special format:
	/* ------------------------------- Imports --------------------------- */
	/* ------------------------------- Constants/Types/Variables --------------------------- */
	/* ------------------------------- Methods/Functions --------------------------- */
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

A variable inside a function can have a short name like "a", if it is clear what it is used for.
Like in this example:
a := asserts.New(t)
a.Equals("Check", someVar)

or in a loop, like in this example:
for k,v := range records {
	println("key:", k)
	println("val:", v)
}

In any other case, it is wise to name the variable after the thing it contains.
If is can hold a collection of things, name it plural, like "users".
If it can only hold one value, name it singular, like "user".
if it is a boolean var, start it with something like "has", or "is".
In some checks, you will find a boolean var like "ok",
which is mostly used for checking if an element is present in a map.

It's also common use, when a variable name holds an abbreviation, that the letters are all capitals, or all lowercase.
like "SQLStatement" or "sqlStatement"

## linting

It is nice to start a linter now and then.
make check, or make check2 will run the linters and will check your files for "mistakes".
Try to improve your code with the hints you get from them.

## Code Quality

I wrote a lint tool, which also checks for cognitive complexity.
If code is "too complex" (which is mostly caused by conditions, loops etc.) we need to refactor the code,
because readable code is easy to maintain in the future.

## read :
https://golang.org/doc/effective_go.html
https://github.com/golang/go/wiki/CodeReviewComments
