
Set up Let's Encrypt certs on an Elastic Beanstalk instance, using Route 53 for domain validation.

* *.ebextensions/01_setup.config* - opens up port 443 in AWSEBSecurityGroup, adds route 53 role permissions.
* *.ebextensions/03_cron.config* schedules the renewal, optionally posts messages to a slack web hook.
* *.platform/nginx/conf.d/https.conf.pre* - https config with placeholders for the key locations.
* *.platform/hooks/predeploy/01-certbot.sh* installs/runs certbot, configures `/etc/nginx/conf.d/https.conf`.

Designed to work with Python 3.7 running on 64bit Amazon Linux 2 (nginx).

![](eb_python_37.png)

Takes two configuration environment variables `CERT_DOMAIN` and `SLACK_WEB_HOOK`.

![](eb_python_env.png)

Handy references:
 * https://certbot.eff.org/docs/using.html
 * https://certbot-dns-route53.readthedocs.io/en/stable/
 * https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux-extend.html
 
Lots of inspiration from: https://github.com/Archinowsk/konsti-server/tree/master/.ebextensions
