/* Jaskaran Saini | A01055847 | 8 December 2021
    This is a pipeline that builds a java application,
    checks for code quality, runs tests,
    and runs the build jar file then returns the build results */

pipeline {
    agent any
    
    parameters {
        booleanParam(defaultValue: false, description: 'Whether to Run the Code', name: 'RUN') 
        stringParam(defaultValue: "Development", description: 'Type of build', name: 'BUILD_TYPE') 
    }

    stages {
        stage('Build') {
            steps {
                echo "Pipeline by: Jaskaran Saini | A01055847 | Group 25"
                echo 'Starting Java Build...'
                sh "mvn -B -DskipTests clean install"
                echo 'Java Build Complete.'
            }
        }
        stage('Code Quality') {
            steps {
                sh "wc -l src\main\java\com\mycompany\app\App.java"
            }
        }
        stage("Test") {
            steps {
                sh "mvn test"
            }
            post {
                when {
                    BUILD_TYPE == 'Development'
                }
                steps 
                    junit 'target/*.xml'
                }
            }
        }
        stage('Run') {
            when {
                RUN == true
            }
            steps {
                sh 'chmod +x deliver.sh'
                sh './deliver.sh'
            }
        }
        stage("Build Results") {
            echo "Build ${BUILD_TYPE} completed successfully"
            echo "I have now completed ACIT 4850! yaaahh...."
        }
    }
}