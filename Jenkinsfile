def groovyFile

pipeline{
    agent any
    parameters{
        choice(name: 'Version',choices: ['1.1.0', '1.2.0','1.2.1'] , description:"This is a parameter choices.")
    }
    environment{
        var='This job is an IaC on terraform platform to create an iam user with out any polices'
        result='Done'
    }
    stages{
        stage ("init"){
            steps {
                script {
                    groovyFile=load "script.groovy"
                }
            }
        }
        stage("build"){
            steps{
                script {
                    groovyFile.buildApp()
                }
            }
        }

        stage("deploy"){
            input {
                message "choose which version you want to deploy"
                parameters {
                    choice(name: 'version', choices: ['1.0','1.1','1.2'], description: 'this is your choices.')
                }
            }
            steps{
                script {
                    groovyFile.deployApp()
                    echo "you have been choiced ${version}"
                }
            }
        }
        stage(test){
            steps{
                /* echo 'this is a test of my first jenkinsFile... '
                echo " go to ${cd /home/mohamed/Desktop/terDir}" */
                script {
                    groovyFile.testApp()
                }
            }
        }        
    }
    post{
        success{
            echo "your job is : ${result}"
        }
    }

}
