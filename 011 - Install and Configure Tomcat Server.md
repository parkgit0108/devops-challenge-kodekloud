# Install and Configure Tomcat Server

---

<aside>

**Purpose:** Install Apache Tomcat on the lab application server, configure it to run on the required port, deploy `ROOT.war`, and verify the web app is reachable.

</aside>

---

### Procedure

#### Task 1: SSH into the app server

1. SSH into the app server specified in the lab:
    
    ```bash
    ssh <user>@<app-server>
    ```
    

#### Task 2: Install Tomcat

1. Install Tomcat:
    
    ```bash
    sudo yum install tomcat -y
    ```
    

#### Task 3: Enable and start the Tomcat service

1. Enable Tomcat on boot:
    
    ```bash
    sudo systemctl enable tomcat
    ```
    
2. Start Tomcat:
    
    ```bash
    sudo systemctl start tomcat
    ```
    
3. Verify service status:
    
    ```bash
    sudo systemctl status tomcat
    ```
    

#### Task 4: Change Tomcat port (server.xml)

1. Edit the Tomcat `server.xml`:
    
    ```bash
    sudo vi /etc/tomcat/server.xml
    ```
    
2. By default, Tomcat runs on port **8080**. Update the connector port to match the lab requirement (example below uses **3003**):
    
    ```xml
    <Connector port="3003" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443"
               maxParameterCount="1000"
    ```
    

#### Task 5: Restart Tomcat

1. Restart the service:
    
    ```bash
    sudo systemctl restart tomcat
    ```
    

#### Task 6: Copy `ROOT.war` from jump host to app server

1. Copy `ROOT.war` from the jump host to the app server.
2. If required, generate an SSH key pair and authorize it on the app server to allow the file transfer.

#### Task 7: Deploy `ROOT.war`

1. Move `ROOT.war` into Tomcat’s `webapps` directory (Tomcat will auto-extract the WAR):
    
    ```bash
    sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/
    ```
    

#### Task 8: Verify the application

1. Verify the page responds on the configured port (example uses **3003**):
    
    ```bash
    curl http://stapp02:3003
    ```
    
2. Expected response should include HTML similar to:
    
    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <title>SampleWebApp</title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
        </head>
        <body>
            <h2>Welcome to xFusionCorp Industries!</h2>
            <br>
        
        </body>
    </html>
    ```
    

---

### Quick check

- **Expected result:** Tomcat is running on the lab-specified port, and `curl http://<app-server>:<port>` returns the SampleWebApp HTML.