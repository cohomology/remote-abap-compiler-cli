# remote-abap-compiler
This is the command line utility for a remote ABAP compiler. The corresponding library is contained
in another node.js project [remote-abap-compiler](https://github.com/cohomology/remote-abap-compiler).

## Usage

The compiler works by calling ABAP in Eclipse APIs (http requests) on a remote ABAP system. For this purpose, temporary
classes are generated and deleted. The source code given by the user is inserted into the "Local types" include of a 
generated ABAP class. 

Prerequsite: The source code of the user must have a class called "MAIN" with a main method, called "RUN", which imports
a parameter of type `REF TO IF_OO_ADT_CLASSRUN_OUT`. Via this parameter, the user can output information to the console. 

If the compilation succeeds, the class is executed and the output is given. If the compilation fails, the syntax errors 
are returned.

## Basic ABAP template

```abap
class main definition.
  public section.
    methods run importing out type ref to if_oo_adt_classrun_out.
endclass.

class main implementation.
  method run.
    out->write( 'Hello World' ).
  endmethod.
endclass.
```

## Building the project
Please have [node.js](https://nodejs.org/en) installed (with npm). As editor, [Visual Studio Code](https://code.visualstudio.com/) is recommended.

The install the prerequisites, type the following in the checked-out repo folder:
```
npm install
```
To build the whole project and install the executable in a shared location, type:
```
npm link
```
## Command line invokation

```
abapc compile -u https://url_of_abap_server:port -n user_name -c client file.abap
```
