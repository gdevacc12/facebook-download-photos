# Download Facebook Photos
While Facebook allows you to [download a copy of your data](https://www.facebook.com/help/212802592074644), this does not include photos that you are tagged in. 
Additionally, some of these photos are not high resolution.
Tony's script that this fork is based on allowed download of Facebook photos that you're tagged in and that you have uploaded. This script can also download photos of other Facebook users that have public pictures.
This fork handles some differences in the facebook sign in workflow that I encountered:
1. a prompt for cookie handling preference
2. a second prompt for the password
3. confirmation of a new sign in, from another already signed in session

This fork adds:
A. Automatic decline of the cookie
B. extending the sign in wait to 60 seconds to allow manual handling of 2 and 3 above.

Tony's code was tested on macOS, but should also work on Windows and Linux.
I ran from a MS-Windows WSL Penguin (Debian) machine.

## Prerequisites

Python 3, git, and Google Chrome

### 1. Create a virtual Python environment
```
python3 -m venv ~/env/fb
source ~/env/fb/bin/activate
```

### 2. Install the selenium package
```
python3 -m pip install --upgrade pip
pip install selenium
pip install webdriver-manager
```
 
### 3. Clone this repository
```
git clone https://github.com/gdevacc12/facebook-download-photos.git
cd facebook-download-photos
```
**NOTE:** 
*Be sure to replace *email* and *password* with your actual Facebook username, email, and password in the commands below*
*See the command reference below if needed*

### 4. Launch the script with one of the options
A. To download all Facebook photos that you are tagged in.
```
python download.py -e you@example.com -p password -a of
```

B. Download photos you have uploaded
```
python download.py -e you@example.com -p password -a by
```
C. Download someone else's photos
```
python download.py -u username -e you@example.com -p password -a of
python download.py -u username -e you@example.com -p password -a by
```
You should see a browser session open.

## 5. The facebook cookie preference should automatically be declined by the script

## 6. At the password prompt, paste in your password and continue

## 7. Check for a facebook notification in an existing session to confirm the new sign in is you.

## 8. Leave the script running.
You will see each photo in the browser before it is copied into a photos subfolder.

## Command reference
```
usage: download.py [-h] -e EMAIL -p PASSWORD [-a {of,by}] [-u USERNAME]

Download photos from Facebook

optional arguments:
  -h, --help            show this help message and exit
  -e EMAIL, --email EMAIL
                        Your Facebook email
  -p PASSWORD, --password PASSWORD
                        Your Facebook password
  -a {of,by}, --album {of,by}
                        Photo album to download (default: of). Use "of" to download
                        tagged photos. Use "by" to download uploaded photos.
  -u USERNAME, --username USERNAME
                        Facebook username to download photos from
  -t TIMEOUT, --timeout TIMEOUT
                        Wait this many seconds between photos (default: 2)
```
