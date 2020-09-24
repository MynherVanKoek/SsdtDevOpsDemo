pipeline {
    agent { label 'windows-2016' }
    
    stages {
        stage('Build Dacpac from SQLProj') {
            steps {
                bat "\"${tool name: 'Visual Studio 2019', type: 'msbuild'}\" /p:Configuration=Release"
                stash includes: 'SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac', name: 'theDacpac'
            }
        }
        stage('Deploy Dacpac to SQL Server') {
            steps {
                unstash 'theDacpac'
                bat "\"C:\\Program Files\\Microsoft SQL Server\\150\\DAC\\bin\\sqlpackage.exe\" /Action:Publish /SourceFile:\"SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac\" /TargetServerName:(local) /TargetDatabaseName:Chinook"
            }
        }
    }
}