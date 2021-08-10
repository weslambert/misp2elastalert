# misp2elastalert
## Convert MISP events to Elastalert rules

NOTE: This project is a WIP -- feedback is welcome!

### Overview
1. Sigma rules are generated from MISP events using [sigmai](https://github.com/0xThiebaut/sigmai).
2. The generated Sigma rules are converted to Elastalert rules using [sigmac](https://github.com/SigmaHQ/sigma#sigmac).

### Prerequisites
It is assumed that Sigmai and the Sigma repo are already downloaded to the machine.

The latest Sigmai release can be obtained from [here](https://github.com/0xThiebaut/sigmai/releases/tag/v1.0.0).

Ensure the Sigmai binary is executable with `chmod +x $sigmaibinaryname`. 

The sigma repo can be cloned with git, like so:

`git clone https://github.com/SigmaHQ/sigma`

You may run into an error with regard to distutils/Python.  In most cases, the following should resolve the issue:

`sudo apt-get install python3-distutils`

### m2s2se
The bash script, `m2s2e` allows for tweaking the various backend options (the ones provided are an example) and other parameters to match your environment.

Change these variables to match your environment, and run the script via cron job, or similar.

The variables defined within the script are as follows:

`MISP="https://misp"` - MISP URL

`APIKEY="ABCD1234"` - API key for MISP

`SIGMAI="/home/onionuser/sigmai"` - Path for sigmai

`SIGMAPATH="/home/onionuser/sigma"` - Path for Sigma repo

`SIGMAC="$SIGMAPATH/tools/sigmac"` - Path for sigmac

`SIGMACONFIGPATH="$SIGMAPATH/tools/config"` - Path for Sigma mappings

`SIGMARULES="/home/onionuser/sigmarules"` - Output path for Sigma rules from MISP

`ELASTALERTRULES="/opt/so/rules/elastalert/misp"`- Output path for Elastalert rules

`CONFIGOPTIONS="-c /home/onionuser/securityonion-baseline.yml"`- Sigmac mappings

`BACKENDOPTIONS="--backend-option alert_methods=email --backend-option emails=blah@mycompany.com --backend-option keyword_whitelist=source.ip,destination.ip,source.port,destination.port --backend-option keyword_field=.keyword --backend-option analyzed_sub_field_name=.security --backend-option wildcard_use_keyword=false"` - Options for sigmac backends

`MISP_INSECURE="--misp-insecure"` - Whether or not to perform verification w/ TLS

`MISP_FILTER="--misp-levels 1,2"` - Filter used for MISP events 
