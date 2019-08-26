#!/usr/bin/env groovy
 
/**
        * Sample Jenkinsfile for Jenkins2 Pipeline
        * from https://github.com/praveenkumarn/TestRepo/edit/master/Jenkinsfile
        * by Praveen
 */
 
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL

timestamps {

node () {

	stage ('CI - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'git@github.com:praveenkumarn/TestRepo.git']]]) 
	}
	stage ('CI - Build') {
 			// Shell build step
sh """ 
#!/bin/bash

 """		// Maven build step
	withMaven { 
 			if(isUnix()) {
 				sh "mvn -f javagithub/pom.xml -U clean package -Dmaven.test.skip=true " 
			} else { 
 				bat "mvn -f javagithub/pom.xml -U clean package -Dmaven.test.skip=true " 
			} 
 		}
     stage ('CI - Nexus') {
 	 nexusArtifactUploader artifacts: [[artifactId: 'javagithub', classifier: '', file: '/var/lib/jenkins/workspace/Build_Push_Nexus/javagithub/target/javagithub-0.0.1.war', type: 'war']], credentialsId: 'nexusadmin', groupId: 'com.mkjavweb', nexusUrl: '172.31.82.72:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'devops_update_site', version: '0.0.1' 	}
}
}
}
