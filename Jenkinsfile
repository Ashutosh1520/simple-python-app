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
		stage("Build") {
			steps {
				sh 'python -m py_compile sources/add2vals.py sources/calc.py'
				stash(name: 'compiled result', includes: 'sources/*.py')
			}
		}
		stage("Test") {
			steps {
				sh 'pytest --junit-xml test-reports/results.xml sources/test_calc.py'
			}
			post {
				always {
					junit 'test-reports/results.xml'
				}
<<<<<<< HEAD
			}	
=======
			}
>>>>>>> fb8ef501b0db0c5ca1507a3f6a96ad1dd2f64032
		}
	}
}
				   
