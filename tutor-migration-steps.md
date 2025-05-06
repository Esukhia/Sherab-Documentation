
# Tutor Migration from Palm (v16.1.8) to Sumac (v19.0.2)

## 💠 Tutor Migration Overview

### ➡️ Migration Process:
1. Upgrade Tutor and its environment from v16.1.8 to v19.0.2
2. Migrate the Open edX codebase from Palm.4 to Sumac.2 (version-by-version)
3. Migrate the theme to be compatible with newer Django versions
4. Upgrade MFE (Micro Frontend) codebase to Sumac.2

---

## ✅ Detailed Migration Steps

### 1. Take Full Backup
- **Backup necessary components:**
  - MySQL
  - MongoDB (if used)
  - Redis (optional)
  - `$(tutor config printroot)/env`
  - `$(tutor config printroot)/data`
  - Custom plugins/themes
  - `.local/share/tutor` directory

**Command for MySQL backup:**
```bash
tutor local do mysql-backup
```

---

### 2. Disable Customizations Temporarily
- Disable custom themes and plugins to avoid conflicts during migration.
```bash
tutor config save --set CMS_THEME_NAME=dummy LMS_THEME_NAME=dummy
```
- Disable non-essential plugins:
```bash
tutor plugins disable <plugin_name>
```

---

### 3. Stop the Server
```bash
tutor local stop
```

---

### 4. Upgrade Tutor Version by Version
- **Incremental upgrade steps (Palm → Quince → Redwood → Sumac):**
1. Upgrade Tutor to the next version.
   ```bash
   pip install --upgrade "tutor==17.0.0"
   tutor config save
   tutor local quickstart
   tutor local launch
   ```
2. Test if the server works fine after each version upgrade (login, course access, etc.).

---

### 5. Upgrade Open edX Codebase
- Tutor automatically handles Open edX upgrades.
- If using a custom fork of `edx-platform`, update the fork's `open-release/<tag>`.
- Build a custom Docker image if needed:
```bash
tutor images build openedx
```

---

### 6. Migrate Custom Themes
- Replace deprecated template tags and static files.
- After upgrading to Sumac, re-enable the theme:
```bash
tutor config save --set LMS_THEME_NAME=mytheme CMS_THEME_NAME=mytheme
tutor images build openedx
```

---

### 7. Upgrade MFE (Micro Frontends)
- Pull and build updated MFEs:
  ```bash
  tutor local mfe build
  tutor local mfe launch
  ```
- Update MFE URLs in `config.yml` if using custom MFE hosting.

---

### 8. Rebuild Custom Docker Images
- Rebuild your custom Docker image after the upgrade:
```bash
tutor images build openedx
```

---

### 9. Re-enable Plugins and Packages
- Enable plugins one-by-one after each upgrade and verify their functionality:
```bash
tutor plugins enable <plugin_name>
```
- After each plugin enablement, run:
```bash
tutor local init
tutor local launch
```

---

### 10. Test Thoroughly
- Test essential functionalities:
  - Registration/login (SSO)
  - Course access
  - Studio course creation
  - MFE behavior
  - Mobile app API compatibility
- Monitor logs:
```bash
docker-compose logs -f
```

---

### 🧹 Optional: Clean Up
- Remove unused plugins:
```bash
tutor plugins disable <plugin>
```
- Remove old Docker images:
```bash
docker image prune
```

---

## 📚 Useful References
- **Tutor Changelog**: [GitHub Changelog](https://github.com/overhangio/tutor/blob/release/CHANGELOG.md)
- **Official Tutor Upgrade Docs**: [Tutor Install Guide](https://docs.tutor.edly.io/install.html#upgrading-to-a-new-open-edx-release)
- **Community Discussions**:
  - [Tutor Upgradation Discussion](https://discuss.openedx.org/t/tutor-upgradation/8360)
  - [Upgrading Tutor to Palm](https://discuss.openedx.org/t/upgrading-tutor-to-palm/10194/6)
  - [Open edX Upgrade Guide](https://discuss.openedx.org/t/how-to-update-open-edx-from-nutmeg-to-last-version/)
