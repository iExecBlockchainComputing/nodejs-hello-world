@Library('global-jenkins-library@1.9.0') _

buildInfo = getBuildInfo()

def nativeImage = buildSimpleDocker_v2(
  buildInfo: buildInfo,
  dockerfileDir: 'cloud-computing',
  dockerImageRepositoryName: 'nodejs-hello-world',
  imageprivacy: 'public'
)

sconeBuildUnlocked(
  nativeImage:     nativeImage,
  imageName:       'nodejs-hello-world',
  imageTag:        buildInfo.imageTag,
  sconifyArgsPath: 'cloud-computing/sconify.args',
  sconifyVersion:  '5.7.1'
)
