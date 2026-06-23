pipeline {
    agent any
    
    stages {
        stage('Preparation & Injection') {
            steps {
                sh 'chmod +x gradlew'
                
                sh '''
                    if [ ! -d "jdk-11" ]; then
                        echo "Mengunduh JDK 11 menggunakan curl..."
                        curl -sL -o jdk11.tar.gz https://github.com/adoptium/temurin11-binaries/releases/download/jdk-11.0.23%2B9/OpenJDK11U-jdk_x64_linux_hotspot_11.0.23_9.tar.gz
                        tar -xzf jdk11.tar.gz
                        mv jdk-11.0.23+9 jdk-11
                        rm jdk11.tar.gz
                    fi
                '''
            }
        }
        stage('Parallel Execution') {
            environment {
                JAVA_HOME = "${WORKSPACE}/jdk-11"
                PATH = "${JAVA_HOME}/bin:${PATH}"
            }
            parallel {
                stage('Build Stage') {
                    steps {
                        sh './gradlew --version' 
                        sh './gradlew build'
                    }
                }
                stage('Test Stage') {
                    steps {
                        sh './gradlew test'
                    }
                }
            }
        }
    }
}