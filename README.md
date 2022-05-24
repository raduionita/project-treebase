# project-treebase
tree structured database

### scope

database with a tree base structure

### usage

`GET /` => returns all resources/collections at root
`GET /accounts` => collection (as a field under root)
`GET /accounts/:aid` // resource
`GET /accounts/:aid/users` => collection
`GET /accounts/:aid/users/:uid` => resource
`GET /accounts/:aid/users/:uid/field` => field(collection or resource)

`SET` => update
`MOD` => update

`PUT` => create
`ADD` => create

`DEL` => delete

`IDX` => create index


### todo

- client (tbase tql --addr :13337) => `> GET /users/:user_id`
- server
- api/sdk (grpc,binary,rest)
- persistance (to drive)
- plug-ins (persistance:local,aws.s3,gdrive|client:javascript,http,tql=sql-ish)
- dump (json,csv,...)
- indices (INDEX /users/:field ?!)
- describe/explain structure
