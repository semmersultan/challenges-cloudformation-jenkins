Table of Contents
=================

   * [Requirements](#requirements)
   * [Procedures](#procedures)
   * [More Resources](#more-resources)

<a href="https://www.dennyzhang.com"><img src="https://raw.githubusercontent.com/DennyZhang/challenges-cloudformation-jenkins/master/images/jenkins_ecs_2nodes.png"/> </a>

# Requirements
1. Start ECS with 2 node
2. Start Jenkins service with 2 instances in ECS. One for master, one for slave.
3. Enable ALB for Jenkins master

# Procedures
[![Launch](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=aws-jenkins&templateURL=https://s3.amazonaws.com/aws.dennyzhang.com/cf-jenkins-main-502.yml)

- Use CF to setup the env
```
export STACK_NAME="aws-jenkins"
export TMP_FILE="file://cf-jenkins-main-502.yml"

[ -n "$SSH_KEY_NAME" ] || export SSH_KEY_NAME="YOUR_SSH_KEYNAME_CUSTOMIZE"
aws cloudformation create-stack --template-body "$TMP_FILE" \
    --stack-name "$STACK_NAME" --parameters \
    ParameterKey=JenkinsUser,ParameterValue=username \
    ParameterKey=JenkinsPassword,ParameterValue=mypassword \
    ParameterKey=KeyName,ParameterValue=$SSH_KEY_NAME
```

```
aws cloudformation delete-stack --stack-name "$STACK_NAME"
```
<a href="https://www.dennyzhang.com"><img align="right" width="185" height="37" src="https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/dns_small.png"></a>

- Verify Jenkins
curl -I http://$server_ip:8080

# More Resources
- https://shuaib.me/ecs-jenkins/
