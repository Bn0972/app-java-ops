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
                git url: 'https://github.com/Bn0972/app-java.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                // Create a directory for compiled classes
                sh 'if not exist build\\classes mkdir build\\classes'
                // Kompilacja Main.java
                sh '"%JAVA_HOME%\\bin\\javac" -d build\\classes Main.java'
            }
        }

        stage('Prepare Manifest') {
            steps {
                // Places the manifest file directly in the buildclasses directory
                sh 'echo Main-Class: Main > build\\classes\\MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
                // Packaging compiled classes into a JAR file with a manifest file
                sh 'if not exist build\\jar mkdir build\\jar'
                // Uses a direct path to the manifest file located in buildclasses
                sh 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvmf MANIFEST.MF ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                // Running an application from a JAR file
                sh '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
    }
}








