# introsde-2016-assignment-2-server

This server is called by the client: **https://github.com/ddellagiacoma/introsde-2016-assignment-2-client**

## IMPLEMENTATION
The server is divided in the following packages and classes:

* introsde.rest.ehealth.app
  * App.java
  * MyApplicationConfig.java
* introsde.rest.ehealth.dao
  * LifeCoachDao.java
* introsde.rest.ehealth.model
  * HealthMeasureHistory.java
  * HealthProfile.java
  * MeasureDefinition.java
  * Person.java
* introsde.rest.ehealth.resources
  * MeasureResource.java
  * PersonCollectionResource.java
  * PersonResource.java

The server includes the **App** and **MyApplicationConfig** classes in order to load resource classes and additional features provided by Jersey.

The **LifeCoachDao** class is used to connect the project model to the database, whereas **HealthMisureHistory**, **HealthProfile** **MeasureDefinition** and **Person** classes are the entities.

Finally, **MeasureResource**, **PersonCorrelationResource** and **PersonResource** classes expose the services through RESTful API.

The model supported by the service includes:
```java
public class Person {
 int idPerson;
 String firstname;
 String lastname;
 Date birthdate
 List<HealthProfile> healthprofile;
}
public class HealthProfile {
 int idMeasure,
 int idMeasureDef;
 int idPerson;
 String value;
 Person person;
}
public class HealthMeasureHistory {
 int idMeasureHistory,
 int idPerson;
 int idMeasureDef
 String value;
 Date timestamp;
 MeasureDefinition measureDefinition
 Person person;
}
public class MeasureDefinition {
 int idMeasureDef,
 String measureName;
 String measureType;
}
```

Moreover, the server implements the following operations:
* **Request #1:** *GET /person* should list all the names in your database (wrapped under the root element "people") 
* **Request #2:** *GET /person/{id}* should give all the personal information plus current measures of person identified by {id} (e.g., current measures means current health profile) 
* **Request #3:** *PUT /person/{id}* should update the personal information of the person identified by {id} (e.g., only the person's information, not the measures of the health profile) 
* **Request #4:** *POST /person* should create a new person and return the newly created person with its assigned id (if a health profile is included, create also those measurements for the new person). The body of the request should contain a **Person resource** that follows the examples presented before, without an id (which should be generated after being created) 
* **Request #5:** *DELETE /person/{id}* should delete the person identified by {id} from the system 
* **Request #6:** *GET /person/{id}/{measureType}* should return the list of values (the history) of {measureType} (e.g. weight) for person identified by {id}
* **Request #7:** *GET /person/{id}/{measureType}/{mid}* should return the value of {measureType} (e.g. weight) identified by {mid} for person identified by {id}
* **Request #8:** *POST /person/{id}/{measureType}* should save a new value for the {measureType} (e.g. weight) of person identified by {id} and archive the old value in the history. The body of the request should contain a **Measure resource** that follows the examples presented before, without an id (which should be generated after being created)
* **Request #9:** *GET /measureTypes* should return the list of measures your model supports

Finally, the **lifecoach.sqlite** database has been modified to fit the requests of the assignment.

## DEPLOYMENT

The server WAR file was deployed to Heroku including the database in this way
```sh
heroku war:deploy IntroSdeAss2.war --includes lifecoach.sqlite --app <nameApp>
```
