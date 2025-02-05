# Malicious Web Content Detecting using ML

## About
This repository is forked from [philomathic-guy](https://github.com/philomathic-guy/Malicious-Web-Content-Detection-Using-Machine-Learning).
I'm just trying to run and mark down what I've done to execute the program.

## Prior Work Done
Create an conda environment with Python 2.7. (The code support Python 2 only)
```
conda create --name py2.7 python=2.7
```

Activate the environment
```
conda activate py2.7
```

Confirm the environment is activated and Python 2.7 is being used
```
python2 -V
```

Then, I fork the project and clone to my Macbook

## Environment Setup
### Python and Packages
Install required packages defined in requirements.txt
```
conda install joblib numpy scikit-learn beautifulsoup4 whois google
```

However, google and whois aren't available so I install without google and whois
```
conda install joblib numpy scikit-learn beautifulsoup4
```

This [answer](https://stackoverflow.com/a/43729857) tells how to use pip to install packages to anaconda environment.

Install pip inside the environment
```
conda install pip
```

Use the pip inside the environment to install whois and google
```
/anaconda3/envs/py2.7/bin/pip install whois google
```

### Web Server
As the built-in WebServer has been removed in new releases of macOS, I follow this [article](https://discussions.apple.com/docs/DOC-13841) to setup.

After setting up the web server, move the whole repository folder to /Library/Server/Documents

Go into the repository folder and create a txt named 'markup.txt'
```
touch markup.txt
```

Give permissions to the markup file
```
sudo chmod 777 markup.txt
```

Find the path of the Python 3.6 in the conda environment
My path is ```/anaconda3/envs/py2.7/bin/python2```

Confirm the path is correct
```
/anaconda3/envs/py2.7/bin/python2 -V
```
The output is ```Python 2.7.16 :: Anaconda, Inc.```

Modify the path of the Python 2.7 installation in clientServer.php as ```/anaconda3/envs/py2.7/bin/python2```

Since I am not using the personal website (~/Sites/) but using the global one (/Library/WebServer/Documents), I don't have to modify LOCALHOST_PATH and DIRECTORY_NAME in features_extraction.py

### Chrome
1. Open Chrome.
1. Go to ```chrome://extensions```
1. Activate "Developer mode"
1. Click on "Load unpacked"
1. Select the "Extension" folder in this repository

### Trial Run
I openned Chrome and clicked the extension.
Then, I clicked "SAFE OR NOT?"
However, I see
> // Purpose - This file acts as a mediator between the client side popup.js and the server side test.py. // It gets the HTML contents which acts as input to the suite of python files. <br /> <b>Warning</b>: Cannot modify header information - headers already sent by (output started at /Library/WebServer/Documents/Malicious-Web-Content-Detection-Using-Machine-Learning/clientServer.php:1) in <b>/Library/WebServer/Documents/Malicious-Web-Content-Detection-Using-Machine-Learning/clientServer.php</b> on line <b>5</b><br /> SAFE

Something is wrong in the clientServer.php

### Fix the Comments Issue
Open "clientServer.php".

Cut the first two lines.
```
// Purpose - This file acts as a mediator between the client side popup.js and the server side test.py.
// It gets the HTML contents which acts as input to the suite of python files.
```

Paste under ```header("Access-Control-Allow-Origin: *");```.

Save and try the extension again.

## Test Results
| Sites | Expected Results | Actual Results |
| --- | --- | --- |
| google.com | SAFE | SAFE |
| bing.com | SAFE | SAFE |
| learn.polyu.edu.hk | SAFE | PHISHING |
| eie.polyu.edu.hk | SAFE | PHISHING |

## 20 Features Used
### Address Bar Based
1. The domain part of URL has IP?
1. The URL length is >75?
1. Is URL shortening service used?
1. Does '//' appear after 'https://' to redirect?
1. Does the domain part of the URL contain '-'?
1. Is the domain a subdomain?
1. Is the domain expiring on a year?
1. Is the favicon loaded from external domain?
1. Does the domain part of the URL contain 'http' or 'https'?

### Abnormal Based
1. Does the webpage contain large percentage of external objects?
1. Does the webpage contain large percentage of hyperlinks linked to external webpage?
1. Does the webpage contain large percentage of meta/script/link tag using external source?
1. Is the Server Form Handler using an external domain?
1. Is there web form submitting data via 'mailto:'?
1. Is the host name from Whois included in the URL?

### HTML & JavaScript
1. Is iframe redirection used?

### Domain Based
1. Is age of domain less than 6 months?
1. Is the Alexa website rank outside top 100,000?
1. Is the web page not indexed by Google?
1. Does the host belong to top phishing IPs / domains based on 3rd party database?
