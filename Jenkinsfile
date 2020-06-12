def sonarVersion="8.2.0.32929"
def buildNumber="1"
if ("master" == "${env.BRANCH_NAME}") {
  common.killOldDeployments()
  node("staging-base") {
      stage("Build") {
          gitCheckout{}
          stash includes: "**/*", name: "source"
          cloud.loginStaging()
          dockerImage.buildPush("docker","sonarqube-de", "${sonarVersion}-${buildNumber}", "--build-arg VERSION=${sonarVersion}")
      }

      stage("Deploy Staging") {
          helm.deploy("sonarqube", "quality", "--set image.tag=${sonarVersion}-${buildNumber}")
      }
	}
}