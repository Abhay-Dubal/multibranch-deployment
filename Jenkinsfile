pipeline {
	agent {
		node{
			label 'master'
			customWorkspace "/mnt/project/22q1"
		}
	}	
	stages {
		
		stage ('copy to slave'){
			agent {
		node{
			label 'master'
			customWorkspace "/mnt/project/22q1"
		}
	}	
			steps{
			sh "cp -r /root/california.pem ."
			sh "chmod -R 777 index.html"
			sh "scp -i california.pem index.html ec2-user@172.31.6.107:/mnt/slave"
			}	
		}
		stage ('depoly on slave htppd'){
		agent{
				node {
					label 'qa'
					
				}
			}
			steps {
				sh "sudo yum install httpd -y"
				sleep 5
				sh "sudo service httpd start"
				sh "sudo cp -r /mnt/slave/index.html /var/www/html"
			}
		}	
	}
	
}
