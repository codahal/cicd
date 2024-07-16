pipeline {
    agent any
    
    environment {
        // Define the backup directory
        BACKUP_DIR = "/Users/ecorfyinc/git"
    }

    stages {
        stage('Prepare Backup') {
            steps {
                script {
                    // Create the backup directory if it doesn't exist
                    sh "mkdir -p ${BACKUP_DIR}"
                }
            }
        }

        stage('Create Backup') {
            steps {
                script {
                    // Get the current timestamp
                    def timestamp = new Date().format("yyyyMMddHHmmss")

                    // Define the backup file name with timestamp
                    def backupFile = "backup_${timestamp}.tar.gz"

                    // Create the backup file
                    sh "tar -czf ${BACKUP_DIR}/${backupFile} /path/to/data/to/backup"

                    // Save the backup file name to an environment variable for later use
                    env.BACKUP_FILE = backupFile
                }
            }
        }

        stage('Store Backup') {
            steps {
                script {
                    // Optionally, you can perform additional actions to store the backup file,
                    // such as copying it to a remote server, uploading to cloud storage, etc.
                    // Example: Copy to remote server (requires SSH setup)
                    // sh "scp ${BACKUP_DIR}/${BACKUP_FILE} user@remote:/path/to/remote/backup/directory"
                    
                    echo "Backup file created: ${BACKUP_DIR}/${BACKUP_FILE}"
                }
            }
        }
    }

    post {
        always {
            script {
                echo "Pipeline completed. Backup file is located at ${BACKUP_DIR}/${env.BACKUP_FILE}"
            }
        }
    }
}

                 
