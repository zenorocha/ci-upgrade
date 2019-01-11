# CI Upgrade

> This repository contains the code and instructions used to upgrade users to the latest CI version.

## Instructions

**A) Deploy new version of the CI service**


```sh
curl -X POST "https://api.us-west-1.liferay.cloud/projects/<PROJECT_ID>/build" \
     -u "<YOUR_EMAIL>:<YOUR_PASSWORD>" \
     -H "Content-Type: application/json" \
     -d $'{
  "masterToken": "<PROJECT_MASTER_TOKEN>",
  "provider": "github",
  "repository": "https://github.com/dxpcloud/ci-upgrade"
}'
```

**B) Remove extra environment variables**

1. Go to the `Environments Variables` tab of the infra service
2. Remove the following variables:
	* GITHUB_TOKEN
	* JENKINS_ADMIN_PASSWORD
	* JENKINS_SMTP_AUTH_PASSWORD
	* JENKINS_SMTP_AUTH_USER_NAME
	* JENKINS_SMTP_HOST
	* JENKINS_SMTP_PORT
	* JENKINS_SMTP_USE_SSL
	* WEDEPLOY_LIFERAY_COM_PASSWORD
	* WEDEPLOY_LIFERAY_COM_USER

**C) Make CI service available to the user**

```sh
curl -X PATCH "https://api.us-west-1.liferay.cloud/projects/<PROJECT_ID>" \
     -u "<YOUR_EMAIL>:<YOUR_PASSWORD>" \
     -H "Content-Type: application/json" \
     -d $'{"metadata": {"hide": false}}'
```
