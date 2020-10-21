# Common Sense Media XML API validator

This script designed specifically to test xml version of API for https://www.commonsensemedia.org/. The script created 
with help of Ruby programming language and implemented as command line tool. The script makes a REST API call, receives
xml response and validates received response against json spec. Results of script execution presented in an output 
html report.

## Prerequisites

Before proceeding to script execution you should preinstall version of Ruby programming language. The best way to do it 
is to install version control system and install the latest stable version of programming language with help of this system.

If you familiar with different version control systems you can use any system of your choice. If you are not familiar 
with any of them you can try to use RVM (more details can be found here: https://rvm.io/).

To install RVM you can simply run next command from command line interface:
```
\curl -sSL https://get.rvm.io | bash -s stable --ruby
```
To use RVM right after installation you need to restart your command line tool or open need tab or just execute:
```
source /Users/[you home folder]/.rvm/scripts/rvm
```
To check a list of installed Ruby versions:
```
rvm list
``` 
You should be able to see something like:
```
=* ruby-2.7.0 [ x86_64 ]

# => - current
# =* - current && default
#  * - default
```

If you see this output, you have Ruby version 2.7 installed in your system. To confirm it, check version of Ruby in command line:
```
 ✗ ruby -v
ruby 2.7.0p0 (2019-12-25 revision 647ee6f091) [x86_64-darwin19]
``` 
With the next step you need to install bundler - the library which allows installing Ruby gems from GemFile:  
```
gem install bundler
```
As the last step you need to install all required gems, make sure you run it from common_sense_media folder where Gemfile located:
```
bundler install
```

Make sure all gems installed without errors. Json gem uses native extension, if you are getting an error here, possible 
solution will be Xcode installation with updated command line tool. Please do a search for installation instructions for 
your particular MacOs version.

Please note: Installation instructions above provided for Mac OS, the script still should work fine on Windows, but you 
need to figure out same installation steps adapted for Windows.

## How to run script

As mentioned before, script implemented as a command line tool, and can be executed from command line with a list of possible options.
For simplicity special file run.sh was created. In this file you can find example of run command.

To run this file you need just execute:
```
sh run_script.sh
```

The uncommented command in a file will be executed (make sure "#" is removed in the beginning of the line).

Command options:

* --domain or -d, Domain name of the website
* --api-key or -k, API key for access
* --element or -e, Element name for API request
* --channel or -c, Channel parameter for API request
* --check-inside-node, Specify symbol or text which you would like to test inside every feed
* --check-ampersand = true, Check ampersand inside every feed
* --limit or -l, Number of product for test-- all or any number
* --log-file-folder, Relative to the log file
* --secured or -s, use secured url, default false
* --input-spec-file or -i, Relative path to the element specification file
* --output-report-directory or -o, The output directory for report file

## Script structure

* **_etc_** folder contains all json specs for xml responses. Every spec represent required elements that should be 
presented in xml response. The response can contain simple elements with some set of possible values, in this case set of 
values specified in spec separated by a comma, or value can be any, in this case spec contains "*" as a value. Element 
also can contain attributes, in this case, attributes and their values specified in spec. The response can also contain 
complex elements with child elements, all child elements also should be represented in a spec followed by the same rules
 as simple elements.
* **_lib_** folder contains the script code. `xml_element_validation.rb` - main script file with all source code. 
* **_common_** folder with common code. 
`custom_error.rb` - special custom error for xml exceptions. 
`test_report_writer.rb` - report writer, if you would like to change report style or update some html elements
 inside report you probably would like to review this file first. 
 `test_spec.rb` - file parcel for json test spec.
* `gitignore` the file responsible for files visible for git repository. If you would like to hide something from hide, you
need to specify them here. 
* `GemFile` file where all required Ruby gems specified.
* `GemFile.lock` Bundler generated file where recorded the exact versions of gems that were installed.
* `run.sh` bash file to simplify test run from the command line.