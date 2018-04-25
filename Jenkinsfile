node('master') {
    docker.withServer('unix:///var/run/docker.sock') {
        stage('Git clone') {
            git 'git@github.com:vivek172/jenkins-apps.git'
        }
        stage('Build') {
            docker
                .image('jenkins-agent-ubuntu')
                .inside('--volumes-from jenkins-master') {
                    echo "Run build scripts here"
                }
        }
        stage('Copy build results') {
            docker
                .image('jenkins-agent-ubuntu')
                .inside('--volumes-from jenkins-master') {
                    sh """
                        sshpass -plol scp \
                            "${WORKSPACE}/build/*.tar.gz" \
                            "backup@1.1.1.1:/build";
                    """
                }
        }
        stage('UI unit tests') {
            docker
                .image('jenkins-agent-ubuntu')
                .inside('--volumes-from jenkins-master') {
                    sh """
                        cd ./tests;
                        bash ./run.sh;
                    """
                }
        }
    }
}