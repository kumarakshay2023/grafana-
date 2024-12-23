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
    

