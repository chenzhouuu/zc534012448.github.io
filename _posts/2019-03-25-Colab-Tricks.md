---
title: Colab Tricks
layout: post
date: 2019-03-25 1:00
image: /assets/images/ColabTricks/colab.jpeg
headerImage: true
tag:
- colab
- google
- tutorial

star: false
category: blog
author: Rohit Midha
---

A collection of a few python scripts I have found to be useful as and when I have used Colab.

This list will be updated as and when I find cooler tricks!

# Contents

- [Upload Computer File into Colab](#upload-computer-file-into-colab)
- [Download Computer File into Colab](#download-computer-file-into-colab)
- [Download and Unzip File stored in Colab](#download-and-unzip-file-stored-in-colab)
- [Download and Unzip File stored in Colab](#download-and-unzip-file-stored-in-colab)
- [Mounting your Google Drive as a Folder](#mounting-your-google-drive-as-a-folder)
- [Send Alert Email at finish with GMail](#send-alert-email-at-finish-with-gmail)
- [Know your RAM and GPU Memory](#know-your-ram-and-gpu-memory)
- [Show GPU Memory while Training](#show-gpu-memory-while-training)

---

### Upload Computer File into Colab


```python
from google.colab import files
uploaded = files.upload()
```



---

### Download Computer File into Colab


```python
files.download('saved_file.h5')
```

---

### Download and Unzip File stored in Colab


```python
!pip install -U -q PyDrive

# Insert your file ID
# Get it by generating a share URL for the file
# An example : https://drive.google.com/file/d/1iz5JmTB4YcBvO7amj3Sy2_scSeAsN4gd/view?usp=sharing
zip_id = '1iz5JmTB4YcBvO7amj3Sy2_scSeAsN4gd'

from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials
import zipfile, os

# 1. Authenticate and create the PyDrive client.
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

if not os.path.exists('MODEL'):
    os.makedirs('MODEL')

# 2. Download Zip
print ("Downloading zip file")
myzip = drive.CreateFile({'id': zip_id})
myzip.GetContentFile('model.zip')

# 3. Unzip
print ("Uncompressing zip file")
zip_ref = zipfile.ZipFile('model.zip', 'r')
zip_ref.extractall('MODEL/')
zip_ref.close()
```

---


### Zip and Upload Folder to Drive


```python
!pip install -U -q PyDrive

from google.colab import files
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials
import zipfile
import os
import sys

zipname = 'model_v0.1'

def zipfolder(foldername, target_dir):            
    zipobj = zipfile.ZipFile(foldername + '.zip', 'w', zipfile.ZIP_DEFLATED)
    rootlen = len(target_dir) + 1
    for base, dirs, files in os.walk(target_dir):
        for file in files:
            fn = os.path.join(base, file)
            zipobj.write(fn, fn[rootlen:])

zipfolder(zipname, '/content/MODEL/')

# 1. Authenticate and create the PyDrive client.
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

# 2. Create & upload a file text file.
file1 = drive.CreateFile()
file1.SetContentFile(zipname+".zip")
file1.Upload()
```

---

### Mounting your Google Drive as a Folder


```python

from google.colab import drive
drive.mount('/content/gdrive',force_remount=True)
```


---

### Send Alert Email at finish with GMail


```python

import smtplib

server = smtplib.SMTP('smtp.gmail.com', 587)
server.starttls()
server.login("sender_gmail_here@gmail.com", "your_password_here")

msg = "COLAB WORK FINISH ALERT!"
server.sendmail("sender_gmail_here@gmail.com", "receiver_gmail_here@gmail.com", msg)
server.quit()
```

---

### Know your RAM and GPU Memory


```python
# memory footprint support libraries/code
!ln -sf /opt/bin/nvidia-smi /usr/bin/nvidia-smi
!pip install gputil
!pip install psutil
!pip install humanize
import psutil
import humanize
import os
import GPUtil as GPU
GPUs = GPU.getGPUs()
# XXX: only one GPU on Colab and isn’t guaranteed
gpu = GPUs[0]
def printm():
  process = psutil.Process(os.getpid())
  print("Gen RAM Free: " + humanize.naturalsize( psutil.virtual_memory().available ), " I Proc size: " + humanize.naturalsize( process.memory_info().rss))
  print("GPU RAM Free: {0:.0f}MB | Used: {1:.0f}MB | Util {2:3.0f}% | Total {3:.0f}MB".format(gpu.memoryFree, gpu.memoryUsed, gpu.memoryUtil*100, gpu.memoryTotal))
printm()
```


---

### Show GPU Memory while Training


```python
!ln -sf /opt/bin/nvidia-smi /usr/bin/nvidia-smi
!pip install gputil
!pip install psutil
!pip install humanize
import psutil
import humanize
import os, time
import GPUtil as GPU

GPUs = GPU.getGPUs()
# XXX: only one GPU on Colab and isn’t guaranteed
gpu = GPUs[0]
def worker():
  if SHOW_GPU_USAGE_TIME == 0:
    return;
  while True:
    process = psutil.Process(os.getpid())
    print("Gen RAM Free: " + humanize.naturalsize( psutil.virtual_memory().available ), " I Proc size: " + humanize.naturalsize( process.memory_info().rss))
    print("GPU RAM Free: {0:.0f}MB | Used: {1:.0f}MB | Util {2:3.0f}% | Total {3:.0f}MB".format(gpu.memoryFree, gpu.memoryUsed, gpu.memoryUtil*100, gpu.memoryTotal))
    time.sleep(SHOW_GPU_USAGE_TIME)

import threading
t = threading.Thread(target=worker, name='Monitor')
t.start()
```
---
