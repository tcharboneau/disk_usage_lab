# disk_usage_lab

## 💻 Part 1: Manual Infrastructure & Storage Lab
**Target Environment:** Linux Mint Cinnamon on Oracle VirtualBox

This phase demonstrates core storage diagnostics, active volume mapping, and persistent filesystem verification.

### Step 1: Volume Diagnostics & Mounting Verification
1. Analyzed overall storage footprint and block utilization using `df` (disk free) metrics.
2. Estimated specific directory consumption weights using `du` (disk usage) to map active allocation points.
3. Evaluated the `/etc/fstab` (filesystem table) configuration file to audit persistent mounting paths, drive UUID bindings, and boot-time attachment parameters.

### Step 2: VirtualBox State Persistence
* Captured the complete virtual machine baseline immediately following filesystem verification.


### Step 3: Human-Readable Storage Diagnostics
Generated localized volume analytics to ensure healthy block provisioning:
```bash
# Create target storage directory for reports
mkdir -p ~/Disk_Console
mkdir -p ~/Disk_Console/Snapshots

# Output human-readable utilization analytics to a report file
df -h / > ~/report

# Append strict free space availability matrices to the report
du -h / >> ~/report
```

## 🤖 Part 2: Automated Maintenance & Script Integration
To optimize system health, I integrated and configured an automated shell scripting framework to handle routine log lifecycle maintenance and threat auditing.

### Script Deployment (`/usr/local/bin/sys_maintenance.sh`)
```bash
#!/bin/bash
# ==============================================================================
# Automated System Maintenance Script
# Target OS: Linux Mint (Ubuntu/Debian Based)
# Requirements: Run with sudo privileges
# ==============================================================================

# Threshold Configurations
LOG_DIR="/var/log"
DAYS_OLD=30
THRESHOLD=85

echo "=== Starting System Maintenance: \$(date) ==="

# 1. Disk Space Monitoring
echo -n "[*] Checking disk space... "
CURRENT_USAGE=\$(df / | grep / | awk '{print \$5}' | tr -d '%')

if [ "\(CURRENT_USAGE" -ge "\)THRESHOLD" ]; then
    echo "WARNING: Disk space critical at \${CURRENT_USAGE}%"
else
    echo "OK (\${CURRENT_USAGE}% utilized)"
fi

# 2. SSH Security Auditing
echo "[*] Auditing failed SSH login attempts..."
if [ -f "/var/log/auth.log" ]; then
    FAILED_COUNT=\$(grep -c "Failed password" /var/log/auth.log)
    echo "Found \${FAILED_COUNT} failed SSH login attempts."
    if [ "\$FAILED_COUNT" -gt 0 ]; then
        echo "Recent unique IP sources:"
        grep "Failed password" /var/log/auth.log | awk '{print \$(NF-3)}' | sort -u | head -n 5
    fi
else
    echo "Log file /var/log/auth.log not found. Ensure SSH service is active."
fi

# 3. Log Retention & Purge (Enforcing 30-Day Policy)
echo "[*] Purging logs older than \({DAYS_OLD} days in\){LOG_DIR}..."
find "\(LOG_DIR" -type f -name "*.log" -mtime +"\)DAYS_OLD" -exec rm -f {} \;
find "\(LOG_DIR" -type f -name "*.gz" -mtime +"\)DAYS_OLD" -exec rm -f {} \;

echo "=== Maintenance Complete ==="
```

### Automation Orchestration (Cron Setup)
To ensure hands-off execution, the maintenance workflow is integrated into the root crontab engine (`sudo crontab -e`) to execute daily at midnight:

```cron
# m h dom mon dow command
0 0 * * * /usr/local/bin/sys_maintenance.sh >> /var/log/sys_maintenance.log 2>&1
```

### Operational Permissions & Verification
```bash
# 1. Move the production-ready script into standard system path
sudo cp sys_maintenance.sh /usr/local/bin/

# 2. Restrict script permissions to privileged root users only
sudo chmod 700 /usr/local/bin/sys_maintenance.sh

# 3. Verify that the background task runner is fully operational
sudo systemctl status cron

