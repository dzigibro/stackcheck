pipeline {
    agent any

    stages {

        stage('Checkout Source') {
    steps {
        checkout([
            $class: 'GitSCM',
            branches: [[name: '*/main']],
            userRemoteConfigs: [[
                url: 'https://github.com/dzigibro/stackcheck.git',
                credentialsId: 'JenkinsGIT'
            ]]
        ])
    }
}

        stage('Debug Workspace') {
            steps {
                sh 'ls -al'
                sh 'ls -al ansible || echo "ansible directory missing"'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t noopoo/stackcheck:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    sh 'docker push noopoo/stackcheck:latest'
                }
            }
        }

        stage('Deploy to VM with Ansible') {
            steps {
                sh 'ansible-playbook -i ansible/hosts.ini ansible/deploy_stackcheck.yml'
                sh 'ls -la'
            }
        }
    }
}
