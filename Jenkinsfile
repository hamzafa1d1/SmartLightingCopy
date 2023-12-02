pipeline {
    agent any
    
    environment {
        GITHUB_REPO_URL = 'https://github.com/hamzafa1d1/SmartLightingCopy.git'
        GITHUB_CREDENTIALS = credentials('githubtoken')
        WILDFLY_HOME = '/opt/wildfly'
        M3_HOME = '/opt/maven'
        PROJECT_DIR = 'smart_lighting'  // Update to your actual project directory
    }
    
    stages {
        
        stage('Initialization') {
             when {
                  branch 'main'
                }
   
            steps {
                echo "GITHUB_REPO_URL: ${GITHUB_REPO_URL}"
                echo "WILDFLY_HOME: ${WILDFLY_HOME}"
                echo "PROJECT_DIR: ${PROJECT_DIR}"
                echo "M3_HOME: ${M3_HOME}"
                echo "PATH: ${PATH}"
            }
        }
        stage('Build') {
            when {
                  branch 'main'
                }
            
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
            when {
                  branch 'main'
                }
            
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
            
            when {
                  branch 'main'
                }
            
            steps {
                dir(PROJECT_DIR) {
                    script {
                        sh "$WILDFLY_HOME/bin/jboss-cli.sh --connect -u=\"admin\" -p=\"admin\"  --command=\"deploy --force target/smartlighting-1.0-SNAPSHOT.war\""
                      
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
