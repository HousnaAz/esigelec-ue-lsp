# Upload your first file in HDFS

## Prerequisites

If you didn't manage to finish the previous step, you can start from fresh using the last step branch from Git.

It assumes that you don't have an existing directory **esigelec-ue-lsp-hdp** in your Ubuntu home directory (**~**).

Open an **Ubuntu** terminal and execute:

```sh
cd ~
git clone https://github.com/adadouche/esigelec-ue-lsp-hdp.git
```

Now checkout the current step branch:

```sh
cd ~/esigelec-ue-lsp-hdp

git reset --hard origin/new-step-01
git clean -dfq
```

## Set your Hadoop environment variables

In your **Ubuntu** terminal, execute:

```sh
source ~/esigelec-ue-lsp-hdp/.set_hadoop_env.sh
```

## Start the HDFS processes

If the HDFS processes are not started yet, you will need to start them.

To check if they are started you can use the ***jps*** command.

If the processes are not started then execute the following commands in your **Ubuntu** terminal:

```sh
rm -r $HADOOP_HOME/tmp/*

hdfs namenode -format -force

start-dfs.sh
```

You can check the processes are started by using the following command:

```sh
jps
```

## Interact with the File System

Let's first create a directory:

```sh
hdfs dfs -mkdir /config
```

Now check the directory is created :

```sh
hdfs dfs -ls /
```

Now let's copy the local configuration file into it

```sh
hdfs dfs -put $HADOOP_HOME/etc/hadoop/*.xml /config
```

And finally, let's check the files are here:

```sh
hdfs dfs -ls /config
```

And visualize one:

```sh
hdfs dfs -cat /config/yarn-site.xml
```

## Check the Name Node Server

You can also get details about HDFS and the Name Node using the following URL:

 - http://localhost:50070/

And access the file system:

 - http://localhost:50070/explorer.html#/

You can also explore the folders stored in **$HADOOP_HOME/tmp/hadoop/dfs/data/current/BP-*/current/finalized/subdir0/subdir0/** using `ls`:

```sh
ls $HADOOP_HOME/tmp/hadoop/dfs/data/current/BP-*/current/finalized/subdir0/subdir0/
```

You can also use the `more` or `cat` command to view the file content.