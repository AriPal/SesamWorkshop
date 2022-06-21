# Sesam workshop
This is a guide to get started with sesam.


## Learning outcome besides the presentation
By the end of this workshop you will learn the following: 
1. How to create a pipe
2. How to add test-data using embedded-data
3. Get better understanding of these DTL's work like `add`, `copy`, `filter`, `apply` and so on
4. How to integrate pipes so one pipe can receive data from another pipe

Highlevel overview of what we are going to create: 
![image](https://user-images.githubusercontent.com/8822677/174827832-ee1692cb-2f2b-4ed9-b8fc-a191ed165f4c.png)


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
7. Verify the pipe is created in pipes page:
![image](https://user-images.githubusercontent.com/8822677/174819092-2ed9b71b-59b1-42a5-ac08-d6cd6df4cd0f.png)



## Assignment 2: Add embedded-data "testdata"
1. Go the the pipe you recently created *cardealer-source-(your name)*. Currently the pipe is not doing anything special except only visible in the GUI platform.
2. Click on the config tab
3. Inside config tab, click on the preview tab
4. The preview tab is extremely helpful during development, it shows two windows on the right side. The window on the top shows the input, the window on the botton shows the output. Keep in mind this is a preview to show how the output will look when data is being sent out. This provides you the oppertunity to change fields/values and see that your transformation logic is working correctly.   
5. Copy and paste this into the pipe after field `"type": "pipe"` 
```json
{
  "_id": "cardealer-source-(yourname)",
  "type": "pipe",
  "source": {
    "type": "embedded",
    "entities": [{
      "_id": "1",
      "type": "XC90",
      "VIN": "YV1LFBABDH1145316",
      "brand": "Volvo",
      "manufacturedYear": 2019,
      "price": 850000,
      "sold": true
    }, {
      "_id": "2",
      "type": "CLA200",
      "VIN": "JH4KA4576KC031014",
      "brand": "Mercedes-Benz",
      "manufacturedYear": 2015,
      "price": 350000,
      "sold": false
    }, {
      "_id": "3",
      "type": "X5",
      "VIN": "2T1BR32E56C640079",
      "brand": "BMW",
      "manufacturedYear": 2013,
      "price": 650000,
      "sold": false
    }, {
      "_id": "4",
      "type": "X3",
      "VIN": "JTHFE2C24A2504933",
      "brand": "BMW",
      "manufacturedYear": 2010,
      "price": 250000,
      "sold": true
    }, {
      "_id": "5",
      "type": "CLA350de",
      "VIN": "J8DE5B16477903094",
      "brand": "Mercedes-Benz",
      "manufacturedYear": 2018,
      "price": 750000,
      "sold": false
    }, {
      "_id": "6",
      "type": "i8",
      "VIN": "JH4CC2560PC005719",
      "brand": "BMW",
      "manufacturedYear": 2014,
      "price": 950000,
      "sold": true
    }, {
      "_id": "7",
      "type": "XC40",
      "VIN": "1G1ZT51806F128009",
      "brand": "Volco",
      "manufacturedYear": 2014,
      "price": 350000,
      "sold": true
    }, {
      "_id": "8",
      "type": "XC60",
      "VIN": "KMHFG4JG1CA181127",
      "brand": "Volco",
      "manufacturedYear": 2021,
      "price": 700000,
      "sold": false
    }]
  }
}
``` 
6. Now click on Save pipe
7. Verify in the preview window bottom-right that the first result is car type Volvo XC90: 
![image](https://user-images.githubusercontent.com/8822677/174818810-7975f0b7-60f7-4d48-977f-ddb01babb5d5.png)

## Assignment 3: Create an inbound pipe
1. Click on create a new pipe
2. Copy and pase this into the pipe (remember to add your name in the end):
```json
{
  "_id": "cardealer-inbound-(yourname)",
  "type": "pipe",
  "source": {
    "type": "dataset",
    "dataset": "cardealer-source-dler"
  }
}

```






