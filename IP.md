```
<?xml version='1.1' encoding='UTF-8'?>
<jenkins.model.JenkinsLocationConfiguration>
  <jenkinsUrl>http://54.210.197.112:8080/</jenkinsUrl>
</jenkins.model.JenkinsLocationConfiguration>
```
```
pipeline {
    agent { label 'test' }
    stages {
        stage('Hello World') {
            steps {
                // This will print "Hello World" to the console
                echo 'Hello World'
            }
        }
    }
}
```
