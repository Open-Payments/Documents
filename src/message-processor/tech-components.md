## Technical Architecture and Components

The Message Processor’s architecture is designed for high scalability, reliability, and efficiency in processing large volumes of transactions. It integrates several key technical components that work together to manage inbound and outbound connections, handle data storage, and ensure smooth workflow execution. Here’s an overview of the core components:

![Technical architecture](../assets/technical-architecture.jpeg)

- **Integration System (Inbound/Outbound Connection)**: The integration layer connects the system with external messaging and event platforms such as **Kafka**, **Pulsar**, **Amazon SQS**, **Google Cloud Pub/Sub**, and **Azure Event Hub**. This layer manages the flow of messages in and out of the system, ensuring reliable communication with various endpoints.

- **Data Storage (MongoDB)**: MongoDB is used to store essential data, including **Workflow Metadata**, **Enrichment Data**, and **Transaction Data**. Workflow metadata defines the steps and logic for each workflow, enrichment data adds necessary context to each message, and transaction data records details of each processed message.

- **Cache Layer (Redis)**: Redis is employed as a caching layer to improve processing speed and handle temporary data. It is also used for **concurrency control**, ensuring that only one instance of the workflow processes a specific message at any time, avoiding duplication and race conditions.

- **Workflow Engine**: The core processing engine executes the workflows defined in the Workflow Metadata. It pulls data from MongoDB and utilizes Redis for concurrency locks, ensuring efficient, accurate, and sequential message processing according to defined rules.

This architecture ensures that messages are processed in a highly controlled and efficient manner, supporting large-scale and real-time transaction processing.

---

