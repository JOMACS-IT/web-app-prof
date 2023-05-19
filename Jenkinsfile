pipeline{
    agent any
    tools{
        maven "maven3.8.8"
    }
    
    stages{
        stage("1. git clone from repo"){
            steps{
                sh "echo start of git clone"
                git branch: 'main', url: 'https://github.com/JOMACS-IT/web-app-prof.git'
                sh "echo end of git clone"
            }
            }
        stage("2. build from maven"){
            steps{
                sh "echo start building from maven"
                sh "mvn clean package"
                sh "echo end of build"
                
            }
        }
        
        stage("3. code quality/scan"){
            steps{
                sh "echo start of sonacode scan"
                sh "mvn sonar:sonar"
                sh "echo end of sonacode scan"
            }
        }
        stage("4. store/deploy artifacts"){
            steps{
                sh "echo start of artifact deploy"
                sh "mvn deploy"
                sh "echo end of deploy"
            }
        }
        
        stage("5. deploy to tomcat in UAT"){
            steps{
                sh "echo start of deploying to tomcat UAT env"
                deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '', url: 'http://3.83.230.130:9090/')], contextPath: null, war: 'target/*.war'
                sh "echo end of deploy to tomcat in UAT env"
            }
        }
        
        stage("6. Email Notification"){
            steps{
                sh "echo send email notification to developers"
                emailext body: 'The Deployment is successful ', subject: 'development success ', to: 'info@jomacsit.com'
                
             }
        }
        }
      }
      
      
