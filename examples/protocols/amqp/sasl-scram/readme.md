# Artemis SCRAM-SHA SASL Example

If you have not already done so, [prepare the broker distribution](../../../../README.md#getting-started) before running the example.

To run the example, simply type **mvn verify** from this directory, or **mvn -PnoServer verify** 
if you want to start and create the broker manually.

This example demonstrates the usage of SCRAM-SHA SASL authentication with ActiveMQ Artemis and AMQP clients.

Of note is the AMQP acceptor configuration restricting the offered mechanisms to SCRAM-SHA-256, and the reference
to the login config scope ``amqp-sasl-scram`` that holds the relevant SCRAM login module.

````
  <acceptor name="amqp">tcp://localhost:5672?protocols=AMQP;saslMechanisms=SCRAM-SHA-256;saslLoginConfigScope=amqp-sasl-scram
````

Also note, the password supplied to the QPID JMS AMQP client is not stored in the users.properties on the broker. It does not
leave the client!.
The secure encoded form of the password has been generated/registered using:

```` 
  java org.apache.activemq.artemis.spi.core.security.jaas.SCRAMPropertiesLoginModule <username> <password> [<iterations>]
````