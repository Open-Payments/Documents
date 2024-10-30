# Message Processor

The Message Processor is the core engine of the Open Payments platform, serving as the central nervous system that orchestrates payment transactions seamlessly from initiation to completion. It streamlines the flow of financial messages through a robust, security-first architecture. Each message passing through the system is:

- **Enriched**: Adds necessary information such as customer verification data and compliance checks, including OFAC screening and AML validations
- **Validated**: Confirms accuracy and compliance with regulatory and business rules, including Regulation guidelines
- **Transformed**: Adjusts message formats to meet internal or external standards, supporting ISO 20022, SWIFT, and proprietary formats
- **Routed**: Directs messages to appropriate systems or networks based on configurable workflows

By efficiently handling inbound messages, applying necessary transformations, and directing them to designated outbound channels, the Message Processor enables seamless integration with a bank's existing systems. Its support for complex, multi-step workflows allows it to adapt to diverse payment formats and regulatory requirements, enhancing interoperability and operational efficiency.

## Use Case #1: FedNow Customer Credit Transfer Flow
In this use case, the Message Processor manages a real-time FedNow Customer Credit Transfer, overseeing each stage from initiation by the sender's bank to final settlement at the clearing house.

- **Initiation**: The sender's bank initiates a credit transfer request formatted according to FedNow specifications. This message is sent to the Message Processor's inbound channel.
- **Enrichment**: Upon receiving the message, the Message Processor enriches it by verifying customer details, checking the availability of funds, and applying regulatory compliance checks through configured enrichment connectors.
- **Workflow Processing**: The message is processed based on predefined rules within the workflow configuration. The Message Processor validates the message format and applies any necessary transformations to align with internal standards.
- **Clearing and Settlement**: After processing, the Message Processor routes the message through the outbound connection to the clearing house for final settlement.
- **Response Handling**: The processor manages acknowledgments and response messages from the clearing house back to the sender's bank, ensuring end-to-end transaction visibility and confirmation.

## Use Case #2: Real-time Payment Processor Integration
In this scenario, the Message Processor functions as an embedded component within a financial institution's internal payment system, managing transactions in real-time before they reach the core banking system.

- **Transaction Intake**: Incoming payment requests from various channels (e.g., mobile apps, web portals) are received by the processor with guaranteed message delivery and deduplication.
- **Initial Screening and Enrichment**: The Message Processor performs initial validations and enrichment, such as Know Your Customer (KYC) checks, anti-fraud assessments, and data standardization.
- **Processing**: Based on preconfigured workflows, the Message Processor validates the message format, applies business rules, and prepares it for core processing. This may include formatting transformations to meet internal standards.
- **Routing to Core System**: Once validated and transformed, the message is routed to the core banking system for final processing and settlement, with built-in failover and retry mechanisms.

## Expanding Capabilities
The Message Processor extends beyond traditional payment processing to serve as a comprehensive solution for message orchestration across financial systems. Its flexible architecture adapts to evolving industry needs, supporting emerging payment methods, real-time settlement networks, and regulatory requirements.