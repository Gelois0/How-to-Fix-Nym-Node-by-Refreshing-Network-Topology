# How to Fix Nym Node by Refreshing Network Topology

If your Nym node is failing to start due to inconsistent network topology data, you can try forcing it to re-download the latest network information. Follow these steps:

![image](https://github.com/user-attachments/assets/5a54f9cb-ee7f-48fc-9012-eb3030a45d95)


![image](https://github.com/user-attachments/assets/fe7995c2-f16d-4ecc-844e-1ba1686e4c5e)

## Steps: 
### 1. Navigate to the Data Directory
First, change into the directory where the database files are stored:
```bash
cd /root/.nym/nym-nodes/hknym1/data/
```

### 2. Backup Existing Database Files
Before making any changes, create a backup of the database files to avoid data loss.
```bash
mkdir -p backup && mv *.sqlite backup/
```
This will move all SQLite database files into a `backup` folder inside the same directory.

### 3. Remove the Network Topology Files
Delete only the specific database files related to network topology:
```bash
rm -f ipr_gateways_info_store.sqlite nr_gateways_info_store.sqlite
```
This ensures that the node will download fresh copies of these files.

### 4. Restart the Nym Node
Now, restart the Nym node service to let it fetch the updated network topology:
```bash
systemctl restart nym-node.service
```

### 5. Restore Backup  && Monitor Logs to Confirm Success
After restoring the backup and restarting the node again, check the logs one more time to confirm that everything is now functioning smoothly.
```bash
mv backup/*.sqlite .
systemctl restart nym-node.service && journalctl -f -u nym-node.service
```

![image](https://github.com/user-attachments/assets/196f6c96-e754-4f92-8dc7-668e5c8402d5)

If the logs indicate successful startup and no errors, the node is now properly fixed and functional. 

**Additional Note:**
This guide is based on my personal experience from a year ago when I encountered similar network topology issues and successfully restored the node following these steps. I would like to extend my thanks to Kaleb for his invaluable help in solving this issue. If you need more help or details, you can check out the following link for further discussion:

[Guide on the experience in Matrix](https://matrix.to/#/!RvSqkbfokAPMVnLbAE:nymtech.chat/$XkQAp3bgjlBwkMJvv_8yI9XF3irSlcBIWr71hjtjq2c?via=matrix.org&via=nymtech.chat&via=hackliberty.org)
