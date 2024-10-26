# Usage
1. **Include the macro in your code**
```rust,noplayground
use samplify_rs::Sampleable;
```
2. **Annotate Your Data Structures**

Use `#[cfg_attr(feature = "sample", derive(Sampleable))]` on your structs and enums.

```rust,noplayground
#[derive(Debug, Serialize, Deserialize)]
#[cfg_attr(feature = "sample", derive(Sampleable))]
struct PaymentInstruction {
    currency: String,
    amount: f64,
}
```

## Example

```rust,noplayground
use samplify_rs::Sampleable;
use serde::{Deserialize, Serialize};
use serde_json;

#[derive(Debug, Serialize, Deserialize, Sampleable)]
struct PaymentInstruction {
    currency: String,
    amount: f64,
}

fn main() -> Result<(), String> {
    let config_json = r#"
    {
        "amount": [10.0, 1000.0],
        "currency": ["USD", "EUR", "GBP"]
    }
    "#;
    let config_map: serde_json::Map<String, serde_json::Value> = serde_json::from_str(config_json).map_err(|e| e.to_string())?;
    let sample_payment = PaymentInstruction::sample(&config_map)?;

    println!("{:?}", sample_payment);

    Ok(())
}
```