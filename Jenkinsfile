pipeline {
    agent any
    stages {
        stage('SonarQube') {
            steps {
                script {
                    def piplineConfig = [
                        sonarqubeServer = 'sonarqube'
                    ]
                    def repositoryUrl = scm.userRemoteConfigs[0].getUrl()
                    def GIT_REPO_NAME = scm.userRemoteConfigs[0].getUrl().tokenize('/').last().split("\\.")[0]
                    def sonarqubeTool = tool 'sonarqube'
                    def SONAR_BRANCH_NAME = env.BRANCH_NAME
                    withSonarQubeEnv(piplineConfig.sonarqubeServer) {
                        sh "sed -i s#{{repo_name}}#${GIT_REPO_NAME}# sonar-project.properties"
                        sh "sed -i s#{{branch_name}}#${SONAR_BRANCH_NAME}# sonar-project.properties"
                        sh "${sonarqubeTool}/bin/sonar-sccaner -Dsonar.projectVersion=${SONAR_BRANCH_NAME} -Dsonar.buildString=Jenkins-${SONAR_BRANCH_NAME}-BLD${env.BUILD_NUMBER}"
                    }
                    
                }
            }
        }
    }
}
