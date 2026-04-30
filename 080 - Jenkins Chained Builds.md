# Jenkins Chained Builds

### Prerequisites

- Jenkins plugin **"Publish Over SSH"** installed
- SSH Server `stapp01` configured in **Manage Jenkins → Configure System → Publish over SSH** with:
    - **Hostname:** `stapp01`
    - **Username:** `tony`
    - **Password:** `Ir0nM@n`
    - **Remote Directory:** `/`

---

### Job 1: `datacenter-app-deployment`

**New Item → Freestyle project → name: `datacenter-app-deployment`**

### Source Code Management

| Field | Value |
| --- | --- |
| Git Repository URL | `http://sarah:Sarah_pass123@gitea:3000/sarah/web.git` |
| Branch | `*/master` |

### Build Steps → Send files or execute commands over SSH

| Field | Value |
| --- | --- |
| SSH Server Name | `stapp01` |
| Source files | *(empty)* |
| Remove prefix | *(empty)* |
| Remote directory | *(empty)* |
| **Exec command** | `cd /var/www/html && sudo git --git-dir=/var/www/html/.git --work-tree=/var/www/html fetch --all && sudo git --git-dir=/var/www/html/.git --work-tree=/var/www/html reset --hard origin/master` |

### Post-build Actions → Build other projects

| Field | Value |
| --- | --- |
| Projects to build | `manage-services` |
| Condition |  **Trigger only if build is stable** |

**Save.**

---

### Job 2: `manage-services`

**New Item → Freestyle project → name: `manage-services`**

### Build Triggers

| Field | Value |
| --- | --- |
| Build after other projects are built |  checked |
| Projects to watch | `datacenter-app-deployment` |
| Condition |  **Trigger only if build is stable** |

### Build Steps → Send files or execute commands over SSH

| Field | Value |
| --- | --- |
| SSH Server Name | `stapp01` |
| Source files | *(empty)* |
| Remove prefix | *(empty)* |
| Remote directory | *(empty)* |
| **Exec command** | `sudo systemctl restart httpd` |

**Save.**

---

### Verify

1. Click **Build Now** on `datacenter-app-deployment`
2. Both jobs go **green** 
3. `manage-services` auto-triggers after deployment