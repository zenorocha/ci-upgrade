# CI Upgrade

> This repository contains the code and instructions used to upgrade users to the latest CI version.

## Instructions

A) Deploy new version of the CI service


```sh
curl -X POST "https://api.us-west-1.liferay.cloud/projects/<PROJECT_ID>/build" \
	 -u "<YOUR_EMAIL>:<YOUR_PASSWORD>" \
     -H "Content-Type: application/json" \
     -d $'{
  "masterToken": "<PROJECT_MASTER_TOKEN>",
  "provider": "github",
  "repository": "https://<GITHUB_TOKEN>@github.com/dxpcloud/ci-upgrade"
}'
```

B) Remove extra environment variables

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

C) Remove hidden definition

```sh
curl -X POST "https://api.us-west-1.liferay.cloud/projects" \
	 -u "<YOUR_EMAIL>:<YOUR_PASSWORD>" \
     -H "Content-Type: application/json" \
     -d $"{\"projectId\": \"<PROJECT_ID>\", \"metadata\": {\"repository\": \"https://github.com/<GITHUB_OWNER>/<PROJECT_ID>\", \"type\": \"non-production\"}}"
```