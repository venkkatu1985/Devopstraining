#!groovy
pipeline {
    agent {
		node {
			label 'master'
			customWorkspace "C://Jenkins//${env.JOB_NAME}".replace('%2F', '_')
		}
	}

	parameters{
		string(	defaultValue: "1.0", 
				description: 'The Major.Minor.Patch for the Component level. This will update the CDA ComponentVersion.', 
				name: 'COMPONENTVERSION' )

		string( defaultValue: "venkkat.u@gmail.com",
				description: 'E-mail Addresses for users who need failed or succesful build e-mails',
				name: 'EMAIL_LIST')

		booleanParam( defaultValue: false,
		        description: 'True false testing mechanism',
				name: 'FULL_BUILD')

	}

	environment {
		ComponentVersion = "${params.COMPONENTVERSION}.${env.BUILD_NUMBER}"
		PROJECT_NAME = 	"project1"
		
	}

   /* options {
	    skipDefaultCheckout() 
        gitLabConnection('GitLab_Generic')	
		timeout(time: 60, unit: 'MINUTES')
    }*/

    /*triggers {
        gitlab(triggerOnPush: true, triggerOnMergeRequest: true, branchFilterType: 'All')
    }*/


    stages {
		stage('Checkout') {
			steps {
				checkout scm

		//checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'WM'], [$class: 'CloneOption', noTags: true, reference: '', shallow: true, timeout: 53], [$class: 'SparseCheckoutPaths', sparseCheckoutPaths: [[path: '/BuildScripts'] ]]], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'SSH_USER_WITH_KEY', url: 'git@git.s.git']]])
			}
		}
stage('Build') {
			steps {
			    println "Starting build"
				dir("C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319") {
					bat "MSBuild.exe" C:\\RaviProject\\Devopstraining\\build\\project.XML /p:SolutionFolder="C:\\RaviProject\\Devopstraining"				
				}
			
			}
		} 

	}

	/*post {

            failure {
			updateGitCommitStatus name: 'build', state: 'failed'
			// Only send e-mail errors when it is the master branch
			script {
				if(env.BRANCH_NAME == 'develop') {
					emailext (
						to: "${params.EMAIL_LIST}", 
						subject: "Build ${env.BUILD_NUMBER} - FAILED (${env.JOB_NAME})" 
					)
				
				}
			}  			          
		}
		success {
			updateGitCommitStatus name: 'build', state: 'success'

			script {
				emailext (
						to: "${params.EMAIL_LIST}", 
						subject: "Build ${env.BUILD_NUMBER} - SUCCESS (${env.JOB_NAME})" 
					)
				
			}
		}  
	} //end of post
	*/
}