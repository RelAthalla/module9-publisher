## Message Size Estimation

### a. How much data will your publisher program send to the message broker in one run?

program sends **5 messages** to the broker, each containing a `UserCreatedEventMessage` struct with two fields:

- `user_id`: `String`
- `user_name`: `String`

#### Borsh Serialization Details:
Each `String` is serialized with a **4-byte length prefix**.

#### Example Message Content:
- `user_id`: `"1"` → 1 byte content + 4 bytes length = **5 bytes**
- `user_name`: `"2306223925-Amir"` → 16 bytes content + 4 bytes length = **20 bytes**

#### Total Per Message:
- 5 × 25 bytes = 125 bytes (approximate, actual size may vary slightly depending on string lengths).

## Broker URL Explanation

### b. What does it mean if the URL is the same in publisher and subscriber?

The URL amqp://guest:guest@localhost:5672 
Specifies the following:

- **Protocol**: `AMQP` (Advanced Message Queuing Protocol)
- **User**: `guest`
- **Password**: `guest`
- **Host**: `localhost` (the local machine)
- **Port**: `5672` (default for RabbitMQ)

### Meaning:
Both the **publisher** and **subscriber** are connecting to the **same RabbitMQ server instance**, running on the **same machine**, with the **same credentials** and **port**.

This setup allows them to **exchange messages** through the same message broker.

## Running RabbitMQ as message broker
![](images/1.png)

## Sending and Processing Event
![](images/2.png)
![](images/3.png)

When RabbitMQ (the message broker) is running and we run both the Publisher and Subscriber programs using cargo run, the Publisher sends data to the message broker, and the Subscriber receives it. As shown in the illustration, the Publisher transmits the data once to the broker, and the Subscriber successfully receives that data.

## Message Flow Between Publisher and Subscriber

When the **RabbitMQ message broker** is running, and both the **Publisher** and **Subscriber** programs are executed using:

The following process occurs:

- The **Publisher** sends data to the RabbitMQ message broker.
- The **Subscriber** receives the data from the message broker.

As illustrated, the data is sent **once** by the Publisher and is successfully **received by the Subscriber** through the broker.

This demonstrates a successful communication flow using **AMQP** via RabbitMQ.

## Monitoring chart based on publisher
![](images/4.png)

In the image above, the **Publisher** was executed multiple times to significantly increase the **message rate**.

### Key Observations:

- The **more frequently** the Publisher sends data to the **message broker**, the **higher the message rate** becomes.
- A **high message rate** indicates that the message broker is receiving a **large volume of data** from the Publisher.
- This behavior results in the **pattern shown in the chart**, reflecting the increased activity.

This demonstrates how message throughput is affected by the frequency of data publishing.