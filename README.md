# GradleConcepts

```shell
gradle compileJava
gradle run
gradle --rerun-tasks build
gradle clean build --refresh-dependencies -x test                                                                                                                                                    ─╯
```

##### Test Reports

```shell
gradle test
```
Runs the tests and creates the report in ```build/reports/tests/test/index.html```

### Gradle Task
Project is the root class under which task can be considered as a method.
```shell
# project.task firstTask
task firstTask{
    println "Gradle First Task!!"
}
```

Check first task and run in two ways
```shell
gradle tasks --all
gradle firstTask
# Same as 
gradle fT
```

Prioritize the tasks

```shell
task deployToStage{
    doLast(){
        println "Deployed to Stage"
    }
}

task deployToProd{
    doLast(){
        println "Deployed to Prod"
    }
}

task cleanUpFiles{
    doLast(){
        println "Clean Up Files"
    }
}

deployToProd.dependsOn deployToStage
deployToProd.finalizedBy cleanUpFiles
#defaultTasks "deployToStage"
```

Outputs the following

```log
❯ gradle deployToProd

> Configure project :
123
Gradle First Task!!
task X

> Task :deployToStage
Deployed to Stage

> Task :deployToProd
Deployed to Prod

> Task :cleanUpFiles
Clean Up Files

BUILD SUCCESSFUL in 566ms
3 actionable tasks: 3 executed

```