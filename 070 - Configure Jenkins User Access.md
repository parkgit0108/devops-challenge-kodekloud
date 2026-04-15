# Configure Jenkins User Access

## Goal

Set up a Jenkins user and restrict access so the user can **only view** a single job (project) using **Project-based Matrix Authorization Strategy**.

## Prerequisites

- Jenkins admin access
- Jenkins is restarted after plugin installation

---

## 1) Create the user

1. Go to **Manage Jenkins → Users → Create User**
2. Set:
    - **Username**
    - **Full name**
    - **Password**
3. Click **Create User**

---

## 2) Install the Matrix Authorization plugin

1. Go to **Manage Jenkins → Plugins → Available plugins**
2. Search for: **Matrix Authorization Strategy**
3. Install the plugin
4. Restart Jenkins

---

## 3) Enable *Project-based Matrix Authorization Strategy* globally

1. Go to **Manage Jenkins → Security**
2. Under **Authorization**, select:
    - **Project-based Matrix Authorization Strategy**
3. Add/update permissions as needed
4. Click **Save** (and **Apply** if shown)

```sql
You must grant the minimum global permissions required for users to log in and navigate. Typically this includes Overall → Read (and sometimes Overall → View depending on Jenkins version/plugins).
```

You must grant the minimum global permissions required for users to log in and navigate.
Typically this includes **Overall → Read** 
and sometimes **Overall → View** depending on Jenkins version/plugins.

</aside>

---

## 4) Restrict a specific job to read-only for a user

1. Go to **Dashboard → HelloWorld → Configure**
2. Enable:
    - **Project-based security**
3. Add user:
    - `mark`
4. Grant **read-only** permissions (minimum):
    - **Job → Read**
    - *(Optional)* **Job → Discover** (helps visibility in UI)
5. Click **Save** (and **Apply** if shown)

---

## Quick verification

- Log in as `mark`
- Confirm `mark` can:
    - Open the **HelloWorld** job page
    - View build history and console output
- Confirm `mark` cannot:
    - Configure the job
    - Trigger builds (unless explicitly allowed)
    - Access other jobs (unless globally permitted)
