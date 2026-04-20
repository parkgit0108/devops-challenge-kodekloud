Almost the same as lab 77.

When creating job, select parameter based and set the values as provided.

add this to the pipeline script
```sql
pipeline {
    agent { label 'stapp01' }

    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Enter branch name')
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    if (params.BRANCH == 'master' || params.BRANCH == 'feature') {
                        sh """
                            cd /var/www/html
                            git fetch origin
                            git checkout ${params.BRANCH}
                            git pull origin ${params.BRANCH}
                        """
                    } else {
                        error("Invalid branch name. Use master or feature only.")
                    }
                }
            }
        }
    }
}
```
