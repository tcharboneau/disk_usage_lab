# disk_usage_lab

## 💻 Part 1: Manual Infrastructure & Storage Lab
**Target Environment:** Linux Mint Cinnamon on Oracle VirtualBox

This phase demonstrates core storage diagnostics, active volume mapping, and persistent filesystem verification.

### Step 1: Volume Diagnostics & Mounting Verification
1. Analyzed overall storage footprint and block utilization using `df` (disk free) metrics.
2. Estimated specific directory consumption weights using `du` (disk usage) to map active allocation points.
3. Evaluated the `/etc/fstab` (filesystem table) configuration file to audit persistent mounting paths.


### Step 2: Human-Readable Storage Diagnostics
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

# Disk Usage Lab - Alternative Scheduling Branch

This branch demonstrates an alternative approach to automating disk usage surveys using a Bash script and Cron jobs. It highlights workflow flexibility and Git branching proficiency.

## Script Details (`disk_usage.sh`)

* **Task**: Surveys disk space usage and logs the output.
* **Schedule**: Automatically runs four times a day at 6:00 AM, 12:00 PM (Noon), 6:00 PM, and 12:00 Midnight.

## Program and Cron Instructions

### Activating the Program
To run or test the disk usage script manually in your terminal:
```bash
# Make the script executable
chmod +x disk_usage.sh

# Run the script manually
./disk_usage.sh
```

### Activating the Cron Feature
To set up the automated schedule (6 AM, 12 PM, 6 PM, Midnight):
```bash
# Open the crontab editor
crontab -e

# Add the following line to schedule the script (adjust path as needed)
0 6,12,18,0 * * * /path/to/disk_usage.sh >> /path/to/disk_log.txt 2>&1
```



