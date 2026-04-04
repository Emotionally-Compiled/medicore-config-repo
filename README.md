# MediCore Centralized Configuration Repository

This repository contains the centralized configuration for the Emotionally Compiled Hospital System (MediCore). It serves as the configuration source for the Spring Cloud Config Server.

## How to Add New Configurations

### 1. Naming Conventions
Configuration files should follow the standard Spring Cloud Config naming pattern:
- `{application}.yml`: Default configuration for a service.
- `{application}-{profile}.yml`: Profile-specific configuration (e.g., `dev`, `prod`).
- `application.yml`: Shared configuration across all services.

Example: For a service named `patient-service` in the `dev` profile, create `patient-service-dev.yml`.

### 2. Adding a Configuration for a New Service
1. Identify the application name (defined in the service's `spring.application.name`).
2. Create a new YAML file in the root of this repository following the naming convention.
3. Add the necessary configuration properties.
4. Commit and push your changes to this repository. The Config Server will automatically detect the new file.

### 3. Modifying Existing Configuration
1. Locate the relevant `{application}.yml` or `{application}-{profile}.yml` file.
2. Apply your changes.
3. Commit and push.

### 4. Shared Configuration
Use `application.yml` or `application-{profile}.yml` for settings that should be applied to all services (e.g., Eureka registration, common security settings).

### 5. Managing Sensitive Information
**Do NOT commit sensitive information (passwords, API keys, etc.) directly to this repository.**

Sensitive data must be managed using environment variables. Reference them in your YAML files using the `${VARIABLE_NAME:DEFAULT_VALUE}` syntax.

Example:
```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: ${KEYCLOAK_ISSUER_URI}
```

Ensure the environment variables are correctly set in the environment where the services are running.
