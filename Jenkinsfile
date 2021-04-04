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
                    { 
                        if (fileExists("/"))
                        {
                            echo "========Folder exists, git pull========" 
                            bat("git pull")
                        }
                        else
                        {
                            echo "========Folder does not exist, git clone========"
                            bat("git clone ${params.gitFilesRepository}")
                        }
                        echo "My cloned folder is ${checkoutFolder}"
                    }
                }
            }
        }

        stage("Backup files"){
            steps
            {
                script{
                    echo("=======Backup files stage init =======")
                    dir("${folderBackup}")
                    {
                        if(!fileExists("/"))
                        {
                            echo("=======Backup folder does not exist, action: create =======")
                            bat("mkdir ${folderBackup}")
                        }
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