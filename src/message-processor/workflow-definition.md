# Workflow Definition Format Specification

## Overview
The Workflow Definition format specifies the structure and sequence of tasks required to process a message in the Open Payments system. Each workflow is event-driven, with tasks executing based on the message's processing state.

## Specification

### Workflow Structure
```json
{
  "id": "string",                    // Unique identifier for the workflow
  "name": "string",                  // Descriptive name
  "description": "string",           // Detailed description of workflow's purpose
  "version": "integer",              // Version number of the workflow definition
  "domain": "string",                // Domain this workflow belongs to
  "status": "string",                // Status: draft, active, or deprecated
  "tasks": [                         // Array of tasks in the workflow
    {
      "task_id": "string",           // Unique identifier for the task
      "name": "string",              // Descriptive name of the task
      "description": "string",        // Description of what the task does
      "trigger_condition": {          // Condition for task execution
        // Processing state conditions that trigger this task
      },
      "function": "string",          // Function type: Validate, Enrich, or Publish
      "input": {                     // Function-specific configuration
        // Configuration varies based on function type
      }
    }
  ]
}
```

### Functions

#### 1. Validate
Validates message data against defined business rules.
```json
{
  "function": "Validate",
  "input": {
    "ruleset": "string"             // Identifier of validation ruleset
  }
}
```

#### 2. Enrich
Enriches message with additional data.
```json
{
  "function": "Enrich",
  "input": {
    "source": {
      "type": "string",             // Type of data source
      "config": {                   // Source-specific configuration
        // Configuration properties
      }
    },
    "mapping": {
      "spec_id": "string"          // Identifier of mapping specification
    }
  }
}
```

#### 3. Publish
Publishes message to external system, with optional transformation.
```json
{
  "function": "Publish",
  "input": {
    "destination": {
      "type": "string",            // queue or topic
      "name": "string"             // Destination name
    },
    "transform": {                 // Optional transformation
      "schema": "string",          // Transform schema identifier
      "target_format": "string"    // Target format
    }
  }
}
```

### Example Implementation

```json
{
  "id": "FEDNOW_CREDIT_TRANSFER",
  "name": "FedNow Credit Transfer Processing",
  "description": "Processes FedNow credit transfer messages",
  "version": 1,
  "domain": "payments",
  "status": "active",
  "tasks": [
    {
      "task_id": "validate_payment",
      "name": "Validate Payment Data",
      "description": "Validates the incoming payment message",
      "trigger_condition": {
        "processing.status": "received"
      },
      "function": "Validate",
      "input": {
        "ruleset": "FEDNOW_CREDIT_TRANSFER_RULES"
      }
    },
    {
      "task_id": "enrich_customer_data",
      "name": "Enrich Customer Information",
      "description": "Enriches the message with customer data",
      "trigger_condition": {
        "processing.progress.prev_task": "validate_payment",
        "processing.progress.prev_status_code": "SUCCESS"
      },
      "function": "Enrich",
      "input": {
        "source": {
          "type": "customer_database",
          "config": {
            "lookup_type": "account"
          }
        },
        "mapping": {
          "spec_id": "CUSTOMER_DATA_MAPPING"
        }
      }
    },
    {
      "task_id": "send_to_fednow",
      "name": "Send to FedNow",
      "description": "Publishes the message to FedNow",
      "trigger_condition": {
        "processing.progress.prev_task": "enrich_customer_data",
        "processing.progress.prev_status_code": "SUCCESS"
      },
      "function": "Publish",
      "input": {
        "destination": {
          "type": "queue",
          "name": "FEDNOW_OUTBOUND"
        },
        "transform": {
          "schema": "FEDNOW_CREDIT_TRANSFER_MAPPING",
          "target_format": "ISO20022"
        }
      }
    }
  ]
}
```

## Key Concepts

### Event-Driven Execution
- Tasks execute based on message processing state
- Each task has a trigger condition
- Processing continues until no tasks are triggered

### Task Functions
- **Validate**: Applies business rules to message data
- **Enrich**: Adds additional data to the message
- **Publish**: Sends message to external system

### Message Processing
- Message state tracked in processing object
- Status codes determine task execution
- Previous task results influence next task

## Best Practices

1. **Task Naming**
   - Use clear, descriptive task IDs
   - Follow consistent naming convention
   - Include purpose in description

2. **Trigger Conditions**
   - Keep conditions simple and clear
   - Consider error scenarios
   - Handle all possible states

3. **Function Configuration**
   - Use meaningful identifiers
   - Configure appropriate error handling
   - Document external dependencies

4. **Workflow Organization**
   - Group related tasks logically
   - Maintain clear task progression
   - Consider maintenance and monitoring