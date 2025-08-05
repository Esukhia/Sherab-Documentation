# LMS Feature Flags

### `FEATURES['CUSTOM_COURSES_EDX'] = True`
Enables Custom Courses for edX (CCX), allowing instructors to create custom versions (sections) of a course for specific learners or groups.

### `FEATURES['ENABLE_CHANGE_USER_PASSWORD_ADMIN'] = True`
Allows admin users to change other users' passwords through the Django admin interface.

### `FEATURES['ENABLE_SPECIAL_EXAMS'] = True`
Enables support for special/proctored exams in courses, typically with integrations for secure/timed assessments.

### `FEATURES['MILESTONES_APP'] = True`
Allows defining course requirements (“milestones”) that learners must complete before progressing (e.g., prerequisites).

### `FEATURES['ENABLE_PREREQUISITE_COURSES'] = True`
Enables prerequisite course functionality — learners must complete one course before enrolling in another.

### `FEATURES['ENABLE_DISCUSSION_HOME_PANEL'] = True`
Activates a panel on the discussions home page for announcements or pinned posts.

### `FEATURES['ENABLE_DISCUSSION_EMAIL_DIGEST'] = True`
Sends periodic email summaries of discussion activity to course participants.

### `FEATURES['ENABLE_ACCOUNT_DELETION'] = False`
Disables the option for users to delete their own accounts via the frontend.

### `FEATURES['CUSTOM_CERTIFICATE_TEMPLATES_ENABLED'] = True`
Allows using custom-designed certificate templates for course completion certificates.

### `FEATURES['SHOW_HEADER_LANGUAGE_SELECTOR'] = True`
Displays a language selector in the website header, enabling users to change the UI language.

### `FEATURES['SHOW_FOOTER_LANGUAGE_SELECTOR'] = False`
Hides the language selector in the website footer.

### `FEATURES['ORGANIZATIONS_APP'] = True`
Enables the Organizations app to group users and courses under organizational units.

### `FEATURES['ENABLE_COURSE_DISCOVERY'] = True`
Allows unauthenticated users to browse/search course offerings through the discovery page.

### `FEATURES['ALWAYS_REDIRECT_HOMEPAGE_TO_DASHBOARD_FOR_AUTHENTICATED_USER'] = False`
If False, logged-in users can access the homepage instead of always being redirected to their dashboard.

### `FEATURES['ENABLE_COMBINED_LOGIN_REGISTRATION'] = True`
Provides a unified screen for both login and registration, streamlining the authentication flow.

### `FEATURES['ENABLE_THIRD_PARTY_AUTH'] = True`
Enables support for third-party authentication providers (Google, Facebook, Apple, SSO, etc.).

### `FEATURES['ENABLE_EXTENDED_COURSE_DETAILS'] = True`
Setting this flag to True unlocks more granular course information across Open edX, benefiting both learners (with richer course views) and administrators/integrators (with more structured course data available for various use cases).
---

# CMS (Studio) Feature Flags

### `FEATURES['ENABLE_SPECIAL_EXAMS'] = True`
Allows course staff to configure special/proctored exams within Studio.

### `FEATURES['MILESTONES_APP'] = True`
Lets authors define learning milestones within the course structure.

### `FEATURES['ENABLE_PREREQUISITE_COURSES'] = True`
Enables prerequisite logic so that access to a course depends on completion of another course.

### `FEATURES['ALLOW_PUBLIC_ACCOUNT_CREATION'] = False`
Disables public creation of Studio accounts. Only admins can create Studio user accounts.
