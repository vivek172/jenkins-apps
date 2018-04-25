node('master') {
    docker.withServer('unix:///var/run/docker.sock') {
        stage('Git clone') {
            git 'git@github.com:vivek172/jenkins-apps.git'
        }
        stage('Build') {
            docker
                .image('jenkins-agent-ubuntu')
                .inside('--volumes-from jenkins-master') {
                    sh "bash ./build.sh;"
                }
        }
        stage('Copy build results') {
            docker
                .image('jenkins-agent-ubuntu')
                .inside('--volumes-from jenkins-master') {
                    sh "bash ./build.sh;"
                }
        }
        stage('UI unit tests') {
            docker
                .image('jenkins-agent-ubuntu')
                .inside('--volumes-from jenkins-master') {
                    sh "bash ./build.sh;"
                }
        }
    }
}