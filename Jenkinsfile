
node('tools'){
def mvnHome = tool 'M3'
env.PATH =
"${mvnHome}/bin:${env.PATH}"
}

stage 'Build'
node {
git credentialsId:
'7176ddc6-3868-4e2b-9aed-4edbb620ef28', url:
'https://github.com/vinzonwsl/connecting-salesforce.git'
sh "mvn -B clean
package"
stash excludes: 'target/', includes: '**', name: 'source'
}
stage
'Quality'
parallel 'Test': {
node {
unstash 'source'
sh "mvn clean verify"
}
}, 'Sonar Analysis': {
node {
unstash 'source'
sh "mvn sonar:sonar
-Psonar-scott"
}
}
stage 'Approve'
timeout(time: 7, unit: 'DAYS') {
input message: 'Do you
want to deploy?', submitter: 'ops'
}

stage name:'Deploy', concurrency: 1
node {
echo 'To Do Deployment'
}