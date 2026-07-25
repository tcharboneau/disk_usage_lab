# disk_usage_lab

## 💻 Part 1: Manual Infrastructure & Storage Lab
**Target Environment:** Linux Mint Cinnamon on Oracle VirtualBox

This phase demonstrates core storage diagnostics, active volume mapping, and persistent filesystem verification.

### Step 1: Volume Diagnostics & Mounting Verification
1. Analyzed overall storage footprint and block utilization using `df` (disk free) metrics.
2. Estimated specific directory consumption weights using `du` (disk usage) to map active allocation points.
3. Evaluated the `/etc/fstab` (filesystem table) configuration file to audit persistent mounting paths.

### Step 2: VirtualBox State Persistence
* Captured the complete virtual machine baseline immediately following filesystem verification.


### Step 3: Human-Readable Storage Diagnostics
Generated localized volume analytics to ensure healthy block provisioning:[1](1__PWD.png), [2](2__DU_REPORT.png), [3](3__FSTAB_REPORT.png), [4](4__REPORT.png)
```bash
# Create target storage directory for reports
mkdir -p ~/Disk_Console
mkdir -p ~/Disk_Console/Snapshots

#Create target storage files for reports
touch ~/Disk_Console/Snapshots/du_report
touch ~/Disk_Console/Snapshots/fstab_head
touch ~/Disk_Console/Snapshots/report

# Output human-readable utilization analytics to a report file
df -h / > ~/report

# Output human-readable utilization analytics to the report
du -h / > ~/du_report

# Output human-readable fstab elements to a report
head /etc/fstab/ > ~/fstab_head
```



