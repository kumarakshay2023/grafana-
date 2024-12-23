# Grafana Enterprise Installation and Setup

## Steps to Install and Run Grafana Enterprise

### 1. Download Grafana Enterprise
Run the following command to download the Grafana Enterprise tarball:
```bash
wget https://dl.grafana.com/enterprise/release/grafana-enterprise-8.4.4.linux-amd64.tar.gz
```

### 2. List Files in the Current Directory
To verify the downloaded file, list the files in the current directory:
```bash
ls
```

### 3. Extract the Grafana Tarball
Extract the downloaded tarball using the `tar` command:
```bash
tar -zxvf grafana-enterprise-8.4.4.linux-amd64.tar.gz
```

### 4. Verify the Extracted Files
List the files again to ensure the extraction was successful:
```bash
ls
```

### 5. Navigate to the Grafana Directory
Change into the extracted Grafana directory:
```bash
cd grafana-8.4.4
```

### 6. Start the Grafana Server
Run the following command to start the Grafana server:
```bash
./bin/grafana-server
```

### 7. Access Grafana in a Browser
- The Grafana server runs on port `3000` by default.
- Open your browser and navigate to:
  ```
  http://<your-server-ip>:3000
  ```

### 8. Configure Security Group for Port 3000
Ensure that port `3000` is open in your server's security group:
1. Log in to your cloud provider's console (e.g., AWS, Azure, or GCP).
2. Navigate to the security group associated with your server.
3. Add an inbound rule to allow traffic on port `3000`:
   - **Protocol:** TCP
   - **Port Range:** 3000
   - **Source:** Your IP address or `0.0.0.0/0` (for public access; use cautiously).

## Notes
- Use the default admin credentials to log in for the first time:
  - **Username:** `admin`
  - **Password:** `admin`
- Update the admin password immediately after the first login for security.

## Troubleshooting
- If Grafana is not accessible:
  - Check if the server is running using the command:
    ```bash
    ps aux | grep grafana-server
    ```
  - Verify the firewall and security group settings.
  - Check Grafana logs for errors:
    ```bash
    ./bin/grafana-server > grafana.log 2>&1
    tail -f grafana.log
    ```

# Docker Server Setup and Prometheus Integration

## Steps to Set Up Docker and Run Containers

### 1. Update Package List
Run the following command to update the package list:
```bash
apt update
```

### 2. Install Docker
Install Docker using the following command:
```bash
apt install docker.io -y
```

### 3. Start Docker Service
Start the Docker service:
```bash
service docker start
```

### 4. Run Ubuntu Containers
Run two Ubuntu containers with the following commands:
```bash
docker run -dt --name c01 ubuntu
docker run -dt --name c02 ubuntu
```

## Prometheus Setup

### 1. Download Prometheus
Download Prometheus using the following command:
```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.34.0/prometheus-2.34.0.linux-amd64.tar.gz
```

### 2. Extract Prometheus Tarball
Extract the downloaded tarball:
```bash
tar zxvf prometheus-2.34.0.linux-amd64.tar.gz
```

### 3. Navigate to Prometheus Directory
Change into the Prometheus directory:
```bash
cd prometheus-2.34.0.linux-amd64
```

### 4. Configure Docker for Prometheus
Prometheus needs to track Docker metrics via port `9323`. Update the Docker daemon configuration:

1. Open the Docker daemon configuration file:
   ```bash
   vi /etc/docker/daemon.json
   ```

2. Press `I` to enter insert mode and add the following configuration:
   ```json
   {
       "metrics-addr" : "0.0.0.0:9323",
       "experimental" : true
   }
   ```

3. Save and exit the file by pressing `Esc`, typing `:wq`, and hitting `Enter`.

4. Restart Docker for the changes to take effect:
   ```bash
   service docker restart