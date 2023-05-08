## API for simple blogging application

Signup User(public endpoint)

| Field    |  Type  | Required | Constrainsts |
| :------- | :----: | :------: | :----------: |
| email    | string |   Yes    | valid email  |
| password | string |   Yes    | min length 5 |
| username | string |   Yes    | min length 3 |

#

### Features

_will be added soon.._

### Schema

#### Tables

1. Users

```sql
CREATE TABLE users(
	id SERIAL PRIMARY KEY,
	created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	username VARCHAR(50) NOT NULL UNIQUE,
	email VARCHAR(100) NOT NULL UNIQUE,
	password VARCHAR(500) NOT NULL,
	bio VARCHAR(250),
	avatar VARCHAR(500)
)
```

2. Posts

```sql
CREATE TABLE posts(
	id SERIAL PRIMARY KEY,
	created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
	thumbnail_url VARCHAR(500),
	title VARCHAR(260) NOT NULL,
	content VARCHAR(10000) NOT NULL
)
```

3. Likes

```sql
CREATE TABLE likes(
	id SERIAL PRIMARY KEY,
	created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
	post_id INTEGER NOT NULL REFERENCES posts(id) ON DELETE CASCADE,
	UNIQUE(user_id, post_id)
)
```

4. Comments

```sql
CREATE TABLE comments(
	id SERIAL PRIMARY KEY,
	created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
	user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
	post_id INTEGER NOT NULL REFERENCES posts(id) ON DELETE CASCADE,
	comment VARCHAR(260) NOT NULL
)
```
