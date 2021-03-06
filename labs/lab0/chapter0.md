## Introduction

In this lab, we are going to leverage a process known as [`oc cluster up`](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md). This enables us to quickly stand up a local OpenShift Container Platform to start our evaluation. The key result of `oc cluster up` is a reliable, reproducible OpenShift environment to iterate on.

Expected completion: 5-10 minutes

## Find your AWS Instance
This lab is designed to accomodate many students. Each student will be given a VM running on AWS. The VM naming convention for the lab is:

**student-##**.sclr.cloud

You will be assigned a number by the instructor.

## Connecting to your AWS Instance
This lab should be performed on **YOUR ASSIGNED AWS INSTANCE** as `ec2-user` unless otherwise instructed.

Retrieve the key from the [here](https://s3-us-west-2.amazonaws.com/aws-ocp-lab/index.html) so that you can _SSH_ into the instances. Linux or Mac users, download the .PEM to your local machine & change the permissions of the .PEM file to 600. Windows users, download the .PPK key, no permission changes required.

**NOTE**: Please be respectful and only connect to your assigned instance. Every instance for this lab uses the same public key so you could accidentally (or with malicious intent) connect to the wrong system. If you have any issues please inform an instructor.
```bash
$ ssh -i af-ocp-lab.pem ec2-user@student-##.sclr.cloud
```
**NOTE**: Windows users will have to use a terminal like [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) to SSH using the private key (.PPK).
```
c:\path\to\putty.exe -i af-ocp-lab.ppk ec2-user@student-##.sclr.cloud
```
For tips on using PuTTY to connect to your AWS instance, [click here.](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html)

## Getting Set Up
For the sake of time, some of the required setup has already been taken care of on your AWS VM. For future reference though, the easiest way to get started is to head over to the OpenShift Origin repo on github and follow the "[cluster up and down instructions](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md)" instructions. The instructions cover getting started on Windows, MacOS, and Linux.

Since some of these labs will have long running processes, it is recommended to use something like `tmux` or `screen` in case you lose your connection at some point so you can reconnect:
```bash
$ sudo yum -y install screen
$ screen
```

In case you get disconnected use `screen -x` to reattach once you reestablish ssh connectivity.

All that's left to do is run OpenShift by executing the `start-oc.sh` script in your home directory. First, let's take a look at what this script is doing, it's grabbing AWS instance metadata so that it can conifigure OpenShift to start up properly on AWS:
```bash
$ cat ~/start-oc.sh
```
Now, let's start our local, containerized OpenShift environment:
```bash
$ ~/start-oc.sh
```

The resulting output should be something of this nature
```bash
   The server is accessible via web console at:
       https://<public-hostname>:8443

   You are logged in as:
       User:     developer
       Password: developer
```
You should get a lot of feedback about the launch of OpenShift. As long as you don't get any errors you are in good shape.

Now that OpenShift is available, let's ask for a cluster status & take a look at our running containers:
```bash
$ oc cluster status
$ docker ps
$ docker images
```
We can also check out the OpenShift console. Open a browser and navigate to `https://<public-hostname>:8443`. Once it loads (and you bypass the certificate error), you can log in to the console using the default developer username/password.
ild from scratch, whatever you can do in a container, and still get the complete lifecycle automation you loved in the older versions.

**Please note:** Labs 1 and 3 will contain objectives that need to be completed in order to perform Lab 5. Labs 2 and 4 are notated as "Optional" because they do NOT need to be completed in order to perform Lab 5. If time permits, feel free to run through Labs 2 and 4.

You are now ready to move on to the [next lab](../lab1/chapter1.md).
