- [Getting All Courses](#getting-all-courses)
- [Adding To Selected Courses](#adding-to-selected-courses)
  - [Function Definition](#function-definition)
- [Get Instance Info](#get-instance-info)
  - [Sample Info](#sample-info)
- [Registering a class](#registering-a-class)

## Getting All Courses
Instance IDs can be extracted from [here.][courselist]

## Adding To Selected Courses
Following function is being used to add a course to a **selected** list. 
```js
/* 
First argument - instance ID that we got earlier  
Second argument - action(1 - add, other numbers -  NO IDEA)
*/ 
addCourseToShopingCart(12130, 1)
```

### Function Definition
This function can be defined 
anywhere, where ```Ext``` javascript 
object is present, e.g. 
you can even add courses from 
[GPA calculator page.][calcgpa]
```js
function addCourseToShopingCart(instanceid, action) { 
	Ext.Ajax.request({ 
		url: '/my-registrar/course-registration/json', 
		method: "GET", 
		params:{ method: 'shoppingCartAddRemove', instanceid:instanceid, action: action }, 
		success: function(response, request) {console.log('E BOI')}, 
		failure: function(response, request) { console.log(response)} 
	}); 
} 
```
Modified version of the function, to add multiple instances to the selected list.
```js
function addInstances(instances) {  
  if (instances.length < 1) return;
  instanceid = instances.shift();
  Ext.Ajax.request({ 
    url: '/my-registrar/course-registration/json', 
    method: "GET", 
    params:{ method: 'shoppingCartAddRemove',
    instanceid:instanceid, action: 1},
    success: function(response, request) {
      addInstances(instances)
    }, 
    failure: function(response, request) {
      console.log(response)
    }
  }); 
}
```

## Get Instance Info
This function can be called on the [selected courses page][selected], it shows info about the courses in your selected list.
```js
function getInfo(instanceid)
{   
	var data = Drupal.settings.instanceSections[instanceid];
	console.log(data)   
}
```
### Sample Info
Particularly interesting attributes are `NAME` and `CLASSSECTIONCODE`, 
they are used in the registering step. 
This example contains info from 4 instances.
```js
{
  "11586": {
    "TITLE": "Writing Fellows I � Composition and Collaboration in Theory and Practice  - Waiting List is available",
    "COMPONENTS": [
      {
        "METHODNAME": "Lecture",
        "CLASSES": [
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 17:00/17:50; W - 17:00/17:50; F - 17:00/17:50; ",
            "NAME": "instance_11586_component_10834",
            "CLASSSECTIONCODE": "1",
            "COURSECOMPONENTID": "10834",
            "CLASSCAPACITY": "20",
            "CLASSSTUDENTS": "18",
            "INSTANCEID": "11586",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-orange.png"
          }
        ]
      }
    ]
  },
  "11626": {
    "TITLE": "Beginning French I - Waiting List is available",
    "COMPONENTS": [
      {
        "METHODNAME": "Lecture",
        "CLASSES": [
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 11:00/11:50; T - 11:00/11:50; W - 11:00/11:50; R - 11:00/11:50; ",
            "NAME": "instance_11626_component_10880",
            "CLASSSECTIONCODE": "1",
            "COURSECOMPONENTID": "10880",
            "CLASSCAPACITY": "20",
            "CLASSSTUDENTS": "6",
            "INSTANCEID": "11626",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-green.png"
          },
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 14:00/14:50; T - 14:00/14:50; W - 14:00/14:50; R - 14:00/14:50; ",
            "NAME": "instance_11626_component_10880",
            "CLASSSECTIONCODE": "2",
            "COURSECOMPONENTID": "10880",
            "CLASSCAPACITY": "20",
            "CLASSSTUDENTS": "14",
            "INSTANCEID": "11626",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-yellow.png"
          },
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 16:00/16:50; T - 16:00/16:50; W - 16:00/16:50; R - 16:00/16:50; ",
            "NAME": "instance_11626_component_10880",
            "CLASSSECTIONCODE": "3",
            "COURSECOMPONENTID": "10880",
            "CLASSCAPACITY": "20",
            "CLASSSTUDENTS": "4",
            "INSTANCEID": "11626",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-green.png"
          }
        ]
      }
    ]
  },
  "12128": {
    "TITLE": "Calculus III - Waiting List is available",
    "COMPONENTS": [
      {
        "METHODNAME": "Lecture",
        "CLASSES": [
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 10:00/10:50; W - 10:00/10:50; F - 10:00/10:50; ",
            "NAME": "instance_12128_component_11663",
            "CLASSSECTIONCODE": "1",
            "COURSECOMPONENTID": "11663",
            "CLASSCAPACITY": "48",
            "CLASSSTUDENTS": "29",
            "INSTANCEID": "12128",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-yellow.png"
          },
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 13:00/13:50; W - 13:00/13:50; F - 13:00/13:50; ",
            "NAME": "instance_12128_component_11663",
            "CLASSSECTIONCODE": "2",
            "COURSECOMPONENTID": "11663",
            "CLASSCAPACITY": "48",
            "CLASSSTUDENTS": "11",
            "INSTANCEID": "12128",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-green.png"
          },
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 16:00/16:50; W - 16:00/16:50; F - 16:00/16:50; ",
            "NAME": "instance_12128_component_11663",
            "CLASSSECTIONCODE": "3",
            "COURSECOMPONENTID": "11663",
            "CLASSCAPACITY": "48",
            "CLASSSTUDENTS": "48",
            "INSTANCEID": "12128",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-red.png"
          }
        ]
      },
      {
        "METHODNAME": "Recitation",
        "CLASSES": [
          {
            "DAYS": "T ",
            "TIMESLOT": "</br>T - 13:30/14:45; ",
            "NAME": "instance_12128_component_11664",
            "CLASSSECTIONCODE": "1",
            "COURSECOMPONENTID": "11664",
            "CLASSCAPACITY": "24",
            "CLASSSTUDENTS": "25",
            "INSTANCEID": "12128",
            "GROUPNAME": "Recitation",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-red.png"
          },
          {
            "DAYS": "T ",
            "TIMESLOT": "</br>T - 15:00/16:15; ",
            "NAME": "instance_12128_component_11664",
            "CLASSSECTIONCODE": "2",
            "COURSECOMPONENTID": "11664",
            "CLASSCAPACITY": "24",
            "CLASSSTUDENTS": "18",
            "INSTANCEID": "12128",
            "GROUPNAME": "Recitation",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-yellow.png"
          },
          {
            "DAYS": "T ",
            "TIMESLOT": "</br>T - 16:30/17:45; ",
            "NAME": "instance_12128_component_11664",
            "CLASSSECTIONCODE": "3",
            "COURSECOMPONENTID": "11664",
            "CLASSCAPACITY": "24",
            "CLASSSTUDENTS": "7",
            "INSTANCEID": "12128",
            "GROUPNAME": "Recitation",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-green.png"
          },
          {
            "DAYS": "R ",
            "TIMESLOT": "</br>R - 13:30/14:45; ",
            "NAME": "instance_12128_component_11664",
            "CLASSSECTIONCODE": "4",
            "COURSECOMPONENTID": "11664",
            "CLASSCAPACITY": "24",
            "CLASSSTUDENTS": "21",
            "INSTANCEID": "12128",
            "GROUPNAME": "Recitation",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-orange.png"
          },
          {
            "DAYS": "R ",
            "TIMESLOT": "</br>R - 15:00/16:15; ",
            "NAME": "instance_12128_component_11664",
            "CLASSSECTIONCODE": "5",
            "COURSECOMPONENTID": "11664",
            "CLASSCAPACITY": "24",
            "CLASSSTUDENTS": "13",
            "INSTANCEID": "12128",
            "GROUPNAME": "Recitation",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-yellow.png"
          },
          {
            "DAYS": "R ",
            "TIMESLOT": "</br>R - 16:30/17:45; ",
            "NAME": "instance_12128_component_11664",
            "CLASSSECTIONCODE": "6",
            "COURSECOMPONENTID": "11664",
            "CLASSCAPACITY": "24",
            "CLASSSTUDENTS": "4",
            "INSTANCEID": "12128",
            "GROUPNAME": "Recitation",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-green.png"
          }
        ]
      }
    ]
  },
  "12130": {
    "TITLE": "Probability - Waiting List is available",
    "COMPONENTS": [
      {
        "METHODNAME": "Lecture",
        "CLASSES": [
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 11:00/11:50; W - 11:00/11:50; F - 11:00/11:50; ",
            "NAME": "instance_12130_component_11666",
            "CLASSSECTIONCODE": "1",
            "COURSECOMPONENTID": "11666",
            "CLASSCAPACITY": "72",
            "CLASSSTUDENTS": "42",
            "INSTANCEID": "12130",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-yellow.png"
          },
          {
            "DAYS": "M ",
            "TIMESLOT": "</br>M - 17:00/17:50; W - 17:00/17:50; F - 17:00/17:50; ",
            "NAME": "instance_12130_component_11666",
            "CLASSSECTIONCODE": "2",
            "COURSECOMPONENTID": "11666",
            "CLASSCAPACITY": "72",
            "CLASSSTUDENTS": "59",
            "INSTANCEID": "12130",
            "GROUPNAME": "Lecture",
            "CLASSCAPACITYIMG": "/sites/all/themes/registrar/images/status-orange.png"
          }
        ]
      }
    ]
  }
}
```
## Registering a class
Link with the following structure is used to 
register the class: 

```python
# Python code
address = "https://registrar.nu.edu.kz/my-registrar/course-registration/json?method=registerSections&sections=" + '&'.join('{0}_section_{1}'.format(NAME[i], CLASSSECTIONCODE[i]) for i in len(NAME))
# Where NAME and CLASSSECTIONCODE are obtained from the previous section.
# One class may require multiple names, if there are labs or recitations alongside the lecture.
```
Example link for Programming Languages with lab
*(notice that it has two components, one for the lecture and another one for the lab)*: 
https://registrar.nu.edu.kz/my-registrar/course-registration/json?method=registerSections&sections=instance_12219_component_11765_section_1&instance_12219_component_11766_section_3


[courselist]: https://registrar.nu.edu.kz/my-registrar/course-registration/json?method=getCourseList
[calcgpa]: https://registrar.nu.edu.kz/my-registrar/calcgpa
[selected]: https://registrar.nu.edu.kz/my-registrar/course-registration/selected
