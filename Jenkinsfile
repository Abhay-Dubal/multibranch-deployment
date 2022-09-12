pipeline {
	agent {
		node{
			label 'master'
			customWorkspace "/mnt/project/22q1"
		}
	}	
	stages {
		stage ('slave permision'){
			agent{
				node {
					label "qa"
					customWorkspace "/mnt/slave"
				}
			}
			steps{
				/*sh "sudo mkdir 22q1"*/
				sh "sudo chmod -R 777 /mnt"
			}
		}
		stage ('copy to slave'){
			agent {
		node{
			label 'master'
			customWorkspace "/mnt/project/22q1"
		}
	}	
			steps{
			sh "cp -r /root/california.pem ."
			sh "scp -i california.pem index.html ec2-user@172.31.6.107:/mnt/slave"
			}	
		}
		stage ('depoly on slave htppd'){
		agent{
				node {
					label "qa"
					customWorkspace "/mnt/slave"
				}
			}
			steps {
				sh "sudo yum install httpd -y"
				sleep 5
				sh "sudo service httpd start"
				sh "sudo chmod -R 777 index.html"
				sh "sudo cp -r index.html /var/www/html"
			}
		}	
	}
	
}
