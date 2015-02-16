Jenkins image with Docker
==================================

This provides a Jenkins image with docker setup on it. This is useful when your CI is responsible for building and
packaging a docker image of your web app or anything you may be building. You could use jenkins to build the 
application and push it to dockerHub. CI could then deploy the docker image on several servers.

## Installation

The installation is as simple as downloading any other docker image.

	docker pull mkulkarni/jenkins-with-docker 

## Usage

The jenkins data needs to be persisted. There are 2 ways to do this:

- Mount data on a Data Volume Container
- Mount host directory as a Data Volume

### Mount data on a Data Volume Container

This is only a prerequisite if you wish to store jenkins data on a Data Volume Container (recommended). To use this 
run the data volume container with name jenkins-data

	docker run --name jenkins-data mkulkarni/jenkins-data-volume-container

The jenkins-data-volume container need not be running at all times. 

Run the jenkins container with data volume you started earlier

	docker run -d -p 8080:8080 --privileged --volumes-from jenkins-data mkulkarni/jenkins-with-docker

### Mount host directory as the Data Volume 

If you wish to use volume on your host, you can just run the following

	docker run -d -p 8080:8080 --privileged -v /jenkins/home/on/host:/var/lib/jenkins-home mkulkarni/jenkins-with-docker

This should start up jenkins on port 8080. Off you go!! 

