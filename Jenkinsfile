@Library('my-shared-library@main') _ 

pipeline {
    agent { label 'slave2' }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                pipeline1.checkout()
            }
        }

        stage('Set up Java 1') {
            steps {
                pipeline1.setupjava()
            }
        }

        stage('Set up Maven') {
            steps {
                pipeline1.setupmaven()
            }
        }

        stage('Build with Maven') {
            steps {
                pipeline1.setupbuild()
            }
        }

        stage('Upload Artifact') {
            steps {
                echo 'Uploading artifact...'
                pipeline1.uploadartifact(String artifactPath)
            }
        }

        stage('Run Application') {
            steps {
                pipeline1.runapplication()
            }
        }

        stage('Validate App is Running') {
            steps {
                pipeline1.validateapp()
            }
        }

        stage('Keeping application up for 2 mins') {
            steps {
                pipeline1.keepapp()
            }
        }

        stage('Gracefully Stop Spring Boot App') {
            steps {
                pipeline1.stopapp()
            }
        }
    }

    post {
        always {
            pipeline1.cleanapp() 
		}
    }
}
