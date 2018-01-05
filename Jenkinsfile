pipeline {
    agent any

    stages {
	stage 'Checkout code'
    	    git 'https://github.com/velvon74/SeleniumNUnitParam.git'
	stage 'Restore NuGet'
    	    bat '"C:/Program Files (x86)/MSBuild/14.0/Bin/nuget.exe" restore SeleniumNUnitParam.sln'
	stage 'Build'
    	    bat '"C:/Program Files (x86)/MSBuild/14.0/Bin/msbuild.exe" SeleniumNUnitParam.sln /p:Confuguration=Debug /p:Platform=\"Any CPU\" /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}'
	stage 'Tests'
    	    bat 'c:/tools/nunit-console/nunit3-console.exe SeleniumNUnitParam\\bin\\Debug\\SeleniumNUnitParam.dll'
    }
}
