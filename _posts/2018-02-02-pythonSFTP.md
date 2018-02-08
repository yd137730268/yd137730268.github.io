---  
layout: post  
title: Python SFTP  
date: 2018-02-02
categories: blog  
tags: [Python]  
description: Python SFTP    
  
---  
```
import paramiko
import os

def connect( ip, username, password, timeout=30):
    ip = ip
    username = username
    password = password
    timeout = timeout
    t = ''
    chan = ''
    try_times = 3
    t = paramiko.Transport(sock=(ip, 22))
    t.connect(username=username, password=password)
    sftp = paramiko.SFTPClient.from_transport(t)
    return sftp

def sftpPut(sftp, local_dir,local_cur, remote_dir):
    all_files = list()
    files = os.listdir(local_cur)
    for x in files:
        filename = os.path.join(local_cur, x)
        remote_filename = filename.replace(local_dir, remote_dir)
        if os.path.isdir(filename):
            print('mkdir' + remote_filename)
            try:
                sftp.mkdir(remote_filename)
            except IOError,e:
                print e.message
            all_files.extend(sftpPut(sftp, local_dir ,filename, remote_dir))
        else:
            print ('Put ' + filename + ' to ' + remote_filename)
            sftp.chdir(os.path.split(remote_filename)[0])
            #print(sftp.getcwd())
            #print(filename)
            #print(os.path.split(remote_filename)[-1])
            sftp.put(filename, os.path.split(remote_filename)[-1])
            all_files.append(remote_filename)
    return all_files

if __name__ == '__main__':
    localpath="/home/algodna/calibration/Calibration_SNAMM_v2.25.0/Calibration/uat_dev"
    remotepath="/tmp/test"

    sftp = connect('sd-df58-b302', 'dy83694', '****')
    sftpPut(sftp, localpath, localpath, remotepath)
```
