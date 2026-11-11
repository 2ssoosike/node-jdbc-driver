<div align="center">
	<h1>Node JDBC Driver</h1> 
	<br>
	<p>node-jdbc-driver is a JDBC API wrapper for Node.js, providing methods to manage database connections, execute queries and update statements, and retrieve database information such as table and column structures in a database-independent manner.</p>
<!-- 	<a href="https://packagephobia.now.sh/result?p=node-jdbc-driver"><img src="https://badgen.net/packagephobia/install/node-jdbc-driver" alt="Bundle size"></a> -->
	<a href="https://img.shields.io/badge/dependencies-up--to--date-brightgreen.svg"><img src="https://img.shields.io/badge/dependencies-up--to--date-brightgreen.svg" alt="Dependencies upto date"></a>
	<a href="https://img.shields.io/badge/status-stable-brightgreen.svg"><img src="https://img.shields.io/badge/status-stable-brightgreen.svg" alt="Status"></a>
	<a href="https://www.npmjs.com/package/node-jdbc-driver"><img src="https://img.shields.io/npm/dw/node-jdbc-driver" alt="Downloads"></a>
	<a href="https://www.npmjs.com/package/node-jdbc-driver"><img src="https://img.shields.io/npm/v/node-jdbc-driver" alt="Npm version"></a><br />
	<a href="mail-pcode027@gmail.com"><img src="https://img.shields.io/badge/author-pcode027@gmail.com-blue.svg" alt="Author"></a>
</div>

---

<!-- DOC -->
- [Features](#features)
- [Installation](#installation)
- [Loading and configuring the module](#loading-and-configuring-the-module)
- [Common Usage](#common-usage)
<!-- /DOC -->

## Features
- **Simplified JDBC Usage**: Provides an intuitive API to manage JDBC database connections, execute queries, and handle update statements, abstracting away low-level complexities.

- **Multiple Database Support**: Seamlessly connect to different types of databases, including Hive, PostgreSQL, Tibero, and SQLite, with a unified interface.

- **Flexible Configuration**: Easily configure database connections using either host, port, database name, username, and password or via custom JDBC connection with driver jars and connection URLs.

- **Connection Pooling**: Benefit from built-in connection pooling support to efficiently manage and reuse database connections, enhancing application performance.

- **Query Execution**: Execute custom SQL queries and retrieve results in a straightforward manner, enabling you to interact with your database effortlessly.

- **Database Structure Information**: Retrieve comprehensive information about table and column structures using simple methods, enabling you to work with your database schema efficiently.

- **Data Manipulation**: Perform essential data manipulation tasks such as counting rows, finding rows based on criteria, retrieving all rows from a table, and more.

- **Data Definition Language (DDL) Support**: Execute DDL queries to manage the structure of your database, including creating and altering tables, views, and indexes.


## Installation
To install the package, use the following command:
```sh
npm install --save node-jdbc-driver
```

### Loading and configuring the module
You can initialize the JDBC driver using either CommonJS or ES6 syntax:
```javascript
// CommonJS
const { default: JdbcDriver, ConnectionType } = require("node-jdbc-driver");

// ES6
import JdbcDriver, { ConnectionType } from 'node-jdbc-driver';
```


## Common Usage
Below are some minimal usage examples demonstrating how to use the `node-jdbc-driver` package.

### Connection Setup
For different types of databases, you need to provide specific connection details.

#### Available Connection types
```javascript
ConnectionType.hive // for hive connection
ConnectionType.postgreSql // for postgreSql connection
ConnectionType.sqlite // for sqlite connection
ConnectionType.tibero // for tibero connection
ConnectionType.custom // Establish a JDBC connection using a custom driver
```

#### Hive and PostgreSQL Connection
For Hive and PostgreSQL connections, provide the host, port, database name, username, and password:
```javascript
const host = '<host>';
const port = '<port>';
const database = '<database_name>';
const username = '<username>';
const password = '<password>';

// Set optional parameters
const minpoolsize = '<min_pool_size>'
const maxpoolsize = '<max_pool_size>'

// For Hive
const jdbc = new JdbcDriver(ConnectionType.hive, { host, port, database, username, password });

// For Hive with connection url
const jdbcUrl = 'jdbc:hive2://<host>:<port>/<database>'
const jdbc = new JdbcDriver(ConnectionType.hive, { jdbcUrl, username, password });

// For PostgreSql
const jdbc = new JdbcDriver(ConnectionType.postgreSql, { host, port, database, username, password });

// For PostgreSql with connection url
const jdbcUrl = 'jdbc:postgresql://<host>:<port>/<database>'
const jdbc = new JdbcDriver(ConnectionType.postgreSql, { jdbcUrl, username, password });

// For tibero connection
const jdbc = new JdbcDriver(ConnectionType.tibero, { host, port, database, username, password });
```
#### SQLite Connection
For SQLite connections, provide the path to the SQLite database file:
```javascript
const path = '<db_path>';

// Set optional parameters
const minpoolsize = '<min_pool_size>'
const maxpoolsize = '<max_pool_size>'

const jdbc = new JdbcDriver(ConnectionType.sqlite, { path });
```

#### JDBC Connection using custom driver
```javascript
 const jdbc = new JdbcDriver(ConnectionType.custom, {
        jars: 'sqlite-jdbc-3.7.2.jar', // local path of your jar file
        driverClass: 'org.sqlite.JDBC', // Driver class of your jar file
        jdbcUrl: 'jdbc:sqlite:/Users/jaynathray/Downloads/demo' // use jdbc url for connection
})
```

```javascript
 const jdbc = new JdbcDriver(ConnectionType.custom, {
        jars: 'sqlite-jdbc-3.7.2.jar', // local path of your jar file
        driverClass: 'org.sqlite.JDBC', // Driver class of your jar file
        path: '/Users/jaynathray/Downloads/demo' // use path for connection
})
```

## Basic Operations
Here are some basic operations you can perform using the `node-jdbc-driver`:

### Check Driver Version
You can check the driver version using the following method:
```javascript
const version = jdbc.get_version();
```

### Count Example
To count the number of rows in a table:
```javascript
const total = await jdbc.count('<table_name>');
```

### Find Example
To find a single row based on a WHERE clause:
```javascript
const row = await jdbc.find('<table_name>', '<where_clause>');
```

### Find All Example
To retrieve all rows from a table:
```javascript
const rows = await jdbc.findAll('<table_name>');
```

### SQL Query Example
To execute a custom SQL query:
```javascript
const results = await jdbc.sql('<sql_query>');
```

### DDL Example
To execute Data Definition Language (DDL) queries:
```javascript
const results = await jdbc.ddl('<sql_query>');
```

### List Table Columns
To retrieve information about table columns:
```javascript
const columns = await jdbc.get_columns('<table_name>');
```

### Describe Table Properties
To get properties of a table:
```javascript
const tblProperties = await jdbc.get_table_properties('<table_name>');
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Build
node.js v22.23.4 에 맞춰서 npm run build 하려면 node.js v22.23.4 / java v1.8.0_332 / visual studio 2019 필요. 현재 푸시된 빌드 환경은 아래 것들 받아서 윈도우 환경에서 빌드함.

- https://nodejs.org/dist/v22.23.4/node-v22.23.4-win-x64.zip
- https://github.com/ojdkbuild/ojdkbuild/releases/download/java-1.8.0-openjdk-1.8.0.332-1.b09/java-1.8.0-openjdk-1.8.0.332-1.b09.ojdkbuild.windows.x86_64.zip
- https://aka.ms/vs/16/release/vs_community.exe

### node.js v22.23.4 에 맞춰 빌드하기 위한 환경 구성 후 추가 작업
- java 패키지 업그레이드
 - "java": "^0.12.1" -> "java": "^0.15.0"
- 데이터 타입 호환성을 위해 nan 패키지 추가
 - "nan": "^2.22.0"
- jdbc 패키지 코드 수정
 - jdbc\node_modules\java\src\javaObject.cpp, NAN_GETTER 함수 안에서 정수형 객체로 명시적 래핑(245 라인)
 - jdbc\node_modules\java\src\utils.cpp, case TYPE_INT 일 때 return 부분 정수형 객체로 명시적 래핑(731 라인)
