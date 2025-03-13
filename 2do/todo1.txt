Round 4 [Coding Scenarios]
16. Shell script to find and delete files older than 30 days
Scenario: You need to clean up old files (e.g., logs, temporary data) to save storage space and maintain a tidy environment.
Key Points / Explanation:

Use the find command to locate files older than a certain number of days.
Combine -mtime +30 (older than 30 days) with -exec or -delete to remove them.
Example Script (Bash):

bash
Copy
#!/bin/bash

TARGET_DIR="/path/to/your/directory"
DAYS_OLD=30

# Find and delete files older than 30 days
find "$TARGET_DIR" -type f -mtime +$DAYS_OLD -exec rm -f {} \;

echo "Cleanup completed for files older than $DAYS_OLD days in $TARGET_DIR."
Why This Matters:

Automates file cleanup, saving storage and preventing clutter.
Reduces manual maintenance tasks.
17. Script to monitor disk usage and send alerts if usage exceeds 80%
Scenario: You want to keep track of disk usage and avoid outages or performance issues caused by full disks.
Key Points / Explanation:

Use df -h to get disk usage information.
Parse the output to check the usage percentage.
If usage > 80%, log the details and send an alert (e.g., via email).
Example Script (Bash):

bash
Copy
#!/bin/bash

THRESHOLD=80
LOGFILE="/var/log/disk_usage.log"
ALERT_EMAIL="admin@example.com"

usage_check() {
  df -h | awk 'NR>1 {print $5 " " $6}' | while read output; do
    usep=$(echo $output | awk '{print $1}' | sed 's/%//')
    partition=$(echo $output | awk '{print $2}')
    if [ $usep -ge $THRESHOLD ]; then
      echo "$(date): CRITICAL - Partition $partition is at $usep% usage." | tee -a $LOGFILE
      mail -s "Disk Usage Alert: $partition" "$ALERT_EMAIL" < $LOGFILE
    fi
  done
}

usage_check
Why This Matters:

Prevents downtime by proactively monitoring disk space.
Sends alerts in time for corrective action.
18. Script to rename all .txt files in a directory by appending the current date
Scenario: You have multiple text files that need to be timestamped for better organization or versioning.
Key Points / Explanation:

Use a simple for loop to iterate over all .txt files.
Append a date format (e.g., YYYYMMDD) to each filename.
Example Script (Bash):

bash
Copy
#!/bin/bash

TARGET_DIR="/path/to/your/directory"
cd "$TARGET_DIR" || exit 1

for file in *.txt; do
  # Skip if no .txt files exist
  [ -e "$file" ] || continue

  # Get current date in YYYYMMDD format
  DATE_STR=$(date +%Y%m%d)

  # Extract the base name (removing .txt) and append date
  mv "$file" "${file%.txt}_$DATE_STR.txt"
done

echo "Renaming completed."
Why This Matters:

Helps track file versions and creation/modification dates.
Improves organization and traceability of text files.
Round 5 [Director Round]
19. Handling incidents or production outages with minimal downtime
Key Points / Explanation:

Incident Management Process: Monitoring, detection, communication, resolution, post-mortem.
Best Practices: Have a clear on-call rotation, use incident management tools (e.g., PagerDuty, Opsgenie), follow runbooks.
Example Answer Approach:

Immediate Containment: Identify the scope and impact, isolate the issue.
Communication: Notify stakeholders and relevant teams quickly.
Root Cause Analysis: Use logs, monitoring dashboards (e.g., Grafana, Kibana) to identify the root cause.
Resolution & Recovery: Implement fixes or roll back changes.
Post-Mortem: Document the incident, share lessons learned, improve runbooks to avoid repeats.
20. Keeping up-to-date with new DevOps tools and best practices
Key Points / Explanation:

Continuous Learning: Attend conferences, follow tech blogs, subscribe to DevOps newsletters, participate in webinars.
Team Knowledge Sharing: Weekly/bi-weekly knowledge-sharing sessions or internal hackathons.
POCs and Prototyping: Experiment with new tools in sandbox environments before production adoption.
Example Answer Approach:

Set aside “Innovation Time” each sprint for trying new technologies.
Encourage reading and certifications (AWS, Kubernetes, Docker, etc.).
Team-Wide Collaboration: Document findings, create internal wikis, and share best practices.
21. Measuring a process and understanding the impact
Key Points / Explanation:

Metrics: Cycle time, lead time, deployment frequency, mean time to recovery (MTTR).
Impact Analysis: Improved efficiency, reduced cost, higher reliability, better team morale.
Example Answer Approach:

Define KPIs (e.g., time to deploy, bug escape rate).
Track Metrics over time using CI/CD analytics, dashboards, or custom scripts.
Evaluate Impact on throughput, quality, and user satisfaction.
22. Example of a real production incident you overcame
Key Points / Explanation:

Provide a concrete scenario (e.g., a microservice went down due to memory leak).
Explain what caused it, how you diagnosed it, and what steps you took to fix it.
Emphasize preventive measures you introduced afterward.
Example Answer Approach:

Incident Description: High CPU usage causing service downtime.
Resolution Steps: Roll back to stable release, analyze logs, fix the memory leak.
Post-Mortem: Improved monitoring alerts, added canary deployments, updated runbooks.
23. Difference between DevOps and Lean
Key Points / Explanation:

DevOps: Focuses on collaboration between development and operations, automation, continuous integration, and delivery.
Lean: Centered on eliminating waste, optimizing processes, and continuous improvement across all business operations.
Example Answer Approach:

Overlap: Both aim to improve flow and reduce waste.
Distinction: DevOps is more technology and pipeline-focused, while Lean is a broader methodology that can be applied to various domains, not just software.
24. Additional DevOps/SRE best practices or reliability discussions
Key Points / Explanation:

Topics might include SRE (Site Reliability Engineering) principles: SLIs (Service Level Indicators), SLOs (Service Level Objectives), error budgets, and reliability planning.
Best Practices: Observability (logs, metrics, traces), infrastructure as code, chaos engineering, and continuous improvement.
Example Answer Approach:

Define SLOs that align with business goals.
Track SLIs (latency, availability, error rates).
Implement Error Budgets to decide between new features vs. reliability improvements.
Tips for Interview Preparation
Practice Your Scripts: Be ready to explain not only the “how” but also the “why” behind each script’s logic.
Highlight Automation: Emphasize how scripting and tooling reduce manual effort and errors.
Show Strategic Thinking: In director or higher-level rounds, discuss process improvements, team collaboration, and the business impact of DevOps practices.
Use Real Examples: Wherever possible, back up your answers with real-life scenarios you’ve faced and how you solved them.
Stay Current: Mention any recent DevOps trends (e.g., GitOps, Platform Engineering, Infrastructure as Data) to demonstrate awareness of the evolving landscape.
Final Note
This summary combines the coding challenges (Round 4) and high-level strategic questions (Round 5). Tailor your answers based on your personal experience and the specific role or company you are interviewing for. By showcasing both technical expertise (scripts, automation, CI/CD) and broader DevOps/Lean strategies, you’ll stand out as a well-rounded candidate.