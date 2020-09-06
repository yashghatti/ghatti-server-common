pipeline {
    agent any

    stages{
    
        stage('Stop elasticsearch'){
            steps{
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo '==> Starting elasticsearch'
                    sh 'sudo docker rm $(sudo docker ps -aqf "name=elastic") -f'
                }    
            }
        }
        stage('Run elasticsearch'){
            steps{
                sh 'sudo docker run -d --name elasticsearch --restart=always -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -v /var/lib/elasticsearch:/usr/share/elasticsearch/data --privileged elasticsearch:7.8.1'
            }
        }
        
        stage('Stop Portainer'){
            steps{
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo '==> Starting Portainer'
                    sh 'sudo docker rm $(sudo docker ps -aqf "name=portainer") -f'
                }    
            }
        }
        stage('Run Portainer'){
            steps{
                sh 'sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --privileged --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce'
            }
        }
        
    }
}
