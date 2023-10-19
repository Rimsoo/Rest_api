# End points
## Books
<details>
    <summary><b>GET Books</b></summary>

### Header
```
GET /books
Accept: application/ld+json, application/json
```
### Response
C'est une collection donc le contexte est a changer
```
HTTP/3.0 200 OK
{
    "@context": "schema.org/Book",
    "@id": "/books",
    "@type": "hydra:Collection",
    "hydra:member": [
        {
            "@id": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
            "@type": "Book",
            "isbn": "978-1-56619-909-4",
            "name": "Zero to One",
            "description": "Notes on Startups, or How to Build the Future",
            "author": "Peter Thiel",
            "publicationDate": "2014-09-16T00:00:00+00:00"
        },
        {
            "@id": "/books/c7d8e9f0-1a2b-3c4d-5e6f-7g8h9i0j1k2l",
            "@type": "Book",
            "isbn": "978-1-56619-909-5",
            "name": "Zero to Two",
            "description": "Notes on Startups, or How to Build the Future",
            "author": "Peter Thiel",
            "publicationDate": "2014-09-16T00:00:00+00:00"
        }
    ],
    "hydra:totalItems": 2
}
```
</details>

<details>
<summary><b>GET Book</b></summary>

### Header
```
GET /books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a
Accept: application/ld+json, application/json
```
### Response

```
HTTP/3.0 200 OK
{
    "@context": "schema.org/Book",
    "@id": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
    "@type": "Book",
    "isbn": "978-1-56619-909-4",
    "name": "Zero to One",
    "description": "Notes on Startups, or How to Build the Future",
    "author": "Peter Thiel",
    "publicationDate": "2014-09-16T00:00:00+00:00"
}
```
</details>

<details>
<summary><b>GET Borrows</b></summary>

### Header
```
GET /books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a/borrows/
Accept: application/ld+json, application/json
```

### Response
```
HTTP/3.0 200 OK
{
    "@context": "schema.org/BorrowAction",
    "@id": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a/borrows",
    "@type": "hydra:Collection",
    "hydra:member": [
        {
            "@id": "/borrows/d3e4f5g6-h7i8-9j0k-l1m2-n3o4p5q6r7s",
            "@type": "Borrow",
            "book": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
            "user": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
            "borrowedAt": "2023-10-18T00:00:00+00:00",
            "returnedAt": null
        },
        { ... }
    ],
}
```
</details>
<details>
<summary><b>GET Borrow</b></summary>

### Header
```
GET /borrows/d3e4f5g6-h7i8-9j0k-l1m2-n3o4p5q6r7s
Accept: application/ld+json, application/json
```

### Response
Ajouter l'entete,
Underfetching: je dois faire une requete pour avoir les informations de l'utilisateur et du livre, fournir plus d'information dans la réponse serai plus interessant.
```
HTTP/3.0 200 OK
{
    "@context": "schema.org/BorrowAction",
    "@id": "/borrows/d3e4f5g6-h7i8-9j0k-l1m2-n3o4p5q6r7s",
    "@type": "Borrow",
    "book": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
    "user": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
    "borrowedAt": "2023-10-18T00:00:00+00:00",
    "returnedAt": null
}
```
</details>

<details>
<summary><b>POST Book</b></summary>

### Header
```
POST /books
Accept: application/ld+json, application/json
Content-Type: application/ld+json
Authorization: Bearer <token with role ROLE_ADMIN>
```

### Body
Pas besoin de @contexte pour le post, le serveur connait le contexte.
```
{
    "@context": "schema.org/Book",
    "@type": "Book",
    "isbn": "978-1-56619-909-4",
    "name": "Zero to One",
    "description": "Notes on Startups, or How to Build the Future",
    "author": "Peter Thiel",
    "publicationDate": "2014-09-16T00:00:00+00:00"
}
```

### Response
```
HTTP/3.0 201 Created
{
    "@context": "schema.org/Book",
    "@id": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
    "@type": "Book",
    "isbn": "978-1-56619-909-4",
    "name": "Zero to One",
    "description": "Notes on Startups, or How to Build the Future",
    "author": "Peter Thiel",
    "publicationDate": "2014-09-16T00:00:00+00:00"
}
```
</details>

<details>
    <summary><b>POST Borrow</b></summary>

### Header
```
POST /books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a/borrows
Accept: application/ld+json, application/json
Content-Type: application/ld+json
Authorization: Bearer <token>
```
## Body
```
{
    "@context": "schema.org/BorrowAction",
    "@type": "Borrow",
    "user": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5"
}
```

### Response
```
HTTP/3.0 201 Created
{
    "@context": "schema.org/BorrowAction",
    "@id": "/borrows/d3e4f5g6-h7i8-9j0k-l1m2-n3o4p5q6r7s",
    "@type": "Borrow",
    "book": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
    "user": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
    "borrowedAt": "2023-10-18T00:00:00+00:00",
    "returnedAt": null
}
```
</details>

## Lenders
<details>
    <summary><b>GET Lender</b></summary>

### Header
```
GET /lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5
Accept: application/ld+json, application/json
Authorization: Bearer <token with role ROLE_ADMIN or same uuid>
```
### Response
```
HTTP/3.0 200 OK
{
    "@context": "schema.org/Person",
    "@id": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
    "@type": "User",
    "name": "admin",
    "email": "admin@localhost",
    "roles": [
        "ROLE_ADMIN"
    ]
}
```
</details>

<details>
    <summary><b>POST Lender</b></summary>

### Header
```
POST /lenders
Accept: application/ld+json, application/json
Content-Type: application/ld+json
```
### Body
```
{
    "@context": "schema.org/Person",
    "@type": "User",
    "name": "admin",
    "email": "admin@localhost",
    "password": "admin",
    "roles": [
        "ROLE_ADMIN"
    ]
}
```
### Response
```
HTTP/3.0 201 Created
{
    "@context": "schema.org/Person",
    "@id": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
    "@type": "User",
    "name": "admin",
    "email": "admin@localhost",
    "roles": [
        "ROLE_ADMIN"
    ]
}
```
</details>

## Admin

<details>
    <summary><b>GET Lenders</b></summary>

### Header
```
GET /admin/lenders
Accept: application/ld+json, application/json
Authorization: Bearer <token with role ROLE_ADMIN>
```
### Response
```
HTTP/3.0 200 OK
{
    "@context": "schema.org/Person",
    "@id": "/lenders",
    "@type": "hydra:Collection",
    "hydra:member": [
        {
            "@id": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
            "@type": "User",
            "name": "admin",
            "email": "admin@localhost",
            "roles": [
                "ROLE_ADMIN"
            ]
        },
        {
            "@id": "/lenders/b6c7d8e9-f0a1-2b3c-4d5e-6f7g8h9i0j1",
            "@type": "User",
            "name": "user",
            "email": "user@localhost",
            "roles": [
                "ROLE_USER"
            ]
        }
    ],
    "hydra:totalItems": 2
}
```
</details>