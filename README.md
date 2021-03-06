# Sample Spring Boot Project

Note this repository is also synched with Travis CI

## The Application
Small Java application that registers for a Java meet up.
The registrations are stored in memory HSQL database.
Once a registration is made, the registration can be viewed using REST end point urls.

* Rest end point to list all registrations: rest/registration/listAll
* Rest end point to list a registration by phone: /rest/registration/phone/{phone}
* Rest end point to list a registration by email: /rest/registration/email/{email id}
* Rest end point to search registrations by a name: /rest/registration/name/{name of the person}

There is one more way to look at the saved registrations. A swing based HSQL DB Manager can be used to look at database during runtime of the application.
Uncomment the @PostConstruct part in class ApplicationBootStrap, and while starting the application, pass the JVM argument -Djava.awt.headless=false     


## Additional Information
An HTML form is created. Boot strap is used in the HTML.
JQuery Validator plugin is added for validation of the form. Although I would prefer React Js in actual products, JQuery was used to build it in short span of time because of readily available validator plugin.

Once the validation is successful, the form data is posted as JSON to the REST end point.

For saving of the registration, JPA is used and HSQL embedded database is automatically configured by spring. 
Following are the Entity classes

* Registration
* AddressComponent

After saving the registration, An attempt is made to recognize some pattern in address to store them as separate components.
Currently only simple German address pattern is recognized like like Werbellin Strasse 69 Neukoeln 12053 Berlin, that contains, street name followed by house no, 5 digit postal code and city name

Another important addition is JINQ streams. With JINQ, the data base queries are treated as simple collections and lamda expressions, and results are obtained as java streams
 
Rest end points are added. The end point save is idempotent, and it is assumed that two people will not register with same phone or email.

* Rest end point to save the registration: rest/registration/save
* Rest end point to list all registrations: rest/registration/listAll
* Rest end point to list a registration by phone: /rest/registration/phone/{phone}
* Rest end point to list a registration by email: /rest/registration/email/{email id}
* Rest end point to search registrations by a name: /rest/registration/name/{name of 
* Rest end point to list any additional address components recognized: 
/rest/registration//addressComponents/{id}

* Rest end point to delete the registration /rest/registration/delete/{id}




## Test cases
Integration test cases are added, that initializes the boot application and tests the actions required using rest template provided by Spring.
These test cases test saving and idempotentence and hence will also test the JPA layer

Unit cases and JPA test cases are not added, since the scope is small and there are no
complex querying of data.


