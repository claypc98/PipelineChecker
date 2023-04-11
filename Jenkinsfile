pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                git branch: 'main', url: 'https://github.com/claypc98/data-design.git'
            }
        }
        
        stage('Check Version Number') {
            steps {
                script {
                    def jsonFile = readJSON file: 'data-design/design/test_model.json'
                    def versionString = jsonFile.version
                    def versionNumber = versionString.replaceAll('[^\\d.]', '')
                    println "Version Number: ${versionNumber}"
                }
            }
        }
    }
}
