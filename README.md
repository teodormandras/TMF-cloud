# TMF-cloud
Exmplu de cod pentru App engine:



common:
  labels:
    gitsha: ${{GITHUB_SHA}}

deploys:
  - name: my-app-deploy
    region: us-central1
    instance_group: my-app-instance-group
    instance_template_base: my-app-instance-template-base
    instance_template: my-app-${{GITHUB_RUN_NUMBER}}-${{GITHUB_SHA}}
    cloud_init: cloud-init.yml # see example dir
    labels: # will also have gitsha from common section
      version: ${{APP_VERSION}}
    tags:
      - my-tag123
    update_policy:
      min_ready_sec: 30

delete_instance_templates_after: false

Exemplu de cod pentru app engine:
- name: Deploy to Google App Engine
  uses: atRobertoFlores/gae_deploy_action@master
  with:
    service_account: ${{ secrets.SERVICE_ACCOUNT }}
    project_name: ${{ secrets.PROJECT_NAME }}
