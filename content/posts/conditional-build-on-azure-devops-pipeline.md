+++
date = 2020-11-16T00:00:00Z
draft = true
title = "Conditional Build on Azure DevOps Pipeline"

+++
# Conditional Build on Azure DevOps Pipeline

We have a yaml file that lists down all the services with the domain name. The build runs nightly, and then creates a scorecard for each service. It's to encourage teams to pay technial debts and to maintain high enginering standard. 

Recently, I worked on this yaml file to auto-generate some wiki pages and noticed that the master branch gets often broken. It was because there wasn't any triggered build for PRs. It's yaml 