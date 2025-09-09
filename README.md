# Text Generation Stack (OCI) – Auto User + Groups

This stack provisions:
- (Optional) Compartment
- Two IAM Groups (GenAI Admin, GenAI User)
- A new **OCI IAM User** (with optional email)
- Policies for access (if defined in the stack)
- Ready to integrate with Gen-AI services

It uses the standard OCI provider (>= 7.13.0) and requires only your tenancy/region and a few names.

---

## 🚀 Deploy with One Click

Replace `<your-username>/<your-repo>` with your GitHub repo path. Use a **tag archive** (recommended) or `heads/main.zip`:

**Tag archive (recommended):**
```
https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/<your-username>/<your-repo>/archive/refs/tags/v1.0.0.zip
```

**Main branch archive:**
```
https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/<your-username>/<your-repo>/archive/refs/heads/main.zip
```

Markdown button you can drop into your repo README:
```md
[![Deploy to Oracle Cloud](https://oci-resourcemanager-plugin.plugins.oci.oraclecloud.com/latest/deploy-to-oracle-cloud.svg)](
  https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/<your-username>/<your-repo>/archive/refs/tags/v1.0.0.zip
)
```

> Tip: Open the `zipUrl` in an incognito window once; it must download a zip without login.

---

## 📦 What to commit

Extract your ZIP and commit the **files** directly at repo root (do not commit a zip):
```
providers.tf
variables.tf
groups.tf
policies.tf
compartment.tf
identity_user.tf
outputs.tf
outputs_user.tf
variables_user.tf
schema.yaml
README.md (optional)
```

---

## 🔧 Inputs (from variables.tf)

Required / common variables:

- `tenancy_ocid` *(string, required)* – Your tenancy OCID
- `region` *(string, required)* – Deployment region (e.g., `ap-mumbai-1`)
- `compartment_name` *(string)* – Name to create (if used)
- `compartment_description` *(string)*
- `create_groups` *(bool)* – Whether to create GenAI admin/user groups
- `genai_admin_group_name` *(string)*
- `genai_user_group_name` *(string)*
- `enable_tagging` *(bool)*, `project_tag` *(string)*, `common_freeform_tags` *(map)* (if you tag resources)
- `user_name` *(string, required)* – New IAM user login
- `user_description` *(string, default: "Auto-created by ORM stack")*
- `user_email` *(string, optional)*

---

## 🧩 Optional: Prefill values in the button

Append `zipUrlVariables=` with **URL-encoded JSON** (leave out `region` if you prefer to select it in Console):

Example JSON:
```json
{
  "create_groups": true,
  "genai_admin_group_name": "GenAI-Admins",
  "genai_user_group_name": "GenAI-Users",
  "user_name": "genai.stack.user",
  "user_email": "user@example.com",
  "user_description": "Created by Quick-Create"
}
```

URL-encoded param to append:
```
&zipUrlVariables=%7B%22create_groups%22%3Atrue%2C%22genai_admin_group_name%22%3A%22GenAI-Admins%22%2C%22genai_user_group_name%22%3A%22GenAI-Users%22%2C%22user_name%22%3A%22genai.stack.user%22%2C%22user_email%22%3A%22user%40example.com%22%2C%22user_description%22%3A%22Created%20by%20Quick-Create%22%7D
```

---

## ✅ Quick-Create checklist (avoid 400 errors)

- Repo is **public** (or host zip in **Object Storage PAR** and use that URL).
- Archive link is **tag or branch archive** (`.../archive/refs/...zip`), not a “blob” link.
- Terraform files exist at the **repo root** in the tag/branch you point to.

---

## 🧹 Clean up

In Resource Manager → your stack → **Jobs** → **Destroy**, then delete the stack.

---

## 🛠️ Git commands (if pushing locally)

```bash
# inside the folder with the files above
git init
git add .
git commit -m "Text Generation stack: user + groups"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main

# create a tag for a stable button link
git tag -a v1.0.0 -m "Initial release"
git push origin v1.0.0
```

Once the tag is pushed, your button works:
```
https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/<your-username>/<your-repo>/archive/refs/tags/v1.0.0.zip
```

---
