@Library('global-jenkins-library@2.3.1') _

buildInfo = getBuildInfo()

baseDir = 'cloud-computing'

buildSimpleDocker_v3(
        buildInfo: buildInfo,
        dockerfileDir: baseDir,
        buildContext: baseDir,
        dockerImageRepositoryName: 'nodejs-hello-world',
        visibility: 'iex.ec'
)
