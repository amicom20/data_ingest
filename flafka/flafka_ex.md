Start the Flume agent (and logging outputs)
```
flume-ng agent --conf /etc/flume-ng/conf --conf-file $DEVSH/exercises/flafka/spooldir_kafka.conf --name agent1 -Dflume.root.logger=INFO,console

2019-03-11 23:42:00,215 (pool-4-thread-1) [INFO - org.apache.flume.client.avro.ReliableSpoolingFileEventReader.readEvents(ReliableSpoolingFileEventReader.java:258)] Last read took us just up to a file boundary. Rolling to the next file, if there is one.
2019-03-11 23:42:00,215 (pool-4-thread-1) [INFO - org.apache.flume.client.avro.ReliableSpoolingFileEventReader.rollCurrentFile(ReliableSpoolingFileEventReader.java:348)] Preparing to move file /flume/weblogs_spooldir/2014-03-07.log to /flume/weblogs_spooldir/2014-03-07.log.COMPLETED
2019-03-11 23:42:00,364 (pool-4-thread-1) [INFO - org.apache.flume.client.avro.ReliableSpoolingFileEventReader.readEvents(ReliableSpoolingFileEventReader.java:258)] Last read took us just up to a file boundary. Rolling to the next file, if there is one.
2019-03-11 23:42:00,364 (pool-4-thread-1) [INFO - org.apache.flume.client.avro.ReliableSpoolingFileEventReader.rollCurrentFile(ReliableSpoolingFileEventReader.java:348)] Preparing to move file /flume/weblogs_spooldir/2014-03-09.log to /flume/weblogs_spooldir/2014-03-09.log.COMPLETED
2019-03-11 23:42:00,509 (pool-4-thread-1) [INFO - org.apache.flume.client.avro.ReliableSpoolingFileEventReader.readEvents(ReliableSpoolingFileEventReader.java:258)] Last read took us just up to a file boundary. Rolling to the next file, if there is one.
2019-03-11 23:42:00,510 (pool-4-thread-1) [INFO - org.apache.flume.client.avro.ReliableSpoolingFileEventReader.rollCurrentFile(ReliableSpoolingFileEventReader.java:348)] Preparing to move file /flume/weblogs_spooldir/2014-03-12.log to /flume/weblogs_spooldir/2014-03-12.log.COMPLETED
```

start a Kafka consumer (and data received)
```
kafka-console-consumer --zookeeper localhost:2181 --topic weblogs

189.4.236.113 - 114360 [14/Jan/2014:00:01:35 +0100] "GET /KBDOC-00173.html HTTP/1.0" 200 7016 "http://www.loudacre.com"  "Loudacre Mobile Browser Sorrento F41L"
189.4.236.113 - 114360 [14/Jan/2014:00:01:35 +0100] "GET /theme.css HTTP/1.0" 200 7025 "http://www.loudacre.com"  "Loudacre Mobile Browser Sorrento F41L"
2.119.58.157 - 50 [14/Jan/2014:00:01:03 +0100] "GET /KBDOC-00002.html HTTP/1.0" 200 12397 "http://www.loudacre.com"  "Loudacre CSR Browser"
2.119.58.157 - 50 [14/Jan/2014:00:01:03 +0100] "GET /theme.css HTTP/1.0" 200 5185 "http://www.loudacre.com"  "Loudacre CSR Browser"
253.219.172.29 - 205 [14/Jan/2014:00:00:40 +0100] "GET /KBDOC-00187.html HTTP/1.0" 200 6891 "http://www.loudacre.com"  "Loudacre CSR Browser"
253.219.172.29 - 205 [14/Jan/2014:00:00:40 +0100] "GET /theme.css HTTP/1.0" 200 3407 "http://www.loudacre.com"  "Loudacre CSR Browser"
248.174.89.153 - 110189 [14/Jan/2014:00:00:37 +0100] "GET /KBDOC-00265.html HTTP/1.0" 200 12506 "http://www.loudacre.com"  "Loudacre Mobile Browser Titanic 2400"
248.174.89.153 - 110189 [14/Jan/2014:00:00:37 +0100] "GET /theme.css HTTP/1.0" 200 17442 "http://www.loudacre.com"  "Loudacre Mobile Browser Titanic 2400"
```

Runnning script "copy-move-weblogs.sh" (and results)
```
$DEVSH/exercises/flafka/copy-move-weblogs.sh /flume/weblogs_spooldir

/home/training/training_materials/devsh/exercises/flafka
[training@localhost flafka]$ $DEVSH/exercises/flafka/copy-move-weblogs.sh /flume/weblogs_spooldir
/flume/weblogs_spooldir exists and is not empty, delete contents? (y/n)
y
Copying and moving files to /flume/weblogs_spooldir
```
