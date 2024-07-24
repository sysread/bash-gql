# SYNOPSIS

A command line tool for working with GraphQL APIs

# DESCRIPTION

`gql` is a command line tool for working with GraphQL APIs. Like Insomnia or
Postman, it allows you to send queries and mutations to a GraphQL API and see
the results, as well as to introspect the schema.

# REQUIREMENTS

- [`curl`](https://github.com/curl/curl)
- [`jq`](https://github.com/jqlang/jq)

# OPTIONAL

- [`gum`](https://github.com/charmbracelet/gum)

# INSTALL

Currently, this tool is just a single script that you can download and run.
Either clone the repo or save it directly.

# USAGE

```
gql --help

gql --host myservice.com/gql --schema

# Oops, forgot to log in first! :D
gql --host myservice.com/gql --query login.gql --input '{"input": {"user": "someone", "password": "fnord"}}' | jq -r '.data.login.token' | tee /tmp/token
gql --host myservice.com/gql --bearer "$(cat /tmp/token)" --schema

gql --host myservice.com/gql --refresh-schema

gql --host myservice.com/gql --mutations
gql --host myservice.com/gql --queries
gql --host myservice.com/gql --types

gql --host myservice.com/gql --query-docs getSomeEntity
gql --host myservice.com/gql --mutation-docs createSomeEntity
gql --host myservice.com/gql --type-docs SomeEntity
```

# AUTHENTICATION

Currently, `gql` only supports bearer tokens for authentication.

```sh
$ gql --host myservice.com/gql \
    --query login.gql \
    --input '{"input": {"user": "someone", "password": "fnord"}}' \
    | jq -r '.data.login.token' \
    | tee /tmp/token

$ gql --host myservice.com/gql \
    --bearer "$(cat /tmp/token)" \
    --query getSomeEntity.gql
    --input '{"input": {"entityId": "fnord-but-as-an-id"}}'
```
