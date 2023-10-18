# End points
## Books
<details>
    <summary>GET Books</summary>

### Books header
```
GET /books
Accept: application/ld+json, application/json
```
### Books response
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
            "title": "Zero to One",
            "description": "Notes on Startups, or How to Build the Future",
            "author": "Peter Thiel",
            "publicationDate": "2014-09-16T00:00:00+00:00"
        },
        {
            "@id": "/books/c7d8e9f0-1a2b-3c4d-5e6f-7g8h9i0j1k2l",
            "@type": "Book",
            "isbn": "978-1-56619-909-5",
            "title": "Zero to Two",
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
<summary>GET Book</summary>

### Book header
```
GET /books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a
Accept: application/ld+json, application/json
```
### Book response

```
HTTP/3.0 200 OK
{
    "@context": "schema.org/Book",
    "@id": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
    "@type": "Book",
    "isbn": "978-1-56619-909-4",
    "title": "Zero to One",
    "description": "Notes on Startups, or How to Build the Future",
    "author": "Peter Thiel",
    "publicationDate": "2014-09-16T00:00:00+00:00"
}
```
</details>

## Lenders

<details>
<summary>GET Lenders</summary>

### Lenders header
```
GET /lenders
Accept: application/ld+json, application/json
Authorization: Bearer <token with role ROLE_ADMIN>
```
### Lenders response
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
            "username": "admin",
            "email": "admin@localhost",
            "roles": [
                "ROLE_ADMIN"
            ]
        },
        {
            "@id": "/lenders/b6c7d8e9-f0a1-2b3c-4d5e-6f7g8h9i0j1",
            "@type": "User",
            "username": "user",
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

<details>
<summary>GET Lender</summary>

### Lender header
```
GET /lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5
Accept: application/ld+json, application/json
Authorization: Bearer <token with role ROLE_ADMIN or same uuid>
```
### Lender response
```
HTTP/3.0 200 OK
{
    "@context": "schema.org/Person",
    "@id": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5",
    "@type": "User",
    "username": "admin",
    "email": "admin@localhost",
    "roles": [
        "ROLE_ADMIN"
    ]
}
```
</details>

## Borrow

<details>
<summary>POST Borrows</summary>

### Borrow header
```
POST /borrows
Accept: application/ld+json, application/json
Content-Type: application/ld+json
Authorization: Bearer <token>
```
## Borrow body
```
{
    "@context": "schema.org/BorrowAction",
    "@type": "Borrow",
    "book": "/books/f7a8c1c9-1e1e-4f4e-9aee-5b6d8a3d8c6a",
    "user": "/lenders/a1b2c3d4-e5f6-4g7h-8i9j-k0l1m2n3o4p5"
}
```

### Borrow response
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