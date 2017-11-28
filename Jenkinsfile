pipeline {
    agent {
        docker {
            image 'minotaurinc/linux:latest'
            args '-v ${WORKSPACE}:/source/'
        }
    }

    stages {
        stage('Build') {
            steps {
                sh 'mkdir -p src/; mv * .* src/ || true;'
                sh 'cd src; build-deb.sh'
            }
        }
        stage("Archive Build Artifacts") {
            steps {
                archiveArtifacts allowEmptyArchive: true, artifacts: '**/*.deb', fingerprint: true
            }
        }
    }

    post {
        always {
            deleteDir()
        }
    }
}
