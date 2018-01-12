pipeline {
    agent any

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
	stage('Tests'){
	    steps {
		echo '######################> Running tests'
    		bat 'c:/tools/nunit-console/nunit3-console.exe SeleniumNUnitParam\\bin\\Debug\\SeleniumNUnitParam.dll'
    	    }
    	}
    }
}
