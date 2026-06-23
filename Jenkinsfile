pipeline {
    agent any
    
    // Blok tools dihapus karena konfigurasi 'jdk11' Anda telah musnah bersama kontainer lama.
    // Jenkins akan otomatis menggunakan JVM native bawaan kontainer.
    
    stages {
        stage('Preparation') {
            steps {
                // Eksekusi izin file dilakukan di stage terpisah agar tidak memblokir paralel
                sh 'chmod +x gradlew'
            }
        }
        stage('Parallel Execution') {
            parallel {
                stage('Build Stage') {
                    steps {
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