node {
   // Mark the code checkout 'stage'....
   stage 'Checkout'

   // Get some code from a GitHub repository
   git url: 'https://github.com/jglick/simple-maven-project-with-tests.git'

   // Mark the code build 'stage'....
   stage 'Build'
   // Run the maven build
   sh "mvn clean package"
}
