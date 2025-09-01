---
icon: code
description: Complete API specification and reference documentation
---

# Swagger Specification

The complete Kick API specification is available in OpenAPI/Swagger format, providing comprehensive documentation for all available endpoints, request/response schemas, and authentication requirements.

## Swagger JSON Endpoint

**URL**: `https://api.kick.com/swagger/v1/doc.json`

This endpoint provides the complete API schema including:

- All available endpoints and HTTP methods
- Detailed request and response schemas
- Authentication and authorization requirements
- Parameter specifications and validation rules
- Error response formats

## Using the Swagger Specification

You can use this URL with any OpenAPI-compatible tool to explore and test the API interactively:

### Interactive Documentation

**KICK provides an interactive API explorer** powered by Scalar that allows you to test endpoints directly in your browser. This interface enables you to authenticate and make real API calls without additional setup. You can also visit [Scalar API client](https://client.scalar.com/?url=https%3A%2F%2Fapi.kick.com%2Fswagger%2Fv1%2Fdoc.json) directly.

**Important**: When testing OAuth 2.1 endpoints (authorize, token, revoke), you'll need to change the base URL from `https://api.kick.com/public/v1` to `https://id.kick.com` in your testing tool.

### Popular Tools

- **Swagger UI**: Paste the URL into [swagger.io/tools/swagger-ui](https://swagger.io/tools/swagger-ui/) for interactive documentation
- **Postman**: Import the OpenAPI specification to automatically generate API collections
- **Insomnia**: Import the specification for API testing and exploration
- **OpenAPI Generator**: Generate client SDKs in various programming languages

**Note**: Generated clients will automatically point to `https://api.kick.com/public/v1` for API calls. OAuth 2.1 endpoints use a different base URL (`https://id.kick.com`).

### Example Usage

```bash
# Fetch the complete API specification
curl -L -o swagger.json https://api.kick.com/swagger/v1/doc.json

# Use with Swagger UI (replace with your local Swagger UI instance)
https://petstore.swagger.io/?url=https://api.kick.com/swagger/v1/doc.json
```

## API Information

Based on the current specification:

- **Version**: 1.0.0
- **Base URL**: `https://api.kick.com/public/v1`
- **OAuth 2.1 Base URL**: `https://id.kick.com`
- **Protocol**: HTTPS only
- **Authentication**: Bearer token (OAuth 2.1)
