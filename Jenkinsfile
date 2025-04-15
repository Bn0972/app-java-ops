pipeline {
    agent any
    tools {
        jdk 'Java'  // 确保你在 Jenkins 配置中有一个名为 "Java" 的 JDK
    }

    environment {
        JAVA_HOME = tool 'Java'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Bn0972/app-java.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                sh '''
                    mkdir -p build/classes
                    javac -d build/classes Main.java
                '''
            }
        }

        stage('Prepare Manifest') {
            steps {
                sh '''
                    echo "Main-Class: Main" > build/classes/MANIFEST.MF
                '''
            }
        }

        stage('Package') {
            steps {
                sh '''
                    mkdir -p build/jar
                    cd build/classes
                    jar cvmf MANIFEST.MF ../jar/MyApplication.jar *
                '''
            }
        }

        stage('Run') {
            steps {
                sh '''
                    java -jar build/jar/MyApplication.jar
                '''
            }
        }
    }
}
