pipeline {
	agent {
		docker { image "python:3.9" }
	}
	triggers {
		githubPush()
	}
	stages {
		stage("Checkout") {
			steps {
				git branch: "master",
				    url: "https://github.com/Ashutosh1520/simple-python-app.git"
			}
		}
		stage("Setup venv") {
			steps {
				sh '''
				    python -m venv venv
				    ./venv/bin/pip install --upgrade pip setuptools wheel
				    ./venv/bin/pip install pytest pyinstaller
				   '''
			}
		}
		stage("Build") {
			steps {
				sh 'python -m py_compile sources/add2vals.py sources/calc.py'
				stash(name: 'compiled result', includes: 'sources/*.py')
			}
		}
		stage("Test") {
			steps {
                sh '''
                   ./venv/bin/pytest --junit-xml=test-reports/results.xml sources/test_calc.py
                '''
            }
			post {
				always {
					junit 'test-reports/results.xml'
				}
			}
		}
		stage("deliver") {
			steps {
				sh '''
				   ./venv/bin/pyinstaller --onefile sources/add22vals.py
				   '''
			}
			post { 
				success {
					archiveArtifacts "dist/add2vals"
				}
			}
		}
	}
}
				   
