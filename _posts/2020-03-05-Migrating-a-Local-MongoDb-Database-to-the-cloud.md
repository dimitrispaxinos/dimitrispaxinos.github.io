---
layout: post
title: How to migrate a local MongoDB database to the cloud for free
tags: mongodb mongo azure cloud migration
---

###  Finding a free cloud solution

I was looking for a cheap way to migrate a local MongoDb database, hosted on my NAS to the cloud. Since it was used for a non-revenue-generating side project, I did not want to pay for the hosting, at least initially.

The best solution I found was to migrate it to [MongoDB Atlas]([https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)), a Database as a Service (DBaaS) version of MongoDB that can be hosted in AWS, Azure or Google Cloud. I chose Azure, since the app I was using it with was also hosted there. This is not important at the moment though.

As we can  see in the image below, there is a forever free tier option: 

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/MongoDbMigration/MongoAtlasPlans.png)

###  Data Migration

After signing up, you can just go and create the new database.

####  Copying  data from the local database using MongoDB Compass

In order to copy your data from the old database:

1) Open MongoDB Compass
2) Go to database and the collections you would like to migrate
3) Go to menu **Collection -->Export Collection** and export each collection to a JSON file

####  Inserting  data to the cloud database

- We must first get the connection string for the cloud database. We go    to the MongoDB Atlas page, follow the steps, as shown in the images below and copy the connection string.

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/MongoDbMigration/Connect.jpg)

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/MongoDbMigration/MongoShell.jpg)

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/MongoDbMigration/ConnectionString.JPG))

- We now return to MongoDB Compass and connect to the cloud database, but, before doing so, **we have to whitelist our IP or disable IP filtering completely.** 
 
![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/MongoDbMigration/IP_Whitelisting.JPG)

- Now, for every collection already backed up in a Json file, we create a collection with the same name. 
- We then go to menu **Collection --> Import Data** and select the JSON file we created previously, in the data export phase. 
- When trying to import the data, we might get the error *"Unexpected end of file"*. After googling a bit, the problem lies on the fact  that all  data in the file are expected to be in one line. This was not that easy to change for more than 70k documents. Thankfully there is a  [workaround](https://stackoverflow.com/questions/56151099/unexpected-end-of-json-input-in-mongodb-compass)
- To solve this, we just have to use the command line and the  following command:

    mongoimport --jsonArray --db **YourDatabase** --collection **YourCollection** --file **Yourfile.json**


You can now enjoy your free cloud MongoDB instance!




