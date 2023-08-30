# sap-api-challenge-aug23
Solution SAP API Challenge by [qmacro](https://twitter.com/qmacro) - [DJ Adams](https://people.sap.com/dj.adams.sap) in a [Node-Red](https://github.com/node-red) way...

Please visit the Wonderful SAP-API Challenege Series. https://blogs.sap.com/2023/08/01/sap-developer-challenge-apis/
It's a LoL - lots of Learnings....

In this Git-Repo you can get the exclusive content on [Node-Red](http://nodered.org/docs) to solve the Challenege Tasks.

![image](https://github.com/sabarna17/sap-api-challenge-aug23/assets/39834671/897aa5cb-b247-4d3f-8737-da68e4d23707)

## If you are New to Node-RED
Node-Red is a very powerful No-code-low-code Open Source platform Built on Node.JS to develop any low/medium complex applications. 
Please go through the [features](https://nodered.org/#features) for details.
For Installation of Node-Red please visit - https://nodered.org/docs/getting-started/local.
You can also explore the SAP Cloud options - https://blogs.sap.com/2020/09/29/all-about-node-red-deployment-in-sap-cloud-foundry/

## [Task-0](https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-0-learn-to-share-your-task/m-p/276058#M2319)
Create a Subflow. Import the flows from file - [SAP-API Hash](https://github.com/sabarna17/sap-api-challenge-aug23/blob/main/SAP-API%20Hash.json)
After Import the flow will look like ->
![image](https://github.com/sabarna17/sap-api-challenge-aug23/assets/39834671/ba9c4a4f-b81a-400a-a84e-524d507bd61d)

This Subflow is going to be reused accross all the Tasks.

### Note: Copy the entire flows from - [API-Challenge](https://github.com/sabarna17/sap-api-challenge-aug23/blob/main/API-Challenge.json)

Now you can see all the flows are in your Node-Red Dashboard.
And Task-0 solution is looking like this ->
![image](https://github.com/sabarna17/sap-api-challenge-aug23/assets/39834671/72a44516-c62d-475d-b71e-676a1603b223)

You can click on the deploy button ![image](https://github.com/sabarna17/sap-api-challenge-aug23/assets/39834671/748fceb6-85bb-47cf-b31f-4e7eea31cac7)
and get ready to click the inject for Task-0. 
Task-0 Flow -
```json
[
    {
        "id": "2676c647950e6a50",
        "type": "subflow",
        "name": "SAP-API Hash",
        "info": "",
        "category": "",
        "in": [
            {
                "x": 60,
                "y": 60,
                "wires": [
                    {
                        "id": "f3d04762c250c19f"
                    }
                ]
            }
        ],
        "out": [],
        "env": [
            {
                "name": "CommunityID",
                "type": "str",
                "value": "sabarna17"
            },
            {
                "name": "topic",
                "type": "str",
                "value": "Task-N"
            }
        ],
        "meta": {},
        "color": "#DDAA99"
    },
    {
        "id": "cb5f9176afe220eb",
        "type": "function",
        "z": "2676c647950e6a50",
        "name": "Encode & Modify HASH URL",
        "func": "msg.url = \"https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='\" + encodeURIComponent(msg.payload) + \"')\";\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 540,
        "y": 240,
        "wires": [
            [
                "9404eed595446ba1",
                "a8894fb198e6b8ad"
            ]
        ]
    },
    {
        "id": "9404eed595446ba1",
        "type": "http request",
        "z": "2676c647950e6a50",
        "name": "GET Method to Hash your String",
        "method": "GET",
        "ret": "txt",
        "paytoqs": "ignore",
        "url": "",
        "tls": "",
        "persist": false,
        "proxy": "",
        "insecureHTTPParser": false,
        "authType": "",
        "senderr": false,
        "headers": [
            {
                "keyType": "other",
                "keyValue": "CommunityID",
                "valueType": "msg",
                "valueValue": "CommunityID"
            }
        ],
        "x": 870,
        "y": 260,
        "wires": [
            [
                "0b6bdd7085e2d059"
            ]
        ]
    },
    {
        "id": "a8894fb198e6b8ad",
        "type": "debug",
        "z": "2676c647950e6a50",
        "name": "Display URL for Hash",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "statusVal": "",
        "statusType": "auto",
        "x": 780,
        "y": 180,
        "wires": []
    },
    {
        "id": "d1a8fa2ecfdd69a6",
        "type": "inject",
        "z": "2676c647950e6a50",
        "name": "",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "CommunityID",
                "v": "CommunityID",
                "vt": "flow"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "string_for_hash",
        "payloadType": "flow",
        "x": 190,
        "y": 120,
        "wires": [
            []
        ]
    },
    {
        "id": "0b6bdd7085e2d059",
        "type": "debug",
        "z": "2676c647950e6a50",
        "name": "Display Hash Value",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 890,
        "y": 320,
        "wires": []
    },
    {
        "id": "f3d04762c250c19f",
        "type": "change",
        "z": "2676c647950e6a50",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "string_for_hash",
                "tot": "global"
            },
            {
                "t": "set",
                "p": "CommunityID",
                "pt": "msg",
                "to": "CommunityID",
                "tot": "env"
            },
            {
                "t": "set",
                "p": "topic",
                "pt": "msg",
                "to": "topic",
                "tot": "env"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 180,
        "y": 60,
        "wires": [
            [
                "a8f367ce948a7806"
            ]
        ]
    },
    {
        "id": "a8f367ce948a7806",
        "type": "switch",
        "z": "2676c647950e6a50",
        "name": "",
        "property": "payload",
        "propertyType": "msg",
        "rules": [
            {
                "t": "null"
            },
            {
                "t": "eq",
                "v": "",
                "vt": "str"
            },
            {
                "t": "neq",
                "v": "",
                "vt": "str"
            }
        ],
        "checkall": "false",
        "repair": false,
        "outputs": 3,
        "x": 330,
        "y": 60,
        "wires": [
            [
                "1b0cccf6856fdcb6"
            ],
            [
                "1b0cccf6856fdcb6"
            ],
            [
                "cb5f9176afe220eb"
            ]
        ]
    },
    {
        "id": "e9045c1cb34131ed",
        "type": "debug",
        "z": "2676c647950e6a50",
        "name": "Error",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 730,
        "y": 60,
        "wires": []
    },
    {
        "id": "1b0cccf6856fdcb6",
        "type": "change",
        "z": "2676c647950e6a50",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Blank Payload. Please validate String.",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 540,
        "y": 60,
        "wires": [
            [
                "e9045c1cb34131ed"
            ]
        ]
    },
    {
        "id": "6fe93fb053dd0205",
        "type": "comment",
        "z": "2cfa3c0919b4ad10",
        "name": "Task-0",
        "info": "",
        "x": 110,
        "y": 40,
        "wires": []
    },
    {
        "id": "367c6886e2c19073",
        "type": "inject",
        "z": "2cfa3c0919b4ad10",
        "name": "Task-0",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "this-is-the-year-of-the-api",
        "payloadType": "str",
        "x": 130,
        "y": 80,
        "wires": [
            [
                "158cfa572054c5dd"
            ]
        ]
    },
    {
        "id": "158cfa572054c5dd",
        "type": "change",
        "z": "2cfa3c0919b4ad10",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "string_for_hash",
                "pt": "global",
                "to": "payload",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 410,
        "y": 80,
        "wires": [
            [
                "89f9427b496e29fe"
            ]
        ]
    },
    {
        "id": "89f9427b496e29fe",
        "type": "subflow:2676c647950e6a50",
        "z": "2cfa3c0919b4ad10",
        "name": "",
        "env": [
            {
                "name": "topic",
                "value": "Task-0",
                "type": "str"
            }
        ],
        "x": 700,
        "y": 80,
        "wires": []
    }
]
```
## [Task-1}(https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-1-list-the-northwind-entity/m-p/276626)
![image](https://github.com/sabarna17/sap-api-challenge-aug23/assets/39834671/4c6668a9-6fd8-407f-86c8-194e0cbfbf8f)

