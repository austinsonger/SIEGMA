# SIΣGMA

This project aims to automate the creation of SIEM rule consumables by leveraging a pre-defined set of configurations/mappings and by utilizing the [Sigma](https://github.com/Neo23x0/sigma) rule format and engine.

<p align="center"><img align="center" src="https://i.imgur.com/laf6vv6.png"></p>

It is also our objective to keep SIEM schemas documented and community-maintained, so you are free to make contributions from a data as well as a programming perspective. Help is welcome!

## Supported SIEM's

* Elastic SIEM
* Splunk Enterprise Security (future release)

# Installation

We'll run the software and install dependencies, for both this project as well as Sigma, under a Python virtual environment. 
      
`pip3 install virtualenv` 
    
* Setup Sigma

```
git clone https://github.com/Neo23x0/sigma
cd sigma
python3 -m virtualenv .venv3
# activate virtual environment
. .venv3/bin/activate
cd tools
pip install -r requirements.txt
```

* Setup SIEGMA

```
# Download Sigma2SIEM repo
# cd into the repo
# create virtual environment
python3 -m virtualenv .venv3
# activate virtual environment
. .venv3/bin/activate
# install required libraries
pip install -r requirements.txt
```

*Note for Windows users*: Powershell must be enabled for command and script execution. Open `Administrative Powershell` and execute following command: `Set-ExecutionPolicy Bypass` 

**Before running SIEGMA:** Sigma rules might not hold all required fields in use by your SIEM. To make sure that all fields are mapped correctly, each product holds a README where we warn you if there are fields that need to be filled before running this software.

Visit your SIEM [config](config/) folder to learn more about this.

## Usage
 
Invoke the script by providing it a Sigma rule or Sigma rule folder as well as the desired SIEM platform. 

Activate the virtual environment:
 
`. .venv3/bin/activate`
   
See the available options:
 
`python siegma.py -h`

Generate an Elastic SIEM output from a single Sigma rule file:
 
`python siegma.py -c config/elastic/elastic-siem.json -r /path/to/rule.yml -sv /path/to/sigma/virtualenv -s /path/to/sigma/folder -sc /path/to/sigma/config/file/sigma/tools/config/file.yml -o rule-output`
 
Generate an Elastic SIEM output from a folder with several Sigma rule files:

`python siegma.py -c config/elastic/elastic-siem.json -r /path/to/folder/with/sigma-rules/ -sv /path/to/sigma/virtualenv -s /path/to/sigma/folder -sc /path/to/sigma/config/file/sigma/tools/config/file.yml -o rule-output`

An example where we utilize our [AWS CloudTrail Sigma configuration](https://blog.3coresec.com/2020/05/contributions-to-sigma-cloudtrailecs.html) to convert a single rule to Elastic SIEM output:

`python siegma.py -c config/elastic/elastic-siem.json -r rules/cloudtrail_rule.yml -sv /path/to/sigma/virtualenv -s sigma/ -sc sigma/tools/config/ecs-cloudtrail.yml -o rule-output`

Once files are created they can be imported into the platform. Support to automate this process is currently being developed.

# Contributions and Development

Want to know more how it all comes together or want to contribute support for a new platform? Check the [development guide](./development-guide.md) for more information. 

## Roadmap

- Additional platform/SIEM support
  - Splunk is currently in development
- Dispatcher functionality - Automatically upload to your SIEM after creating the consumable

# Feedback

Found this interesting? Have a question/comment/request? Let us know! 

Feel free to open an [issue](https://github.com/3CORESec/SIEGMA/issues) or ping us on [Twitter](https://twitter.com/3CORESec).

[![Twitter](https://img.shields.io/twitter/follow/3CORESec.svg?style=social&label=Follow)](https://twitter.com/3CORESec)