\### MDR Helm Version

| Version          | Fix/Feature implemented                                                                 | Rule Added              |
|------------------|-----------------------------------------------------------------------------------------|-----------------------  |
| 1.0.1            | Fixed ingress tagging issue.                                                            |Corrected tag of LB added App=MDR tag|
|                  | Updated CPU and memory values from `md` & `sm` to `xl`.                                 |Update the Value to CPU and Memory to x Series|
|                  | Added worker pod as deployment.                                                         |Worker Pod configuration added in deployment file and 5190 container port opened|
|                  | Introduced DBPool.                                                                      |included db_pool: "10" value in common values|
|                  | Added `env.common` parameter.                                                           |Added common environment Variable for DD_AGENT_HOST| 
| 1.1.0            | Fixed issue with ingress tagging                                                        |                         |
|                  | Added `Sendgrid_username` variable and API key.                                         |Sendgrid Username and Api key is added in k8s charts|
|                  | Added AWS key in secrets.                                                               |Added Global Secret Prefix value in k8s secret file|                   
|  1.1.1           | Included `SESSION_TIMEOUT` variable in MDR charts.                                      |Introduced SESSION_TIMEOUT value and added default value of 30 sec|
|                  | Added WAF configuration to load balancer.                                               | WAF acl arn is added to lb  using ingress kubernetes fils|
|  1.1.2           | Enabled DD profiling and DBM propagation.                                               |DD_TRACE_SAMPLE_RATE=1,DD_DBM_PROPAGATION_MODE=full,DB_POOL is enabled |
|  1.1.3           | Enabled maintenance mode.                                                               |enable_maintenance_mode default value is set to false |
|                  | Added node/POD affinity to pods.                                                        |Included node selector and node affinity ON DEMAND value in deployment file|
|                  | Added `Workoff_wait` time, made it optional, and set the default flag to false.         |Included workoff-wait-rake in volumeMount for job scheduling|
|                  | Fixed Nginx host header and server fingerprinting issue.                                |Included Header in Nginx for Trasnport Security and Proxy|
|  1.1.4           | Included Nginx SSL ciphers.                                                             |Disabled Weak Cipher and Enabled strong Cipher using nginx-cm file|
|  1.1.5           | Included Heimdall configuration.                                                        |Included Heimdall configuration using deployment|
|  1.1.6            |Delayed job workoff SIGTERM handling.                                                  |                         |        
|                  | Enabled DB backup job.                                                                  | enable_database_backup  |
|  1.1.7           | Fixed TLS support for TLS 1.3.                                                          |                         |
|  1.2.0           | Removed AWS key dependency; added `Role-arn` as an environment variable.                |                         |
|  1.2.1           | Added support for TLS 1.2 and TLS 1.3.                                                  |                         |
|                  | Improved DB disconnect exception handling code.                                         |                         |
|                  | Fixed backend file upload issue.                                                        |                         |
|                  | Scaled job split into multiple groups based on resource requirements.                   |                         |
