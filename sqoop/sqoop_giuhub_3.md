-강준우 06001-

3. Finally save in /loudacre/accounts/CA only clients whose state is from California. Save the file
in parquet format and compressed using gzip. From the terminal, display some of the records
that you just imported. Take a screenshot and save it as CA_only.

```
[training@localhost ~]$ sqoop eval --connect jdbc:mysql://localhost/loudacre --username training --password training --query "select distinct state from accounts"

19/03/10 22:29:28 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 22:29:28 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 22:29:28 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
------------------------
| state                |
------------------------
| CA                   |
| OR                   |
| NV                   |
| AZ                   |
------------------------

[training@localhost ~]$ sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training --table accounts --target-dir /loudacre/accounts/CA --columns "acct_num,first_name,last_name,state" --fields-terminated-by "\t" --as-parquetfile --compression-codec org.apache.hadoop.io.compress.GzipCodec --where "state='CA'"

19/03/10 22:51:30 INFO mapreduce.ImportJobBase: Transferred 948.376 KB in 45.5371 seconds (20.8264 KB/sec)
19/03/10 22:51:30 INFO mapreduce.ImportJobBase: Retrieved 92416 records.

[training@localhost ~]$ parquet-tools head hdfs://localhost/loudacre/accounts/CA/
acct_num = 64881
first_name = Virginia
last_name = Etter
state = CA

acct_num = 64882
first_name = Thomas
last_name = Jones
state = CA

acct_num = 64883
first_name = Jennifer
last_name = Spangler
state = CA

acct_num = 64884
first_name = Kathleen
last_name = Blubaugh
state = CA

acct_num = 64887
first_name = Marcia
last_name = Hall
state = CA

hue화면은 스크린샷 파일 참조  : 3.jpg
```


