---
title: "Jenkins script code"
slug: jenkins-script-code

---

```yaml
pipeline
{
    agent
    {
        node
        {
            label 'Dev'
        }
    }
    stages
    {
        stage("Clone code")
        {
            steps
            {
                git url: "https://github.com/LondheShubham153/django-notes-app.git" , branch: "main"
                echo "Code was written by devloper"
            }
        }
        stage("Build")
        {
            steps
            {
            sh "docker build . -t notes-app:latest"
            echo "Docker will build"
            }
        }
        stage("Test")
        {
            steps
            {
            sh "docker run -d -p 8000:8000 --name notes-app notes-app:latest"
            echo "Docker will test"
            }
        }
        stage("Deploy")
        {
            steps
            {
            echo "Aws will deploy"
            }
        }
    }
}
```