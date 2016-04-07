node {
   // Mark the code checkout 'stage'....
   stage 'Checkout'

   // Get some code from a GitHub repository
   git credentialsId: '7176ddc6-3868-4e2b-9aed-4edbb620ef28', url: 'https://github.com/vinzonwsl/connecting-salesforce.git'

   // Get the maven tool.
   // ** NOTE: This 'M3' maven tool must be configured
   // **       in the global configuration.           
   def mvnHome = tool 'M3'
   env.PATH = "${mvnHome}/bin:${env.PATH}"

   // Mark the code build 'stage'....
   stage 'Build'
   // Run the maven build
   sh "mvn clean install"

   // Mark the code sonar analysis 'stage'....
   stage 'Sonar Analysis'
   // Run sonar analysis
   sh "mvn sonar:sonar -Psonar-scott"
}
