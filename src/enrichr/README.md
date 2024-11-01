# enrichr-rs 📦

A derive macro to enrich Rust structs using declarative transformation specs.

## Overview

`enrichr-rs` provides a simple yet powerful way to enrich Rust structs using JSON path mapping specifications. It enables declarative transformation of data from one structure to another through a derive macro, making it ideal for data enrichment, ETL processes, and API response handling.

## Key Features

- ✨ Derive macro for automatic implementation
- 🗺️ JSON path-based field mapping
- 🎯 Type-safe transformations
- ⚡ Zero-copy when possible
- 🛡️ Comprehensive error handling
- 📝 Clear validation messages

## Quick Start

Add to your `Cargo.toml`:
```toml
[dependencies]
enrichr = "0.1.0"
```

Basic usage:
```rust
use enrichr::Enrichable;
use serde::Deserialize;

#[derive(Enrichable, Default, Deserialize)]
struct User {
    name: String,
    age: u32,
}

fn main() -> Result<(), Error> {
    let data = HashMap::from([
        ("user_data", json!({
            "full_name": "John Doe",
            "details": { "age": 30 }
        }))
    ]);

    let spec = r#"{
        "name": "$.user_data.full_name",
        "age": "$.user_data.details.age"
    }"#;

    let mut user = User::default();
    user.enrich(&data, spec)?;
    
    assert_eq!(user.name, "John Doe");
    assert_eq!(user.age, 30);
    Ok(())
}
```

## Documentation

- [Usage Guide](./usage.md) - Detailed examples and use cases
- [Error Handling](./errorhandling.md) - Comprehensive error handling guide
