def wrapStep(String stepName, Closure step) {
  println "In wrapStep ${stepName}"
  try {
    step(stepName)
  } catch (e) {
    notify('FAILED', stepName)
    throw e
  }
}

node {
  if (env.BRANCH_NAME == 'master') {
    wrapStep('clone', { name -> stage(name) { checkout scm } })
    wrapStep('deploy_dashboard', { name -> stage(name) { sh 'rsync -arv -e "ssh -2" package.json sshacs@unprotected.upload.akamai.com:/114034/insightsbeta/platform/storybook/' } })
  }
}
