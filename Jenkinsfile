pipeline {
    agent any
    
    environment {
        // Define the backup directory
        BACKUP_DIR = "/Users/ecorfyinc/git"
        // Define the path to the data you want to back up
        DATA_TO_BACKUP = "/Users/ecorfyinc/data/to/backup"
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

        stage('Verify Data to Backup') {
            steps {
                script {
                    // List contents of the directory to back up
                    echo "Listing contents of ${DATA_TO_BACKUP}:"
                    sh "ls -la ${DATA_TO_BACKUP} || echo 'Directory does not exist or is empty'"
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
                    sh "tar -czf ${BACKUP_DIR}/${backupFile} -C $(dirname ${DATA_TO_BACKUP}) $(basename ${DATA_TO_BACKUP}) || echo 'Backup failed: Directory or files not found'"

                    // Save the backup file name to an environment variable for later use
                    env.BACKUP_FILE = backupFile
                }
            }
        }

        stage('Store Backup') {
            steps {
                script {
                    echo "Backup file created: ${BACKUP_DIR}/${env.BACKUP_FILE}"
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

      
                   

   
