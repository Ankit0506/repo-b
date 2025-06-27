Helm Version 

1.0.1
  - Ingress Tagging issue fixed
  - Fixed CPU and Memory Value from md & sm to xl
  - Added Worker pod as deployment
  - DBPool introduced
  - Introduced AWS key in secrets
  - Added env.common Parameter 
1.1.0
  - Fixed issue with ingress tagging for MDR helm chart version 1.1.0
  - Added Sendgrid_username Variable and apikey 

1.1.1
  - SESSION_TIMEOUT Variable included to MDR Charts
  - WAF configuration added to load balancer

1.1.2
 
  - DD Profiling & DBM Propagation enabled

1.1.3
  - Maintenance mode enabled
  - Fixed Duplicate config image issue for nginx container
  - Node/POD Affinity added to PODS
  - Added Workoff_wait time and made optional and by default flat is set to false.
  - Nginx Host Header and Server fingerPrinting issue fixed
    
1.1.4
  - Included Nginx SSL ciphers
    
1.1.5
  - Heimdall config included
  - 
1.1.6
  - Removed DB connection handing code
  - Delayed job workoff sigterm handling
  - DB backup job enabled
    
1.1.7
  - Fixed TLS support TLS1.3
    
1.2.0
  - Removed AWS Key dependency added Role-arn as env variable
1.2.1
  - Added TLS 1.2 and TLS1.3
  - Improved DB disconnect exception handing code
  - Fixed backed file upload issue
  - Scaled job splitted into multiple group on resource requirement.

