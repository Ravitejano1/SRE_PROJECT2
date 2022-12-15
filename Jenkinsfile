node{

                 stage('Clone repo'){
                 git branch: 'main', credentialsId: 'Githubcredentials', url: 'https://github.com/Ravitejano1/SRE_PROJECT2.git'
                }

                stage('Maven Build'){
                def mavenHome = tool name: "Maven-3.8.6", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} clean package"
                }

                stage('SonarQube analysis') {
                withSonarQubeEnv('Sonar-Server-7.8') {
                def mavenHome = tool name: "Maven-3.8.6", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} sonar:sonar"
                }
        }

                stage('upload war to nexus'){
                        nexusArtifactUploader artifacts: [
                        [
                                artifactId: 'sreproject',
                                classifier: '',
                                file: 'target/raviproject.jar',
                                type: 'jar'
                                ]
                        ],
                                credentialsId: 'nexus3',
                                groupId: 'com.SRE',
                                nexusUrl: 'http://18.209.164.184:8081/repository/Srerelease/',
                                nexusVersion: 'nexus3',
                                repository: 'Srerelease/',
                                protocol: 'http',
                                version: '2.0.0'
                        }
        }
