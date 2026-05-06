# Jenkins Multistage Pipeline

### Complete Step-by-Step Guide

### Step 1: Update index.html in Gitea

SSH into App Server 1:

```sql
ssh sarah@stapp01
# password: Sarah_pass123

cd /var/www/html
echo "Welcome to xFusionCorp Industries" > index.html
git add index.html
git commit -m "Update index.html"
git push origin master
exit
```

---

### Step 2: Install Java 17 on stapp01

```sql
ssh sarah@stapp01

sudo yum install -y java-17-openjdk
# password when prompted: Sarah_pass123

java -version
# should show openjdk 17
exit
```

---

### Step 3: Create Jenkins Agent Directory on stapp01

```sql
ssh sarah@stapp01

mkdir -p /home/sarah/jenkins_agent
exit
```

---

### Step 4: Add Credentials in Jenkins UI

1. Go to **Manage Jenkins → Credentials → System → Global credentials → Add Credentials**
2. Fill in:
```sql
Kind:        Username with password
Scope:       Global
Username:    sarah
Password:    Sarah_pass123
ID:          stapp01
Description: Sarah on stapp01

```

1. Click **Save**

---

### Step 5: Add stapp01 as Jenkins Agent

1. Go to **Manage Jenkins → Nodes → New Node**
2. Fill in:
```sql
Node name:   App Server 1
Type:        Permanent Agent
```

1. Click **Create**, then configure:

```sql
Description:            App Server 1
Executors:              2
Remote root directory:  /home/sarah/jenkins_agent
Labels:                 stapp01
Usage:                  Use this node as much as possible
Launch method:          Launch agents via SSH
Host:                   stapp01
Credentials:            sarah (stapp01)
Host Key Verification:  Non verifying Verification Strategy
````

1. Click **Save**

---

### Step 6: Verify Agent is Online

1. Go to **Manage Jenkins → Nodes → App Server 1**
2. Click **Launch agent**
3. Check the log — you should see:

`Agent successfully connected and online`

---

### Step 7: Create the Pipeline Job

1. Go to **Jenkins → New Item**
2. Fill in:

`Name:  deploy-job

Type:  Pipeline  ← (NOT Multibranch Pipeline)`

1. Click **OK**
2. Scroll down to **Pipeline** section
3. Paste this script:

groovy

```sql
pipeline {
    agent { label 'stapp01' }
    stages {
        stage('Deploy') {
            steps {
                sh '''
                    cd /var/www/html
                    git pull origin master
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    curl -f http://stlb01:8091
                '''
            }
        }
    }
}
```

1. Click **Save**

---

### Step 8: Run the Pipeline

1. Click **Build Now**
2. Click on the build number → **Console Output**
3. You should see:

```sql
Cloning/pulling from master...
Deploy complete
curl http://stlb01:8091
Welcome to xFusionCorp Industries
Finished: SUCCESS
```

---

### Step 9: Verify in Browser

Click the **App** button or visit `http://stlb01:8091`

You should see:

`Welcome to xFusionCorp Industries`
