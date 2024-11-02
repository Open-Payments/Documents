# datamorph-rs
A powerful Rust library for transforming data structures using declarative specifications. Built for performance, type safety, and extensibility.

## Overview

`datamorph-rs` allows you to transform data structures using simple JSON-based specifications. It's designed to be easy to use while remaining flexible and extensible.

## Features

- 🚀 Simple, declarative JSON transformation specifications
- 🔧 Built-in transformation functions
- 🎯 Type-safe transformations
- 🔄 Support for multiple transformations
- ⚡ Zero-copy where possible
- 📝 Clear error messages

## Quick Start

Add to your `Cargo.toml`:
```toml
[dependencies]
datamorph-rs = "0.1.0"
```

Basic example:
```rust
use datamorph_rs::Datamorph;
use serde_json::json;

// Define your transformation spec
let spec = r#"{
    "mappings": {
        "name": {
            "target": "fullName",
            "transform": "uppercase"
        }
    }
}"#;

// Create transformer
let transformer = Datamorph::from_json(spec)?;

// Transform data
let input = json!({ "name": "john doe" });
let result: serde_json::Value = transformer.transform(input)?;

assert_eq!(result["fullName"], "JOHN DOE");
```

## Documentation

- [Usage Guide](usage.md) - Detailed usage instructions
- [API Reference](reference.md) - Complete API documentation
