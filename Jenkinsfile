def checkoutFolder = "${env.WORKSPACE}/FilesTransfer"
def folderBackup = "${env.WORKSPACE}/Backup"

pipeline{
    agent any
    
    stages{
        stage("Setup parameters"){
            steps{
                script { 
                    properties([
                        parameters([
                            string(
                                defaultValue: 'https://github.com/ElectroGio/FilesTransfer.git', 
                                name: 'gitFilesRepository', 
                                trim: false
                            ),
                            string(
                                defaultValue: 'E:/FilesTransfer', 
                                name: 'destinationPath', 
                                trim: false
                            )
                        ])
                    ])
                }

            }
        }

        stage("External Checkout"){
            steps{
                script{
                    echo "========Git Checkout to files======== ${params.gitFilesRepository}" 
                    dir("${checkoutFolder}")  
                    if (fileExists("/"))
                    {
                         bat("git pull")
                    }
                    else
                    {
                         bat("git clone ${params.gitFilesRepository}")
                    }
                    echo "My cloned folder is ${checkoutFolder}"
                }
            }
        }

        stage("Backup files"){
            steps
            {
                script{
                    echo("=======Backup files stage init =======")
                    dir("${folderBackup}")
                    if(!fileExists("/"))
                    {
                        bat("mkdir ${folderBackup}")
                    }
                }
            }
        }

        stage("Moving files"){
            steps
            {
                echo("=======Moving files to ${params.destinationPath} =======")
                bat("move ${checkoutFolder} ${folderBackup}")
            }
        }
    }
}