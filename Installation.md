# Installation

Relevant software to install: Anaconda (open source distribution of python) and atom (a very good source code editor that supports multiple languages)

### Python & Code Editor 
Uninstall any previous versions of python or anaconda, if any.

#### Install Anaconda3-4.1.1 [64-bit](https://repo.continuum.io/archive/Anaconda3-4.1.1-Windows-x86_64.exe) or [32-bit](https://repo.continuum.io/archive/Anaconda3-4.1.1-Windows-x86.exe) (click on the relevant link) on your local windows computer.

By default, Anaconda will install jupyter notebooks and spyder code editors.

#### Install Atom from this [link.](https://atom.io/) If you prefer any other code editor install that.

### Enviornment & Libraries

To install the libraries that are required for Dashboard, you have to create an environment first.

#### 1) Open Anaconda prompt, run it as admin.

#### 2) Enter following command in prompt:
```
$ pip install virtualenv
```

#### 3) Create an evironment (navigate in command prompt to the folder where you want to save env folder)
```
$ virtualenv my_environment
```
This will create a my_environment folder. You have to activate this environment before installing the libraries. 

#### 4) Activate env. There should be a Scripts folder in name_of_environment folder. It will contain activate.bat file copy this filepath.

(If I created env folder in Documents folder then you have to enter below command in prompt)
```
$ C:\Users\username\Documents\my_environment\Scripts\activate.bat
```
Whenever you are working on Dashboard you should activate this environment.

#### 5) There is a requirements.txt in project's github home folder. Download and save it to the folder your command prompt is on. And enter the following command:
```
$ pip install -r requirements.txt
```
This will install all the libraries required for Dashboard.
