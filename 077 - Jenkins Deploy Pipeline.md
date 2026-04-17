# Jenkins Deploy Pipeline

---

<aside>

**Purpose:** Configure a Jenkins SSH agent node on `stapp01` and run a **scripted pipeline** to clone the `web_app` repo from Gitea and deploy it to Apache at `/var/www/html`.

</aside>

---

### Procedure

#### Task 1: Prepare stapp01 (Java for Jenkins agent)

1. SSH into `stapp01`.
2. Install Java (version depends on the lab image; example shown):
    
    ```bash
    sudo dnf install -y java-21-openjdk
    ```
    

#### Task 2: Log into Jenkins

1. Open Jenkins and sign in:
    
    ```
    Username: admin
    Password: Adm!n321
    ```
    

#### Task 3: Log into Gitea and confirm repo details

1. Open Gitea and sign in:
    
    ```
    Username: sarah
    Password: Sarah_pass123
    ```
    
2. Confirm the repository exists:
    
    ```
    sarah / web_app
    ```
    
3. Copy the clone URL (example):
    
    ```
    http://gitea.stratos.xfusioncorp.com:3000/sarah/web_app.git
    ```
    

#### Task 4: Configure the Jenkins SSH agent node (App Server 1)

1. In Jenkins, go to:
    
    ```
    Manage Jenkins → Nodes → New Node
    ```
    
2. Create a permanent agent and set the following:
    
    ```
    Name: App Server 1
    Labels: stapp01
    Remote root directory: /home/sarah/jenkins_agent
    Launch method: Launch agents via SSH
    Host: stapp01
    Credentials: sarah / Sarah_pass123
    Host key verification: Non verifying Verification Strategy
    ```
    
3. Save and verify the node becomes **Online**.

#### Task 5: Fix sudo on stapp01 (required for deploy copy)

1. On `stapp01`, edit sudoers:
    
    ```bash
    sudo visudo
    ```
    
2. Add:
    
    ```
    sarah ALL=(ALL) NOPASSWD:ALL
    ```
    

#### Task 6: Create the Jenkins pipeline job

1. From the Jenkins dashboard, create a new item:
    
    ```
    New Item → nautilus-webapp-job → Pipeline → OK
    ```
    
2. In the job configuration, under **Pipeline**, set:
    
    ```
    Definition: Pipeline script
    ```
    

#### Task 7: Paste the scripted pipeline (working)

1. Paste the following:
    
    ```
    node('stapp01') {
    
        stage('Deploy') {
    
            dir('/home/sarah/jenkins_agent') {
    
                sh '''
                    rm -rf web_app
    
                    git clone http://gitea.stratos.xfusioncorp.com:3000/sarah/web_app.git
    
                    sudo cp -r web_app/* /var/www/html/
                '''
            }
        }
    }
    ```
    
2. Replace the Gitea URL with the exact clone URL from your lab if it differs.

#### Task 8: Run the build

1. Save the job.
2. Click:
    
    ```
    Build Now
    ```
    

---

### Quick check

- Confirm the agent node is online:
    
    ```
    Manage Jenkins → Nodes → App Server 1 → Online
    ```
    
- Expected console output (example):
    
    ```
    Cloning repository
    Copying files
    Finished: SUCCESS
    ```
    
- Verify the site via the Load Balancer URL:
    
    ```
    https://<LBR-URL>
    ```
    
- Expected:
    - Site loads directly
    - No `/web_app` path