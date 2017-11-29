apiVersion: v1
kind: Template
labels:
metadata:
  annotations:
    description: Jenkins Pipeline for process automation
    iconClass: icon-java
  name: jenkins-pipeline
objects:
- kind: BuildConfig
  apiVersion: v1
  metadata:
    labels:
      app: cicd-pipeline
      name: cicd-pipeline
    name: cicd-pipeline
    annotations:
      pipeline.alpha.openshift.io/uses: '[{"name": "jenkins", "namespace": "", "kind": "DeploymentConfig"}]'
  spec:
    triggers:
      - type: GitHub
        github:
          secret: ${WEBHOOK_SECRET}
      - type: Generic
        generic:
          secret: ${WEBHOOK_SECRET}
    runPolicy: Serial
    source:
      type: Git
      git:
        uri: 'http://gogs:3000/gogs/application.git'
        ref: master
    strategy:
      type: JenkinsPipeline
      jenkinsPipelineStrategy:
        jenkinsfilePath: Jenkinsfile
        env:
        - name: "TEST_PROJECT_PARAM"
          value: "${TEST_PROJECT}"
        - name: "PROD_PROJECT_PARAM"
          value: "${PROD_PROJECT}"
    output: {}
    resources: {}
    postCommit: {}
    nodeSelector: {}
  status:
    lastVersion: 1
