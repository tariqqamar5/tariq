node {
    
    notify('Started')
    
    stage('Git CheckOut'){
        git 'https://github.com/amitvashisttech/devops-acc-20200113.git'
    }
    
    def project_path = "02-Jenkins/atmosphere/spring-boot-samples/spring-boot-sample-atmosphere"
    dir(project_path) {
    
    stage('Maven Clean'){
    sh label: '', script: 'mvn clean'
    }
    
     stage('Maven Compile'){
    sh label: '', script: 'mvn compile'
    }
    
     stage('Maven Test'){
    sh label: '', script: 'mvn test'
    }
    
      stage('Maven Package'){
    sh label: '', script: 'mvn package'
    }
    
    stage('Archive Artifacts'){
    archiveArtifacts 'target/*.jar'
    }

   
    stage('Atmosphere Deployment to Stage Env.'){
    sh label: '', script: 'docker-compose up --build -d'
    }

    
    stage('Atmosphere Deployment to PROD Env.'){
    sh label: '', script: 'cp -rf target/*.jar ../../../../04-Ansible/03-Playbook-Jenkins/templates/atmosphere-v1.jar'
    sh label: '', script: "echo '<h1>TASK_ID: '${env.JOB_NAME}[${env.BUILD_NUMBER}]'</h1>' > ../../../../04-Ansible/03-Playbook-Jenkins/templates/jenkins.html"
    sh label: '', script: 'cd ../../../../04-Ansible/03-Playbook-Jenkins;ansible-playbook webserver.yaml'
    }
    
    }
    notify('Completed')
    
}

def notify(status){
    emailext (
        to: "amitvashist7@gmail.com",
        subject: "${status}: Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]'",
        body: """<p>"${status}: Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]'"</p>""",
)
    
}
