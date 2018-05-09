# OSIPi REST Api Integration

## About OSIPi Rest

The OSIPi REST API is HATEOAS based, and provides access to the entire Asset Framework Structure.
For more information about the API itself, please take a look at [the official page](https://techsupport.osisoft.com/Documentation/PI-Web-API/help/getting-started.html). Also, this [article](https://pisquare.osisoft.com/community/developers-club/restful-pi-system-access/blog/2015/04/17/getting-started-with-pi-web-api) goes a long way explaining the concepts.

## Thingworx Implementation.

In thingworx, the following functionality is available:

* Automatically generate the Thingmodel based on the AF from Pi. Generation can be recursive (meaning create a thing for each element in the AF structure) or flat, meaning that you only go one level deep.
* Automatically update the properties values based on the latest OSIPi data.

### Thingworx Entities

* `OsiPiWebConnectorThingTemplate`: Responsable for connecting to OSIPi, and doing basic requests
* `OsiPiWebTransformerThing`: Handles transforming the OSiPi data into an infotable, as well as generating the Thingmodel based on that infotable. 
    * The flat method also looks at the tagId for each property, and includes it in the property name.
    * The generated property descriptions contains essential information about the property, linking it to OsiPi. It cannot be manually modified.
* `OsiPiWebThingShape`: ThingShape that marks all the OSIPi exported elements. A service is availalbe on each allowing the automatic property updates
* `OsiPiUpdaterScheduler`: Automatically updates all properties of all things marked with the above thingshape.