---
layout: post
title: unix shell sendmail with attachment
date: 2016-12-01
categories: blog
tags: [unix]
description: unix shell sendmail with attachment

---


export MAILPART="$(uuidgen)"


export MAILFROM="dy83694@imcap.ap.ssmb.com"
export MAILTO="dy83694@imcap.ap.ssmb.com"
export SUBJECT="YB monitor"
export ATTACH="ybmonitor.csv"


export BODY="YB API monitor"


echo "To: $MAILTO
From: $MAILFROM
Subject: $SUBJECT
Content-Type: multipart/mixed; boundary=\"$MAILPART\"
MIME-Version: 1.0


This is a multi-part message in MIME format.
--$MAILPART
Content-Type: text/html
Content-Disposition: inline


<html><body>$BODY.</body></html>


--$MAILPART
Content-Transfer-Encoding: base64
Content-Type: application/octet-stream; name=ybmonitor.csv
Content-Disposition: attachment; filename=ybmonitor.csv


`base64 ybmonitor.csv`
--$MAILPART--" | /usr/sbin/sendmail -t


<img src="/assets/image/test.png" alt="替代文本" title="标题文本" width="200" height = "100" />

