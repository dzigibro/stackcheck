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
        stage('Validate Inventory') {
    steps {
        sh 'ansible-inventory -i ansible/inventory.ini --list'
    }
}

        stage('Deploy to VM with Ansible') {
            steps {
                sh '''
                     ANSIBLE_HOST_KEY_CHECKING=False \
                     ansible-playbook -i ansible/inventory.ini ansible/deploy_stackcheck.yml
                                                                                               '''
            }
        }
    }
}
