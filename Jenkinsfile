node {
	stage("checkout") {
		git url:'https://github.com/itecor/itecor-sample-web.git', branch: 'master'
	}

    stage("build") {
        dir('spring-boot-sample-data-jpa') {
            sh 'mvn clean compile'
        }
    }

    stage("test") {
        dir('spring-boot-sample-data-jpa') {
            try {
                sh 'mvn test -B'
                junit 'target/surefire-reports/*.xml'
            } catch(err) {                
                if (currentBuild.result == 'UNSTABLE')
                    currentBuild.result = 'FAILURE'
                throw err
            }
        }
    }
    
    stage("pre-deploy") {
        dir('spring-boot-sample-data-jpa') {
            sh 'mvn package'
            stash name: 'binary', includes: 'target/*.jar'
        }
        stash name: 'docker-file', includes: 'Dockerfile'
    }
    
}
 

    stage("deploy") {
    }


stage("tag") {
}