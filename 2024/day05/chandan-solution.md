# Day 5 Tasks: Advanced Linux Shell Scripting for DevOps Engineers with User Management

## Overview

In this task, you will learn to create directories using shell scripting, automate backups, manage users, and more.

## 1. Create Directories Using Shell Script

### Script: `createDirectories.sh`

Create a bash script named `createDirectories.sh` with the following content:

```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 3 ]; then
    echo "Usage: $0 <directory_name> <start_number> <end_number>"
    exit 1
fi

directory_name=$1
start_number=$2
end_number=$3

# Create directories in the specified range
for ((i=start_number; i<=end_number; i++)); do
    mkdir "${directory_name}${i}"
done

echo "Created directories from ${directory_name}${start_number} to ${directory_name}${end_number}"
