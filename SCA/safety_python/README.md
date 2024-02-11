# Software Component Analysis using Safety
# Local


## Download the source code

First, we need to download the source code of the project from our git repository.

```
git clone URL webapp
```
```
cd webapp
```

> Safety checks your installed dependencies for known security vulnerabilities. By default, it uses the open Python vulnerability database Safety DB but can be upgraded to use pyup.io’s Safety API using the –key option.
<br>Source:<br> 
https://pypi.org/project/safety<br>
https://github.com/pyupio/safety

## Install Safety Tool
To perform scans on Python dependencies for known security vulnerabilities, let's install the Safety tool on the system.
```
pip3 install safety==2.3.5
```

## Explore Safety Options
To explore the options provided by Safety, you can use the following command:
```
safety check --help
```
## Run the scanner
```
safety check -r requirements.txt --json | tee safety-output.json
```
-r flag used to specify the input file.<br>
--json flag tells that output should be in the JSON format.


# GitHub

# Create the pipeline
add this to the ```.github/workflows/main.yml```
```yml
  oast:
    runs-on: ubuntu-20.04
    needs: test
    steps:
      - uses: actions/checkout@v2

      - run: docker run --rm -v $(pwd):/src hysnsec/safety check -r requirements.txt --json | tee oast-results.json

      - uses: actions/upload-artifact@v2
        with:
          name: Safety
          path: oast-results.json
        if: always()                    
```

# GitLab


Add this job to ```.gitlab-ci.yml```

```yml
test:
  stage: test
  script:
    # We are going to pull the hysnsec/safety image to run the safety scanner
    - docker pull hysnsec/safety
    # third party components are stored in requirements.txt for python, so we will scan this particular file with safety.
    - docker run --rm -v $(pwd):/src hysnsec/safety check -r requirements.txt --json > oast-results.json
  artifacts:
    paths: [oast-results.json]
    when: always # What does this do?
  allow_failure: true
```

