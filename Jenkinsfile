
stage 'build' 
node {
git credentialsId:'7176ddc6-3868-4e2b-9aed-4edbb620ef28', url:'https://github.com/vinzonwsl/connecting-salesforce.git' withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
sh "mvn -B –Dmaven.test.failure.ignore=true clean package"
}
}
stage 'test'
parallel 'integration': {
node {
withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
sh "mvn clean verify" 
        }
}
}, 'quality': {
node {
withEnv(["PATH+MAVEN=${tool 'M3'}/bin"]) {
sh "mvn sonar:sonar -Psonar-scott" 
        }
} 
}

