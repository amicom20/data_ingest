-강준우 06001-

2. This time save the same in parquet format with snappy compression. Save it in
/loudacre/accounts/user_compressed. Provide.a screenshot of HUE with the new directory created.

```
[training@localhost ~]$ sqoop import --connect jdbc:mysql://localhost/loudacre --username training --password training --table accounts --target-dir /loudacre/accounts/user_compressed --columns "acct_num,first_name,last_name" --fields-terminated-by "\t" --as-parquetfile --compression-codec org.apache.hadoop.io.compress.SnappyCodec


19/03/10 21:53:37 INFO mapreduce.ImportJobBase: Transferred 1.2446 MB in 43.6941 seconds (29.1678 KB/sec)
19/03/10 21:53:37 INFO mapreduce.ImportJobBase: Retrieved 129761 records.

[training@localhost ~]$ parquet-tools head hdfs://localhost/loudacre/accounts/user_compressed
acct_num = 32441
first_name = Peter
last_name = Zachary

acct_num = 32442
first_name = Duane
last_name = Ruiz

acct_num = 32443
first_name = Desiree
last_name = Beall

acct_num = 32444
first_name = Molly
last_name = Pinder

acct_num = 32445
first_name = Melissa
last_name = Carlson

hue화면은 스크린샷 파일 참조  :2.jpg
```
