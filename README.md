# dbt-investigations
### The goal of this project is to launch and connect DBT to Clickhouse and MySQL.
### We are trying to show and solve  dbt-core and dbt-MySQL incompatible versions.

# Installation

## step 1: running mysql and clickhouse
```bash
docker compose up -d
```

## step 2.1: install dbt-core
```
pip install dbt-core
```
## step 2.2: check dbt version
```
dbt --version
```
## step 2.3: install dbt-mysql
```
pip install dbt-mysql
```
## step 2.4: check dbt version again
```
dbt --version
```
`NOTE` dbt version must be downgraded


## step 3: init dbt and config profile cononections
```
dbt init
#input your project name to initialize it.
cp profiles.yml <project-dir>/
cd <project-dir>/
nano profiles.yml
# change profile connection configs
```
## step 4: test dbt connections
```
dbt debug
```
#### you must see this
```
11:53:36  adapter type: mysql
11:53:36  adapter version: 1.7.0
11:53:36  Configuration:
11:53:36    profiles.yml file [OK found and valid]
11:53:36    dbt_project.yml file [OK found and valid]
11:53:36  Required dependencies:
11:53:36   - git [OK found]

11:53:36  Connection:
11:53:36    server: localhost
11:53:36    unix_socket: None
11:53:36    port: 3306
11:53:36    database: None
11:53:36    schema: dbt
11:53:36    user: root
11:53:36  Registered adapter: mysql=1.7.0
11:53:36    Connection test: [OK connection ok]

11:53:36  All checks passed!

```
## step 5: upgrade dbt-core or install dbt-mysql with local directory
```
pip install --upgrade dbt-core
```
`or`
```
pip install ./dbt-mysql/
```
we forked dbt-mysql and change `dbt-mysql/dbt/adapters/mysql/__version__.py` to last dbt-core version.
## step 6: run debug and see the Error
```
dbt debug
```
```
from dbt.adapters.factory import adapter_management, register_adapter, get_adapter
ModuleNotFoundError: No module named 'dbt.adapters.factory'
```

## step 7: solving
### look at communities
https://github.com/dbeatty10/dbt-mysql/issues/170

https://github.com/dbt-labs/dbt-core/issues/10135

https://github.com/dbt-labs/dbt-core/discussions/9798
