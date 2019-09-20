# quickstart-bitnami-wordpress
## WordPress High Availability by Bitnami on the AWS Cloud

This Quick Start deploys WordPress High Availability by Bitnami, which includes WordPress and Amazon Aurora, in a highly available environment on AWS in about 40 minutes.

WordPress is a web publishing platform for building blogs and websites. It can be customized via a wide selection of themes, extensions, and plugins. WordPress High Availability by Bitnami installs the WordPress application on multiple servers (Amazon EC2 instances) in the AWS Cloud for high performance and availability. It also sets up an Aurora relational database to help you reduce costs, simplify configuration tasks, and scale with ease. The database and WordPress application are set up on different EC2 instances to help improve security and access control. Optionally, you can deploy an Amazon ElastiCache for Memcached server to cache database queries.


The Quick Start offers two deployment options:

- Deploying WordPress High Availability by Bitnami into a new virtual private cloud (VPC) on AWS
- Deploying WordPress High Availability by Bitnami into an existing VPC on AWS

You can also use the AWS CloudFormation templates as a starting point for your own implementation.

![Quick Start architecture for WordPress High Availability by Bitnami on AWS](https://d0.awsstatic.com/partner-network/QuickStart/datasheets/bitnami-wordpress-on-aws-architecture.png)

For architectural details, best practices, step-by-step instructions, and customization options, see the 
[deployment guide](https://fwd.aws/arqWN).

To post feedback, submit feature ideas, or report bugs, use the **Issues** section of this GitHub repo.
If you'd like to submit code for this Quick Start, please review the [AWS Quick Start Contributor's Kit](https://aws-quickstart.github.io/). 

## Notable changes

### 5.2.3-0 (2019/09/08)

https://github.com/aws-quickstart/quickstart-bitnami-wordpress/commit/511126369dc4e543c3cc12df17e8ebb3836a628e
* This release fixes a bug in PHP-FPM's Logrotate configuration which could cause high disk space and/or inodes usage, if logs were rotated multiple times. Existing users can fix it by running the commands below:

      $ sudo rm -rf /opt/bitnami/php/logs/*
      $ sudo sed -i 's/\* /*.log /' /etc/logrotate.d/com.bitnami.php

  The */etc/logrotate.d/com.bitnami.php* configuration file should look like this:

      /opt/bitnami/php/logs/*.log {
        weekly
        rotate 150
        dateext
        compress
        copytruncate
        missingok

      }
