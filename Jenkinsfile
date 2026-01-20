pipeline {
    agent any

    stages {
        stage('Matrix Build') {
            matrix {
                axes {
                    axis {
                        name 'OS'
                        values 'linux', 'windows'
                    }
                    axis {
                        name 'ENV'
                        values 'dev', 'qa'
                    }
                }

                // Optional: exclude combinations
                excludes {
                    exclude {
                        axis {
                            name 'OS'
                            values 'windows'
                        }
                        axis {
                            name 'ENV'
                            values 'qa'
                        }
                    }
                }

                stages {
                    stage('Checkout') {
                        steps {
                            checkout scm
                        }
                    }

                    stage('Build & Test') {
                        steps {
                            script {
                                if (env.OS == 'windows') {
                                    bat '''
                                    echo OS=%OS%
                                    echo ENV=%ENV%
                                    mvn clean test
                                    '''
                                } else {
                                    sh '''
                                    echo "OS=$OS"
                                    echo "ENV=$ENV"
                                    mvn clean test
                                    '''
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
