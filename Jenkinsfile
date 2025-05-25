pipeline {
    agent any

//     environment {
//         JENKINS_HOME = "$JENKINS_HOME"
//         BUILD = "${JENKINS_HOME}/workspace/mlops_final"
//     }

    stages {
         stage('Start') {
            steps {
                script {
                    echo 'Начало работы скриптов.'
                }
            }
        }
        stage('Preparation') {
            steps {
                // Очистка рабочего пространства
                cleanWs()
                checkout scm
            }
        }

        stage('Checkout') {
            steps {
                script {
                    // Получаем исходный код из репозитория Git
                    // git branch: 'main', url: 'https://github.com/lastinm/mlops_final.git'
                }
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                // Создание виртуального окружения
                script {
                    sh 'python -m venv venv'
                }
            }
        }

        stage('Activate venv') {
            steps {
                // Активация виртуального окружения
                script {
                    sh './venv/scripts/activate.sh'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                // установка зависимостей
                script {
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Create dataset Titanic') {
            steps {
                script {
                    // Создаем и обучаем модель
                    dir('src') {
                        // Можно выбрать хороший датасет или модифицированный (плохой) датасет
                        sh 'python make_dataset_titanic.py'
                        //sh 'python dataset_titanic_modifed.py'
                        }
                    }
                }
            }
        }

        stage('Create model Titanic') {
            steps {
                script {
                    // Создаем и обучаем модель
                    dir('src') {
                        sh 'python model_titanic.py'
                    }
                }
            }
        }

        stage('App tests') {
            steps {
                script {
                    sh 'pytest -v'
                }
            }
        }

        stage('Build Docker image') {
            steps {
                 script {
                    // Для Линукс
                    sh 'docker build -t titanic-img .'
                 }
            }
        }

        stage('Finish') {
            steps {
                script {
                    echo 'Работа скриптов завершена успешно'
                }
            }
        }
    }
}