# Sesam workshop
This is a guide to get started with sesam.

References:
- [Sesam GUI platform](https://portal.sesam.io/)
- [List of all DTL's](https://docs.sesam.io/DTLReferenceGuide.html#concat-dtl-function)


## Learning outcome besides the presentation
By the end of this workshop you will learn the following: 
1. Create a pipe
2. Start a pipe (send data to ouput)
3. Preview data for debugging
4. Establish connection between pipes
5. Add mock-data using embedded-data
6. Get better understanding of various DTL's like `add`, `copy`, `filter`, `apply`

## Problem statement
Cardealer has a system that shows cars that are sold and not sold like Volvo, Mercedes-Benz and BMW and so on. One of his supplier has asked him if he can create an endpoint with the following information: 


The supplier wants to get: 
- Only cars that are sold
- Only cars that cost over 500.000
- If car cost more than 800.000, add a field `expensive:true`
- Create a field `brandType` that concats field `brand` and `type` e.g. `brandType: Volvo XC90`
- Remove field brand and type


The work tasks that needs to be solved (note when each pipe has been saved, remember to start the pipe so it can output the result): 
1. Create a cardealer-source-(yourname) pipe that sends embedded data out 
2. Create a cardealer-inbound-(yourname) pipe that only receives data from cardealer-source-(yourname) and sends out without doing any changes to the data 
3. Create a global-cardealer-(yourname) pipe that only receives data from cardealer-inbound-(yourname) and sends out without doing any changes to the data 
4. Create a cardealer-preperation-(yourname) pipe that only receives data from global-cardealer-(yourname) and sends out without doing any changes to the data
5. Create a cardealer-endpoint-(yourname) pipe that only receives data from cardealer-preperation-(yourname) and sends out without doing any changes to the data
6. Go to the cardealer-preperation-(yourname) pipe as previously created, and add the following changes using DTL's as shown in the presentation or can be find [here](https://docs.sesam.io/DTLReferenceGuide.html#concat-dtl-function): 

- Only cars that are sold (Hint: filter)
- Only cars that cost over 500.000 (hint: filter)
- If car cost more than 800.000, add a field `expensive:true` (hint: if)
- Create a field `brandType` that concats field `brand` and `type` e.g. `brandType: Volvo XC90` (hint: concat)
- Remove field brand and type (hint: remove)

Input we receive in cardealer-preperation-(yourname) pipe: 
```json
{
  "cardealer-source-dler:VIN": "JH4CC2560PC005719",
  "cardealer-source-dler:brand": "BMW",
  "cardealer-source-dler:manufacturedYear": 2014,
  "cardealer-source-dler:price": 950000,
  "cardealer-source-dler:sold": true,
  "cardealer-source-dler:type": "i8"
}
```

Output we send out in cardealer-preperation-(yourname) pipe (expected result): 
```json
{
  "cardealer-preperation-dler:brandModel": "BMW i8",
  "cardealer-preperation-dler:expensive": true,
  "cardealer-source-dler:VIN": "JH4CC2560PC005719",
  "cardealer-source-dler:manufacturedYear": 2014,
  "cardealer-source-dler:price": 950000,
  "cardealer-source-dler:sold": true
}
```

Once all tasks are completed the outcome should look like this (your name in the end of each pipe). Keep in mind the embedded-data pipe is not something we will create in this workshop, it has been added to illustrate that this data will come from an actual system (external service). In our case we have created some mock-up data in cardealer-inbound-(yourname) pipe. 
![image](https://user-images.githubusercontent.com/8822677/174970799-c80f789f-f12f-492f-8d26-82ae1f5c83c2.png)

## Solution 1: Create a pipe with embedded-data
1. Click on create a new pipe
2. Copy and paste this into the pipe (remember to add your name in the end of pipe name):
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
7. Start the pipe
8. Go to output tab and verify data is being sent out

## Solution 2: Create an inbound pipe
1. Click on create a new pipe
2. Copy and paste this into the pipe (remember to add your name in the end of pipe name):
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
3. Now click on Save pipe
4. Start the pipe
5. Go to output tab and verify data is being sent out

## Solution 3: Create a global pipe
1. Click on create a new pipe
2. Copy and paste this into the pipe (remember to add your name in the end of pipe name):
```json
{
  "_id": "global-cardealer-dler",
  "type": "pipe",
  "source": {
    "type": "dataset",
    "dataset": "cardealer-inbound-dler"
  },
  "metadata": {
    "global": true
  }
}
```
3. Now click on Save pipe
4. Start the pipe
5. Go to output tab and verify data is being sent out

## Solution 4: Create a preperation pipe
1. Click on create a new pipe
2. Copy and paste this into the pipe (remember to add your name in the end of pipe name):
```json
{
  "_id": "cardealer-preperation-dler",
  "type": "pipe",
  "source": {
    "type": "dataset",
    "dataset": "global-cardealer-dler"
  }
}
```
3. Now click on Save pipe
4. Start the pipe
5. Go to output tab and verify data is being sent out

## Solution 5: Create an endpoint pipe
1. Click on create a new pipe
2. Copy and paste this into the pipe (remember to add your name in the end of pipe name):
```json
{
  "_id": "cardealer-endpoint-dler",
  "type": "pipe",
  "source": {
    "type": "dataset",
    "dataset": "cardealer-preperation-dler"
  }
}
```
3. Now click on Save pipe
4. Start the pipe
5. Go to output tab and verify data is being sent out

## Solution 6: Add transformation logic to preperation pipe
1. Gå to pipe *cardealer-preperation-(yourname)*
2. Add field transformation like: 
```json
{
  "_id": "cardealer-preperation-dler",
  "type": "pipe",
  "source": {
    "type": "dataset",
    "dataset": "global-cardealer-dler"
  },
  "transform": {
    "type": "dtl",
    "rules": {
      "default": [
        ["filter",
          ["and",
            ["eq", "_S.sold", true],
            ["gt", "_S.price", 500000]
          ]
        ],
        ["copy", "*"],
        ["if",
          ["gt", "_S.price", 500000],
          ["add", "expensive", true]
        ],
        ["add", "brandModel",
          ["concat", "_S.brand", " ", "_S.type"]
        ],
        ["remove", "brand"],
        ["remove", "type"]
      ]
    }
  }
}

```
4. Start the pipe
5. Go to output tab and verify data is being sent out

The following describes what each DTL in the code above does: 
- The `filter` DTL gets only cars that are sold equal to true and price over 500.000 KR
- The `copy` DTL copies everything from input to output
- The `concat` DTL is used to put text-values together
- The `remove` DTL is used to remove a field or multiple fields
- The `if` DTL is a contional statement used to add an field if condition is true







