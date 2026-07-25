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


# 2. Restrict script permissions to privileged root users only
sudo chmod 700 /usr/local/bin/sys_maintenance.sh

# 3. Verify that the background task runner is fully operational
sudo systemctl status cron

