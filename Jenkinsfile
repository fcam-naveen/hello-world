pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                sh 'python3 -m py_compile hello.py' 
                sh 'docker build -t hello-app:latest .'
            }
        }
        stage('Test'){
            steps {
                sh 'docker run -d -p 8080:8080 --name simple_hello_app -it hello-app'
                sh 'curl http://localhost:8080 > result.txt'
                sh 'if grep Hello! result.txt; then echo "Test1 Success"; else error("Test1 Failed");fi'
                sh 'curl http://localhost:8080/healthz > result.txt'
                sh 'if grep OK result.txt ; then echo "Test2 Success"; else error("Test2 Failed"); fi'
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "Copy the remote repo. Deploy then using deployment code"'
            }
        }
    }
}
