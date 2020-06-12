# Sonarqube Helm Chart

##  Upgrade Sonar
Repo: https://github.com/totalwinelabs/sonarqube-helm

### Check for new version available
https://admin.staging.twmlabs.com/sonarqube/admin/system

### Check for version id for the Developer edition from link to new version
Grab new version id and put in Jenkinsfile 

### Update any plugins in the /docker/plugins directory to latest
ie. https://github.com/dependency-check/dependency-check-sonar-plugin
Upgrade to latest of any plugins

### Push Code and let Jenkins build
Validate sonarqube is running and new in the quality namespace
```kubectl -n quality get pods```

### Upgrade database from setup page in sonarqube once it's up
Navigate to https://admin.staging.twmlabs.com/sonarqube/setup
Upgrade database