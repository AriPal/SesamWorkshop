# Sesam workshop
This is a guide to get started with sesam.


## Learning outcome besides the presentation
By the end of this workshop you will learn the following: 
1. How to create a pipe
2. How to add test-data using embedded-data
3. Get better understanding of these DTL's work like `add`, `copy`, `filter`, `apply` and so on
4. How to integrate pipes so one pipe can receive data from another pipe

## Assignment 1: Create a pipe

1. Go to https://portal.sesam.io/
2. Find the node and click on it *DELE 01.1 Workshop Trainee Node*
3. On the left menu, click on the tab pipes
4. On the top right click on the button create pipe
5. Name the pipe *cardealer-source-petter*, add your name in the end
```json
{
  "_id": "cardealer-source-petter",
  "type": "pipe"
}
```
6. Now click on Save pipe


## Assignment 2: Add embedded-data "testdata"
1. Go the the pipe you recently created *cardealer-source-(your name)*. Currently the pipe is not doing anything special except only visible in the GUI platform.
2. Click on the config tab
3. Inside config tab, click on the preview tab
4. The preview tab is extremely helpful during development, it shows two windows on the right side. The window on the top shows the input, the window on the botton shows the output. Keep in mind this is a preview to show how the output will look when data is being sent out. This provides you the oppertunity to change fields/values and see that your transformation logic is working correctly.   
5. Copy and paste this into the pipe after field `"type": "pipe"` 
```json
"source": {
  "type": "embedded",
  "entities": [{
    "_id": "1",
    "VIN": "YV1LFBABDH1145316",
    "price": 850000,
    "model": "Volvo XC90"
  }, {
    "_id": "2",
    "VIN": "JH4KA4576KC031014",
    "price": 350000,
    "model": "Mercedes Benz CLA200"
  }, {
    "_id": "3",
    "VIN": "2T1BR32E56C640079",
    "price": 650000,
    "model": "BMW X5"
  }, {
    "_id": "4",
    "VIN": "JTHFE2C24A2504933",
    "price": 250000,
    "model": "BMW X3"
  }, {
    "_id": "5",
    "VIN": "J8DE5B16477903094",
    "price": 750000,
    "model": "Mercedes GLC 350de"
  }, {
    "_id": "6",
    "VIN": "JH4CC2560PC005719",
    "price": 950000,
    "model": "BMW i8"
  }, {
    "_id": "7",
    "VIN": "1G1ZT51806F128009",
    "price": 350000,
    "model": "Volco XC40"
  }, {
    "_id": "8",
    "VIN": "KMHFG4JG1CA181127",
    "price": 700000,
    "model": "Volco XC60"
  }]
}
``` 
6. Now click on Save pipe


