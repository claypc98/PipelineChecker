pipeline {
    agent any

  

    stages {
      stage('Checkout') {
    steps {
        git branch: 'main',  url: 'https://github.com/example/your-repo.git'
        dir('application') {
            git branch: 'master', url: 'https://github.com/claypc98/application.git'
        }
    }
}

        stage('Check Version Number') {
            steps {
                script {
                    def jsonFile = readJSON file: 'design/test_model.json'
                    def versionString = jsonFile.version
                    def versionNumber = versionString.replaceAll('[^\\d.]', '')
                    println "JSON File Version Number: ${versionNumber}"

                    
              
                    def sqlFiles = new File("${env.WORKSPACE}/application/sql").listFiles().findAll { it.isFile() && it.name.endsWith('.sql') }.collect { it.name }
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
