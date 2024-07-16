pipeline {
    agent any

    environment {
        // Define the format for the timestamp
        TIMESTAMP = new Date().format("yyyyMMddHHmmss")
        
        // Specify the paths for the project folder and the backup directory
        PROJECT_FOLDER = "/path/to/your/project"
        BACKUP_DIR = "/path/to/backup"
        BACKUP_FILE = "${BACKUP_DIR}/project_backup_${TIMESTAMP}.tar.gz"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the project..."
                // Your build steps here
            }
        }
        stage('Backup Project Folder') {
            steps {
                script {
                    // Create the backup directory if it does not exist
                    sh "mkdir -p ${env.BACKUP_DIR}"
                    
                    // Create a tar.gz backup of the project folder with the timestamped filename
                    sh "tar -czf ${env.BACKUP_FILE} -C ${env.PROJECT_FOLDER} ."
                    
                    echo "Project folder backed up to ${env.BACKUP_FILE}"
                }
            }
        }
    }

    post {
        always {
            // Optionally, you can archive the backup file as an artifact in Jenkins
            archiveArtifacts artifacts: "${env.BACKUP_FILE}", allowEmptyArchive: true
        }
    }
}

