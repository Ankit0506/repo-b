Version 1.0.1

    Updated CPU and memory resource requests and limits to:
    → requests: cpu: md, memory: sm
      limits: cpu: xxl, memory: md

    Included worker pod as deployment.
    → Added worker pod configuration in the deployment file and opened container port 5190.
      Introduced worker/templates/deployment.yaml to define a dedicated Deployment for the worker service.
      Integrates:
          env.common.with.db and common-secrets.envvars for environment variables.
          ConfigMap (-cm) and Datadog-specific metadata.
          Configurable resource requests and limits.
          DB pool size via DB_POOL and value from values.yaml.
  
    App Deployment Enhancements
    → Added DB_POOL environment variable to app container using value from values.yaml.
      Changed startup command to use:
      Improved container readiness with consistent tcpSocket probe on port 5190.

    This sets up scalable, tagged worker processing with dynamic configuration and monitoring support.
    → Added DBPool configuration.
      Added db_pool under config in common/values.yaml to define database connection pool size.
      Referenced DB_POOL in common-cm.yaml config map for environment variable injection.
      Added db_pool_size: 10 to worker/values.yaml to align resource-specific pool settings.

    Introduced Datadog parameter.
    → Common values are defined as environment variables required for Datadog integration. These include:
      DD_AGENT_HOST: Automatically set to the pod's host IP
      DD_ENV, DD_SERVICE, DD_VERSION: Dynamically fetched from pod metadata labels (tags.datadoghq.com/*)
      Custom environment variables from values.yaml under datadogContainerEnv are also appended

Version 1.1.0

    Added SendGrid Configuration for Miami release.
    → Introduced SENDGRID_USERNAME environment variable in common-cm.yaml and corresponding value sendgrid_username in values.yaml under the Mail & SendGrid section.

    Added AWS Credentials to Secret Configuration
    → Enhanced secrets.yaml to include two new secrets:
      aws_access_key
      aws_secret

Version 1.1.1

    Introduced SESSION_TIMEOUT variable in MDR charts.
    → Set the default value of SESSION_TIMEOUT to 30 seconds.

    Configured WAF settings for the load balancer.
    → Added WAF ACL ARN to the load balancer using the ingress Kubernetes file.

    Fixed the ingress tagging issue.
    → Corrected the tag of the load balancer by adding the App=MDR tag.

Version 1.1.2

    Enabled Datadog profiling and database monitoring propagation.
    → Set DD_TRACE_SAMPLE_RATE=1, DD_DBM_PROPAGATION_MODE=full, and enabled DB_POOL.

Version 1.1.3

    Enabled maintenance mode.
    → Set the default value of enable_maintenance_mode to false.

    Added node and pod affinity configurations.
    → Included node selector and node affinity ON DEMAND value in the deployment file.

    Made Workoff_wait time optional and set the default flag to false.
    → Included workoff-wait-rake in volumeMount for job scheduling.

    Fixed Nginx host header and server fingerprinting issue.
    → Included necessary headers in Nginx for transport security and proxy.

Version 1.1.4

    Configured Nginx SSL ciphers.
    → Disabled weak ciphers and enabled strong ciphers using the nginx-cm file.

Version 1.1.5

    Added Heimdall configuration.
    → Included Heimdall configuration in the deployment.

Version 1.1.6

    Improved SIGTERM handling for delayed job workoff.
    → Added code in workoff_wait.rake to manage jobs locked by pods.

    Enabled database backup.
    → Activated the database backup dump job with a default value of false for enable_database_backup.

Version 1.1.7

    Fixed TLS support for TLS 1.3.
    → Included SSL Policy: ELBSecurityPolicy-TLS13-1-3-2021-06 and configuration in nginx-cm.

Version 1.2.0

    Removed AWS key dependency; added role-arn as an environment variable.
    → Removed AWS secrets from the common-secret file and added role-arn in the helper configuration.

Version 1.2.1

    Added support for TLS 1.2 and TLS 1.3.
    → Included ssl_protocols TLSv1.3; in nginx-cm to enable TLS 1.3.

    Improved database disconnect exception handling code.
    → Added code in workoff_wait.rake to address database exceptions.

    Scaled job processing by splitting into multiple groups based on resource requirements.
    → Included ScaledJob (scaled-job-common and scaled-job-xlarge files).

    Disabled email notifications.
    → Removed the DISABLE_EMAIL_NOTIFICATION flag from common-cm and values.yaml.
