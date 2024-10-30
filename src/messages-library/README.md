# Messages Library
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Open-Payments/messages)

The library provides tools for parsing, validating, and transforming financial messages, with support for ISO 20022 and FedNow message formats. The library is designed to help developers integrate financial message handling into their Rust applications, using serde for (de)serialization.

---

## Features
- **ISO 20022 Support**: Comprehensive support for key ISO 20022 payment message types.
- **FedNow Message**: Full support for FedNow message formats.
- **(De)serialization**: Using serde for easy conversion between XML and JSON.
- **Extensibility**: Easily extendable to support additional message types or custom formats.

### Supported Messages
The library supports a variety of financial message formats from both ISO 20022 and FedNow, covering key areas of the payment lifecycle.

#### ISO 20022 Messages
- **pacs**: Payment Clearing and Settlement
- **pain**: Payment Initiation
- **admi**: Administrative messages
- **auth**: Authorization messages
- **camt**: Cash Management
- **reda**: Reference Data
- **remt**: Remittance Advice
- **acmt**: Account Management
- **head**: Header messages

#### FedNow Messages
- **Customer Credit Transfer**
- **Payment Status Report**
- **Payment Return**

---

This extensive support for ISO 20022 messages enables comprehensive coverage of the payment message lifecycle, including administrative processes, investigations, status reports, and transaction instructions.
