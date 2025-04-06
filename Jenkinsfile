pipeline {
    agent any

    parameters {
        booleanParam (name: 'sonarScan', defaultValue: true, description: 'To run scan in pipeline')
        
    }
    
    stages {
        stage ("code") {
            steps {
                echo "coding completed"
            }
        }
        stage ("build") {
            steps {
            echo "building completed"
            }
        }
        stage ("test") {
            steps {
             echo "testing completed"  
            }     
        }
        stage ("depoly") {
            steps {
            echo "deploying code"  
            }
        }
    }
}