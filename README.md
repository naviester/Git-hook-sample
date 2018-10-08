# Git-hook-sample
Demo on basic use of ***"pre-commit"*** hook to check for lint errors or warnings in Android application.

Basics of git-hooks can be learnt from[here.](https://githooks.com/)

####How it works?
Let's get down to understanding how this sample works and integrates pre-commit git hook.
* Initially when the code base is checked out, everything is normal and silent as standard Android codebase.
* Navigate to project directory and checkout following directory ***'.git/hooks'***. These are hooks are executed as per there names indicated.You will find many hook files like:
    * pre-commit.sample
    * pre-push.sample
* Traverse through the following files in codebase viz:***git-hooks.gradle***,***pre-commit.sh***and***build.gradle.***
* Launch *'Terminal'* in Android Studio.
* Initiate following command *'./gradlew clean'*.
* This will copy **pre-commit** file into ****.git/hooks*** directory at project level.
* Post this, whenever an effort is made to commit anything to designated repository, ***lint*** check will be executed automatically before the commit succeeds.

##Important files

*   **git-hooks.gradle**: <p>Contains methods responsible for copying pre-commit file to designated directory '/.git'. 
    *   **installGitHooks()**: Initiates the copying of pre-commit.sh to /.git/hooks from ../git-hooks directory.
    *   **copyGitHooks()**: Renames 'pre-commit.sh' to 'pre-commit' and copies the same in .git directory.
*   **pre-commit.sh**:<p>As the name suggests 'pre-commit', it get's executed prior to any commit in local git repository.
    In current example this file contains script to initiate **lint** check in current Android project. 
*   **build.gradle (app level)**:<p>It's the heart of Android application at module level. This file calls methods in *git-hooks.gradle.* 
At line no. 31 following code can be encountered.<br><br>```afterEvaluate { clean.dependsOn installGitHooks}```<br><br>
This line of script justifies that gradle ***clean*** command will only be executed only when the execution of ***installGitHooks*** method's execution is completed.  

####Sample Screenshot from SourceTree of lint check while committing
![Sample Screenshot](/source_tree.png)