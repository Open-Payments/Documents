# Usage Guide

This guide covers various use cases and patterns for using `enrichr-rs`.

## Table of Contents
- [Basic Usage](#basic-usage)
- [Complex Mappings](#complex-mappings)
- [Type Conversions](#type-conversions)
- [Array Handling](#array-handling)
- [Optional Fields](#optional-fields)
- [Custom Types](#custom-types)

## Basic Usage

The simplest use case involves direct field mapping:

```rust
#[derive(Enrichable, Default)]
struct Person {
    name: String,
    age: u32,
}

let spec = r#"{
    "name": "$.person.name",
    "age": "$.person.age"
}"#;
```

## Complex Mappings

### Nested Objects

```rust
#[derive(Enrichable, Default)]
struct Employee {
    name: String,
    department: Department,
}

#[derive(Enrichable, Default)]
struct Department {
    id: String,
    name: String,
}

let spec = r#"{
    "name": "$.employee.personal.full_name",
    "department.id": "$.employee.dept.dept_id",
    "department.name": "$.employee.dept.dept_name"
}"#;
```

### Array Handling

```rust
#[derive(Enrichable, Default)]
struct Team {
    name: String,
    members: Vec<String>,
}

let spec = r#"{
    "name": "$.team.name",
    "members": "$.team.member_list[*].name"
}"#;
```

### Optional Fields

```rust
#[derive(Enrichable, Default)]
struct User {
    name: String,
    email: Option<String>,
}

let spec = r#"{
    "name": "$.user.name",
    "email": "$.user.contact.email"
}"#;
```

## Type Conversions

The library handles various type conversions automatically:

```rust
#[derive(Enrichable, Default)]
struct Metrics {
    count: u32,           // From number
    enabled: bool,        // From boolean
    ratio: f64,          // From number
    tags: Vec<String>,   // From array
}
```

## Custom Types

For custom types that implement `Deserialize`:

```rust
#[derive(Deserialize)]
enum Status {
    Active,
    Inactive,
}

#[derive(Enrichable, Default)]
struct Account {
    id: String,
    status: Status,
}
```