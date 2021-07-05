@Library('jenkins-library@1.0.4') _

def tasks = [:]
tasks["nodejs"] = {
    stage ("Build cloud-computing hello-world"){
        def nativeImage = buildSimpleDocker_v2(dockerfileDir: 'cloud-computing',
                dockerImageRepositoryName: 'nodejs-hello-world', imageprivacy: 'public')
        sconeBuildAllTee(nativeImage: nativeImage, targetImageRepositoryName: 'nodejs-hello-world',
                sconifyArgsPath: 'cloud-computing/sconify.args')
    }
}
parallel tasks
