# Creat API Design Forum App

## Requirement/User Stories:

- As a user, I want to be able to Register
- As a user, I want to be able to Log In
- As a user, I want to be able to Create new Thread
- As a user, I want to be able to Create new Reply (on a Thread)
- As a user I want to be able to Update my Personal profile
- As a user, I want to be able to Save/Bookmark Threads
- As a user, I want to be able to UnSave/UnBM Threads

# Core Entity

> [!User]
> id, fullName, userName, email, password, avatarUrl

> [!Thread]
> id, title, category, content, authorId

> [!Reply]
> id, threadId, replyContent, replyerId

> [!Bookmark]
> id, threadId, bookmark, bookmarkerId

# Api Design

## Authentication

### Register

- Endpoint : /api/auth/register
- Method : post

- Request body :

  - fullName : string (required)
  - userName : string (required)
  - email : string (required)
  - password : string (required)
  - avatarUrl : string (optional)

- Respond :

  - message : string
  - status : number

- Example Respond :
  - Success : {message : "Registration successfully"}, status(201)
  - Conflic : {message : "Email already used"}, status(400)
  - Error : {message : "Registration error"}, status(500)

### Login

- Endpoint : /api/auth/login
- Method : post

- Request body :

  - email : string (required)
  - password : string (required)

- Respond :

  - message : string
  - status : number

- Example Respond :
  - Success : {message : "Login successfully"} status(200)
  - Error : {message : "Email or password invalid"} status(401)
  - Error : {message : "Login error"} status(500)

## Thread

### Creat Thread

- Endpoint : /api/threads?filter=title,category,content,authorId.userName
- Method : post

- Request body :

  - title : string (required)
  - category : string (optional)
  - content : string (required)

- Respond :

  - message : string
  - status : number
  - data : object

- Example Respond :
  - Success : {message : "Successfully creat new thread"}, status(201), data : {
    title : "Javascript vs Java",
    category : "technology",
    content : "lorem ipsum"
    author : "user 1"
    }
  - Error : {message : "error"} status(500)

### Creat Reply

- Endpoint : /api/threads/:id/replys?filter=threadId.title,replayContent,replyerId.userName
- Method : post

- Request body :

  - replyContent : string (required)

- Respond :

  - message : string
  - status : number
  - data : object

- Example Respond :
  - Success : {message : "Successfully creat new reply"}, status(201), data : {
    title : "Jago Javascript",
    replycontent : "lorem ipsum",
    replyer : "user 2"
    }
  - Error : {message : "error"} status(500)

### Bookmarks

- Endpoint : /api/threads/:id/bookmarks?threadId.title,bookmark,bookmarkerId.userName
- Method : post

- Request body :

  - bookmark : boolean (required)

- Respond :

  - message : string
  - status : number
  - data : object

- Example Respond :
  - Success : {message : "Successfully add bookmark"}, status(201), data : {
    title : "Api Design",
    bookmark : 1,
    bookmarker : "user 2"
    }
  - Error : {message : "error"} status(500)

### Unbookmarks

- Endpoint : /api/bookmarks/:id
- Method : delete

- Request body :

  -

- Respond :

  - message : string
  - status : number

- Example Respond :
  - Success : {message : "Successfully remove bookmark"}, status(200)
  - Error : {message : "error"} status(500)

## User

### Update Profile

- Endpoint : /api/users/:id
- Method : patch

- Request body :

  - fullName : string (optional)
  - userName : string (optional)
  - email : string (optional)
  - password : string (optional)
  - avatarUrl : string (optional)

- Respond :

  - message : string
  - status : number
  - data : object

- Example Respond :
  - Success : {message : "Update profile successfully"}, status(200), data : {
    fullName : "mark clekc",
    userName : "mark_user",
    email : "mark@gmail.com",
    password : "12345",
    avatarUrl : "http://qwd43.com"
    }
  - Error : {message : "error"} status(500)
