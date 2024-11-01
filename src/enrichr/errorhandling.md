# Error Handling Guide

`enrichr-rs` provides detailed error handling to help you identify and fix issues quickly.

## Error Types

```rust
#[derive(Debug, Error)]
pub enum Error {
    #[error("Invalid enrichment spec: {0}")]
    InvalidSpec(#[from] serde_json::Error),
    
    #[error("Invalid JSON path: {0}")]
    InvalidPath(String),
    
    #[error("Path not found: {0}")]
    PathNotFound(String),
    
    #[error("Type conversion failed for field {field}: {details}")]
    TypeConversion { field: String, details: String },
    
    #[error("Unknown field: {0}")]
    UnknownField(String),
}
```

## Error Scenarios

### Invalid Spec
```rust
// Invalid JSON in spec
let spec = r#"{ invalid json }"#;
assert!(matches!(
    user.enrich(&data, spec),
    Err(Error::InvalidSpec(_))
));
```

### Path Not Found
```rust
let spec = r#"{
    "name": "$.user.nonexistent.field"
}"#;
assert!(matches!(
    user.enrich(&data, spec),
    Err(Error::PathNotFound(_))
));
```

### Type Conversion
```rust
// Trying to convert string to number
let spec = r#"{
    "age": "$.user.name"  // name is a string, age expects u32
}"#;
assert!(matches!(
    user.enrich(&data, spec),
    Err(Error::TypeConversion { .. })
));
```

## Error Handling Best Practices

1. **Granular Error Handling**
```rust
match user.enrich(&data, spec) {
    Ok(_) => println!("Enrichment successful"),
    Err(Error::PathNotFound(path)) => {
        println!("Missing data at path: {}", path);
        // Handle missing data gracefully
    },
    Err(Error::TypeConversion { field, details }) => {
        println!("Invalid type for field {}: {}", field, details);
        // Handle type mismatch
    },
    Err(e) => println!("Other error: {}", e),
}
```

2. **Validation Before Enrichment**
```rust
// Validate spec before processing
if let Err(e) = validate_spec(spec) {
    println!("Invalid spec: {}", e);
    return;
}
```

3. **Logging Integration**
```rust
use log::{error, warn, info};

match user.enrich(&data, spec) {
    Ok(_) => info!("Enrichment successful"),
    Err(e) => {
        error!("Enrichment failed: {}", e);
        // Additional error handling
    }
}
```