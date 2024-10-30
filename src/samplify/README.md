# Samplify Library
***A Powerful and Flexible Sample Data Generator for Rust***
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Open-Payments/samplify-rs)

**samplify-rs** is a Rust library designed to simplify the process of generating sample data for testing, prototyping, and development purposes. Leveraging Rust’s powerful procedural macros and conditional compilation features, samplify-rs allows you to automatically generate realistic and customizable sample instances of your data structures without polluting your production code.

## Features

- **Automatic Derivation**: Use the Sampleable derive macro to automatically implement sample generation for your structs and enums.
- **Field-Level Customization**: Annotate your fields with attributes to specify value ranges, patterns, choices, lengths, and inclusion probabilities.
- **Support for Complex Structures**: Handle deeply nested and complex data structures with optional fields and variations effortlessly.
- **Conditional Compilation**: Enable or disable sample generation code using a feature flag, keeping your production builds clean and efficient.
- **Extensibility**: Easily integrate with existing projects and extend functionality without modifying original data structures.


## Key Benefits
- **Non-Intrusive**: Does not require modification of your production codebase; sample code is conditionally compiled.
- **Customizable Data Generation**: Fine-tune how sample data is generated for each field.
- **Improved Testing**: Quickly generate realistic test data to enhance your testing processes.
- **Lightweight**: Excludes sample generation code from production builds, ensuring optimal performance and binary size.
