def checkoutFolder = "FilesTransfer"
def folderBackup = "Backup"

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

                echo "========Printing env variables ========"
                echo "${env.BUILD_ID}"
                echo "${env.BUILD_NUMBER}"
                echo "${env.BUILD_TAG}"
                echo "${env.BUILD_URL}"
                echo "${env.EXECUTOR_NUMBER}"
                echo "${env.JAVA_HOME}"
                echo "${env.JENKINS_URL}"
                echo "${env.JOB_NAME}"
                echo "${env.NODE_NAME}"
                echo "${env.WORKSPACE}"

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
                            bat("git pull origin master")
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
                bat("move ${checkoutFolder} ${destinationPath}")
            }
        }
    }
}