pipeline {
    agent any
    
    // PERINGATAN ARSITEKTUR: Pastikan Anda telah mengonfigurasi JDK 11 dengan 
    // variabel 'jdk11' di Manage Jenkins -> Tools seperti pada Latihan 2 laporan Anda.
    tools {
        jdk 'jdk11' 
    }
    
    stages {
        stage('Integrative Parallel Execution') {
            steps {
                // Memberikan izin eksekusi on-the-fly pada lingkungan Linux
                sh 'chmod +x gradlew'
                
                // Memecah komputasi menjadi dua utas (worker) independen
                parallel (
                    "build stage": { 
                        sh './gradlew build' 
                    },
                    "test stage": { 
                        sh './gradlew test' 
                    }
                )
            }
        }
    }
}