
stage 'Checkout'
node {
git credentialsId: '7176ddc6-3868-4e2b-9aed-4edbb620ef28', url: 'https://github.com/vinzonwsl/connecting-salesforce.git'
}

stage 'Build' 
node {
withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
sh "mvn -B clean package"
}
stash excludes: 'target/', includes: '**', name: 'source'
}
stage 'Quality'
parallel 'Test': {
node {
unstash 'source' withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
sh "mvn clean verify" 
        }
}
}, 'Sonar Analysis': {
node {
unstash 'source' withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
sh "mvn sonar:sonar -Psonar-scott" 
        }
} 
}
stage 'Approve'
timeout(time: 7, unit: 'DAYS') {
input message: 'Do you want to deploy?', submitter: 'ops'
}

stage name:'Deploy', concurrency: 1
node {
	echo 'To Do Deployment'
}

