# Untitled

<aside>
<img src="https://www.notion.soi" alt="https://www.notion.soi" width="40px" />

**Goal:** Add 3 Jenkins SSH build agents (stapp01/stapp02/stapp03) and ensure Java 17 is installed on each app server.

</aside>

## 1) Prep each app server (Java 17)

Run on **each** app server:

```bash
sudo yum install -y java-17-openjdk
```

## 2) Install the SSH Build Agents plugin (Jenkins)

In Jenkins:

- **Manage Jenkins → Plugins → Available plugins**
- Search: **SSH Build Agents**
- Install (restart if prompted)

## 3) Create credentials (Global)

In Jenkins:

- **Manage Jenkins → Credentials**
- Select: **(global) → Add Credentials**
- **Kind:** Username with password
- **Scope:** Global

Create **one credential per app server**:

### Credential: stapp01

- **Username:** `tony`
- **Password:** (lab password for `stapp01` user)
- **ID:** `stapp01-creds` (recommended)
- **Description:** `stapp01 SSH`

### Credential: stapp02

- **Username:** `steve`
- **Password:** (lab password for `stapp02` user)
- **ID:** `stapp02-creds`
- **Description:** `stapp02 SSH`

### Credential: stapp03

- **Username:** `banner`
- **Password:** (lab password for `stapp03` user)
- **ID:** `stapp03-creds`
- **Description:** `stapp03 SSH`

## 4) Add Jenkins nodes (agents) via SSH

Go to:

- **Manage Jenkins → Nodes → New Node**
- **Select:** Permanent Agent

Repeat the steps below for each server.

### Node: App_server_1 (stapp01)

**Basic settings**

- **Node name:** `App_server_1`
- **Number of executors:** `1`
- **Remote root directory:** `/home/tony/jenkins`
- **Labels:** `stapp01`
- **Usage:** Use this node as much as possible

**Launch method**

- **Launch agents via SSH**
    - **Host:** `stapp01`
    - **Credentials:** `stapp01-creds` (or the matching credential you created)
    - **Host Key Verification Strategy:** Non verifying Verification Strategy

Click **Save**.

### Node: App_server_2 (stapp02)

**Basic settings**

- **Node name:** `App_server_2`
- **Number of executors:** `1`
- **Remote root directory:** `/home/steve/jenkins`
- **Labels:** `stapp02`

**Launch method**

- **Launch agents via SSH**
    - **Host:** `stapp02`
    - **Credentials:** `stapp02-creds`
    - **Host Key Verification Strategy:** Non verifying Verification Strategy

Click **Save**.

### Node: App_server_3 (stapp03)

**Basic settings**

- **Node name:** `App_server_3`
- **Number of executors:** `1`
- **Remote root directory:** `/home/banner/jenkins`
- **Labels:** `stapp03`

**Launch method**

- **Launch agents via SSH**
    - **Host:** `stapp03`
    - **Credentials:** `stapp03-creds`
    - **Host Key Verification Strategy:** Non verifying Verification Strategy

Click **Save**.