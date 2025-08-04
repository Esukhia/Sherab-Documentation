# Partner-Organization Mapping Guide

This document describes how to add and manage mappings between **Partners** and **Organizations** using the `PartnerOrganizationMapping` model. These mappings are used to define which organizations are linked to which partners and whether they should be shown in the **mobile app** UI for filtering the courses.

---

## 🧱 Model Overview

The `PartnerOrganizationMapping` model links a `Partner` with an `Organization`, with optional fields to control how they appear in the mobile app:

| Field                | Description                                                           |
| -------------------- | --------------------------------------------------------------------- |
| `partner`            | Foreign key reference to the Partner.                                 |
| `organization`       | Foreign key reference to the Organization.                            |
| `show_in_mobile_app` | Boolean flag to include/exclude this mapping from the mobile app API. |
| `display_name`       | (Optional) Custom name shown for this partner in the UI/mobile app.   |

The combination of `partner` and `organization` must be unique.

---

## ✅ Steps to Add a Mapping

You can add a partner-organization mapping via the Django admin panel.

### 1. Open the Django Admin

Navigate to your Django admin panel (typically at `/admin/`).

---

### 2. Go to **Partner-Organization Mappings**

Under the app `Course Partnerships`, click on **Partner-Organization Mappings**.

---

### 3. Click "Add Partner-Organization Mapping"

You’ll be presented with a form with the following fields:

* **Partner**: Select an existing Partner.
* **Organization**: Select the Organization to link with the partner.
* **Show in mobile app**: Check this if the mapping should be visible in the mobile app.
* **Display name** *(optional)*: Set a custom name to be shown in the mobile app UI. If left blank, the partner's default name is used.

---

### 4. Save the Mapping

Click **Save**. If the combination of Partner and Organization already exists, you will get a validation error due to the unique constraint.

---

## 🔍 Admin Features

In the admin list view, you can:

* See columns: `Partner`, `Organization`, `Display Name`, and `Show in mobile app`.
* Filter by: `Partner`, `Organization`, `Show in mobile app`.
* Search by:

  * Partner name
  * Organization name
  * Organization short name
  * Display name

---

## 📱 Mobile App Integration

Only mappings where `show_in_mobile_app=True` will be exposed to the mobile app via the following API:

```
GET /api/partners/
```

### Sample Response:

```json
[
  {
    "partner_name": "Name of the partner",
    "logo": "https://yourdomain.com/.../partner_logo.png",
    "organization": "organization_short_name"
  },
  ...
]
```

* `partner_name`: Uses `display_name` if provided, else falls back to the partner's default name.
* `logo`: Fully qualified URL to the partner's logo.
* `organization`: The `short_name` of the organization.

---
