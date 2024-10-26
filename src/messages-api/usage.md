# Usage
## Request:

- **Method**: `POST`
- **Content-Type**: `application/xml`
- **Body**: The XML content of the payment message (e.g., pacs.008, pacs.002, etc.).

### Example Request:
```xml
<FIToFICstmrCdtTrf>
  <!-- Example XML content based on FedNow ISO20022 format -->
</FIToFICstmrCdtTrf>
```

---

## Response:

- **Content-Type**: `application/json`
- **Body**: The parsed payment message in JSON format, with details of the validation status.

### Example Successful Response:
```json
{
  "status": "success",
  "message": {
    "FIToFICstmrCdtTrf": {
      "GrpHdr": {
        "MsgId": "ABC123456",
        "CreDtTm": "2024-10-01T12:00:00Z"
      },
      ...
    }
  }
}
```

### Example Validation Error Response:
```json
{
  "status": "error",
  "errors": [
    {
      "field": "GrpHdr.MsgId",
      "message": "Message ID is missing or invalid"
    }
  ]
}
```

---
