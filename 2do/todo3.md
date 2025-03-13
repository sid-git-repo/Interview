Round 3
9. Designing the Istio Setup for Your Kubernetes Cluster
Key Points / Explanation:
Istio is a service mesh that provides traffic management, security, and observability.
Typically, you install Istio in the istio-system namespace using istioctl or Helm.
You can enable sidecar injection on specific namespaces by adding labels.
Example Approach:
Install Istio (e.g., istioctl install --set profile=demo -y).
Enable Sidecar Injection by labeling the target namespace (kubectl label namespace <your-namespace> istio-injection=enabled).
Configure Traffic Rules using VirtualService and DestinationRule to manage routing, retries, and circuit-breaking.
10. AWS EventBridge Creation and Setup via Terraform
Key Points / Explanation:
AWS EventBridge allows you to route events from AWS services or custom applications to targets like Lambda, SQS, etc.
Terraform can define EventBridge rules, targets, and permissions in code.
Example Approach:
Create a Rule using Terraform’s aws_cloudwatch_event_rule.
Attach Targets with aws_cloudwatch_event_target.
Configure Permissions for the target (e.g., aws_lambda_permission if it’s a Lambda).
Validate in AWS console to ensure events trigger correctly.
11. Command to Add Annotations and Labels to Existing Resources
Key Points / Explanation:
Labels and annotations are metadata you can attach to Kubernetes objects.
You can modify them via kubectl annotate and kubectl label.
Example Command:
bash
Copy
# Add or update a label
kubectl label deployment my-deployment environment=staging --overwrite

# Add or update an annotation
kubectl annotate pod my-pod owner="teamA" --overwrite
Why This Matters:
Labels help with grouping or selecting resources.
Annotations store non-identifying metadata (e.g., contact info, version details).
12. Designing the Kubernetes Cluster with Ingress
Key Points / Explanation:
Ingress abstracts external access to services in a cluster, typically via HTTP/HTTPS.
Common controllers include NGINX, Traefik, HAProxy, or cloud-specific ones (e.g., ALB Ingress Controller).
Example Approach:
Deploy an Ingress Controller (e.g., helm install ingress-nginx).
Create Ingress Resources specifying host/path rules pointing to internal Services.
TLS Configuration for secure traffic if required (e.g., via Cert-Manager).
13. Designing a Web Application to Route Traffic from the Website to Microservices
Key Points / Explanation:
Typically involves an Ingress or a load balancer that routes incoming requests to different microservices.
Might also involve a service mesh (e.g., Istio) for more advanced routing and policies.
Example Approach:
Frontend (Website): DNS points to your ingress or load balancer.
Routing Rules: In the Ingress or Istio VirtualService, define paths (/api/v1/, /auth/) that map to different microservices.
Security/Observability: Use Istio or sidecar proxies to apply security policies and gather telemetry data.
14. (or 15) Setting or Changing the Name of a Docker Container
Key Points / Explanation:
You can specify a container name in docker run using --name <container_name>.
To rename a running container, use docker rename <old_name> <new_name>.
Example Commands:
bash
Copy
# Set the container name at runtime
docker run --name my-app-container -d my-app:latest

# Rename an existing container
docker rename old-container-name new-container-name
15. Reducing the Size of a Dockerfile (or Docker Image)
Key Points / Explanation:
Use smaller base images (e.g., alpine, distroless).
Combine layers or remove unnecessary packages.
Clean up caches and temporary files.
Example Approach:
Start with Alpine (e.g., FROM alpine:3.14) instead of ubuntu.
Combine RUN Commands to reduce the number of layers.
Use Multi-Stage Builds for compiling and then copying only required artifacts into a minimal runtime image.
Round 4 [Coding Scenarios]
16. Shell Script to Find and Delete All Files Older Than 30 Days
Key Points / Explanation:
Use find with -mtime +30 and -exec rm or -delete.
Example Script:
bash
Copy
#!/bin/bash
find /path/to/directory -type f -mtime +30 -exec rm -f {} \;
echo "Deleted files older than 30 days."
17. Script to Monitor Disk Usage and Send Alerts if Usage Exceeds 80%
Key Points / Explanation:
Use df -h to get disk usage.
Parse output with awk, compare against threshold, and send an alert (e.g., email).
Example Script:
bash
Copy
#!/bin/bash
THRESHOLD=80
df -h | awk 'NR>1 {print $5 " " $6}' | while read output; do
  usep=$(echo $output | awk '{print $1}' | sed 's/%//')
  partition=$(echo $output | awk '{print $2}')
  if [ $usep -ge $THRESHOLD ]; then
    echo "Partition $partition usage is at ${usep}%"
    # Send email or Slack notification here
  fi
done
18. Script to Rename All .txt Files in a Directory by Appending the Current Date
Key Points / Explanation:
Loop through each .txt file, strip .txt, then append the date string.
Example Script:
bash
Copy
#!/bin/bash
DATE_STR=$(date +%Y%m%d)
for file in /path/to/*.txt; do
  [ -e "$file" ] || continue
  mv "$file" "${file%.txt}_$DATE_STR.txt"
done
Round 5 [Director Round]
19. Handling Incidents or Production Outages
Key Points / Explanation:
Focus on quick detection, communication, containment, and root cause analysis.
Post-mortem process to prevent future recurrences.
Example Answer Approach:
Incident Triage: Identify impacted services, gather logs and metrics.
Communication: Notify stakeholders and users as appropriate.
Resolution: Roll back or hotfix. Document findings in a post-incident report.
20. Keeping Yourself and Your Team Updated with New DevOps Tools/Best Practices
Key Points / Explanation:
Continuous learning via blogs, webinars, conferences.
Internal knowledge-sharing sessions and hackathons.
Example Answer Approach:
Establish a Learning Culture: Regular brown-bag sessions, internal demos.
Allocate “Innovation Time” each sprint for exploration.
21. Measuring a Process (KPIs/Impact)
Key Points / Explanation:
Common DevOps metrics: deployment frequency, lead time for changes, mean time to recovery (MTTR).
Link improvements to tangible outcomes (fewer outages, faster releases).
Example Answer Approach:
Define Key Metrics: e.g., deployment frequency, bug rate.
Track Over Time: Use CI/CD pipelines, project management tools.
Analyze Impact: Did it reduce costs or improve customer satisfaction?
22. Balancing Technical Debt and New Feature Development
Key Points / Explanation:
Addressing tech debt ensures long-term stability but can slow new features.
Need to find the right ratio (e.g., 80% new features, 20% tech debt).
Example Answer Approach:
Justify Tech Debt Efforts: Show how ignoring debt leads to bigger problems later.
Prioritize: Evaluate the criticality of technical debt vs. feature demands.
23. Difference Between DevOps and Lean
Key Points / Explanation:
DevOps: Primarily about collaboration, automation, CI/CD in software delivery.
Lean: Broad methodology focusing on eliminating waste, continuous improvement in any business process.
Example Answer Approach:
Both aim to increase efficiency and reduce waste, but DevOps is more software-centric while Lean can apply to any domain.
24. Additional Best Practices or Closing Discussion
Key Points / Explanation:
SRE principles (SLIs, SLOs, error budgets), chaos engineering, continuous improvement.
Emphasize culture of ownership, collaboration, and transparency.
Example Answer Approach:
Talk about implementing progressive delivery (canary, blue-green), robust monitoring, and a blameless post-mortem culture.
Final Preparation Tips
Technical Depth + Big Picture: Show that you understand the “how” (scripts, YAML) and the “why” (business value, reliability).
Use Real Examples: When discussing scenarios (outages, microservices design), reference personal or well-known incidents you’ve handled.
Automation & Observability: Emphasize how you automate repeated tasks and monitor systems to catch issues early.
Continuous Learning: Mention courses, conferences, or community involvement that keep you up-to-date on DevOps trends.
Collaboration & Communication: Especially in director or higher-level rounds, highlight how you communicate with stakeholders and lead teams effectively.
By focusing on these areas and structuring your answers clearly, you’ll demonstrate both your technical proficiency and your strategic thinking in a DevOps context.