### MDR Helm Version

| Version          | Fix/Feature implemented                                                                 | Rule Added |
|------------------|-----------------------------------------------------------------------------------------|------------|
| 1.0.1            | Fixed ingress tagging issue.                                                            |            |
|                  | Updated CPU and memory values from `md` & `sm` to `xl`.                                 |            |
|                  | Added worker pod as deployment.                                                         |            |
|                  | Introduced DBPool.                                                                      |            |
|                  | Added AWS key in secrets.                                                               |            |
|                  | Added `env.common` parameter.                                                           |            |
| 1.1.0            | Fixed issue with ingress tagging for MDR Helm chart version 1.1.0.                      |            |
|                  | Added `Sendgrid_username` variable and API key.                                         |            |
|  1.1.1           | Included `SESSION_TIMEOUT` variable in MDR charts.                                      |            |
|                  | Added WAF configuration to load balancer.                                               |            |
|  1.1.2           | Enabled DD profiling and DBM propagation.                                               |            |
|  1.1.3           | Enabled maintenance mode.                                                               |            |
|                  | Fixed duplicate config image issue for Nginx container.                                 |            |
|                  | Added node/POD affinity to pods.                                                        |            |
|                  | Added `Workoff_wait` time, made it optional, and set the default flag to false.         |            |
|                  | Fixed Nginx host header and server fingerprinting issue.                                |            |
|  1.1.4           | Included Nginx SSL ciphers.                                                             |            |
|  1.1.5           | Included Heimdall configuration.                                                        |            |
|  1.1.6           | Removed DB connection handling code.                                                    |            |
|                  | Delayed job workoff SIGTERM handling.                                                   |            |
|                  | Enabled DB backup job.                                                                  |            |
|  1.1.7           | Fixed TLS support for TLS 1.3.                                                          |            |
|  1.2.0           | Removed AWS key dependency; added `Role-arn` as an environment variable.                |            |
|  1.2.1           | Added support for TLS 1.2 and TLS 1.3.                                                  |            |
|                  | Improved DB disconnect exception handling code.                                         |            |
|                  | Fixed backend file upload issue.                                                        |            |
|                  | Scaled job split into multiple groups based on resource requirements.                   |            |
