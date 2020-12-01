word count analysis using hadoop mapreduce and java

How to run the program
step 1:
Install docker: 
$ sudo apt-get remove docker docker-engine docker.io containerd runc
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
$ sudo docker run hello-world

step 2:
Pull docker image:
$ sudo docker pull kiwenlau/hadoop:1.0

step 3:
Clone the github repository:
$ git clone https://github.com/kiwenlau/hadoop-cluster-docker

step 4:
Create hadoop network
$ sudo docker network create --driver=bridge hadoop

step 5:
Start hadoop container clusters:
$ cd hadoop-cluster-docker
$ sudo ./start-container.sh

step 6:
Start hadoop clusters
$ ./start-hadoop.sh

step 7:
Resize the cluster
exit the master and resize the cluster 
$ sudo ./resize-cluster.sh 5

step 8:
vim start-container.sh and resize the number of nodes to 5 which results in 1 master and 4 slaves

step 9:
Once the resizing process succeeds, start the hadoop containers
$ sudo ./start-container.sh

step 10:
Let’s compile the above WordCount program:
$ export HADOOP_CLASSPATH=$JAVA_HOME/lib/tools.jar
$ hadoop com.sun.tools.javac.Main WordCount.java
$ jar cf wc.jar WordCount*.class

step 11:
Edit the run-wordcount.sh with the input file
cp text.txt input/text.txt
and include the below mentioned line
$ hadoop jar wc.jar WordCount input output

step 12:
clear the inputs
$ hadoop fs -rm -r -f o1

step 13:
run the program
$ ./run-wordcount.sh

Output
$ and 18











