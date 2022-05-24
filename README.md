# project-treebase
tree structured database

### scope

database with a tree base structure

### architecture

key-value store

add KEY (`/accounts`) with VALUE (`{}`)

`/`   
.L `/transactions`   
.L `/accounts`     
....L `/accounts/1`    
.......L `/accounts/1/users`    
..........L `/accounts/1/users/1`   
..........L `/accounts/1/users/2`   

`SET`+`/`+`value`   
`SET`+`/transactions`+`value`   
`SET`+`/accounts`+`value`   
`SET`+`/accounts/1`+`value`   
`SET`+`/accounts/1/users`+`value`   
`SET`+`/accounts/1/users/1`+`value`   
`SET`+`/accounts/1/users/2`+`value`   


### api

store resources(entities) inside collections (of entities)

#### select

`GET`+`/` (root) returns all resources/collections at root
```json
"ok",{
  "accounts":"R#/accounts",
  "products":"R#/products",
  "pi": 3.14
}
```

`GET`+`/accounts` => collection (as a field under root)
```json
"ok",[
  "uuid",
  "uuid"
]
```

`GET`+`/accounts/:aid` => resource/value
```json
"ok",{
  "id":"uuid",
  "users": "R#/accounts/:aid/users",
  "created": 31241231424
}
```

`GET`+`/accounts/:aid/users` => collection
```json
"ok",[
  "uuid",
  "uuid"
]
```

`GET`+`/accounts/:aid/users/:uid` => resource
```json
"ok",{
  "email":"string"
}
```

`GET`+`/accounts/:aid/users/:uid/email` => field(collection or resource)
```json
"ok","string"
```

#### update

`SET`+`/accounts/:aid`+`{"field":"value"}` => update(patch) account `:aid`
```json
"ok","ok"
```

`MOD`+`/accounts/:aid/field`+`"value"` => update account's `:aid` `field` with `"value"`
```json
"ok"
```

#### insert/create

`PUT`+`/accounts`+`{"field":"value", "users":?}` => create account
```json
"ok",{
  "field":"value"
}
```

`ADD`+`/accounts/:aid/users`+`{"email":"string"}` => create user
```json
"ok",{
  "email":"string"
}
```

#### fetch & delete

`POP`+`/accounts/:aid/users/:uid` => find resource, remove it and return it
```json
"ok",{
  "email":"string"
}
```

#### delete

`DEL`+`/accounts/:aid` => delete account
```json
"ok"
```

#### index

`IDX`+`?` => create index
```json
"ok"
```

#### count

`CNT`+`/accounts` => count accounts
```json
"ok",10
```

### todo

- client (tbase tql --addr :13337) => `> GET /users/:user_id`
- server
- api/sdk (grpc,binary,rest)
- persistance (to drive)
- plug-ins (persistance:local,aws.s3,gdrive|client:javascript,http,tql=sql-ish)
- dump (json,csv,...)
- indices (INDEX /users/:field ?!)
- describe/explain structure
