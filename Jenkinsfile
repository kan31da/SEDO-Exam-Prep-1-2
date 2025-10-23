pipeline {
    agent any

    stages {
        stage("Restore the dependencies") {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "feature/.*", comparator: "REGEXP"
                }
            }
            steps {
                bat 'dotnet restore'
            }
        }

        stage("Build the application") {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "feature/.*", comparator: "REGEXP"
                }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage("Run Unit and Integration Test") {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "feature/.*", comparator: "REGEXP"
                }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        success {
            echo '✅ Build and tests successful!'
        }
        failure {
            echo '❌ Build or tests failed.'
        }
    }
}
