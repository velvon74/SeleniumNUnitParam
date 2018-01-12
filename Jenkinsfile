pipeline {
    agent any
    environment {
	JAVA_HOME = 'C:\\Program Files\\Java\\jre1.8.0_151\\'
    }

    stages {
	stage('Checkout code'){
	    steps {
		echo '######################> Downloading code from repo'
    		git 'https://github.com/velvon74/SeleniumNUnitParam.git'
    		echo "Building ${env.TAG_NAME} from ${env.BRANCH_NAME}"
    	    }
    	}
	stage('Restore NuGet') {
	    steps {
		echo '######################> Downloading NuGet'
    		bat '"C:/Program Files (x86)/MSBuild/14.0/Bin/nuget.exe" restore SeleniumNUnitParam.sln'
    	    }
    	}
	stage('Build'){
	    steps {
		echo "######################> Building version 1.0.0.${env.BUILD_NUMBER}"
    		bat "\"${tool 'MSBuild'}\" SeleniumNUnitParam.sln /m /target:clean,build /p:Confuguration=Debug /p:Platform=\"Any CPU\" /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
    	    }
    	}
	stage('SonarQube test'){
	    steps {
		echo '#####################> SONAR ########################'
		bat 'c:/sonarqube/scan/SonarQube.Scanner.MSBuild.exe begin /k:"org.sonarqube:sonarqube-scanner-msbuild" /n:"SeleniumNUnit" /d:sonar.host.url="http://localhost:9000" /d:sonar.login="7ab26ba9f5504b9658ff16a2838ce9142726528c"'
		bat "\"${tool 'MSBuild'}\" /t:Rebuild"
		bat "c:/sonarqube/scan/SonarQube.Scanner.MSBuild.exe end"
            }
	}
	stage('Tests'){
	    steps {
		echo '######################> Running tests'
    		bat 'c:/tools/nunit-console/nunit3-console.exe SeleniumNUnitParam\\bin\\Debug\\SeleniumNUnitParam.dll' 
   	    }
    	}
	stage ('Print Data'){
	    steps {
	        echo "######################> Ok!"
		bat 'set > env.txt' 
	    }
	}
    }
}
