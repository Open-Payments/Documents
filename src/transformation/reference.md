# API Reference

## Core Types

### Datamorph

Main entry point for transformations.

```rust
pub struct Datamorph {
    spec: TransformSpec,
}

impl Datamorph {
    /// Create a new instance from JSON specification
    pub fn from_json(spec: &str) -> Result<Self>

    /// Transform input data according to specification
    pub fn transform<T, U>(&self, input: T) -> Result<U>
    where
        T: Serialize,
        U: DeserializeOwned
}
```

### TransformSpec

Defines the transformation specification.

```rust
pub struct TransformSpec {
    pub mappings: HashMap<String, Mapping>,
}

impl TransformSpec {
    /// Parse from JSON string
    pub fn from_json(json: &str) -> Result<Self>

    /// Transform a value
    pub fn transform(&self, input: &Value) -> Result<Value>
}
```

### Error Types

```rust
pub enum Error {
    /// Failed to parse specification
    SpecParseError(String),

    /// Error during transformation
    TransformError(String),

    /// JSON serialization/deserialization error
    JsonError(serde_json::Error),

    /// Other errors
    Other(String),
}
```

## Specification Format

### Basic Specification
```json
{
    "mappings": {
        "sourceField": {
            "target": "targetField",
            "transform": "transformFunction"
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

### String Functions
| Function    | Description                 | Input Type | Output Type |
|-------------|----------------------------|------------|-------------|
| uppercase   | Convert to uppercase       | String     | String      |
| lowercase   | Convert to lowercase       | String     | String      |
| toString    | Convert value to string    | Any        | String      |

## Examples

### Basic Transform
```rust
use datamorph_rs::Datamorph;
use serde_json::json;

let spec = r#"{
    "mappings": {
        "name": {
            "target": "fullName",
            "transform": "uppercase"
        },
        "age": {
            "target": "userAge",
            "transform": "toString"
        }
    }
}"#;

let input = json!({
    "name": "john doe",
    "age": 30
});

let transformer = Datamorph::from_json(spec)?;
let result: serde_json::Value = transformer.transform(input)?;

assert_eq!(result["fullName"], "JOHN DOE");
assert_eq!(result["userAge"], "30");
```

### Error Handling
```rust
use datamorph_rs::{Datamorph, Error};

let spec = r#"{
    "mappings": {
        "age": {
            "target": "userAge",
            "transform": "invalidFunction"
        }
    }
}"#;

match Datamorph::from_json(spec) {
    Ok(transformer) => {
        let input = json!({ "age": 30 });
        match transformer.transform(input) {
            Ok(result) => println!("Success: {}", result),
            Err(e) => eprintln!("Transform error: {}", e),
        }
    },
    Err(e) => eprintln!("Spec parse error: {}", e),
}
```