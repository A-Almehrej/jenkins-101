pipeline {
  // Select which agent to run this job on
  // Uses agent labeling
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    triggers {
        // Poll every minute - if there're changes, runs pipeline
        pollSCM '* * * * *'
    }
  // Stages contain each stage which can be further broken down into steps
  // If an upstream (previous) stage fails, all downstream (subsequent) stages will fail.
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                // Runs a shell command
                // Install required python libraries
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                // Run the python script in both modes (default param/customer param)
                sh '''
                cd myapp
                python3 hello.py
                python3 hello.py -- name=Abe
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}