# 🛠️ Fixing Transifex Resource Names for Open edX

This guide explains how to fix or update resource names in Transifex using the `openedx-translations` scripts.

---

### 1. Clone the Repository

```
git clone https://github.com/Esukhia/openedx-translations.git
cd openedx-translations
```

---

### 2. Set Up a Virtual Environment

```
python3 -m venv venv
source venv/bin/activate
```

---

### 3. Install the Requirements

```
make translations_scripts_requirements
```

---

### 4. Update the Organization Slug in the Script

Edit the file: `scripts/fix_transifex_resource_names.py`

Locate the following line:

```
openedx_org = transifex_api.Organization.get(slug='open-edx')
```

Replace it with your actual organization slug. For example, if your organization slug is `sherab`, update it as follows:

```
openedx_org = transifex_api.Organization.get(slug='sherab')
```

---

### 5. Set Required Environment Variables

Before running the script, make sure to define the following environment variables in the `Makefile` located at the root of the `openedx-translations` repository:

```
export TRANSIFEX_PROJECT_SLUG=openedx-translations-sherab
export TRANSIFEX_API_TOKEN=your-api-token
```

`TRANSIFEX_PROJECT_SLUG`: Replace this with the slug of your actual Transifex project.
Example: `openedx-translations-sherab`

`TRANSIFEX_API_TOKEN`: Replace this with your personal API token from Transifex.

> 🔐 If you haven’t created your token yet, follow this guide:
> [Transifex API Token Generation](./transifex-token-generation.md)

---

### 6. Run a Dry Run (Preview)

Before applying any actual changes, it's strongly recommended to run a **dry run** to preview what updates will be made to the resource names:

```
make fix_transifex_resource_names_dry_run
```

This command simulates the renaming process without sending any updates to Transifex.
Carefully review the output to ensure that the expected changes are correct.

---

### 7. Apply the Changes

Once you've verified the output from the dry run and you're confident everything looks correct, go ahead and apply the changes:

```
make fix_transifex_resource_names
```

This command will perform the actual renaming of resources in your Transifex project based on the script logic

---

## 📌 Notes

- Make sure your Transifex API token has sufficient permissions.
- Always check the dry run output before applying actual changes.
- This process helps standardize and clean up resource names in your Transifex project.

---

◀️ [Previous: User Roles and Access in Transifex](./user-roles-access-for-transifex.md)

▶️ [Go Back: Transifex Setup and Management](../../transifex-setup-and-management.md)
