# AISetConnections

Atrium Integrator Connection - workaround to stop the pain!

If you are using Atrium Integrator in your ITSM System I'm sure you already had issues with you connections.
Maybe you also made the mistake and you created more than one connection, for each of your environments [dev,qa,prod] and ended up in changing all the connections for each step, while staging them to another environment

At on premise system it already helps, if you are using one connection with the same name in all stages, and your Spoon UI is configured to not overwriting connection while importing  transformations. (which need to be set in every single Spoon UI)

But dealing with AI connections in helix environment become much more complicated than I've ever expected.
We can develop and debug the AI jobs in our system using a client gateway to the helix server, but you need to use different connections for development/debug and serverside execution. even if you are working on the same stage!
Means if you have a transformation, which for example 5 AR Input/AR Output,CMDB Output or AR Upsert/ Table Input steps, and you need to do some debugging, to run the same job in spoon you need to change ALL connections, do your debugging/change stuff and again change all connections back to run it on serverside

It's not hard to see that this will cause big problems, because maybe you will forget of one or to steps.

# How to get this solved?

I've created a transformation which set all your connections, depending on the system you run the transformations, by using variables.

 

This means you need to setup your connections once for using variables.

Like this for example:

 




Afterwards you need to configure how to set this variables for each in the transformations "set constants" step. 
 

You need to set all your variables for each different connection. (AR, DBs)

add your devlopment hostnames into the javascript step:
 



# IMPORTANT:
#This transformation need to be the first transformation in each job. To set the connection corret for serverside executions.  In your local dev system after opening spoon you should run this transformation to set your connections.


You can run it locally, on your client gateway, or on your server, on DEV, QA, Prod stage it doesn't matter - no more need to change connection. If you set up once.



