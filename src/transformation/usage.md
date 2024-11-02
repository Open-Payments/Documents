# Usage Guide

This guide provides detailed instructions for using datamorph-rs in your projects.

## Table of Contents

1. [Installation](#installation)
2. [Basic Usage](#basic-usage)
3. [Transformation Specifications](#transformation-specifications)
4. [Built-in Functions](#built-in-functions)
5. [Error Handling](#error-handling)
6. [Best Practices](#best-practices)

## Installation

Add datamorph-rs to your project:
```toml
[dependencies]
datamorph-rs = "0.1.0"
```

## Basic Usage

### Simple Field Transformation
```rust
use datamorph_rs::Datamorph;
use serde_json::json;

let spec = r#"{
    "mappings": {
        "name": {
            "target": "fullName",
            "transform": "uppercase"
        }
    }
}"#;

let input = json!({
    "name": "john doe"
});

let transformer = Datamorph::from_json(spec)?;
let result: serde_json::Value = transformer.transform(input)?;
```

### Multiple Transformations
```rust
let spec = r#"{
    "mappings": {
        "description": {
            "target": "summary",
            "transform": ["trim", "uppercase"]
        }
    }
}"#;
```

## Transformation Specifications

### Basic Structure
```json
{
    "mappings": {
        "sourceField": {
            "target": "targetField",
            "transform": "transformationFunction"
        }
    }
}
```

### Multiple Transformations
```json
{
    "mappings": {
        "sourceField": {
            "target": "targetField",
            "transform": ["function1", "function2"]
        }
    }
}
```

## Built-in Functions

### String Transformations
- `uppercase`: Convert string to uppercase
- `lowercase`: Convert string to lowercase
- `toString`: Convert value to string

### Examples
```json
{
    "mappings": {
        "name": {
            "target": "upperName",
            "transform": "uppercase"
        },
        "age": {
            "target": "ageString",
            "transform": "toString"
        }
    }
}
```

## Error Handling

```rust
use datamorph_rs::{Datamorph, Error};

match Datamorph::from_json(spec) {
    Ok(transformer) => {
        match transformer.transform(input) {
            Ok(result) => println!("Success: {}", result),
            Err(Error::TransformError(msg)) => eprintln!("Transform failed: {}", msg),
            Err(e) => eprintln!("Other error: {}", e),
        }
    },
    Err(e) => eprintln!("Failed to parse spec: {}", e),
}
```

## Best Practices

1. **Specification Organization**
   - Keep specifications simple and focused
   - Use meaningful field names
   - Document complex transformations

2. **Error Handling**
   - Always handle potential errors
   - Validate specifications before use
   - Log transformation errors

3. **Performance**
   - Minimize number of transformations
   - Use appropriate data types
   - Consider batch processing for large datasets