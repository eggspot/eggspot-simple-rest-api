Dear candidate, thank you to join our code test interview. 

Kindly notes: for the code test
- You don't need to write a complete implementation code. Only simple and minimum code to demonstrate your idea, and your solution to solve the problem. 
- We would like to see how you will solve the problem in code and your solution for it.
 
We are expecting you to demonstrate mastery in the following areas:
- Clean & Maintainable Code
- Test-Driven Development
- SOLID principles
- KISS principles
- Design Patterns

A huge plus is you will demonstrate:
- Domain-Driven Development
- CQRS approach
- Event Sourcing
- Behavior-Driven Development


---
NodeJs with ExpresJS + Typescript will be used for code & unit tests.
- Use any IDE you want.
- Use any unit test framework you love.
- Update and change any settings, or configurations in the projects as you want.

For data storage,
- You could choose to use a real database (MySQL, Postgres) or fake data (JSON file, the object in NodeJs, or any).

# Tasks: API implementation
## 1. Site and Game APIs: get, add, update, delete
- 1 site can have many games
- Site code is unique
- Game code is unique
```json
{
    "site": {
        "id": number,
        "code": string,
        "games": [
            {
                "id": number,
                "code": string
            }
        ]
    }
}
```

## 2. Transactions API
- Method Post: two actions `"play" and "win"`
- Has idempotency check with "id" ref here https://www.oreilly.com/library/view/hands-on-restful-api/9781788992664/f75ee8f9-056b-41df-b250-e40f0fdfd639.xhtml
- Concurrent: one player can only play 1 game at the same time.
- Amount: will accumulate in `playerBalance` by each player.
    - `+` with win
    - `-` with play
- Can not `play` if the `playerBalance` is less than zero, throw error.
- Can not `play` if the amount less than zero, throw an error.
- Can not `win` if the amount less than zero, throw an  error.

- If the player wins a big amount - greater than 100: send a notification to the system. 
    - Notes: implement send a notification is code pattern only.

Request:
```json
{
    "transaction": {
        "id": number,
        "playerId": number,
        "action": "play or win",
        "amount": number,
        "gameId": number,
    }
}
```
Response:

On Success
```json
{
    "id": number,
    "playerBalance": number
}
```
On Error:
```json
{
    "code": string,
    "message": string
}
```

# 3. (Optional - plug if you could do) Docker & CI setup
- Add the dockerfile 
- Add .yml for Github actions