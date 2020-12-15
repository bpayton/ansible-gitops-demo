# ansible-gitops-demo

This demo uses Ansible Tower's ability to provide a webhook interface to a job template, or workflow template, and integrates provisioning, build, and deploy job templates in a workflow triggered by a Github push event.  Please don't use this in production.  This demo uses a simple NodeJS web application as an example, but the playbooks could be modified to accommodate many build/deploy processes.  

## Requirements
Ansible Tower 3.7.x (should work with 3.8 but untested) 
  RHPDS ideally so you get code-server

AWS account with permissions to create ec2 instances

AWS Access and Secret keys for account

An existing security group in AWS with port 22 and 80 open (default should be fine for this)

## Steps to setup demo - the automated version, finally!
1. SSH to your tower host, or use the included Code-Server VS Code instance provided by RHPDS
2. Clone this repo into your studentX home folder 
3. update login_info.yml with your ansible password, and your AWS keys, security token and the ssh key
4. update group_vars/all.yml with your name instead of mine 
5. run `ansible-galaxy collection install awx.awx` to get the needed tools to setup the demo
6. Run `ansible-playbook demo_setup.yml` to create the project, inventories, credentials, playbooks and a basic workflow.
7. On the workflow template, enable the webhook and select the GitHub type, then save, it will generate the url and token you'll need in the next step.  
8. On the [simple-web-app](https://github.com/corumj/simple-demo-app) git repo (fork it so you can make changes to it yourself) setup a webhook according to Github's instructions and copy and paste the webhook URL for your Tower Webhook.  Be prepared, it will kick of the webhook instantly as a test, make sure in the response you get a `{"message": "Job queued."}` response and check in Tower to make sure the workflow is running.
