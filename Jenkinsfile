pipeline {
    agent any
    parameters {
        string name: 'systemTestList',
            defaultValue: '',
            trim: true,
            description: '''Comma-separated list of system test(s) to build and run
                during the 'Build/run System Tests' stage. Leaving this blank
                runs all tests.'''
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Test') {
            steps {
                script {
                    systemTestListArg = ''
                    if (params.systemTestList) {
                        systemTestListArg = "-DTEST_LIST=${params.systemTestList}"
                    }
                }
                echo "call buildRunSystemTests.cmd ${systemTestListArg}"
            }
        }
    }
    post {
        always {
            echo "This build done: ${env.BUILD_URL}"
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
