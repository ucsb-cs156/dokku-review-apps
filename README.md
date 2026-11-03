Getting Started With Review Apps:

## Organization Level Secrets
For convenience, you'll need to configure the following actions secrets at the organizational level. Go to this url, substituting `<your-organization>` for your GitHub Organization:
```
https://github.com/organizations/<your-organization>/settings/secrets/actions
```

Add the following secrets:
- `SSH_USERNAME`: Set this to the username for the service account on Dokku; For CS156 this is `dokkudeploy`.
- `PORT`: Set to 22 unless instructed otherwise.

## Organization Level OIDC
Our implementation of OpkSSH requires a custom OIDC sub template. This can be set on the organization level at this page, replacing `<your-organization>` for your GitHub organization:
```
https://github.com/organizations/<your-organization>/settings/actions/oidc-configuration
```

Set the subject claim template to `repo, job_workflow_ref` and ensure that "Use Immutable Subject Claim" is enabled.
<img width="1496" height="1005" alt="image" src="https://github.com/user-attachments/assets/52ee81fd-3f0e-49a4-9704-58b2f89cebf0" />


## Repo Level Variables
You'll need the two following GitHub Actions Variables. These are usually set at the repository level (under settings -> secrets and variables -> actions -> variables):
- `HOST_URL`: This is the base DNS name for the dokku server that's been configured for Review Apps, for example `dokku-00.cs.ucsb.edu`.
- `TEMPLATE_APP_NAME`: This variable points to a valid app on the Dokku server that you'd like to serve as the base template for Review Apps.

## Setting up a template app
To set up a template app, set up the app as you normally would; Follow all of the app-specific steps. You only need to add one additional env var:
```bash
dokku config:set --no-restart <template-app-name> IS_TEMPLATE_APP=true
```

## Using Keycloak with Review Apps
To use keycloak with Review apps, for now, you'll need wildcard credentials. For information on issuing them, see [here](https://ucsb-cs156.github.io/topics/keycloak/qa_deployment_with_keycloak.html#need-to-issue-keycloak-credentials-look-here)
