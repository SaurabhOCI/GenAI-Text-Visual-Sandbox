# Gen-AI Platform Setup for OCI (v3 clean)

This package creates:
- A **compartment**
- **Two IAM groups** (admins and users) – optional via `create_groups`
- **Two IAM policies** (admins and users) using valid OCI policy aggregates

**Note:** There is **no** `genai_service_policy` block anymore. We only grant access to resource families via groups.

## Deploy in ORM
Upload the ZIP in Resource Manager → Stacks → Create Stack → Upload. Configure variables, Plan, Apply.

## Valid policy examples (what this stack uses)
- Admins: `manage generative-ai-family`, AI Language/Document/Speech/Vision, Data Science, Object Storage, Logging, Monitoring
- Users: `use generative-ai-family`, limited Object Storage (regex `/genai-.*/` for object writes), read Logging/Monitoring

> Note: This stack uses **freeform tags** only. If you need defined tags, first create your tag namespace/keys and then add them in the TF code.
