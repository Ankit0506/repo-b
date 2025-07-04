### MDR Feature/Fix Implemented

| Version          | Fix/Feature implemented                                                                 | Rule Added              |
|------------------|-----------------------------------------------------------------------------------------|-----------------------  |
| 1.0.1            | Fixed ingress tagging issue.                                                            |Corrected tag of LB added App=MDR tag|
|                  | Updated CPU and memory values from `md` & `sm` to `xl`.                                 |Updated the Value to CPU and Memory to x Series|
|                  | Included worker pod as deployment.                                                      |Worker Pod configuration added in deployment file and 5190 container port opened|
|                  | Included DBPool.                                                                        |Included db_pool: "10" value in common values|
|                  | Included `env.common` parameter.                                                        |Added common environment Variable for DD_AGENT_HOST| 
| 1.1.0            | Included `Sendgrid_username` variable and API key.                                      |Sendgrid Username and Api key is added in k8s charts|
|                  | Included AWS key as secrets.                                                            |Added Global Secret Prefix value in k8s secret file|                   
|  1.1.1           | Included `SESSION_TIMEOUT` variable in MDR charts.                                      |Introduced SESSION_TIMEOUT value and added default value of 30 sec|
|                  | Included WAF configuration to load balancer.                                            | WAF acl arn is added to lb  using ingress kubernetes fils|
|  1.1.2           | Enabled DD profiling and DBM propagation.                                               |DD_TRACE_SAMPLE_RATE=1,DD_DBM_PROPAGATION_MODE=full,DB_POOL is enabled |
|  1.1.3           | Enabled maintenance mode.                                                               |enable_maintenance_mode default value is set to false |
|                  | Included node/POD affinity to pods.                                                     |Included node selector and node affinity ON DEMAND value in deployment file|
|                  | Included `Workoff_wait` time, made it optional, and set the default flag to false.      |Included workoff-wait-rake in volumeMount for job scheduling|
|                  | Fixed Nginx host header and server fingerprinting issue.                                |Included Header in Nginx for Trasnport Security and Proxy|
|  1.1.4           | Included Nginx SSL ciphers.                                                             |Disabled Weak Cipher and Enabled strong Cipher using nginx-cm file|
|  1.1.5           | Included Heimdall configuration.                                                        |Included Heimdall configuration using deployment|
|  1.1.6           | Delayed job workoff SIGTERM handling.                                                   |Code added in workoff_wait.rake to handle the job locked by pod|        
|                  | DB Backup enabled                                                                       |Enabled DB Backup Dump job having default value false of enable_database_backup|
|  1.1.7           | Fixed TLS support for TLS 1.3.                                                          |Included SSL Policy:ELBSecurityPolicy-TLS13-1-3-2021-06 and configuration in nginx-cm to supportTLS1.3|
|  1.2.0           | Removed AWS key dependency; added `Role-arn` as an environment variable.                |Removed AWS Secrets from from common-secret file and added role-arn in helper configuration|
|  1.2.1           | Included support for TLS 1.2 and TLS 1.3.                                               |Added ssl_protocols TLSv1.3; in nginx-cm to enable TLS1.3|
|                  | Improved DB disconnect exception handling code.                                         |Included code in workoff_wait.rake file to fix DB exception|
|                  | Scaled job split into multiple groups based on resource requirements.                   |Included ScaledJob (scaled-job-common and scaled-job-xlarge file) to Split into mutiple group|
|                  | Disabled Email Notification                                                             |Removed DISABLE_EMAIL_NOTIFICATION flag from common-cm and values.yaml file|
