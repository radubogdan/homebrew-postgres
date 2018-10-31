# homebrew-postgres965

Potgres 9.6.5 formula via homebrew tap

Installing postgres@9.6 will pull last release of 9.6 and cannot specify a specific release. This tap solved the need to brew postgres 9.6.5

## Installation

### Prerequisite:

```sh
# Upgrade homebrew
brew update

# Cleanup any previous postgres/postgis
brew uninstall postgis --force
brew uninstall postgresql --force
brew cleanup
brew services stop postgresql
```

### Tap this :)

```sh
brew tap radubogdan/homebrew-postgres965
```

Install latest version of postgres and unlink

```sh
brew install postgresql
brew unlink postgresql
```

The last version of postgres runs `initdb` and is incompatible with 9.6.5.

```sh
rm -rf /usr/local/var/postgres
```

```sh
brew install radubogdan/postgres965
brew switch postgresql 9.6.5
brew install postgis
```

Start postgres

```sh
brew services start postgresql
```

Create postgres user

```sh
createuser -s -d postgres
```

Connect to postgres

```
psql -U postgres
```

```sh
drop extension postgis;
create extension postgis;

-- Test if postgis is working :)

select ST_Distance(
  ST_GeometryFromText('Point(56.1629 10.2039)', 4326), -- Aarhus
  ST_GeometryFromText('Point(46.7712 23.6236)', 4326) -- Cluj-Napoca
);
```