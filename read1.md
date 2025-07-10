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

    Added SESSION_TIMEOUT Config to Common ConfigMap
    → Introduced a new environment variable SESSION_TIMEOUT in common-cm.yaml, sourced from values.yaml under .Values.config.session_timeout.

Version 1.1.2

    Application Deployment Improvements
    → Introduced readinessProbe for NGINX using a status file (/app/status_running.sock) for better health signaling.
      Added lifecycle postStart and preStop hooks to manage the status file and gracefully shut down NGINX.
      Enabled Datadog APM/Profiling in the app container:
        DD_PROFILING_ENABLED: true
        DD_TRACE_SAMPLE_RATE: 1
        DD_DBM_PROPAGATION_MODE: full
        DD_TRACE_DELAYED_JOB_ENABLED: true

    WAF Integration Support in ALB Ingress
    → Introduced conditional support for AWS WAFv2 in ingress.yaml. 
      When enabled in values.yaml (ingress.alb.waf.enabled: true), the following annotation is added to the ALB Ingress:
      alb.ingress.kubernetes.io/wafv2-acl-arn: "<WAF_ACL_ARN_FROM_VALUES>"
      This allows integration with AWS WAF for added security at the load balancer level.

    PostgreSQL DBM Integration
    → Enhanced the datadog-dbm-postgres-service.yaml to include:
      Activity, statement, and function metrics collection.
      Datadog tag added with: customer, org, app, app_type, and app_version.

Version 1.1.3

    Maintenance mode changes
    → Wrapped resources like restart-cronjob.yaml, scaled-job.yaml, and scaled-object.yaml with conditional logic:
      global.enable_maintenance_mode to skip non-essential jobs in maintenance mode.
    
    Affinity & Scheduling Logic Updates
    → Added custom affinity rules to prefer:
        On-demand nodes and karpenter-managed pools.
      Conditional rendering of tolerations, nodeSelector, and affinity rules.

    Delayed Job Workoff Improvements
    → New Configurable Wait Logic Introduced:
        Added wait block in values.yaml with:
            enabled: Toggle wait mode for DJ worker.
            wait_time: Max time (in seconds) to wait with no jobs before exiting.
            sleep_interval: Polling interval between DJ job checks.
    Custom Rake Task (workoff_wait):
        Loops up to MAX_WAIT_TIME, processing jobs and waiting if none found.
        Resets timer when jobs are processed, improving job handling efficiency.
        Mounts workoff_wait.rake dynamically if wait.enabled: true.

    NGINX Configuration Updates
    → Replaced default image with nginx-with-headers-module for enhanced security headers.
      Security Enhancements:
      Added more_clear_headers, proxy_hide_header, and disabled server_tokens.
      Injected Strict-Transport-Security header.
      Refactored and extended the nginx.conf to support custom modules and better control.

Version 1.1.4

    Security Hardening Changes in nginx-cm.yaml
    → Header Sanitization
      Cipher Suite Enforcement
      Timeouts & Buffers
      Compression & Caching

Version 1.1.5

    Heimdall Database Configuration Support
    → Added conditional heimdall support in environment variables
      Added support to inject Heimdall proxy values when global.heimdall.enabled = true. This allows redirecting database traffic through the Heimdall proxy if enabled.
      Modified resources:
        create-db/templates/batch.yaml
        migrate-db/templates/batch.yaml
        worker/templates/scaled-job.yaml
      Injected env vars when heimdall.enabled is true: DATABASE_HOST , DATABASE_PORT , POSTGRES_HOST

Version 1.1.6

    Delayed Job Workoff with Graceful Shutdown
    → Added graceful signal handling (SIGTERM, SIGINT)
      forks child process to run Delayed::Worker.work_off in loop
      Automatically releases locked jobs back to queue on shutdown
      Enforces MAX_WAIT_TIME logic to terminate idle job runner
      Logs job IDs and cleanup status

    Backup DB Job Introduced
    → Added: New backup-db job for DB backups
    job implemented to:
        Perform a pg_dump of the database
        Upload the .dump file to S3 under DBDUMP/ path
        Clean up backup from local volume
    Conditional execution based on:
    global.enable_database_backup parameter

Version 1.1.7

    Fixed TLS support for TLS 1.3.
    → Included SSL Policy: ELBSecurityPolicy-TLS13-1-3-2021-06 and configuration in nginx-cm.

    Ingress & TLS Security Enhancements
    → Updated: ingress.yaml and nginx-cm.yaml
    Improved SSL Policy:
    Replaced ssl_ciphers (legacy cipher list)

Version 1.2.0

    Credentials improvement
    → Removed: AWS Secrets from Config and Secrets
    Added IAM role annotation to serviceAccount helper
    Removed AWS secrets from the common-secret file and added role-arn in the helper configuration.

Version 1.2.1

    Security & Network Enhancements
    → Ingress Config Update
    File: app/templates/ingress.yaml
    Change:
        Upgraded SSL policy:
            From: ELBSecurityPolicy-TLS13-1-2-2021-06
            To: ELBSecurityPolicy-TLS13-1-3-2021-06

    Nginx Configuration Hardened
    → TLS Protocols Improved
    File: nginx-cm.yaml
    Change:
        Removed: ssl_ciphers (legacy ciphers)
        Added:
            ssl_protocols TLSv1.3
            ssl_conf_command Ciphersuites TLS_AES_256_GCM_SHA384:TLS_AES_128_GCM_SHA256:TLS_CHACHA20_POLY1305_SHA256

    Migration Control Flag
    → File: migrate-db/templates/batch.yaml
    Added conditional freshdb logic:
        true → runs rails db:migrate_fresh
        false → default db:migrate
    default value:
        freshdb: false

