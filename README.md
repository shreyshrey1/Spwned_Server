# Spwned_Server
Backend for Spwned, CS498RK Final Project

- [Setting Up](#setting-up)
- [Authentication](#authentication)
  - [Registration](#registration)
  - [Sign In](#sign-in)
- [Game](#game)
  - [Game List](#game-list)
  - [Specific Game](#specific-game)
  - [Create Game](#create-game)
  - [Join Game](#join-game)
  - [Start Game](#start-game)
  - [Delete Game](#delete-game)
- [Player](#player)
  - [Player List](#player-list)
  - [Specific Player](#specific-player)
  - [Report Kill](#report-kill)
- [Message] (#message)
  - [Message List] (#message-list)


Setting Up
=============
**Insall npm modules**
    
    npm intall
    
**Run the server**
    
    nodemon server.js
    

 
Authentication
=============

### Registration
    
    POST /api/register
    

**Input**

|   Name   |  Type  | Description | Example |
|:--------:|:------:|:-----------:|:-----------:|
| first_name | string |   **Required** | Alex
| last_name | string |   **Required** | Duh
| email | string |   **Required** | ripped@math.com
| password | string |   **Required** | luigi1234


**Response**

    {
        "message": "register OK",
        "data": {
            "__v": 0,
            "first_name": "Alex",
            "last_name": "Duh",
            "email": "ripped@math.com",
            "password": "$2a$10$.ykPNx3Gq/rcAAuQtjHmIu8roUIS03vjgExKeK4HWSakUJOxlp0LS",
            "_id": "55487085a0608480245f0693",
            "dateCreated": "2015-05-05T07:25:57.186Z"
        }
    }

### Sign In
    
    POST /api/signin
    

**Input**

|   Name   |  Type  | Description | Example |
|:--------:|:------:|:-----------:|:-----------:|
| email | string |   **Required** | ripped@math.com
| password | string |   **Required** | luigi1234


**Response**

    {
        "message": "signin OK",
        "data": {
            "_id": "55487085a0608480245f0693",
            "first_name": "Alex",
            "last_name": "Duh",
            "email": "ripped@math.com",
            "password": "$2a$10$.ykPNx3Gq/rcAAuQtjHmIu8roUIS03vjgExKeK4HWSakUJOxlp0LS",
            "__v": 1,
            "games": [
                "554ab75a9dfab5b206f15cdd"
            ],
            "dateCreated": "2015-05-05T07:25:57.186Z"
        }
    }

Game
=============

### Game List
    
    GET /api/game
    
**Supported Parameters**

|   Name   | Description | Example |
|:--------:| :-----------:|:-----------:|
| where |Game ID|where={"_id":"554ab58e9dfab5b206f15cdc"}
| count |True/False| count=true
    
**Response**

    {
        "message": "game list OK",
        "data": [
            {
                "_id": "554ab2479dfab5b206f15cdb",
                "admin_id": "55487085a0608480245f0693",
                "start_date": "1970-01-01T00:00:01.234Z",
                "end_date": "1970-01-01T00:00:01.234Z",
                "capacity": 15,
                "title": "Brawl Related Spwned",
                "description": "Kill your enemies with GCN Controllers",
                "__v": 0,
                "dateCreated": "2015-05-07T00:31:03.177Z",
                "messages": [],
                "all_kills": [],
                "players": []
            },
            {
                "_id": "554ab58e9dfab5b206f15cdc",
                "admin_id": "55487085a0608480245f0693",
                "start_date": "1970-01-01T00:00:01.234Z",
                "end_date": "1970-01-01T00:00:01.234Z",
                "capacity": 15,
                "title": "Ice Breaker",
                "description": "Meet your roommates at GT",
                "__v": 0,
                "dateCreated": "2015-05-07T00:45:02.075Z",
                "messages": [],
                "all_kills": [],
                "players": []
            }
        ]
    }
    
### Create Game
    
    POST /api/game
    

**Input**

|   Name   |  Type  | Description | Example |
|:--------:|:------:|:-----------:|:-----------:|
| title | string |   **Required** | Brawl Related Spwned
| description | string |   **Required** | Kill your enemies with GCN Controllers
| admin_id | string |   **Required** | 55487085a0608480245f0693 
| start_date | string |   **Required** | TBD
| end_date | string |   **Required** | TBD
| capacity | number |   **Required** | 15


**Response**

    {
        "message": "game creation OK",
        "data": {
            "__v": 0,
            "admin_id": "55487085a0608480245f0693",
            "start_date": "1970-01-01T00:00:01.234Z",
            "end_date": "1970-01-01T00:00:01.234Z",
            "capacity": 15,
            "title": "Brawl Related Spwned",
            "description": "Kill your enemies with GCN Controllers",
            "_id": "554ab75a9dfab5b206f15cdd",
            "dateCreated": "2015-05-07T00:52:42.760Z",
            "messages": [],
            "all_kills": [],
            "players": []
        }
    }
    
### Specific Game
    
    GET /api/game/:id
    
**Supported Parameters**

|   Name   | Description | Example |
|:--------:| :-----------:|:-----------:|
| none |none|none
    
**Response**

    {
        "message": "game ID OK",
        "data": {
            "_id": "554ab75a9dfab5b206f15cdd",
            "admin_id": "55487085a0608480245f0693",
            "start_date": "1970-01-01T00:00:01.234Z",
            "end_date": "1970-01-01T00:00:01.234Z",
            "capacity": 15,
            "title": "Brawl Related Spwned",
            "description": "Kill your enemies with GCN Controllers",
            "__v": 6,
            "dateCreated": "2015-05-07T00:52:42.760Z",
            "messages": [],
            "all_kills": [],
            "players": [
                {
                    "killed": [],
                    "isAlive": true,
                    "dateCreated": "2015-05-08T04:37:45.815Z",
                    "_id": "554c3d9980f70334099d27b9",
                    "user_id": "55487085a0608480245f0693"
                }
            ]
        }
    }
    
### Join Game
    
    PUT /api/game/:id/join  
    

**Input**

|   Name   |  Type  | Description | Example |
|:--------:|:------:|:-----------:|:-----------:|
| user_id | string |   **Required** | 55487085a0608480245f0693 

**Response**

    {
        "message": "game join OK",
        "data": {
            "user_id": "55487085a0608480245f0693",
            "player_id": "554c3d9980f70334099d27b9",
            "game_id": "554ab75a9dfab5b206f15cdd"
        }
    }
    
### Start Game
    
    PUT /api/game/:id/start
    

**Input**

|   Name   |  Type  | Description | Example |
|:--------:|:------:|:-----------:|:-----------:|
| none | none |   none | none

**Response**

    {
        "message": "game start OK",
        "data": {
            "game_id": "554ab75a9dfab5b206f15cdd"
        }
    }



### Delete Game
    
    DELETE /api/game/:id

**Response**

    {
        TBD
    }
    
Player
=============

### Player List
    
    GET /api/player/
    
**Supported Parameters**

|   Name   | Description | Example |
|:--------:| :-----------:|:-------------:|
| where |User ID + Game ID|where={"user_id":"554ab15cdc","game_id":"55415cdd"}
| count |True/False| count=true
    
**Response**

    {
        "message": "player list OK",
        "data": [
            {
                "_id": "554d1e383bad7b454a9a7259",
                "user_id": "55487085a0608480245f0693",
                "game_id": "554d1e0d3bad7b454a9a7258",
                "__v": 4,
                "dateCreated": "2015-05-08T20:36:08.361Z",
                "secret_code": "HI8H",
                "isAlive": true,
                "killed": [
                    "554d20f7da2240bf507c6dc9",
                    "554d212fda2240bf507c6dca",
                    "554d21e0e9c013ba522df532",
                    "554d21e7e9c013ba522df533"
                ],
                "killer_id": null,
                "target_id": "554d1e433bad7b454a9a725a"
            },
            {
                "_id": "554d1e433bad7b454a9a725a",
                "user_id": "554cd2279f6de9303d1a4310",
                "game_id": "554d1e0d3bad7b454a9a7258",
                "__v": 0,
                "dateCreated": "2015-05-08T20:36:19.212Z",
                "secret_code": "GYPB",
                "isAlive": false,
                "killed": [],
                "killer_id": "554d1e383bad7b454a9a7259",
                "target_id": "554d1e383bad7b454a9a7259"
            }
        ]
    }

### Specific Player
    
    GET /api/player/:id
    
**Supported Parameters**

|   Name   | Description | Example |
|:--------:| :-----------:|:-----------:|
| none |none|none
    
**Response**

    {
        "message": "player ID OK",
        "data": {
            "_id": "554d1e383bad7b454a9a7259",
            "user_id": "55487085a0608480245f0693",
            "game_id": "554d1e0d3bad7b454a9a7258",
            "__v": 4,
            "dateCreated": "2015-05-08T20:36:08.361Z",
            "secret_code": "HI8H",
            "isAlive": true,
            "killed": [
                "554d20f7da2240bf507c6dc9",
                "554d212fda2240bf507c6dca",
                "554d21e0e9c013ba522df532",
                "554d21e7e9c013ba522df533"
            ],
            "killer_id": null,
            "target_id": "554d1e433bad7b454a9a725a"
        }
    }

### Report Kill
    
    PUT /api/player/:id/report
    
**Supported Parameters**

|   Name   | Description | Example |
|:--------:| :-----------:|:-----------:|
| secret_code |string|GYPB
    
**Response**

    {
        "message": "player Report OK",
        "data": {
            "killer_id": "554d1e383bad7b454a9a7259",
            "target_id": "554d1e433bad7b454a9a725a",
            "game_id": "554d1e0d3bad7b454a9a7258",
            "_id": "554d21e7e9c013ba522df533",
            "dateCreated": "2015-05-08T20:51:51.759Z",
            "timeOfKill": "2015-05-08T20:51:51.759Z"
        }
    }
    
Message
=============
### Message List
    
    GET /api/p/:id  // where id refers to playerid
    
**Supported Parameters**

|   Name   |  Type  | Description | Example |
|:--------:|:------:|:-----------:|:-----------:|
| recipient_id | Player ID or NULL |   **Required** | 55487085a0608480245f0693 
| sender_id | Player ID |   **Required** | 554d1908d3317a9b11a1a34c
| body | String |   **Required** | "hello world"
| predecessor | Message ID |   **Required** | 554d2b488277a3ca39b354be

**Response**

    {
        "message": "message OK",
        "data": {
            "__v": 0,
            "sender_id": "554d1908d3317a9b11a1a34c",
            "body": "testing with id",
            "_id": "554d2b488277a3ca39b354be",
            "predecessor": null,
            "dateCreated": "2015-05-08T21:31:52.583Z",
            "recipient_id": "554ab75a9dfab5b206f15cdd"
        }
    }
