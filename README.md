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