### MDR Feature/Fix Implemented

| Version          | Fix/Feature implemented                                                                 | Rule Added              |
|------------------|-----------------------------------------------------------------------------------------|-----------------------  |
| 1.0.1            | Fixed the ingress tagging issue.                                                        |Corrected the tag of the load balancer by adding the App=MDR tag.|
|                  | Updated CPU and memory values from md and sm to xl.                                     |Updated the CPU and memory values to the x Series.|
|                  | Included worker pod as deployment.                                                      |Added worker pod configuration in the deployment file and opened container port 5190.|
|                  | Added DBPool configuration.                                                             |Included db_pool: "10" value in common values.|
|                  | Introduced env.common parameter.                                                        |Added a common environment variable for DD_AGENT_HOST| 
| 1.1.0            | Added Sendgrid_username variable and API key.                                           |Included Sendgrid username and API key in Kubernetes charts|
|                  | Included AWS key as secrets.                                                            |Added global secret prefix value in the Kubernetes secret file|                   
|  1.1.1           | Introduced SESSION_TIMEOUT variable in MDR charts.                                      |Set the default value of SESSION_TIMEOUT to 30 seconds|
|                  | Configured WAF settings for the load balancer.                                          |Added WAF ACL ARN to the load balancer using the ingress Kubernetes file|
|  1.1.2           | Enabled Datadog profiling and database monitoring propagation.                          |Set DD_TRACE_SAMPLE_RATE=1, DD_DBM_PROPAGATION_MODE=full, and enabled DB_POOL|
|  1.1.3           | Enabled maintenance mode.                                                               |Set the default value of enable_maintenance_mode to false|
|                  | Added nod and pod affinity configurations.                                              |Included node selector and node affinity ON DEMAND value in the deployment file|
|                  | Made Workoff_wait time optional and set the default flag to false.                      |Included workoff-wait-rake in volumeMount for job scheduling|
|                  | Fixed Nginx host header and server fingerprinting issue.                                |Included necessary headers in Nginx for transport security and proxy|
|  1.1.4           | Configured Nginx SSL ciphers.                                                           |Disabled weak ciphers and enabled strong ciphers using the nginx-cm file|
|  1.1.5           | Added Heimdall configuration.                                                           |Included Heimdall configuration in the deployment|
|  1.1.6           | Improved SIGTERM handling for delayed job workoff.                                      |Added code in workoff_wait.rake to manage jobs locked by pods|        
|                  | Enabled database backup.                                                                |Activated the database backup dump job with a default value of false for enable_database_backup|
|  1.1.7           | Fixed TLS support for TLS 1.3.                                                          |Included SSL Policy: ELBSecurityPolicy-TLS13-1-3-2021-06 and configuration in nginx-cm to support TLS 1.3|
|  1.2.0           | Removed AWS key dependency; added Role-arn as an environment variable.                  |Removed AWS secrets from the common-secret file and added role-arn in the helper configuration|
|  1.2.1           | Added support for TLS 1.2 and TLS 1.3.                                                  |Included ssl_protocols TLSv1.3; in nginx-cm to enable TLS 1.3|
|                  | Improved database disconnect exception handling code                                    |Added code in workoff_wait.rake file to address database exceptions|
|                  | Scaled job processing by splitting into multiple groups based on resource requirements. |Included ScaledJob (scaled-job-common and scaled-job-xlarge files) to split into multiple groups|
|                  | Disabled email notifications.                                                           |Removed the DISABLE_EMAIL_NOTIFICATION flag from common-cm and values.yaml file|







