   environment {
        GITHUB_REPO_URL = 'https://github.com/J4wHar/CoTProject.git'
        GITHUB_CREDENTIALS = credentials('githubtoken')
        WILDFLY_HOME = '/opt/wildfly'
        M3_HOME = '/opt/maven'
        PROJECT_DIR = 'server'  // Update to your actual project directory
    }
    
    when{
      branch 'main'
    }
    stages {
        stage('Initialization') {
            steps {
                echo "GITHUB_REPO_URL: ${GITHUB_REPO_URL}"
                echo "WILDFLY_HOME: ${WILDFLY_HOME}"
                echo "PROJECT_DIR: ${PROJECT_DIR}"
                echo "M3_HOME: ${M3_HOME}"
                echo "PATH: ${PATH}"
            }
        }
        stage('Build') {
            steps {
                dir(PROJECT_DIR) {
                    script {
                        // Assuming your project uses Maven for building
                        sh "$M3_HOME/bin/mvn clean install"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                dir(PROJECT_DIR) {
                    script {
                        // Assuming your project uses Maven for running tests
                        sh "$M3_HOME/bin/mvn test"
                    }
                }
            }
        }

        stage('Deploy to WildFly') {
            steps {
                dir(PROJECT_DIR) {
                    script {
                        sh "$WILDFLY_HOME/bin/jboss-cli.sh --connect -u=\"admin\" -p=\"admin\" --command=\"deploy target/jakartaee-hello-world.war\""
                      
                    }
                }
            }
        }
    }

    // post {
    //     always {
    //         deleteDir()
    //     }
    // }
}
