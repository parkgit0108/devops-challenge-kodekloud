ssh into app server and follow below commands.

```sql
#switch to root user
sudo -i
```
```sql
#create Dockerfile
cat > /python_app/Dockerfile << 'EOF'
FROM python:3.9

WORKDIR /app

COPY src/requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY src/ .

EXPOSE 3003

CMD ["python", "server.py"]
EOF
```
```sql
#build the image
cd /python_app
docker build -t nautilus/python-app .

#run the container
docker run -d \
  --name pythonapp_nautilus \
  -p 8099:3003 \
  nautilus/python-app

#verify
docker ps
curl http://localhost:8099
```
