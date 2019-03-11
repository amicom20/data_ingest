강준우(06001)

flume_ex.conf file
```
# Name the components on this agent
agent1.sources = s1
agent1.sinks = k1
agent1.channels = c1

# Describe/configure the source
agent1.sources.s1.type = netcat
agent1.sources.s1.bind = localhost
agent1.sources.s1.port = 44444
agent1.sources.s1.channels = c1

# Describe the sink
agent1.sinks.k1.type = logger
agent1.sinks.k1.channel = c1

# Use a channel which buffers events in memory
agent1.channels.c1.type = memory
agent1.channels.c1.capacity = 1000
agent1.channels.c1.transactionCapacity = 100
```

Run Flume Agent
```
$ flume-ng agent --conf /etc/flume-ng/conf --conf-file /home/training/flume_ex.conf --name agent1 -Dflume.root.logger=INFO,console
```

Result: telnet connection
```
[training@localhost ~]$ telnet localhost 44444
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
Hello world~!~!
OK
```

Result: flume agent result
```
2019-03-11 01:23:36,594 (lifecycleSupervisor-1-3) [INFO - org.apache.flume.source.NetcatSource.start(NetcatSource.java:169)] Created serverSocket:sun.nio.ch.ServerSocketChannelImpl[/127.0.0.1:44444]
2019-03-11 01:24:22,603 (SinkRunner-PollingRunner-DefaultSinkProcessor) [INFO - org.apache.flume.sink.LoggerSink.process(LoggerSink.java:94)] Event: { headers:{} body: 48 65 6C 6C 6F 20 77 6F 72 6C 64 7E 21 7E 21 0D Hello world~!~!. }
```
