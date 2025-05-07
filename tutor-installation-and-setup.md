# 💻 Local Tutor Installation and Customization Guide

This guide explains how to install Tutor locally, use a custom Open edX platform (`edx-platform`), apply a custom theme (`sherab`), and add a configuration plugin with custom settings.

---

## ✅ 1. Install Tutor Locally

Use the [tutor-installation-and-upgrade guide](https://github.com/Esukhia/Sherab-Documentation/blob/main/tutor_install_and_upgrade_guide.md) to install tutor locally and connect the database.

---

## 🚀 2. Check tutor version
Make sure you are on the latest or the required tutor version 
(current tutor version : **19.0.2** Sumac)

---

## 🎨 3. Install Custom [Sherab Theme](https://github.com/Esukhia/Sherab-theme)

Navigate to the Open edX themes directory:

```bash
cd "$(tutor config printroot)/env/build/openedx/themes"
```

Clone the custom Sherab theme:

```bash
git clone https://github.com/Esukhia/Sherab-theme.git 
```

---

## 🛠 4. Use Custom [edx-platform](https://github.com/Esukhia/edx-platform) (Sherab Version)

### a. Clone the Custom Platform

Navigate to the Tutor root directory:

```bash
cd "$(tutor config printroot)"
```

Clone the Sherab platform:

```bash
git clone --depth=1 -b sherab-dev https://github.com/Esukhia/edx-platform.git
```

### b. Mount the Platform

```bash
tutor mounts add ./edx-platform
```

---

## 🔁 5. Relaunch Tutor with Custom Platform

```bash
tutor dev launch
```

This will now use your custom `edx-platform` and theme.

---

## ⚙️ 6. Add Configuration Plugins

### a. Create Plugin Directory

```bash
mkdir -p tutor-plugins/configuration_plugin
cd tutor-plugins/configuration_plugin
```

### b. Create `plugin.yml`

```yaml
name: configuration_plugin
version: 0.0.1

patches:
  openedx-lms-development-settings: |
    FEATURES['CUSTOM_COURSES_EDX'] = True
    FEATURES['ENABLE_CHANGE_USER_PASSWORD_ADMIN'] = True
    FEATURES['ENABLE_SPECIAL_EXAMS'] = True
    FEATURES['MILESTONES_APP'] = True
    FEATURES['ENABLE_PREREQUISITE_COURSES'] = True
    FEATURES['ENABLE_DISCUSSION_HOME_PANEL'] = True
    FEATURES['ENABLE_DISCUSSION_EMAIL_DIGEST'] = True
    FEATURES['ENABLE_ACCOUNT_DELETION'] = False
    FEATURES['CUSTOM_CERTIFICATE_TEMPLATES_ENABLED'] = True
    FEATURES['SHOW_HEADER_LANGUAGE_SELECTOR'] = True
    FEATURES['SHOW_FOOTER_LANGUAGE_SELECTOR'] = False
    FEATURES['ORGANIZATIONS_APP'] = True
    FEATURES['ENABLE_COURSE_DISCOVERY'] = True
    FEATURES['ALWAYS_REDIRECT_HOMEPAGE_TO_DASHBOARD_FOR_AUTHENTICATED_USER'] = False
    DEFAULT_FROM_EMAIL = "contact@sherab.org"
    CONTACT_EMAIL = "contact@sherab.org"
    DEFAULT_FEEDBACK_EMAIL = "contact@sherab.org"
    TECH_SUPPORT_EMAIL = "contact@sherab.org"
    COMMUNITY_FORUM_URL = "https://community.sherab.org/"
    SEARCH_SKIP_ENROLLMENT_START_DATE_FILTERING = True
    LANGUAGES += [('bo', 'བོད་སྐད།')]
```

### c. Create `mount_python_package.py`

```python
from tutor import hooks

hooks.Filters.MOUNTED_DIRECTORIES.add_item(
    ("openedx", "sherab-custom-plugin")  # Adjust path as needed
)
```

---

## 🧩 7. Clone Your [Custom Django App](https://github.com/Esukhia/sherab-custom-plugin)

Clone your custom plugin (e.g., wishlist):

```bash
cd "$(tutor config printroot)"
git clone https://github.com/Esukhia/sherab-custom-plugin.git
```

---

## 📦 8. Mount the Custom App

```bash
tutor mounts add ./sherab-custom-plugin
```

> Adjust path if different.

---

## 🔍 9. Verify Mounts

```bash
tutor mounts list
```

---

## ✅ 10. Enable the Plugin

```bash
tutor plugins enable plugin_name
```

Please make sure to enable other plugins as needed.

---
## 🏗 11. Rebuild Docker Image

```bash
tutor images build openedx --no-cache
```
> This may take time on the first run.

After this, run 
```bash
tutor dev stop
tutor dev start -d
```
to reflect the changes.

---
## ✅ 12. Check if the plugin is installed in the lms container

a. Get the lms container id

```bash
docker ps 
```
b. Enter the container
```bash
docker exec -it container_id bash
```
c. Check if the sherab-custom-plugin is installed
```bash
pip list | grep sherab
```
If it’s not installed, you can install it by running:
```bash
pip install -e /mnt/sherab-custom-plugin
```
if getting error, check if the app is mounted in the /mnt dir
```bash
cd ../../mnt && ls
```

exit the container after that and restart tutor with 
```bash
tutor dev restart
```
---

You're now ready to run your custom Open edX instance with the Sherab theme and custom plugins.
