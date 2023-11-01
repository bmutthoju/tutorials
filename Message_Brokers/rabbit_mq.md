# Rabbit MQ #
1. Open Source Distributed Message Queue
	1. Written in Erlang
2. Supports many communication protocol
	1. Problem solved: Spaggetti architecture problem (as against ESB)
3. Table of content:
	1. RabbitMQ Components
	2. Spin RabbitMQ server with Docker
	3. Write a Publisher client in NodeJS
	4. Write a Consumer client in NodeJS
	5. My thoughts about this tech
	6. Summary

## RabbitMQ Components ##
1. Topics:
	1. AMQP Protocol
	2. Channel
	3. Publisher
	4. Consumer
	5. Exchange
	6. ...
2. Architecture:
	1. Used for clients to talk to other clients
		1. Instead of each client having a knowledge of other clients, a layer is created in between
			1. RabbitMQ Server (Port: 5672)
				1. Uses TCP protocol
				2. It could be distributed and replicated
			2. Publisher: Publishes a message for consumers to consume
				1. Establishes a stateful TCP connection with server (for two way communication)
				2. AMQP (or other protocol) is used on top of TCP
					1. It has its own format (with headers and body, ...)
					2. Enables both publisher and server to send messages to each other
				3. connection - abstraction
			3. Consumer: Consumes messages published by a publisher
				1. Establishes stateful bidirectional TCP connection to the server with AMQP (or another protocol)
					1. Says hei to server and asks for sending messages
					2. Server **pushes** messages to the consumer (when consumer is ready)
			4. Channel:
				1. It is a **logical connection** within a TCP connection
					1. Separates consumer connection from multiple sub-consumers inside the consumer
						1. Example: 3 channels using same TCP connection
						2. **Done using multiplexing**
							1. **HTTP/2 uses multiplexing as well**
								1. **Messages can be sent using channel id**
									1. Used for segregation
						3. **Publisher can publish to a channel**
							1. Or multiple channels (or else we will be forced to write separate publishers for each channel)
			5. Queue:
				1. Messages are sent to queue and pulled from queue
					1. Publishers and consumers are not aware of queues but are aware of exchanges
			6. Exchange:
				1. We send information to exchange and exchange will take care of propagating it to a queue (default exchange exists)
					1. Exchange uses different algorithms to fan-out and do round robbin to different queues etc...
				2. We can have multiple exchanges
3. Implementation:
	1. Docker:
	
			docker run hello-world
			
	2. RabbitMQ message server:
	
			docker run --name rabbitmq -p 5672:5672 rabbitmq
			
	3. Async Job Manager:
		1. A publisher publishes a job (for execution)
		2. A consumer takes a job and executes it
		3. Jobs could be heavy
			1. Map-reduce
			2. Mathematically intense (CPU expensive)
			3. DB Batch jobs (I/O intensive)
		4. Install VS Code:
			1. Open terminal
			2. Run the following:
			
					npm init -y
					
			3. New file:
			
					const amqp = require('amqplib'); // promise based
					const msg = {number: 19};
					connect();
					async function connect() {
						try {
							const connection = await amqp.connect("amqp://localhost:5672");
							const channel = await connection.createChannel();
							const result = await channel.assertQueue("jobs", Buffer.from(JSON.stringify(msg))); // ensures a queue exists or else constructs one (default)
							console.log(`Job sent successfully ${msg.number}`);
						} catch (ex) {
							console.error(ex);
						}
					}
					
				1. Install node module:
				
						npm install amqplib --save
						
		5. 
		