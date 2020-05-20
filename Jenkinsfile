pipeline {
   agent any

   stages {
        stage('Build') {
            steps {
                // Example AWS credentials
                withCredentials(
                [[
                    // Pass the AWS ID credentails as jenkins secret using AWS Secret SDK plug in
                    $class: 'AmazonWebServicesCredentialsBinding',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    credentialsId: 'AWSID',  // ID of credentials in Jenkins
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    echo "Listing contents of an S3 bucket."
                    // sh "aws ec2 create-snapshot --volume-id vol-0af86b25055e1dc70 --region=us-east-2 "
                    sh "aws ebs list-snapshot-blocks --region us-east-2 --snapshot-id snap-01d21f616268c96d3 --starting-block-index 1000 --max-results 100"
                }
            }
        }
      
      
   }
}
