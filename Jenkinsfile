@Library('global-jenkins-library@2.3.1') _

buildInfo = getBuildInfo()

baseDir = 'cloud-computing'
def nativeImage = buildSimpleDocker_v3(
        buildInfo: buildInfo,
        dockerfileDir: baseDir,
        buildContext: baseDir,
        dockerImageRepositoryName: 'nodejs-hello-world',
        visibility: 'docker.io'
)

stage('Build Gramine') {
    gramineBuildInfo = buildInfo.clone()
    dockerfileDir = baseDir + '/gramine'
    dockerImageRepositoryName = 'tee-nodejs-hello-world'
    gramineBuildInfo.imageTag += '-gramine'
    visibility = 'iex.ec'
    productionImageName = ''
    stage('Build Gramine production image') {
        productionImageName = buildSimpleDocker_v3(
            buildInfo: gramineBuildInfo,
            dockerfileDir: dockerfileDir,
            buildContext: baseDir,
            dockerImageRepositoryName: dockerImageRepositoryName,
            visibility: visibility
        )
    }
    stage('Build Gramine test CA Gramine image') {
        testCaSuffix = 'test-ca'
        gramineBuildInfo.imageTag += '-' + testCaSuffix
        buildSimpleDocker_v3(
            buildInfo: gramineBuildInfo,
            dockerfileDir: dockerfileDir,
            dockerfileFilename: 'Dockerfile.' + testCaSuffix,
            dockerBuildOptions: '--build-arg BASE_IMAGE=' + productionImageName,
            dockerImageRepositoryName: dockerImageRepositoryName,
            visibility: visibility
        )
    }
}

sconeBuildUnlocked(
        nativeImage: nativeImage,
        imageName: 'nodejs-hello-world',
        imageTag: buildInfo.imageTag,
        sconifyArgsPath: baseDir + '/sconify.args',
        sconifyVersion: '5.7.1'
)
