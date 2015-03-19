API Code Style
==============

The API is written in PHP, and so respect the PHP style guide.

We are using PHP-5.4, with the intention to move to Hack.


## Namespace

Main namespace is Expensify, but different namespace are existing for the different tools:
Expencli, Supportal, etc

It is recommended to use namespace for all new code.

## AutoLoading

Most of our class can be autoloaded, removing the need to include them by hand.

- Class using namespace MUST follow PSR-4
- The namespace -> directory mapping is defined in ```composer.json``` as we are using Composer built-in PSR-4 autoloader.

- Class without a namespace must be place in the directory `lib` and follow PSR-0. ( Class name is the path to the file, using `_` as directory seperator ).


The logic for autoloading is defined in `_autoload.php`. We are delegating to Composer most of it.
The impact of autoloading is negligeable for the performance of the application. Neveless, we are optimizing it by running Composer with the `optimize` flag which create a class map of our class name and there location, avoiding unecessary disk I/O.

The class map MUST never been edited by hand.


## Composer

External libraries are included through Composer. For PCI Compliance reason, we are commiting them in the repo, and all the composer logic around them.


## Super Globals

The super globlas $_GET, $_POST, $_COOKIES are destroyed by the WAF and merged into $_REQUEST.

The only files allow to use $_REQUEST are the external interfaces ( aka api.php ).
Never use the email from $_REQUEST, always extract it from the AuthToken using ```User_Store::getEmail```.


## Directories

- **_devportal**: Directory storing all the documentation, and the internal tools for 
- **_support**: The support tools.
- **_tasks**: The Core of SmartScan
- **_testify**: Script to help tests some feature in the dev env. NOT DEPLOYED
- **_tests**: All our test scripts. NOT DEPLOYED
    - **integration**: Test the relation between PHP and Auth.
    - **ui**: UI testing, using Selenium. Run and maintained by QA
    - **unit**: PHP Unit testing. Run by Travis on git push.
- **_tools**: Things necessary for the dev env or the build. NOT DEPLOYED
- **_utilities**: Internal API for internal things
- **api**: Public API.
- **externalLib**: where to put the external libraries that can not use composer.
- **lib**: Where all the magic happen.
- **pages**: None "Web-App" pages.
- **script**: location for cli script that need to run on prodution
- **site**: The Web App home folder
- **vendor**: external libraries coming from composer. NO EDIT ARE ALLOWED


## How to deprecated a function or method

Removing a function in 1 pull request without a fallback mechanism is very dnagerous. Please follow these steps:

1. Add the PHPDoc tag `deprecated` with an indication of the replacement method if existing.
2. Add your tag and a date
2. Add a log line, using `Log::deprecated`. 
3. If there is a new function, empty the function and call the wrapper inside.
4. Deploy 
5. After some times, check the log and make sure nobody has used the function
6. Remove it

```PHP
/**
 * 2014-05-02 genintho
 * @deprecated Authentication::validateSessionOrRedirect
 */
function ValidateSession(){
    Log::deprecated( "ValidateSession: use Authentication::validateSessionOrRedirect" );
    Authentication::validateSessionOrRedirect();
}
```
