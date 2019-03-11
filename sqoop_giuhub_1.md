1. From the accounts table, import only the primary key, along with the first name, last name to
HDFS directory /loudacre/accounts/user_info. Please save the file in text format with tab
delimiters.
Hint: You will have to figure out what the name of the table columns are in order to complete
this exercise.

[training@localhost ~]$ sqoop list-tables --connect jdbc:mysql://localhost/loudacre --username training --password training
19/03/10 21:31:05 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 21:31:05 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 21:31:05 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.

accountdevice
accounts
basestations
customerservicerep
device
knowledgebase
mostactivestations
webpage

[training@localhost ~]$  mysql -h localhost -u training -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 335
Server version: 5.1.73 Source distribution

Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hue                |
| loudacre           |
| metastore          |
| mysql              |
| test               |
+--------------------+
6 rows in set (0.00 sec)

mysql> use loudacre;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+--------------------+
| Tables_in_loudacre |
+--------------------+
| accountdevice      |
| accounts           |
| basestations       |
| customerservicerep |
| device             |
| knowledgebase      |
| mostactivestations |
| webpage            |
+--------------------+
8 rows in set (0.00 sec)

mysql> desc accounts;
+----------------+--------------+------+-----+---------+-------+
| Field          | Type         | Null | Key | Default | Extra |
+----------------+--------------+------+-----+---------+-------+
| acct_num       | int(11)      | NO   | PRI | NULL    |       |
| acct_create_dt | datetime     | NO   |     | NULL    |       |
| acct_close_dt  | datetime     | YES  |     | NULL    |       |
| first_name     | varchar(255) | NO   |     | NULL    |       |
| last_name      | varchar(255) | NO   |     | NULL    |       |
| address        | varchar(255) | NO   |     | NULL    |       |
| city           | varchar(255) | NO   |     | NULL    |       |
| state          | varchar(255) | NO   |     | NULL    |       |
| zipcode        | varchar(255) | NO   |     | NULL    |       |
| phone_number   | varchar(255) | NO   |     | NULL    |       |
| created        | datetime     | NO   |     | NULL    |       |
| modified       | datetime     | NO   |     | NULL    |       |
+----------------+--------------+------+-----+---------+-------+
12 rows in set (0.00 sec)

mysql> Bye

[training@localhost ~]$ sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training --table accounts --target-dir /loudacre/accounts/user_info --columns "acct_num,first_name,last_name" --fields-terminated-by "\t" --as-textfile

19/03/10 21:44:35 INFO mapreduce.ImportJobBase: Transferred 2.4947 MB in 38.3612 seconds (66.5936 KB/sec)
19/03/10 21:44:35 INFO mapreduce.ImportJobBase: Retrieved 129761 records.
[training@localhost ~]$ hdfs dfs ^C
[training@localhost ~]$ hdfs dfs -ls /loudacre/accounts/user_info
Found 5 items
-rw-rw-rw-   1 training supergroup          0 2019-03-10 21:44 /loudacre/accounts/user_info/_SUCCESS
-rw-rw-rw-   1 training supergroup     638090 2019-03-10 21:44 /loudacre/accounts/user_info/part-m-00000
-rw-rw-rw-   1 training supergroup     649567 2019-03-10 21:44 /loudacre/accounts/user_info/part-m-00001
-rw-rw-rw-   1 training supergroup     649000 2019-03-10 21:44 /loudacre/accounts/user_info/part-m-00002
-rw-rw-rw-   1 training supergroup     679263 2019-03-10 21:44 /loudacre/accounts/user_info/part-m-00003
[training@localhost ~]$ hdfs dfs -tail /loudacre/accounts/user_info/part-m-00000
lsh
32390   Olga    Lipson
32391   Eddie   Hedrick
32392   Alvin   Phillips
32393   Travis  Ainsworth
32394   Allen   Pruitt
32395   Clay    Sherrill
32396   Janice  Padgett
32397   Lisa    Backes
32398   Albert  Walters
32399   Anna    Rathbone
32400   Gwen    Nelson
32401   Judith  Sullivan
32402   Linda   Davis
32403   Deborah Felipe
32404   Tami    Ketcham
32405   Suzanne Alexander
32406   Anita   Byrd
32407   Kenneth Khalil
32408   Jennifer        Merida
32409   Kevin   Gibson
32410   Sheila  Morgan
32411   Kenny   Conger
32412   Angel   Scoggins
32413   Ida     Castro
32414   Tammy   Buxton
32415   James   Ward
32416   Emma    Carmichael
32417   Carmen  Lane
32418   Andrea  Holt
32419   Catherine       Roberts
32420   Erin    Little
32421   Johnny  Graves
32422   Leonard Lamm
32423   Dennis  Hodge
32424   Nadine  Frias
32425   Juan    Mendel
32426   Dorothy Thompson
32427   Tara    Jenkins
32428   Philip  Gamble
32429   Marvin  Potts
32430   Stephanie       Wootton
32431   Judith  Lindgren
32432   Darlene Gonzales
32433   Nicholas        Monger
32434   Anne    Boyle
32435   Marjorie        Morrison
32436   Helen   Perez
32437   Melissa Hayes
32438   Violet  Searcy
32439   Eunice  Myers
32440   Robert  Huskey