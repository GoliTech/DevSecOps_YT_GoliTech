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

