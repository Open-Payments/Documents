## Getting Started

### Prerequisites

You’ll need the following installed to build and use this library:

- [Rust](https://www.rust-lang.org/tools/install) (latest stable version)
- [Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html) (Rust package manager)

### Installation

Add the following to your `Cargo.toml` to start using the library in your Rust project:

```toml
[dependencies]
# This dependency includes support for the entire ISO 20022 message formats.
# The "payments" feature enables various ISO 20022 message categories, such as pacs, pain, camt, etc.
# If you only need specific message types, you can enable just those features (e.g., "pacs", "pain").
open-payments-iso20022 = { version = "1.0.1", features = ["payments"] }

# This dependency provides support for the FedNow message formats.
# You get full support for parsing and serializing FedNow messages out of the box.
open-payments-fednow = "1.0.1"
```

### Features

The ISO20022 message library `open-payments-iso20022` provides several features to allow you to include only the message types relevant to your use case. Here’s a breakdown of the available features:

```toml
[features]
default = ["head"]  # Default feature, includes the basic header message.
iso20022 = ["payments"]  # Enables all payment-related ISO 20022 messages.
payments = ["acmt", "admi", "auth", "camt", "head", "pacs", "pain", "reda", "remt"]  # Includes all payments-related ISO 20022 message types.

# Individual ISO 20022 message modules:
acmt = ["open-payments-iso20022-acmt"]  # Account Management messages
admi = ["open-payments-iso20022-admi"]  # Administrative messages
auth = ["open-payments-iso20022-auth"]  # Authorization messages
camt = ["open-payments-iso20022-camt"]  # Cash Management messages
head = ["open-payments-iso20022-head"]  # Basic Header messages (default)
pacs = ["open-payments-iso20022-pacs"]  # Payment Clearing and Settlement messages
pain = ["open-payments-iso20022-pain"]  # Payment Initiation messages
reda = ["open-payments-iso20022-reda"]  # Reference Data messages
remt = ["open-payments-iso20022-remt"]  # Remittance Advice messages
```

By configuring the features, you can optimize the library for your specific message requirements, minimizing unnecessary dependencies.
