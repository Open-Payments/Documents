# Usage

**Example: Creating an ISO 20022 Message Object**
```rust,noplayground
use open_payments_iso20022::document::Document;
use open_payments_iso20022_admi::admi_002_001_01::Admi00200101;

fn main() {
    let doc = Document::Admi00200101(Box::new(Admi00200101::default()));

    println!("{:?}", doc)
}
```

**Example: Creating a FedNow Message Object**

Similarly, here’s an example of how to create a FedNow message object:

```rust,noplayground
use open_payments_fednow::document::Document;
use open_payments_fednow::iso::pacs_008_001_08::FIToFICustomerCreditTransferV08;

fn main() {
    let doc = Document::FIToFICustomerCreditTransferV08(Box::new(FIToFICustomerCreditTransferV08::default()));

    println!("{:?}", doc)
}
```
