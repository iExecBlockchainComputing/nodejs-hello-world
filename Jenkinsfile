@Library('global-jenkins-library@2.3.0') _

buildInfo = getBuildInfo()

baseDir = 'cloud-computing'
def nativeImage = buildSimpleDocker_v3(
        buildInfo: buildInfo,
        dockerfileDir: baseDir,
        buildContext: baseDir,
        dockerImageRepositoryName: 'nodejs-hello-world',
        visibility: 'docker.io'
)

buildSimpleDocker_v3(
        buildInfo: buildInfo,
        dockerfileDir: baseDir + '/gramine',
        buildContext: baseDir,
        dockerImageRepositoryName: 'tee-gramine-nodejs-hello-world',
        visibility: 'iex.ec'
)

sconeBuildUnlocked(
        nativeImage: nativeImage,
        imageName: 'nodejs-hello-world',
        imageTag: buildInfo.imageTag,
        sconifyArgsPath: baseDir + '/sconify.args',
        sconifyVersion: '5.7.1'
)
