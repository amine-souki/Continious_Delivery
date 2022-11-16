pipeline
{
    agent any
    stages {
        stage ('Pull to github'){
            steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: 'MyGithub',
                            url: 'https://github.com/amine-souki/Continious_Delivery.git']]])
                }
            }
        }
	stage ('Build project'){
            steps{
                script{
                    sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml"
                }
            }
        }
	stage ('Build image docker'){
	     steps{
	         script{
		     sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml --become-user=jenkins" 
                 }
              
             }
        }

        stage ('Push to docker hub'){
             steps{
                 script{
                     sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml"
                 }

             }
        }	
     }
}
