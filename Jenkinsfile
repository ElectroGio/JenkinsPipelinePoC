pipeline{
    agent any
    def checkoutFolder = "${env.WORKSPACE}/FilesTransfer"
    def folderBackup = "${env.WORKSPACE}/Backup"
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
            echo("=======Backup files stage init =======")
            script{
                dir("${folderBackup}")
                if(!fileExists("/"))
                {
                     bat("mkdir ${folderBackup}")
                }
            }
        }

        stage("Moving files"){
            echo("=======Moving files to ${params.destinationPath} =======")
            bat("move ${checkoutFolder} ${folderBackup}")
        }
    }
}