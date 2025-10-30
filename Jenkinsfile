pipeline {
    // Jenkins 노드에 Java 17이 설치되어 있다고 가정하고 기본 agent를 사용합니다.
    agent any

    // Gradle 캐시를 위한 환경 변수 설정 (기존과 동일)
    environment {
        GRADLE_USER_HOME = "${WORKSPACE}/.gradle"
    }

    stages {
        stage('Build & Test') {
            steps {
                // gradlew 스크립트에 실행 권한을 부여합니다 (중요)
                sh 'chmod +x ./gradlew'

                // 빌드 및 테스트를 실행합니다.
                sh './gradlew clean test'
            }
        }
    }

    // 빌드 후 결과 리포트를 수집합니다 (기존과 동일)
    post {
        always {
            junit 'build/test-results/test/*.xml'
            archiveArtifacts artifacts: 'build/reports/tests/test/**/*', allowEmptyArchive: true
        }
    }
}
