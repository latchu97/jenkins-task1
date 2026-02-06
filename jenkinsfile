pipeline {
  agent any

  environment {
    TARGET_DIR = "C:\\deploy\\myapp"
  }

  stages {
    stage('Checkout develop') {
      steps {
        checkout scm
      }
    }

    stage('Copy code to folder') {
      steps {
        bat '''
          echo Copying files...
          echo Workspace: %WORKSPACE%
          echo Target: %TARGET_DIR%

          if not exist "%TARGET_DIR%" mkdir "%TARGET_DIR%"

          robocopy "%WORKSPACE%" "%TARGET_DIR%" /MIR /XD ".git" /R:2 /W:2

          if %ERRORLEVEL% LEQ 7 (exit 0) else (exit %ERRORLEVEL%)
        '''
      }
    }
  }
}
