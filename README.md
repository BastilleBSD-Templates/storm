# storm
Bastille Template to create an Apache Storm Jail

Fill in mandatory configurations into storm.yaml
The Storm release contains a file at conf/storm.yaml that configures the Storm daemons. You can 
see the default configuration values here. storm.yaml overrides anything in defaults.yaml. There's 
a few configurations that are mandatory to get a working cluster:

1) storm.zookeeper.servers: This setting is a list of the hostnames in the ZooKeeper cluster. It 
   should look something like:

	storm.zookeeper.servers:
	  - "111.222.333.444"
	  - "555.666.777.888"

If the port that your Zookeeper cluster uses is different than the default, you should set 
storm.zookeeper.port as well.

2) storm.local.dir: The Nimbus and Supervisor daemons require a directory on the local disk to 
   store small amounts of state (like jars, confs, and things like that). You should create that 
   directory on each machine, give it proper permissions, and then fill in the directory location 
   using this config. For example:

	storm.local.dir: "/mnt/storm"

3) nimbus.host: The worker nodes need to know which machine is the master in order to download 
   topology jars and confs. For example:

	nimbus.host: "111.222.333.44"

4) supervisor.slots.ports: For each worker machine, you configure how many workers run on that 
   machine with this config. Each worker uses a single port for receiving messages, and this 
   setting defines which ports are open for use. If you define five ports here, then Storm will allocate up to five workers to run on this machine. If you define three ports, Storm will only run up to three. By default, this setting is configured to run 4 workers on the ports 6700, 6701, 6702, and 6703. For example:

supervisor.slots.ports:
    - 6700
    - 6701
    - 6702
    - 6703


If there are configuration changes needed the following sites are the go to sites:

	http://www.corejavaguru.com/bigdata/storm/setting-up-a-storm-cluster

	https://storm.apache.org/


