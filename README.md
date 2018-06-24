# VersioningDemo

A quick demo to display how to handle versioning with maven

In order to get this setup you clone this repository into your own github account. Then you follow the description [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) to set your ssh keys up for github.

When this is done you should be able to push new changes using ssh and that's required to push the new release.

If you have any questions of additions to this documentation then please create a pull request or issue.

I made a video explaining this repo in full. Please watch [https://www.youtube.com/edit?o=U&video_id=8j7Jn2uHK3Y](https://www.youtube.com/edit?o=U&video_id=8j7Jn2uHK3Y)

### Commands for building

To create a package of your build
```
mvn package
```

To prepare a build and create a new release tag on github
```
mvn release:prepare
```

To perform the actual release and get the source, javadoc and jar-with-dependencies
```
mvn release:perform
```

### Notes
#### Release and Perform
##### release:prepare when POM has <version>0.61-SNAPSHOT</version>
```text
What is the release version for "VersioningDemo"? (org.ea:VersioningDemo) 0.61: : 
What is SCM release tag or label for "VersioningDemo"? (org.ea:VersioningDemo) VersioningDemo-0.61: : 
What is the new development version for "VersioningDemo"? (org.ea:VersioningDemo) 0.62-SNAPSHOT: :
```

If press Enter, it'd do following:
- increment POM to <version>0.62-SNAPSHOT</version> on local and origin
- build VersioningDemo-0.61.jar on local
- create a tag = VersioningDemo-0.61 on local and origin
- create VersioningDemo-0.61.zip and VersioningDemo-0.61.tar.gz on Releases page

##### release:perform
This goal creates the following.
```text
target\checkout\target\apidocs\*\*.html
target\checkout\target\VersioningDemo-0.61.jar
target\checkout\target\VersioningDemo-0.61-javadoc.jar
target\checkout\target\VersioningDemo-0.61-sources.jar
```


#### Release With POM
##### release:prepare-with-pom when POM has <version>0.62-SNAPSHOT</version>
```text
What is the release version for "VersioningDemo"? (org.ea:VersioningDemo) 0.62: :
What is SCM release tag or label for "VersioningDemo"? (org.ea:VersioningDemo) VersioningDemo-0.62: :
What is the new development version for "VersioningDemo"? (org.ea:VersioningDemo) 0.63-SNAPSHOT: :
```

If press Enter, it'd do following:
- increment POM to <version>0.63-SNAPSHOT</version> on local but not staged
- change POM to <version>0.62</version> and <tag>VersioningDemo-0.62</tag> on origin
- create release-pom.xml with <version>0.62</version> and <tag>@{project.version}</tag> on origin but delete on local
- build VersioningDemo-0.62.jar on local
- create a tag = VersioningDemo-0.62 on local and origin
- create VersioningDemo-0.62.zip and VersioningDemo-0.62.tar.gz on Releases page

##### release:perform
```text
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building VersioningDemo 0.63-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-release-plugin:2.5.3:perform (default-cli) @ VersioningDemo ---
[ERROR] Cannot perform release - the preparation step was stopped mid-way. Please re-run release:prepare to continue, or perform the release from an SCM tag.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.963 s
[INFO] Finished at: 2018-06-24T21:36:02+08:00
[INFO] Final Memory: 12M/220M
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-release-plugin:2.5.3:perform (default-cli) on project VersioningDemo: Cannot perform release - the preparation step was stopped mid-way. Please re-run release:prepare to continue, or perform the release from an SCM tag. -> [Help 1]
[ERROR] 
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR] 
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoFailureException

Process finished with exit code 1
```


#### Branch
##### release:branch when POM has <version>0.60-SNAPSHOT</version>
```text
What is the new working copy version for "VersioningDemo"? (org.ea:VersioningDemo) 0.61-SNAPSHOT: :
``` 
If press Enter, it'd do the following:
- increment POM to <version>0.61-SNAPSHOT</version> on master for local and origin
- create new branch but keep POM at <version>0.60-SNAPSHOT</version> on new branch for local and origin

