pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                git branch: 'main', url: 'https://github.com/example/repo.git'
            }
        }
        
        stage('Check Version Number') {
            steps {
                script {
                    def jsonFile = readJSON file: 'path/to/json/file.json'
                    def versionString = jsonFile.version
                    def versionNumber = versionString.replaceAll('[^\\d.]', '')
                    println "Version Number: ${versionNumber}"
                }
            }
        }
    }
}
