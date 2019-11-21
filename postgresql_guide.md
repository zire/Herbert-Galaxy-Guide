# Command Comands for PostgreSQL

## Convention

A few conventions to follow:

1. Use `singular` form for database
2. Use `plural` form for table

## Basic Usage on Mac

List all available databases from console

```
$ psql -l
```

Connect to a database to arrive at psql prompt

```
$ psql XXX
```

List all available databases from postgresql prompt

```
\l
```

Create a database `startup` with default settings

```
CREATE DATABASE startup;
```

Connect to this newly created database

```
\c startup
```

List all tables from current database

```
\dt
```

## Reference

[table-naming-dilemma-singular-vs-plural-names](https://stackoverflow.com/questions/338156/table-naming-dilemma-singular-vs-plural-names)

***

[Back to HitichHikder's Guide by Herbert](README.md)