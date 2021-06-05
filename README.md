 # aws-template

This template is the result of completing the course [The Good Parts of AWS](https://www.educative.io/courses/good-parts-of-aws), offered through [educative.io](https://www.educative.io), and lots of personal time spent debugging.

The original objective of this repo was to create a scalable infrastructure-as-code solution for a project codenamed [Bondfire](https://bitbucket.org/software-amigos/). Ultimately the project was too ambitious and fizzled out, but this CloudFormation template was one of the features that reached fruition. 

Use this repository to bootstrap an AWS environment with staging and production environments, application load balancers, auto-scaling groups, port-forwarding, subnets, NAT gateway, HTTPS, and CI/CD pipeline via CloudFormation.

### Prerequisites:
1) AWS account; you can [create one here](https://portal.aws.amazon.com/billing/signup).
2) User with IAM administrator access, or follow [these directions](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html).
3) AWS CLI version 2; download can be [accessed from here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html).
4) CLI profile configured. [Instructions are here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html). Note: the profile referenced in this repository is bondfireCLI; you can name your profile whatever you like, just be sure to change references to bondfireCLI when you fork the code.
5) Register a domain through Amazon or migrate an existing domain's DNS to AWS's Route 53 by following [these instructions](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/MigratingDNS.html) and then [set up a hosted zone](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/migrate-dns-domain-in-use.html) with the default NS and SOA records.
6) [Create a TLS certificate](https://console.aws.amazon.com/acm) for the domain to enable HTTPS. 

### Run the template:
0) Fork this repository.
1) Change references to "bondfire" and "bondfireCLI" in `deploy-infra.sh` to the stack name and CLI profile name you'd prefer, respectively. Then update the domain environment variable to the domain name that you set up the hosted zone.
2) Create a new [GitHub access token](https://github.com/settings/tokens/new). Give it `repo` and `admin:repo_hook` permissions. Take note of the token value, we'll need it next step. 
3) The deploy-script needs environmental variables, so prepare them with the following code (replace the values inside the \<>): 
```
mkdir -p ~/.github
echo "aws-template" > ~/.github/aws-template-repo
echo "<github username>" > ~/.github/aws-template-owner
echo "<access token>" > ~/.github/aws-template-access-token
```
4) Run the `deploy-infra.sh` script. If it is not executable, change the permissions by running `chmod +x deploy-infra.sh` within its directory.
5) You'll need to either use the AWS console to SSH into your EC2 instances or use the [SSM plugin for the AWS CLI](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html).