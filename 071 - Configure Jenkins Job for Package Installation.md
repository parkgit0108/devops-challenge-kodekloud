Log in to jenkins with provided credentials.

Create a new jenkins job named as requested.

Add parameter PACKAGE

In the build steps, choose excute shell and enter below:

```sql
ssh natasha@ststor01 "sudo dnf makecache && sudo dnf install -y $PACKAGE"
```

ssh into jenkins server and create ssh key for storage server
```ssl
#in jenkins server
ssh-keygen -t rsa
ssh-copy-id natasha@ststor01
```
Back to Jenkins web page, Build with Parameters with "vim-enhanced"

Build should be successful

Check output console for any issues.

