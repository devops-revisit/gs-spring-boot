pipeline
{
    agent any
    tools
    {
        maven "maven3.9"
    }
    stages
    {
        stage ('Checkout')
        {
	       steps
            	{
                	git branch: 'main', credentialsId: 'github', url: 'https://github.com/devops-revisit/gs-spring-boot.git'
            	}
        }
	stage ('Build')
	{
	   	steps
		{
			dir ('complete') {
			sh "mvn clean package"
			}	
		}
	}
	stage ('Test')
	{
		steps
		{
			sh 'mvn test || true'
			echo 'Test completed!'
		}
	}
	stage ('SonarQube Check')
	{
		steps
		{
			withSonarQubeEnv('SonarQube')
			{
				dir ('complete') {
				sh """
				vn sonar:sonar \
                    		-Dsonar.projectKey=${JOB_NAME} \
                    		-Dsonar.projectName=${JOB_NAME}
                    		"""
				}
			}
		}
	}
    }
}
