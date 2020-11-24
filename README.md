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

Exemplu pentru SQL:
uses: mattes/gce-cloudsql-proxy-action@v1
with:
  creds: ${{ secrets.GOOGLE_APPLICATION_CREDENTIALS }}
  instance: my-project:us-central1:instance-1

Exemplu pentru incarcarea de fisiere in GCS:
For uploading a file

steps:
  - id: upload-file
    uses: google-github-actions/upload-cloud-storage@main
    with:
      path: /path/to/file
      destination: bucket-name/file

   Example of using the output
  - id: uploaded-files
    uses: foo/bar@master
    env:
      file: ${{steps.upload-file.outputs.uploaded}}

The file will be uploaded to gs://bucket-name/file
For uploading a folder

steps:
  - id: upload-files
    uses: google-github-actions/upload-cloud-storage@main
    with:
      path: /path/to/folder
      destination: bucket-name

   Example of using the output
  - id: uploaded-files
    uses: foo/bar@master
    env:
      files: ${{steps.upload-files.outputs.uploaded}}
Exemplu de cod pentru dezvoltarea de funtii google cloud:
steps:
- id: deploy
  uses: google-github-actions/deploy-cloud-functions@main
  with:
    name: my-function
    runtime: nodejs10
    credentials: ${{ secrets.gcp_credentials }}

Example of using the output
- id: test
  run: curl "${{ steps.deploy.outputs.url }}"




