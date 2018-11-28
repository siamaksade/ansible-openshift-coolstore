Ansible Role: CoolStore Demo on OpenShift
[![Build Status](https://travis-ci.org/siamaksade/ansible-openshift-coolstore.svg?branch=master)](https://travis-ci.org/siamaksade/ansible-openshift-coolstore)
=========

Ansible Role for deploying [CoolStore Microservices](https://github.com/jbossdemocentral/coolstore-microservice.git) demo on OpenShift

Role Variables
------------

| Variable                         | Default Value              | Description   |
|-------------------------------   |----------------------------|---------------|
|`src_github_account`                  | jbossdemocentral           | GitHub account for [coolstore microservice code](https://github.com/jbossdemocentral/coolstore-microservice.git) |
|`src_github_ref`                      | master                     | GitHub repo branch for [coolstore microservice code](https://github.com/jbossdemocentral/coolstore-microservice.git) |
|`maven_mirror_url`                | -                          | Maven repository mirror url |
|`keep_build_configs`              | true                       | Do not remove the buildconfigs after build completes |
|`bluegreen_image`                 | inventory                  | Image name to promote to blue and green versions  |
|`prune_deployments_selector`      | -                          | Remove deployments using this selector after deployment  |
|`prune_deployments_selector_prod` | -                          | Remove deployments in prod project using this selector after deployment  |
|`prune_deployments_selector_stage`| -                          | Remove deployments in stage project using this selector after deployment  |
|`prune_builds_selector`           | -                          | Remove builds using this selector after deployment  |
|`enable_cicd`                     | true                       | Enable CI/CD for CoolStore |
|`project_cicd`                    | cicd                       | CI/CD project name |
|`project_prod`                    | coolstore-prod             | Prod project name |
|`project_prod_name`               | CoolStore PROD             | Prod project display name |
|`project_prod_desc`               | CoolStore PROD Environment | Prod project description |
|`project_stage`                   | coolstore-test             | Prod project name |
|`project_stage_name`              | CoolStore TEST             | Prod project display name |
|`project_stage_desc`              | CoolStore TEST Environment | Prod project description |
|`project_test`                    | coolstore-test             | Prod project name |
|`project_test_name`               | CoolStore DEV              | Prod project display name |
|`project_test_desc`               | CoolStore DEV Environment  | Prod project description |
|`project_dev`                     | developer                  | Prod project name |
|`project_dev_name`                | Developer Project          | Prod project display name |
|`project_dev_desc`                | Personal Developer Project | Prod project description |
|`project_default`                 | coolstore                  | Default project name |
|`project_default_name`            | CoolStore MSA              | Default project display name |
|`project_default_desc`            | CoolStore MSA              | Default project description |
|`project_annotations`             | demo=demo-modern-arch      | Project annotations |
|`project_admin`                   | -                          | The user to assign as project admin, if running the playbooks as system:admin |
|`project_join_with`               | cicd                       | Join project networks with *cicd* project |
|`prebuilt_images_project_name`    | coolstore-image-builds     | Project name for pre-built coolstore container images. If images exist, the won't be rebuilt during deployment |
|`disable_stage_project`           | false                      | If true, disable stage project and promote apps from DEV to PROD |
|`gogs_hostname`                   | gogs-gogs.127.0.0.1.nip.io | Gogs git server hostname |
|`gogs_admin_user`                 | gogs                       | Gogs admin user |
|`gogs_admin_password`             | gogs                       | Gogs admin password |
|`gogs_user`                       | developer                  | Gogs user |
|`gogs_password`                   | developer                  | Gogs password |
|`openshift_master`                | 127.0.0.1.nip.io:8443      | OpenShift master url |
|`hostname_suffix`                 | apps.127.0.0.1.nip.io      | Route suffix for containers on OpenShift | 
|`openshift_cli`                   | oc                         | OpenShift CLI command and arguments (e.g. auth)       | 

OpenShift Version Compatibility
------------
When listing this role in `requirements.yml`, make sure to pin the version of the role via one of the tags:

```
- src: siamaksade.openshift_coolstore
  version: 1.3.0
```  

The following tables shows the version combinations that are tested and verified:

| Role Version      | OpenShift Version |
|-------------------|-------------------|
| 1.0.x   | 3.7.x   |
| 1.1.x   | 3.9.x   |
| 1.2.x   | 3.10.x  |
| 1.3.x   | 3.11.x  |

Note that if a version combination is not listed above, it does **NOT** mean that it won't work on that 
version. The above table is merely the combinations that we have verified and tested.


Example Playbook
------------

```
name: Example Playbook
hosts: localhost
tasks:
- import_role:
    name: siamaksade.openshift_coolstore
  vars:
    project_name: "coolstore"
    openshift_cli: "oc --server http://master:8443"
```