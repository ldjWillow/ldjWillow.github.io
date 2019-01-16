---
title: 数据库驱动和url格式
copyright: true
date: 2019-01-15 20:45:46
categories: 数据库
tags: [数据库,mysql,oracle,sqlserver,db2]
---

### Oracle

驱动：oracle.jdbc.driver.OracleDriver

URL：jdbc:oracle:thin:@localhost:1521:dbname

###  mysql

驱动：com.mysql.jdbc.Driver

URL：jdbc:mysql://localhost:3306/dbname

###  SQL Server

驱动：com.microsoft.jdbc.sqlserver.SQLServerDriver

URL：jdbc:mirosoft:sqlserver://<localhost><:1433>;DatabaseName=<dbname>

### DB2

驱动：com.ibm.db2.jdbc.app.DB2Driver

URL：jdbc：db2://<localhost><:5000>/dbname