# Git Merge Branches

---

<aside>

**Purpose:** Create a branch, add `index.html`, merge back into `master`.

</aside>

---

### Steps

ssh into storage server.

```bash
sudo su
cd /usr/src/kodekloudrepos/media

git checkout master
git pull origin master

git checkout -b datacenter
cp /tmp/index.html .

git add index.html
git commit -m "Add index.html from /tmp to datacenter branch"
git push origin datacenter

git checkout master
git merge datacenter
git push origin master
```

---

### Quick check

```bash
git branch
git log --oneline -n 5
ls -l index.html
```