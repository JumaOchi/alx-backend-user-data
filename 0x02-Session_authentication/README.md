# Simple API

Simple HTTP API for playing with `User` model.


## Files

### `models/`

- `base.py`: base of all models of the API - handle serialization to file
- `user.py`: user model

### `api/v1`

- `app.py`: entry point of the API
- `views/index.py`: basic endpoints of the API: `/status` and `/stats`
- `views/users.py`: all users endpoints


## Setup

```
$ pip3 install -r requirements.txt
```


## Run

```
$ API_HOST=0.0.0.0 API_PORT=5000 python3 -m api.v1.app
```


## Routes

- `GET /api/v1/status`: returns the status of the API
- `GET /api/v1/stats`: returns some stats of the API
- `GET /api/v1/users`: returns the list of users
- `GET /api/v1/users/:id`: returns an user based on the ID
- `DELETE /api/v1/users/:id`: deletes an user based on the ID
- `POST /api/v1/users`: creates a new user (JSON parameters: `email`, `password`, `last_name` (optional) and `first_name` (optional))
- `PUT /api/v1/users/:id`: updates an user based on the ID (JSON parameters: `last_name` and `first_name`)

********* update session *********

Otherwise, return `user_id` from the `session` dictionary.
Update [api/v1/app.py](api/v1/app.py) to instantiate `auth` with `SessionExpAuth` if the environment variable `AUTH_TYPE` is equal to `session_exp_auth`.

 **Sessions in database**
Since the beginning, all Session IDs are stored in memory. It means, if your application stops, all Session IDs are lost.
To avoid that, you will create a new authentication system, based on Session ID stored in database (for us, it will be in a file, like `User`).
To avoid that, you will create a new authentication system, based on Session ID stored in database (for us, it will be in a file, like `User`).
Create a new model `UserSession` in [models/user_session.py](models/user_session.py) that inherits from `Base`:
Implement the `def __init__(self, *args: list, **kwargs: dict):` like in `User` but for these 2 attributes:`user_id`: string.