---
title: "Day 10 : Log Analyzer and Report Generator Scenario"
seoTitle: "Log Analyzer & Report Generator Guide"
seoDescription: "Automate log analysis and report generation using a Bash script to enhance server management efficiency and security. Ideal for system administrators"
datePublished: Tue Jul 23 2024 18:00:32 GMT+0000 (Coordinated Universal Time)
cuid: clyyq1fsw000309mgcwbw1bza
slug: day-10-log-analyzer-and-report-generator-scenario
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721757312628/03467c35-8259-430d-9b85-ac164d61cd8b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721757344953/15b3206f-b2cd-4d54-98d3-d2f48a4522f5.png
tags: linux, bash, devops, 90daysofdevops, trainwithshubham

---

## DAY 10 : TASK

## • Scenario

As a system administrator, managing a network of servers is a critical part of your job. Every day, each server generates a log file containing essential system events and error messages. Analyzing these logs is vital for maintaining the health and security of the servers. To streamline this process, we'll create a Bash script that automates log analysis and report generation.

### • Task

Your task is to write a Bash script that automates the process of analyzing log files and generating a daily summary report. The script should perform the following steps:

1. **Input**: The script should take the path to the log file as a command-line argument.
    
2. **Error Count**: Analyze the log file and count the number of error messages. An error message can be identified by a specific keyword (e.g., "ERROR" or "Failed"). Print the total error count.
    
3. **Critical Events**: Search for lines containing the keyword "CRITICAL" and print those lines along with the line number.
    
4. **Top Error Messages**: Identify the top 5 most common error messages and display them along with their occurrence count.
    
5. **Summary Report**: Generate a summary report in a separate text file. The report should include:
    
    * Date of analysis
        
    * Log file name
        
    * Total lines processed
        
    * Total error count
        
    * Top 5 error messages with their occurrence count
        
    * List of critical events with line numbers
        
6. **Optional Enhancement**: Add a feature to automatically archive or move processed log files to a designated directory after analysis.
    

### • Tips

* Use `grep`, `awk`, and other command-line tools to process the log file.
    
* Utilize arrays or associative arrays to keep track of error messages and their counts.
    
* Use appropriate error handling to manage cases where the log file doesn't exist or other issues arise.
    

```bash
#!/bin/bash

if [ -z "$1" ]; then
  echo "Usage: $0 <path_to_log_file>"
  exit 1
fi

log_file=$1
report_file="summary_report_$(date +%Y%m%d).txt"

if [ ! -f "$log_file" ]; then
  echo "Log file not found!"
  exit 1
fi

total_lines=$(wc -l < "$log_file")
error_count=$(grep -cE "ERROR|Failed" "$log_file")
critical_events=$(grep -n "CRITICAL" "$log_file")

declare -A error_messages

while IFS= read -r line; do
  if [[ "$line" =~ ERROR|Failed ]]; then
    error_message=$(echo "$line" | awk -F']' '{print $NF}')
    ((error_messages["$error_message"]++))
  fi
done < "$log_file"

top_errors=$(for message in "${!error_messages[@]}"; do
  echo "${error_messages[$message]} $message"
done | sort -rn | head -n 5)

echo "Date of analysis: $(date)" > "$report_file"
echo "Log file name: $log_file" >> "$report_file"
echo "Total lines processed: $total_lines" >> "$report_file"
echo "Total error count: $error_count" >> "$report_file"
echo "Top 5 error messages with their occurrence count:" >> "$report_file"
echo "$top_errors" >> "$report_file"
echo "List of critical events with line numbers:" >> "$report_file"
echo "$critical_events" >> "$report_file"

# Optional: Move processed log file to archive directory
archive_dir="log_archive"
mkdir -p "$archive_dir"
mv "$log_file" "$archive_dir/"

echo "Analysis complete. Report generated: $report_file"
```

### • Summary

automating log analysis and report generation with a Bash script can significantly enhance the efficiency and effectiveness of server management. By systematically counting errors, identifying critical events, and summarizing key information, system administrators can maintain server health and security more effectively. Implementing such a script not only saves time but also ensures that important issues are promptly identified and addressed, contributing to the overall stability and reliability of the network infrastructure.

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>