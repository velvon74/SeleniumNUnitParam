pipeline {
    agent any

    stages {
	stage('Checkout code'){
	    steps {
		echo '######################> Downloading code from repo'
    		git 'https://github.com/velvon74/SeleniumNUnitParam.git'
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
		echo '#####################> SONAR ########################'
		bat 'c:/sonarqube/scan/SonarQube.Scanner.MSBuild.exe begin /k:"SeleniumNUnit" /d:sonar.host.url="http://localhost:9000" /d:sonar.login="7ab26ba9f5504b9658ff16a2838ce9142726528c"'
		bat "\"${tool 'MSBuild'}\" /t:Rebuild"
	}
	stage('Tests'){
	    steps {
		echo '######################> Running tests'
    		bat 'c:/tools/nunit-console/nunit3-console.exe SeleniumNUnitParam\\bin\\Debug\\SeleniumNUnitParam.dll'
    	    }
    	}
    }
}
