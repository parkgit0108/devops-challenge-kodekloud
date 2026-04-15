```sql
ssh into jenkins server
ssh root@jenkins
password: <in lab>
```
link for installing Jenkins - https://www.jenkins.io/doc/book/installing/linux/#fedora-stable
```sql
#update
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
```
```sql
#run below to install jenkins
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
```
```sql
sudo systemctl enable jenkins
service jenkins start
```
login to Jenkins UI and follow instructions.
initial admin pass can be found 
```sql
cat /var/lib/jenkins/secrets/initialAdminPassword
```
