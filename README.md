# KafkaLogstashGraphiteGrafana
Docker compose setup for sending json events to a grafana front end via kafka, logstash and graphite. This is for playing around with config rather than production, hence the rather lax security.

## Requirements

 - Docker

## Setup

 - **If using windows and boot2docker/docker toolbox make sure you place this repository somewhere beneath C:\Users as it's a pain to try and set up other file locations to share with the docker host** - if you don't see the logstash.conf file copied across then you may be running into this issue.  
 - Change the volume path in the logstash docker configuration to match where you've placed this repository
 - Change the IP on the kafka configuration to be that of your docker host
 - Change logstash.d/logstash.conf so that you know which kafka topic is being listened to and what's being outputted.
 - Run docker-compose up -d
 - Visit port 3000 on your dockerhost to setup grafana
   - Log in with the default settings of admin/admin
   - Go to datasources, click Add New
   - Give it a name and use `http://graphite:80` as the address - **make sure the access type is proxy or it won't resolve graphite**
   - Save
 - Go back to dashboards and create a new one, you should now be able to use graphite as a source for your data queries.
 - Post some JSON events to your chosen kafka topic and you should see the graphs update.

## To Do

 - automatically register graphite as a data source to grafana