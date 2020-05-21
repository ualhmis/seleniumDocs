pipeline {
    agent any
    environment {
        DRIVERS_LOC = "/var/lib/jenkins/selenium-drivers/"
    }
    tools {
        // Usa aquí el nombre de tu instalación de Maven en Jenkins Tools
        maven "maven-3.6.3"
    }
    stages {
        stage('Git clone') {
            steps{
                git 'https://github.com/ualhmis/seleniumWebDriverJUnit.git'
            }
        }
        stage('Firefox tests') {
            steps {
                // Run Maven on xvfb environment display.
                // Update the path/to/your/pom.xml as necessary
                sh "xvfb-run mvn -f seleniumWebDriver/pom.xml clean test -Dwebdriver.gecko.driver=${DRIVERS_LOC}/geckodriver"
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results 
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
    }
}
