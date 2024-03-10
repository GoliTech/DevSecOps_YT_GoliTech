# Software Component Analysis using NPM Audit
# Local
## Download the source code
first, we need to download the source code of the project from our git repository.
```
git clone https://gitlab.practical-devsecops.training/pdso/django.nv webapp
```
```
cd webapp
```
## Install NPM
> NPM has security build in since npm@6, this command allow you to analyze dependencies in your existing code to identify insecure dependencies, have a good security report, and also easy to implement it into CI/CD pipeline without install any packages except NPM itself.

We will install NodeJS and also NPM with the following command.
```
curl -sL https://deb.nodesource.com/setup_14.x | bash -
```
```
apt install nodejs -y
```
npm audit tool is part of npm and it gets installed when you install node.js. Let’s check the help menu of npm audit to understand its feature set.
```
npm audit -h
```
We can run the basic command without any extra arguments, however the output is not suitable for a CI/CD pipeline because the output is not in a machine readable format.
First, we need to install the dependencies using npm install.
```
npm install
```
Let’s run the npm audit command.
```
npm audit
```
As we can see, the basic command gives us the report in a table format, We can save the output in JSON format using --json flag.
```
npm audit --json | tee results.json
```


# GitHub

```yml
name: Django                                  # workflow name
on:
  push:
    branches:                                
      - main
  workflow_dispatch:

jobs:

  oast_npm_audit:                             # workflow name
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2             # Checkout our code

      - uses: actions/setup-node@v2           # Provisioning node on the server
        with:
          node-version: '18'
      
      - run: npm install                      # Install the dependencies on the server for the scan
      - run: npm audit --json | tee npm_audit_report.json

      - uses: actions/upload-artifact@v2
        with:
          name: nmp_audit
          path: npm_audit_report.json
```











