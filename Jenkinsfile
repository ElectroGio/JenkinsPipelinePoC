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
                echo "========Git Checkout to files======== ${params.gitFilesRepository}"
                sh("git clone ${params.gitFilesRepository}")
            }
        }
    }
}