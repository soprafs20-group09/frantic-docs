# frantic-docs
A documentation repository for frantic. Contains [REST](#frantic-restful-api) and [WebSocket](#frantic-websocket-api) API.

---
---

## Frantic RESTful API

### GET /lobbies
get list of lobbies

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| q | query | filter lobby names or creators | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | list of lobbies |

#### POST /lobbies
create a lobby from username

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | lobby created |
| 400 | Bad request. Request body is missing or invalid. |

### PUT /lobbies/{id}
join a lobby with username

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 201 | OK. Username added to lobby. |
| 400 | Bad request. Request body is missing or invalid. |
| 403 | Forbidden. Lobby is private. |
| 404 | Lobby not found. |
| 409 | Username already exists on this server. |

---
---

## Frantic Websocket API

###  `publish` /app/register

*Register Connection* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>token </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "token": "123-abc-456-def"
}
```
---


###  `subscribe` /user/queue/register

*Player Registered Successfully* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>username </td>
  <td>string</td>
</tr>
<tr>
  <td>lobbyId </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "username": "user1",
  "lobbyId": "1"
}
```
---


###  `publish` /app/lobby/:id/settings

*Set Lobby Settings* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>lobbyName </td>
  <td>string</td>
</tr>
<tr>
  <td>duration </td>
  <td>string</td>
</tr>
<tr>
  <td>turnDuration </td>
  <td>string</td>
</tr>
<tr>
  <td>publicLobby </td>
  <td>boolean</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "lobbyName": "kyrill's lobby",
  "duration": "medium",
  "turnDuration": "normal",
  "publicLobby": "false"
}
```
---


###  `subscribe` /user/queue/lobby/:id/lobby-state

*Update Lobby* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>players </td>
  <td>array</td>
</tr>
<tr>
  <td>players.username </td>
  <td>string</td>
</tr>
<tr>
  <td>players.admin </td>
  <td>boolean</td>
</tr>
<tr>
  <td>settings </td>
  <td>object</td>
</tr>
<tr>
  <td>settings.lobbyName </td>
  <td>string</td>
</tr>
<tr>
  <td>settings.duration </td>
  <td>string</td>
</tr>
<tr>
  <td>settings.durationItems </td>
  <td>array</td>
</tr>
<tr>
  <td>settings.durationItems.name </td>
  <td>string</td>
</tr>
<tr>
  <td>settings.durationItems.value </td>
  <td>string</td>
</tr>
<tr>
  <td>settings.publicLobby </td>
  <td>boolean</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "players": [
    {
      "username": "kyrill",
      "admin": false
    }
  ],
  "settings": {
    "lobbyName": "kyrill's lobby",
    "duration": "medium",
    "durationItems": [
      {
        "name": "Short",
        "value": "short"
      }
    ],
    "publicLobby": true
  }
}
```
---


###  `publish` /app/lobby/:id/kick

*Kick Player* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>username </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "username": "kyrill"
}
```
---


###  `subscribe` /user/queue/disconnect

*Disconnect Player* 

##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>reason </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "reason": "Lobby was closed"
}
```
---


###  `publish` /app/lobby/:id/chat

*Send Message* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>message </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "message": "I'm ready"
}
```
---


###  `subscribe` /user/queue/lobby/:id/chat

*Update Chat* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>type </td>
  <td>string</td>
</tr>
<tr>
  <td>username </td>
  <td>string</td>
</tr>
<tr>
  <td>icon </td>
  <td>string</td>
</tr>
<tr>
  <td>message </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "type": "msg",
  "username": "kyrill",
  "icon": "avatar:kyrill",
  "message": "I'm ready"
}
```
---


###  `publish` /app/lobby:id/start-game

*Start Game* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>Message Payload </td>
  <td>object</td>
</tr>
    </tbody>
</table>

###### Example of payload 

```json
{}
```
---


###  `subscribe` /user/queue/lobby/:id/start-game

*Start Game* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>Message Payload </td>
  <td>object</td>
</tr>
    </tbody>
</table>

###### Example of payload 

```json
{}
```
---


###  `subscribe` /user/queue/lobby/:id/start-round

*Start Game Round* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>Message Payload </td>
  <td>object</td>
</tr>
    </tbody>
</table>

###### Example of payload 

```json
{}
```
---


###  `subscribe` /user/queue/lobby/:id/game-state

*Game State* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>discardPile </td>
  <td>object</td>
</tr>
<tr>
  <td>discardPile.type </td>
  <td>string</td>
</tr>
<tr>
  <td>discardPile.value </td>
  <td>string</td>
</tr>
<tr>
  <td>discardPile.color </td>
  <td>string</td>
</tr>
<tr>
  <td>discardPile.key </td>
  <td>integer</td>
</tr>
<tr>
  <td>players </td>
  <td>array</td>
</tr>
<tr>
  <td>players.username </td>
  <td>string</td>
</tr>
<tr>
  <td>players.points </td>
  <td>integer</td>
</tr>
<tr>
  <td>players.cards </td>
  <td>array</td>
</tr>
<tr>
  <td>players.cards.type </td>
  <td>string</td>
</tr>
<tr>
  <td>players.skipped </td>
  <td>boolean</td>
</tr>
<tr>
  <td>players.admin </td>
  <td>boolean</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "discardPile": {
    "type": "number",
    "value": "1",
    "color": "red",
    "key": 35
  },
  "players": [
    {
      "username": "kyrill",
      "points": 12,
      "cards": [
        {
          "type": "back"
        }
      ],
      "skipped": false,
      "admin": true
    }
  ]
}
```
---


###  `subscribe` /user/queue/lobby/:id/hand

*Hand* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>cards </td>
  <td>array</td>
</tr>
<tr>
  <td>cards.type </td>
  <td>string</td>
</tr>
<tr>
  <td>cards.value </td>
  <td>string</td>
</tr>
<tr>
  <td>cards.color </td>
  <td>string</td>
</tr>
<tr>
  <td>cards.key </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "cards": [
    {
      "type": "number",
      "value": "3",
      "color": "red",
      "key": 35
    },
    {
      "type": "special",
      "value": "fuck-you",
      "color": "multicolor",
      "key": 48
    }
  ]
}
```
---


###  `subscribe` /user/queue/lobby/:id/playable

*Playable* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>cards </td>
  <td>array</td>
</tr>
<tr>
  <td>canDraw </td>
  <td>boolean</td>
</tr>
<tr>
  <td>canEnd </td>
  <td>boolean</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "cards": [
    3,
    5
  ],
  "canDraw": true,
  "canEnd": false
}
```
---


###  `subscribe` /user/queue/lobby/:id/timer

*Timer* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>seconds </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "seconds": 30
}
```
---


###  `subscribe` /user/queue/lobby/:id/animation-speed

*Animation Speed* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>hand </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "hand": 0
}
```
---


###  `subscribe` /user/queue/lobby/:id/start-turn

*Start Turn* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>currentPlayer </td>
  <td>string</td>
</tr>
<tr>
  <td>timebombRounds </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "currentPlayer": "Kyrill",
  "timebombRounds": 3
}
```
---


###  `publish` /app/lobby/:id/play

*Play Card* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>index </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "index": 3
}
```
---


###  `subscribe` /user/queue/lobby/:id/action-response

*Response to Action Card* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>action </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "action": "gift"
}
```
---


###  `publish` /app/lobby/:id/action/gift

*Gift* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>cards </td>
  <td>array</td>
</tr>
<tr>
  <td>target </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "cards": [
    3,
    5
  ],
  "target": "kyrill"
}
```
---


###  `publish` /app/lobby/:id/action/exchange

*Exchange* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>cards </td>
  <td>array</td>
</tr>
<tr>
  <td>target </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "cards": [
    3,
    5
  ],
  "target": "kyrill"
}
```
---


###  `publish` /app/lobby/:id/action/skip

*Skip* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>target </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "target": "kyrill"
}
```
---


###  `publish` /app/lobby/:id/action/fantastic

*Fantastic* 



Accepts **one of** the following messages:

### #1

##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>number </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "number": 3
}
```
---
### #2

##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>color </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "color": "red"
}
```
---
###  `publish` /app/lobby/:id/action/fantastic-four

*Fantastic Four* 



Accepts **one of** the following messages:

### #1

##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>targets </td>
  <td>object</td>
</tr>
<tr>
  <td>number </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "targets": {
    "kyrill": 1,
    "remy": 3
  },
  "number": 3
}
```
---
### #2

##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>targets </td>
  <td>object</td>
</tr>
<tr>
  <td>color </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "targets": {
    "kyrill": 1,
    "remy": 3
  },
  "color": "red"
}
```
---
###  `subscribe` /user/queue/lobby/:id/attack-window

*Counter Attack / Nice Try Opportunity* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>time </td>
  <td>integer</td>
</tr>
<tr>
  <td>playable </td>
  <td>array</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "time": 5,
  "playable": [
    3,
    5
  ]
}
```
---


###  `subscribe` /user/queue/lobby/:id/attack-turn

*Counter Attack Turn* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>currentPlayer </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "currentPlayer": "Kyrill"
}
```
---


###  `publish` /app/lobby/:id/action/counterattack

*Counter Attack* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>color </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "color": "red"
}
```
---


###  `publish` /app/lobby/:id/action/nice-try

*Nice Try* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>color </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "color": "red"
}
```
---


###  `publish` /app/lobby/:id/action/equality

*Equality* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>target </td>
  <td>string</td>
</tr>
<tr>
  <td>color </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "target": "kyrill",
  "color": "red"
}
```
---


###  `subscribe` /user/queue/lobby/:id/event

*Event Happens* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>event </td>
  <td>string</td>
</tr>
<tr>
  <td>message </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "event": "tornado",
  "message": "All cards in the hands of the players…"
}
```
---


###  `publish` /app/lobby/:id/action/surprise-party

*Surprise Party* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>card </td>
  <td>integer</td>
</tr>
<tr>
  <td>target </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "card": 3,
  "target": "kyrill"
}
```
---


###  `publish` /app/lobby/:id/action/merry-christmas

*Merry Christmas* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>targets </td>
  <td>array</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "targets": [
    {
      "kyrill": [
        3,
        5
      ]
    }
  ]
}
```
---


###  `subscribe` /user/queue/lobby/:id/gambling-man-window

*Gambling Man Selection* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>playable </td>
  <td>array</td>
</tr></tbody>
</table>


###### Example of payload 

```json
{
  "playable": [
    3,
    5
  ]
}
```
---


###  `subscribe` /user/queue/lobby/:id/recession

*Recession Amount* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>amount </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "amount": 2
}
```
---


###  `publish` /app/lobby/:id/action/recession

*Recession* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>cards </td>
  <td>array</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "cards": [
    3,
    5
  ]
}
```
---


###  `subscribe` /user/queue/lobby/:id/market-window

*Market Selection* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>cards </td>
  <td>array</td>
</tr>
<tr>
  <td>cards.type </td>
  <td>string</td>
</tr>
<tr>
  <td>cards.value </td>
  <td>string</td>
</tr>
<tr>
  <td>cards.color </td>
  <td>string</td>
</tr>
<tr>
  <td>cards.key </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "cards": [
    {
      "type": "number",
      "value": "3",
      "color": "red",
      "key": 35
    },
    {
      "type": "special",
      "value": "fuck-you",
      "color": "multicolor",
      "key": 48
    }
  ]
}
```
---


###  `publish` /app/lobby/:id/action/market

*Market* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>card </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "card": 3
}
```
---


###  `publish` /app/lobby/:id/draw

*Draw Card* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>Message Payload </td>
  <td>object</td>
</tr>
    </tbody>
</table>

###### Example of payload 

```json
{}
```
---


###  `subscribe` /user/queue/lobby/:id/draw

*Draw Card Animation* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>amount </td>
  <td>integer</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "amount": 5
}
```
---


###  `publish` /app/lobby/:id/end-turn

*End Turn* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>Message Payload </td>
  <td>object</td>
</tr>
    </tbody>
</table>

###### Example of payload 

```json
{}
```
---


###  `subscribe` /user/queue/lobby/:id/end-round

*Game Round is Over* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>players </td>
  <td>object</td>
</tr>
<tr>
  <td>changes </td>
  <td>object</td>
</tr>
<tr>
  <td>pointLimit </td>
  <td>integer</td>
</tr>
<tr>
  <td>icon </td>
  <td>string</td>
</tr>
<tr>
  <td>message </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "players": {
    "kyrill": 54,
    "remy": 63
  },
  "changes": {
    "kyrill": 12,
    "remy": 14
  },
  "pointLimit": 168,
  "icon": "event:doomsday",
  "message": "Doomday happened."
}
```
---


###  `subscribe` /user/queue/lobby/:id/end-game

*Game is Over* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>players </td>
  <td>object</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "players": {
    "kyrill": 120,
    "remy": 80
  }
}
```
---


###  `publish` /app/lobby/:id/rematch

*Rematch* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>Message Payload </td>
  <td>object</td>
</tr>
    </tbody>
</table>

###### Example of payload 

```json
{}
```
---


###  `subscribe` /user/queue/reconnect

*Reconnect* 




##### Payload
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
<tr>
  <td>token </td>
  <td>string</td>
</tr></tbody>
</table>

###### Example of payload 

```json
{
  "token": "abc-123-abc-123"
}
```
---
