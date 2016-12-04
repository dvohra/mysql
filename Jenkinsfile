node("docker") {
    docker.withRegistry('https://index.docker.io/v1/', 'dvohra-dockerhub') {
        deleteDir()
      
        git url: "https://github.com/dvohra/mysql.git", credentialsId: 'dvohra-github'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        sh "ls -l"
        sh "docker"
        def app = docker.build "dvohra/mysql"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
