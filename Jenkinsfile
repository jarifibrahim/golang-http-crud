@Library('github.com/fabric8io/osio-pipeline@master') _

osio {

  config runtime: 'node'

  ci {

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources

  }

  cd {

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    def cm = loadResources(file: ".openshiftio/service.yaml")

    // performs an s2i build
    build resources: [resources]
    deploy resources: [resources,  cm], env: 'stage'
    deploy resources: [resources,  cm], env: 'run', approval: 'manual'
  }
}
