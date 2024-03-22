> [!IMPORTANT]
> This guide is written with the assumption that you are using a Windows machine, macOS users might find differences in setup and execution while following this guide.

# SimplyStars setup guide
## 1. First of all, head here: https://github.com/diheng99/SimplyStars

> [!NOTE]
> You need access to this repository before you're able to see its contents

## 2. Download its contents either through inbuilt tools in your code editor such as VSCode or manually unzip the files.

**Optional:** You can set up a Python environment if you have conflicting Python versions that are already installed on your machine!
Create the environment with:
```
python -m venv venv
```
this only has to be run **ONCE** and never again for that folder/version.
On **Windows** machine, change the execution policy of scripts with:
```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```
After changing this, activate the environment with:
```
venv\Scripts\activate
```
> [!CAUTION]
> You need to run both bolded statements above whenever you want to enter the environment. SimplyStars might not run if you do not enter the environment from now on.

> [!TIP]
> This method can also be used if your machine cannot detect dependencies that you've installed. Be sure to create the environment again and install all dependencies again.
**When you want to stop working on/using SimplyStars,**
Turn off the environment with: 
```
deactivate
```
Reset execution policies with: 
```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Restricted
```
> [!CAUTION]
> Forgetting to reset your execution policy opens up your machine to security risks as malicious actors can now run scripts in your terminal without administrator approval.
## 3. **Install these Python dependencies with pip:**
```
pip install bs4
pip install lxml
pip install flask
pip install requests
pip install flask_wtf
pip install flask_login
pip install flask_bcrypt
pip install flask_migrate
pip install flask_sqlalchemy

pip install email_validator
pip install google-auth-oauthlib
pip install google-api-python-client
```

## Additional Server Setup
Install MAMP here https://www.mamp.info/en/windows/

### Set MAMP >> Preferences to: 

#### Start/Stop
When starting MAMP: 
- [x] Start servers

#### Ports (Might not apply to all users)
Apache Port: 80
Nginx Port: 80
MYSQL Port: [Likely dynamically Set based on machine]

#### Server
Web Server >> Apache
Document Root >> C:\MAMP\htdocs
### Copy ALL php files [here](https://github.com/diheng99/SimplyStars/tree/master/PHP%20files) into "C:\MAMP\htdocs" as well.

## Gmail OTP API setup
#### Change the google API file location in "gmailAPI.py" so that it links to the location on YOUR machine.
```
SCOPES = ['https://www.googleapis.com/auth/gmail.send']
#filePathCred = 'C:\\Users\\Di heng\\Desktop\\SCSE Y2S2\\SC2006 Software Engineering\\Project\\credentials.json'
filePathCred = 'C:\\Users\\NAIRB\\Downloads\\SimplyStars 180224\\credentials.json'
#filePathToken = 'C:\\Users\\Di heng\\Desktop\\SCSE Y2S2\\SC2006 Software Engineering\\Project\\token.json'
filePathToken = 'C:\\Users\\NAIRB\\Downloads\\SimplyStars 180224\\token.json'
```
* On Windows Machine, hold shift and right-click to see the  "copy as path" option.
* On a MacOS Machine, use Command + Option + C shortcut to get this information instead.

## GMAIL API OTP Token Management
The "token.json" file contains the Gmail API OTP token that ***WILL*** expire every few days. The error below will appear if the token file has expired. 
```
google.auth.exceptions.RefreshError: ('invalid_grant: Token has been expired or revoked.', {'error': 'invalid_grant', 'error_description': 'Token has been expired or revoked.'})
```
**It is likely that every user/contributor MUST create their own token file before using SimplyStars.**

**This is because the token file links the OTP administrator email to the person who created the token file, i.e., The email that the OTP is sent from will be YOUR email.**

### If you encounter the issue mentioned above, setting up a new token is easy:
1. Delete the "token.json" file in your folder.
2. Rerun SimplyStars (go to run.py and hit Run Python File Icon)
3. SimplyStars will open a new webpage and ask you to sign into your Gmail account to recreate the "token.json" file.
4. After signing in and confirming that it was successful, close the tab and rerun SimplyStars.

# Additional Details
### You can view the Database file in instance >> SimplyStars.db with [DB Browser](https://sqlitebrowser.org/dl/)
The Database already comes with a default account:
```
Username: test
Password: 123
```

> This account can be used to log into SimplyStars if the user does not want to create an account, or has trouble with the Gmail OTP API and cannot create one themselves. 

# Current To Do List (Front End)
> **Note:** Backend last retrieved on 22th Mar 2024

* Make it so that cells merge when there are consecutive hours of the same session (rowspan)
* Cannot logout/signout
* Show alert when wrong OTP (or when cannot generate OTP)
* always generate one timetable if the same preferences and courses
* Add a notice to show that timetable generation is no longer possible


## Extra Features to be done but absolutely optional
* Allow users to select course index
* When searching for index codes, autogenerate the course names so people can select them (optional but a major non-functional plus point if working)
* Button to minimize details in the timetable
* NO more clashes allowed, don't need to make functionality for it, but would be good if we make a warning/highlight text in red in the case that SimplyStars fails to stop schedule clashes from showing up.
