pipeline {
    agent any
    tools {
        // Use the JDK version named "Java 21" configured in Jenkins
        jdk 'Java'
    }

    environment {
        // Defining JAVA_HOME may be optional, depending on your Jenkins configuration
        JAVA_HOME = tool 'Java'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'YOUR_OWN_APPLICATION_REPO_URL', branch: 'YOUR_BRANCH'
            }
        }

        stage('Compile') {
            steps {
                // Create a directory for compiled classes
                bat 'if not exist build\\classes mkdir build\\classes'
                // Kompilacja Main.java
                bat '"%JAVA_HOME%\\bin\\javac" -d build\\classes Main.java'
            }
        }

        stage('Prepare Manifest') {
            steps {
                // Places the manifest file directly in the buildclasses directory
                bat 'echo Main-Class: Main > build\\classes\\MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
                // Packaging compiled classes into a JAR file with a manifest file
                bat 'if not exist build\\jar mkdir build\\jar'
                // Uses a direct path to the manifest file located in buildclasses
                bat 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvmf MANIFEST.MF ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                // Running an application from a JAR file
                bat '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
    }
}
