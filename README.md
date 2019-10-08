# Malicious Web Content Detecting using ML

## About
This repository is forked from [philomathic-guy](https://github.com/philomathic-guy/Malicious-Web-Content-Detection-Using-Machine-Learning).
I'm just trying to run and mark down what I've done to execute the program.

---

## Prior Work Done
I created an conda environment with Python 3.6.
(I choose 3.6 because 3.7 may be too new that something may not support)
```
conda create --name py3.6 python=3.6
```

Activate the environment
```
conda activate py3.6
```

Confirm the environment is activated and Python 3.6 is being used
```
python3 -V
```

Then I fork the project and clone to my Macbook

---

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
/anaconda3/envs/py3.6/bin/pip install whois google
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
My path is ```/anaconda3/envs/py3.6/bin/python3```

Confirm the path is correct
```
/anaconda3/envs/py3.6/bin/python3 -V
```
The output is ```Python 3.6.9 :: Anaconda, Inc.```

