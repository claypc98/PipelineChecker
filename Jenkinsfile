pipeline {
    agent any

    tools {
        git 'git'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/claypc98/data-design.git'
            }
        }

        stage('Check Version Number') {
            steps {
                script {
                    def jsonFile = readJSON file: 'design/test_model.json'
                    def versionString = jsonFile.version
                    def versionNumber = versionString.replaceAll('[^\\d.]', '')
                    println "JSON File Version Number: ${versionNumber}"

                    def gitRepoPath = "${env.WORKSPACE}/application"
                    sh "git clone https://github.com/claypc98/application.git ${gitRepoPath}"
                    def sqlFiles = sh(script: "ls ${gitRepoPath}/sql", returnStdout: true).trim().split('\n')
                    def latestNumber = 0
                    sqlFiles.each { file ->
                        def number = file.replaceAll('[^\\d]', '').toInteger()
                        if (number > latestNumber) {
                            latestNumber = number
                        }
                    }
                    println "SQL File Latest Number: ${latestNumber}"

                    if (versionNumber == latestNumber.toString()) {
                        println "Version number matches the latest SQL file number"
                    } else {
                        println "Version number does not match the latest SQL file number"
                    }
                }
            }
        }
    }
}
