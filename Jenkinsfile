pipeline {
	agent any
		stages{
			stage('Upload to exchange') {
				environment {
					USER_NAME = credentials('USER_NAME')
					PASSWORD = credentials('PASSWORD')
				}
				steps {
					echo 'USER_NAME %USER_NAME%'					
					bat 'mvn -B -U -e -V clean -DskipTests -Dusername="%USER_NAME%" -Dpassword="%PASSWORD%" deploy -s settings.xml'
				}
			}		
			stage('Build Clean package') {
				steps {
					bat 'mvn -B -U -e -V clean -DskipTests package'
					echo 'Success'
				}
			}
// 			stage('TEST') {
// 				steps {
// 					echo 'Go to step Test-App-With-Environment'
// 					bat 'mvn -Denv=dev test -X'
// 				}
// 			}
			stage('Deployment') {
				steps {
					bat 'mvn -B -U -e -V clean -DskipTests -Pdev deploy -DmuleDeploy'
				}
			}
 		}
}