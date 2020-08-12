pipeline {
    agent any

    stages{
    
        stage('Stop elasticsearch'){
            steps{
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo '==> Starting elasticsearch'
                    sh 'sudo podman rm $(sudo podman ps -aqf "name=elastic") -f'
                }    
            }
        }
        stage('Run elasticsearch'){
            steps{
                sh 'sudo podman run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -v /var/lib/elasticsearch:/usr/share/elasticsearch/data --network=host --privileged elasticsearch:7.8.1'
            }
        }
        
    }
}
