### MDR Helm Version

| Version          | Fix/Feature implemented                                                                 | Rule Added              |
|------------------|-----------------------------------------------------------------------------------------|-----------------------  |
| 1.0.1            | Fixed ingress tagging issue.                                                            |Corrected tag of LB added App=MDR tag|
|                  | Updated CPU and memory values from `md` & `sm` to `xl`.                                 |Update the Value to CPU and Memory to x Series|
|                  | Added worker pod as deployment.                                                         |                         |
|                  | Introduced DBPool.                                                                      |db_pool                  |
|                  | Added `env.common` parameter.                                                           |Added common environment Variable for DD_AGENT_HOST| 
| 1.1.0            | Fixed issue with ingress tagging                                                        |                         |
|                  | Added `Sendgrid_username` variable and API key.                                         |Sendgrid Username and Api key is added in k8s charts|
|                  | Added AWS key in secrets.                                                               |secret_prefix            |                   
|  1.1.1           | Included `SESSION_TIMEOUT` variable in MDR charts.                                      |session_timeout          |
|                  | Added WAF configuration to load balancer.                                               |                         |
|  1.1.2           | Enabled DD profiling and DBM propagation.                                               |                         |
|  1.1.3           | Enabled maintenance mode.                                                               |enable_maintenance_mode  |
|                  | Fixed duplicate config image issue for Nginx container.                                 |                         |
|                  | Added node/POD affinity to pods.                                                        |                         |
|                  | Added `Workoff_wait` time, made it optional, and set the default flag to false.         |                         |
|                  | Fixed Nginx host header and server fingerprinting issue.                                |                         |
|  1.1.4           | Included Nginx SSL ciphers.                                                             |                         |
|  1.1.5           | Included Heimdall configuration.                                                        |                         |
|  1.1.6           | Removed DB connection handling code.                                                    |                         |
|                  | Delayed job workoff SIGTERM handling.                                                   |                         |            
|                  | Enabled DB backup job.                                                                  | enable_database_backup  |
|  1.1.7           | Fixed TLS support for TLS 1.3.                                                          |                         |
|  1.2.0           | Removed AWS key dependency; added `Role-arn` as an environment variable.                |                         |
|  1.2.1           | Added support for TLS 1.2 and TLS 1.3.                                                  |                         |
|                  | Improved DB disconnect exception handling code.                                         |                         |
|                  | Fixed backend file upload issue.                                                        |                         |
|                  | Scaled job split into multiple groups based on resource requirements.                   |                         |
