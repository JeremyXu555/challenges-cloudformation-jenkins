[![LinkedIn](https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/linkedin.png)](https://www.linkedin.com/in/dennyzhang001) <a href="https://www.dennyzhang.com/slack" target="_blank" rel="nofollow"><img src="http://slack.dennyzhang.com/badge.svg" alt="slack"/></a> [![Github](https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/github.png)](https://github.com/DennyZhang)

File me [tickets](https://github.com/DennyZhang/challenges-cloudformation-jenkins/issues) or star [the repo](https://github.com/DennyZhang/challenges-cloudformation-jenkins).

<a href="https://github.com/DennyZhang?tab=followers"><img align="right" width="200" height="183" src="https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/fork_github.png" /></a>

Table of Contents
=================

   * [Requirements](#requirements)
   * [Procedures](#procedures)

<a href="https://www.dennyzhang.com"><img src="https://raw.githubusercontent.com/DennyZhang/challenges-cloudformation-jenkins/master/images/jenkins_vm_aio.png"/> </a>

# Requirements
1. Start 1 jenkins master and 1 jenkins slave
2. Jenkins master offload request to jenkins slave

# Procedures
[![Launch](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=aws-jenkins&templateURL=https://s3.amazonaws.com/aws.dennyzhang.com/cf-jenkins-main-401.yml)

- Use CF to setup the env
```
export STACK_NAME="aws-jenkins"
export TMP_FILE="file://cf-jenkins-main-401.yml"

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
