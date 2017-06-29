# MavenVersionsSample
Project for verifying set versions plugin behaviour

Download the project and run the following command from root pom.xml:
mvn versions:set -DnewVersion=137.0.18 -DprocessDependencies=false

And then run
mvn versions:set -DnewVersion=137.0.19 -DprocessDependencies=true

it doesn't update the dependency.

Here is the output:

Rams-MacBook-Pro:myartifact ramgaddam$ mvn versions:set -DnewVersion=137.0.23 -DprocessDependencies=false
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO]
[INFO] myartifact
[INFO] myutils
[INFO] myutilsb
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myartifact 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- versions-maven-plugin:2.3:set (default-cli) @ myartifact ---
[INFO] Searching for local aggregator root...
[INFO] Local aggregation root: /Users/ramgaddam/SourceCode/SampleMavenVersion/myartifact
[INFO] Processing change of com.mycompany:myartifact:0.0.1-SNAPSHOT -> 137.0.23
[INFO] Processing com.mycompany:myartifact
[INFO] Updating project com.mycompany:myartifact
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO]
[INFO] Processing com.mycompany:myutils
[INFO] Updating parent com.mycompany:myartifact
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO]
[INFO] Processing com.mycompany:myutilsb
[INFO] Updating parent com.mycompany:myartifact
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] myartifact ......................................... SUCCESS [ 1.027 s]
[INFO] myutils ............................................ SKIPPED
[INFO] myutilsb ........................................... SKIPPED
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.445 s
[INFO] Finished at: 2017-06-28T17:19:29+05:30
[INFO] Final Memory: 12M/155M

And then I executed the following:
Rams-MacBook-Pro:myartifact ramgaddam$ mvn versions:set -DnewVersion=137.0.24 -DprocessDependencies=true
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO]
[INFO] myartifact
[INFO] myutils
[INFO] myutilsb
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myartifact 137.0.23
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- versions-maven-plugin:2.3:set (default-cli) @ myartifact ---
[INFO] Searching for local aggregator root...
[INFO] Local aggregation root: /Users/ramgaddam/SourceCode/SampleMavenVersion/myartifact
[INFO] Processing change of com.mycompany:myartifact:137.0.23 -> 137.0.24
[INFO] Processing com.mycompany:myartifact
[INFO] Updating project com.mycompany:myartifact
[INFO] from version 137.0.23 to 137.0.24
[INFO]
[INFO] Processing com.mycompany:myutils
[INFO] Updating parent com.mycompany:myartifact
[INFO] from version 137.0.23 to 137.0.24
[INFO]
[INFO] Processing com.mycompany:myutilsb
[INFO] Updating parent com.mycompany:myartifact
[INFO] from version 137.0.23 to 137.0.24
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] myartifact ......................................... SUCCESS [ 1.274 s]
[INFO] myutils ............................................ SKIPPED
[INFO] myutilsb ........................................... SKIPPED
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.697 s
[INFO] Finished at: 2017-06-28T17:19:44+05:30
[INFO] Final Memory: 12M/155M

If I ran with processDependencies as true first. The following is the output:
Rams-MacBook-Pro:myartifact ramgaddam$ mvn versions:set -DnewVersion=137.0.23 -DprocessDependencies=true
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO]
[INFO] myartifact
[INFO] myutils
[INFO] myutilsb
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myartifact 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- versions-maven-plugin:2.3:set (default-cli) @ myartifact ---
[INFO] Searching for local aggregator root...
[INFO] Local aggregation root: /Users/ramgaddam/SourceCode/SampleMavenVersion/myartifact
[INFO] Processing change of com.mycompany:myartifact:0.0.1-SNAPSHOT -> 137.0.23
[INFO] Processing com.mycompany:myartifact
[INFO] Updating project com.mycompany:myartifact
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO] Updating dependency com.mycompany:myutils
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO]
[INFO] Processing com.mycompany:myutils
[INFO] Updating parent com.mycompany:myartifact
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO]
[INFO] Processing com.mycompany:myutilsb
[INFO] Updating parent com.mycompany:myartifact
[INFO] from version 0.0.1-SNAPSHOT to 137.0.23
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] myartifact ......................................... SUCCESS [ 1.176 s]
[INFO] myutils ............................................ SKIPPED
[INFO] myutilsb ........................................... SKIPPED
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.637 s
[INFO] Finished at: 2017-06-28T17:18:41+05:30
[INFO] Final Memory: 12M/155M
