pipeline {
    agent {
        label "windows"
    }

    tools {
        git 'git'
    }

    stages {
        stage('Checkout') {
            steps {
                bat 'git clone https://github.com/claypc98/data-design.git'
            }
        }

        stage('Check Version Number') {
            steps {
                script {
                    def jsonFile = readJSON file: 'data-design/design/test_model.json'
                    def versionString = jsonFile.version
                    def versionNumber = versionString.replaceAll('[^\\d.]', '')
                    println "JSON File Version Number: ${versionNumber}"

                    def gitRepoPath = "${env.WORKSPACE}/application"
                    bat "git clone https://github.com/claypc98/application.git ${gitRepoPath}"
                    def sqlFiles = bat(script: "dir /B ${gitRepoPath}\\sql", returnStdout: true).trim().split('\r?\n')
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
