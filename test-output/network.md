```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-q2k01f@email.com",
    "username": "author-q2k01f",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-q2k01f@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1xMmswMWYiLCJpYXQiOjE2MDQzNjczNTEsImV4cCI6MTYwNDU0MDE1MX0.OF9YhKzT8ASMwsa7ryWAAuTXkZdBAMFL-rY2d3Y6zKs",
    "username": "author-q2k01f",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-sii1dn@email.com",
    "username": "authoress-sii1dn",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-sii1dn@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1zaWkxZG4iLCJpYXQiOjE2MDQzNjczNTIsImV4cCI6MTYwNDU0MDE1Mn0.MWKm-XPqbbazMp8TpuCfe3A3OYAVbXDeY2kOCDBnjpQ",
    "username": "authoress-sii1dn",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-pup16d@email.com",
    "username": "non-author-pup16d",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-pup16d@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItcHVwMTZkIiwiaWF0IjoxNjA0MzY3MzUyLCJleHAiOjE2MDQ1NDAxNTJ9.6jCHNdZuY6Vnm1ZOhzX5t_465QLMImxRT1PwHX7eSps",
    "username": "non-author-pup16d",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-68j1tb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367352190,
    "updatedAt": 1604367352190,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5jj7ax",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367352234,
    "updatedAt": 1604367352234,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-68j1tb
```
```
200 OK

{
  "article": {
    "createdAt": 1604367352190,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-68j1tb",
    "updatedAt": 1604367352190,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-5jj7ax
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1604367352234,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-5jj7ax",
    "updatedAt": 1604367352234,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/191noq
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [191noq]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-5jj7ax

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1604367352234,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-5jj7ax",
    "updatedAt": 1604367352234,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-5jj7ax

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1604367352234,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-5jj7ax",
    "updatedAt": 1604367352234,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-5jj7ax

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1604367352234,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-5jj7ax",
    "updatedAt": 1604367352234,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-5jj7ax

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-5jj7ax

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-5jj7ax

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-5jj7ax

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-5jj7ax]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-5jj7ax

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-q2k01f]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-68j1tb/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1604367352190,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-68j1tb",
    "updatedAt": 1604367352190,
    "favoritedBy": [
      "non-author-pup16d"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-68j1tb
```
```
200 OK

{
  "article": {
    "createdAt": 1604367352190,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-68j1tb",
    "updatedAt": 1604367352190,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-68j1tb/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-68j1tb_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-68j1tb_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-68j1tb/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1604367352190,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-68j1tb",
    "updatedAt": 1604367352190,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-68j1tb
```
```
200 OK

{}
```
```
GET /articles/title-68j1tb
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-68j1tb]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-5jj7ax
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-q2k01f]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qfgfp4",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ywhr38",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353352,
    "updatedAt": 1604367353352,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qfgfp4",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "49km38",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wo95vu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353405,
    "updatedAt": 1604367353405,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "49km38",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "zexxak",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mzv29u",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353451,
    "updatedAt": 1604367353451,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "zexxak",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ana1sa",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ggr1yj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353504,
    "updatedAt": 1604367353504,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ana1sa",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "vh325e",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lghyt5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353551,
    "updatedAt": 1604367353551,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "vh325e",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5sj3d2",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-rilzd0",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353602,
    "updatedAt": 1604367353602,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5sj3d2",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "m6ec4i",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-khd1nv",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353644,
    "updatedAt": 1604367353644,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "m6ec4i",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7k8tnd",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-l5lkpg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353671,
    "updatedAt": 1604367353671,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7k8tnd",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "-z5zq1g",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-h3fr6u",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353711,
    "updatedAt": 1604367353711,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "-z5zq1g",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "37ykh2",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ef438x",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353754,
    "updatedAt": 1604367353754,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "37ykh2",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "amszvu",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ydumql",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353782,
    "updatedAt": 1604367353782,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "amszvu",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "cku0x8",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mq6o6b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353808,
    "updatedAt": 1604367353808,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "cku0x8",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8e6n56",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7g705q",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353833,
    "updatedAt": 1604367353833,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8e6n56",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "577vin",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ykfo5b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353859,
    "updatedAt": 1604367353859,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "577vin",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5wtm4p",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xxdki",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353885,
    "updatedAt": 1604367353885,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5wtm4p",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "u9gy2w",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gxr72b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353912,
    "updatedAt": 1604367353912,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "u9gy2w",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dz9ik5",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-b1ld2p",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353949,
    "updatedAt": 1604367353949,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dz9ik5",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nh9qrq",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-atbta3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367353975,
    "updatedAt": 1604367353975,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nh9qrq",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "pn19be",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-8amtg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367354002,
    "updatedAt": 1604367354002,
    "author": {
      "username": "authoress-sii1dn",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "pn19be",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "6qc0h4",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4qp0hp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367354036,
    "updatedAt": 1604367354036,
    "author": {
      "username": "author-q2k01f",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "6qc0h4",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "6qc0h4",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367354036,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qp0hp",
      "updatedAt": 1604367354036,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pn19be",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367354002,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8amtg",
      "updatedAt": 1604367354002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nh9qrq",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353975,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-atbta3",
      "updatedAt": 1604367353975,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz9ik5",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353949,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b1ld2p",
      "updatedAt": 1604367353949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "u9gy2w"
      ],
      "createdAt": 1604367353912,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gxr72b",
      "updatedAt": 1604367353912,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5wtm4p",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353885,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxdki",
      "updatedAt": 1604367353885,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "577vin",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353859,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ykfo5b",
      "updatedAt": 1604367353859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8e6n56",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353833,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7g705q",
      "updatedAt": 1604367353833,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cku0x8",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353808,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mq6o6b",
      "updatedAt": 1604367353808,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "amszvu",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353782,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ydumql",
      "updatedAt": 1604367353782,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "37ykh2",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353754,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ef438x",
      "updatedAt": 1604367353754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z5zq1g",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353711,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h3fr6u",
      "updatedAt": 1604367353711,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7k8tnd",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353671,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l5lkpg",
      "updatedAt": 1604367353671,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m6ec4i",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353644,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-khd1nv",
      "updatedAt": 1604367353644,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5sj3d2",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353602,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rilzd0",
      "updatedAt": 1604367353602,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "vh325e"
      ],
      "createdAt": 1604367353551,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lghyt5",
      "updatedAt": 1604367353551,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ana1sa",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353504,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggr1yj",
      "updatedAt": 1604367353504,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "zexxak"
      ],
      "createdAt": 1604367353451,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mzv29u",
      "updatedAt": 1604367353451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "49km38",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353405,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wo95vu",
      "updatedAt": 1604367353405,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfgfp4",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353352,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ywhr38",
      "updatedAt": 1604367353352,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7k8tnd",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353671,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l5lkpg",
      "updatedAt": 1604367353671,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "nh9qrq",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353975,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-atbta3",
      "updatedAt": 1604367353975,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5wtm4p",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353885,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxdki",
      "updatedAt": 1604367353885,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cku0x8",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353808,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mq6o6b",
      "updatedAt": 1604367353808,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z5zq1g",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353711,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h3fr6u",
      "updatedAt": 1604367353711,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5sj3d2",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353602,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rilzd0",
      "updatedAt": 1604367353602,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "zexxak"
      ],
      "createdAt": 1604367353451,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mzv29u",
      "updatedAt": 1604367353451,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-sii1dn
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "pn19be",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367354002,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8amtg",
      "updatedAt": 1604367354002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz9ik5",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353949,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b1ld2p",
      "updatedAt": 1604367353949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5wtm4p",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353885,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxdki",
      "updatedAt": 1604367353885,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8e6n56",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353833,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7g705q",
      "updatedAt": 1604367353833,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "amszvu",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353782,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ydumql",
      "updatedAt": 1604367353782,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z5zq1g",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353711,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h3fr6u",
      "updatedAt": 1604367353711,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m6ec4i",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353644,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-khd1nv",
      "updatedAt": 1604367353644,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "vh325e"
      ],
      "createdAt": 1604367353551,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lghyt5",
      "updatedAt": 1604367353551,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "zexxak"
      ],
      "createdAt": 1604367353451,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mzv29u",
      "updatedAt": 1604367353451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfgfp4",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353352,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ywhr38",
      "updatedAt": 1604367353352,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-pup16d
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-q2k01f&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "6qc0h4",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367354036,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qp0hp",
      "updatedAt": 1604367354036,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nh9qrq",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353975,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-atbta3",
      "updatedAt": 1604367353975,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-q2k01f&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "u9gy2w"
      ],
      "createdAt": 1604367353912,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gxr72b",
      "updatedAt": 1604367353912,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "577vin",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353859,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ykfo5b",
      "updatedAt": 1604367353859,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "6qc0h4",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367354036,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qp0hp",
      "updatedAt": 1604367354036,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pn19be",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367354002,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8amtg",
      "updatedAt": 1604367354002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nh9qrq",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353975,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-atbta3",
      "updatedAt": 1604367353975,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz9ik5",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353949,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b1ld2p",
      "updatedAt": 1604367353949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "u9gy2w"
      ],
      "createdAt": 1604367353912,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gxr72b",
      "updatedAt": 1604367353912,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5wtm4p",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353885,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxdki",
      "updatedAt": 1604367353885,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "577vin",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353859,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ykfo5b",
      "updatedAt": 1604367353859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8e6n56",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353833,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7g705q",
      "updatedAt": 1604367353833,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cku0x8",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353808,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mq6o6b",
      "updatedAt": 1604367353808,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "amszvu",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353782,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ydumql",
      "updatedAt": 1604367353782,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "37ykh2",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353754,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ef438x",
      "updatedAt": 1604367353754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z5zq1g",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353711,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h3fr6u",
      "updatedAt": 1604367353711,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7k8tnd",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353671,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l5lkpg",
      "updatedAt": 1604367353671,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m6ec4i",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353644,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-khd1nv",
      "updatedAt": 1604367353644,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5sj3d2",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353602,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rilzd0",
      "updatedAt": 1604367353602,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "vh325e"
      ],
      "createdAt": 1604367353551,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lghyt5",
      "updatedAt": 1604367353551,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ana1sa",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353504,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggr1yj",
      "updatedAt": 1604367353504,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "zexxak"
      ],
      "createdAt": 1604367353451,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mzv29u",
      "updatedAt": 1604367353451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "49km38",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353405,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wo95vu",
      "updatedAt": 1604367353405,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfgfp4",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353352,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ywhr38",
      "updatedAt": 1604367353352,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-sii1dn/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-sii1dn",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "pn19be",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367354002,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8amtg",
      "updatedAt": 1604367354002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz9ik5",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353949,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b1ld2p",
      "updatedAt": 1604367353949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5wtm4p",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353885,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxdki",
      "updatedAt": 1604367353885,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8e6n56",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353833,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7g705q",
      "updatedAt": 1604367353833,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "amszvu",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353782,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ydumql",
      "updatedAt": 1604367353782,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z5zq1g",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353711,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h3fr6u",
      "updatedAt": 1604367353711,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m6ec4i",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353644,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-khd1nv",
      "updatedAt": 1604367353644,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "vh325e"
      ],
      "createdAt": 1604367353551,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lghyt5",
      "updatedAt": 1604367353551,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "zexxak"
      ],
      "createdAt": 1604367353451,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mzv29u",
      "updatedAt": 1604367353451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfgfp4",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353352,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ywhr38",
      "updatedAt": 1604367353352,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-q2k01f/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-q2k01f",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "6qc0h4",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367354036,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qp0hp",
      "updatedAt": 1604367354036,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "pn19be",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367354002,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8amtg",
      "updatedAt": 1604367354002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nh9qrq",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353975,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-atbta3",
      "updatedAt": 1604367353975,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dz9ik5",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353949,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b1ld2p",
      "updatedAt": 1604367353949,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "u9gy2w"
      ],
      "createdAt": 1604367353912,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gxr72b",
      "updatedAt": 1604367353912,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5wtm4p",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353885,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xxdki",
      "updatedAt": 1604367353885,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "577vin",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353859,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ykfo5b",
      "updatedAt": 1604367353859,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8e6n56",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353833,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7g705q",
      "updatedAt": 1604367353833,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cku0x8",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353808,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mq6o6b",
      "updatedAt": 1604367353808,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "amszvu",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353782,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ydumql",
      "updatedAt": 1604367353782,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "37ykh2",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353754,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ef438x",
      "updatedAt": 1604367353754,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "-z5zq1g",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353711,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h3fr6u",
      "updatedAt": 1604367353711,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7k8tnd",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353671,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l5lkpg",
      "updatedAt": 1604367353671,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m6ec4i",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353644,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-khd1nv",
      "updatedAt": 1604367353644,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5sj3d2",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1604367353602,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-rilzd0",
      "updatedAt": 1604367353602,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "vh325e"
      ],
      "createdAt": 1604367353551,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lghyt5",
      "updatedAt": 1604367353551,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ana1sa",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353504,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ggr1yj",
      "updatedAt": 1604367353504,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "zexxak"
      ],
      "createdAt": 1604367353451,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mzv29u",
      "updatedAt": 1604367353451,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "49km38",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1604367353405,
      "author": {
        "username": "author-q2k01f",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wo95vu",
      "updatedAt": 1604367353405,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfgfp4",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1604367353352,
      "author": {
        "username": "authoress-sii1dn",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ywhr38",
      "updatedAt": 1604367353352,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "m6ec4i",
    "tag_6",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "amszvu",
    "tag_10",
    "tag_mod_3_1",
    "dz9ik5",
    "tag_16",
    "ana1sa",
    "tag_3",
    "tag_mod_2_1",
    "tag_4",
    "vh325e",
    "37ykh2",
    "tag_9",
    "cku0x8",
    "tag_11",
    "tag_mod_3_2",
    "nh9qrq",
    "tag_17",
    "8e6n56",
    "tag_12",
    "5sj3d2",
    "tag_5",
    "tag_a",
    "tag_b",
    "tag_2",
    "zexxak",
    "7k8tnd",
    "tag_7",
    "49km38",
    "tag_1",
    "pn19be",
    "tag_18",
    "qfgfp4",
    "tag_0",
    "tag_15",
    "u9gy2w",
    "5wtm4p",
    "tag_14",
    "577vin",
    "tag_13",
    "-z5zq1g",
    "tag_8",
    "6qc0h4",
    "tag_19"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-7kfjr7@email.com",
    "username": "author-7kfjr7",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-7kfjr7@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci03a2ZqcjciLCJpYXQiOjE2MDQzNjczNTUsImV4cCI6MTYwNDU0MDE1NX0.Syt8hrSCu_8XGEh8bOt7trNdzd7-Nk2i6ledTF3THbA",
    "username": "author-7kfjr7",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-llo2ud@email.com",
    "username": "commenter-llo2ud",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-llo2ud@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1sbG8ydWQiLCJpYXQiOjE2MDQzNjczNTUsImV4cCI6MTYwNDU0MDE1NX0.aT-3Nj1nlltSJLnTRBuGAWmDsx5MXtWafQ8Lh86cN5U",
    "username": "commenter-llo2ud",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-yhn33h",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1604367355639,
    "updatedAt": 1604367355639,
    "author": {
      "username": "author-7kfjr7",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment 6qh1bz"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ce4c7341-f648-4ca1-aef6-ed8ff0f2aeb1",
    "slug": "title-yhn33h",
    "body": "test comment 6qh1bz",
    "createdAt": 1604367355678,
    "updatedAt": 1604367355678,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment 7edtvt"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "c21b3a46-1bc4-4f50-810b-c6613ad3b5ba",
    "slug": "title-yhn33h",
    "body": "test comment 7edtvt",
    "createdAt": 1604367355715,
    "updatedAt": 1604367355715,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment vvea6e"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "b3e0c388-0982-4608-9b9d-6ea9a648cc0d",
    "slug": "title-yhn33h",
    "body": "test comment vvea6e",
    "createdAt": 1604367355744,
    "updatedAt": 1604367355744,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment gban6y"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "1914fd76-dcb0-47fb-a7c1-be32c744f96d",
    "slug": "title-yhn33h",
    "body": "test comment gban6y",
    "createdAt": 1604367355773,
    "updatedAt": 1604367355773,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment uvi66f"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "bdd2b5ee-1c79-497e-9c9f-c6cda345446d",
    "slug": "title-yhn33h",
    "body": "test comment uvi66f",
    "createdAt": 1604367355805,
    "updatedAt": 1604367355805,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment ykko3l"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "68703b4f-598c-476b-baec-df161824d3fe",
    "slug": "title-yhn33h",
    "body": "test comment ykko3l",
    "createdAt": 1604367355843,
    "updatedAt": 1604367355843,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment nwpuft"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "536c2e41-2cf4-43ec-9b6d-29fda1a96e4a",
    "slug": "title-yhn33h",
    "body": "test comment nwpuft",
    "createdAt": 1604367355879,
    "updatedAt": 1604367355879,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment we4fwf"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "7ccf6d04-680b-44eb-bb8a-24199272a65b",
    "slug": "title-yhn33h",
    "body": "test comment we4fwf",
    "createdAt": 1604367355915,
    "updatedAt": 1604367355915,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment yw80sp"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "68b9adf5-106e-4219-95b7-16feebe25164",
    "slug": "title-yhn33h",
    "body": "test comment yw80sp",
    "createdAt": 1604367355964,
    "updatedAt": 1604367355964,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-yhn33h/comments

{
  "comment": {
    "body": "test comment 72a4iw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e9f4e212-642b-4bb4-8f71-19f6f44db500",
    "slug": "title-yhn33h",
    "body": "test comment 72a4iw",
    "createdAt": 1604367356002,
    "updatedAt": 1604367356002,
    "author": {
      "username": "commenter-llo2ud",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-yhn33h/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-yhn33h/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment ewx5o"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-yhn33h/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1604367355843,
      "id": "68703b4f-598c-476b-baec-df161824d3fe",
      "body": "test comment ykko3l",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355843
    },
    {
      "createdAt": 1604367355879,
      "id": "536c2e41-2cf4-43ec-9b6d-29fda1a96e4a",
      "body": "test comment nwpuft",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355879
    },
    {
      "createdAt": 1604367356002,
      "id": "e9f4e212-642b-4bb4-8f71-19f6f44db500",
      "body": "test comment 72a4iw",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367356002
    },
    {
      "createdAt": 1604367355715,
      "id": "c21b3a46-1bc4-4f50-810b-c6613ad3b5ba",
      "body": "test comment 7edtvt",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355715
    },
    {
      "createdAt": 1604367355964,
      "id": "68b9adf5-106e-4219-95b7-16feebe25164",
      "body": "test comment yw80sp",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355964
    },
    {
      "createdAt": 1604367355805,
      "id": "bdd2b5ee-1c79-497e-9c9f-c6cda345446d",
      "body": "test comment uvi66f",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355805
    },
    {
      "createdAt": 1604367355773,
      "id": "1914fd76-dcb0-47fb-a7c1-be32c744f96d",
      "body": "test comment gban6y",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355773
    },
    {
      "createdAt": 1604367355678,
      "id": "ce4c7341-f648-4ca1-aef6-ed8ff0f2aeb1",
      "body": "test comment 6qh1bz",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355678
    },
    {
      "createdAt": 1604367355744,
      "id": "b3e0c388-0982-4608-9b9d-6ea9a648cc0d",
      "body": "test comment vvea6e",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355744
    },
    {
      "createdAt": 1604367355915,
      "id": "7ccf6d04-680b-44eb-bb8a-24199272a65b",
      "body": "test comment we4fwf",
      "slug": "title-yhn33h",
      "author": {
        "username": "commenter-llo2ud",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1604367355915
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-yhn33h/comments/ce4c7341-f648-4ca1-aef6-ed8ff0f2aeb1
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-yhn33h/comments/c21b3a46-1bc4-4f50-810b-c6613ad3b5ba
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-llo2ud]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-yhn33h/comments/c21b3a46-1bc4-4f50-810b-c6613ad3b5ba
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-yhn33h/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "username": "user1-0.vzm7s99hni",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM",
    "username": "user1-0.vzm7s99hni",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "username": "user1-0.vzm7s99hni",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.vzm7s99hni]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.vzm7s99hni@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.vzm7s99hni@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM",
    "username": "user1-0.vzm7s99hni",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.7t555rlhp2p",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.7t555rlhp2p]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "password": "0.qfo6ea6x6ym"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.vzm7s99hni@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM",
    "username": "user1-0.vzm7s99hni",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.vzm7s99hni
```
```
200 OK

{
  "profile": {
    "username": "user1-0.vzm7s99hni",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.otwsi38nl3
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.otwsi38nl3]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE2MDQzNjczNTYsImV4cCI6MTYwNDU0MDE1Nn0.qVy7iq6tEmXDJwmed5aKvmJaKs7RIceEq5UMFjRSgzs",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.3pvzq017aje",
    "email": "user2-0.3pvzq017aje@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.3pvzq017aje@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuM3B2enEwMTdhamUiLCJpYXQiOjE2MDQzNjczNTYsImV4cCI6MTYwNDU0MDE1Nn0.A0lF7ANPtQO4rspSO285vWgghYlPAoM8HO7ymSum9mk",
    "username": "user2-0.3pvzq017aje",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.vzm7s99hni@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vzm7s99hni",
    "email": "updated-user1-0.vzm7s99hni@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vzm7s99hni",
    "email": "updated-user1-0.vzm7s99hni@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vzm7s99hni",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vzm7s99hni",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnptN3M5OWhuaSIsImlhdCI6MTYwNDM2NzM1NiwiZXhwIjoxNjA0NTQwMTU2fQ.c73WFCieOAKbJ4Wrj79GiAAUt4uf0HXyGpcyQ-ih3HM"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.tp6njwpkgdr@email.com",
    "username": "user2-0.tp6njwpkgdr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.tp6njwpkgdr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAudHA2bmp3cGtnZHIiLCJpYXQiOjE2MDQzNjczNTcsImV4cCI6MTYwNDU0MDE1N30.Xvai2INsWwDt1-XERW_ostCET1QlHvs0HDV46veunmk",
    "username": "user2-0.tp6njwpkgdr",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.tp6njwpkgdr@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.tp6njwpkgdr@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-11-03T01:35:57.125Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
