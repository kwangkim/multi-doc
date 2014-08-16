# How to capture Live Streaming RTSP using FFmpeg
* Yum Repository
```sh
# cd /etc/yum.repos.d/
# vi rpmforge.repo
### Name: RPMforge RPM Repository for RHEL 6 - dag
### URL: http://rpmforge.net/
[rpmforge]
name = RHEL $releasever - RPMforge.net - dag
baseurl = http://apt.sw.be/redhat/el6/en/$basearch/rpmforge
mirrorlist = http://mirrorlist.repoforge.org/el6/mirrors-rpmforge
#mirrorlist = file:///etc/yum.repos.d/mirrors-rpmforge
enabled = 1
protect = 0
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmforge-dag
gpgcheck = 1

[rpmforge-extras]
name = RHEL $releasever - RPMforge.net - extras
baseurl = http://apt.sw.be/redhat/el6/en/$basearch/extras
mirrorlist = http://mirrorlist.repoforge.org/el6/mirrors-rpmforge-extras
#mirrorlist = file:///etc/yum.repos.d/mirrors-rpmforge-extras
enabled = 0
protect = 0
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmforge-dag
gpgcheck = 1

[rpmforge-testing]
name = RHEL $releasever - RPMforge.net - testing
baseurl = http://apt.sw.be/redhat/el6/en/$basearch/testing
mirrorlist = http://mirrorlist.repoforge.org/el6/mirrors-rpmforge-testing
#mirrorlist = file:///etc/yum.repos.d/mirrors-rpmforge-testing
enabled = 0
protect = 0
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmforge-dag
gpgcheck = 1
# vi epel-testing.repo
[epel-testing]
name=Extra Packages for Enterprise Linux 6 - Testing - $basearch
#baseurl=http://download.fedoraproject.org/pub/epel/testing/6/$basearch
mirrorlist=https://mirrors.fedoraproject.org/metalink?repo=testing-epel6&arch=$basearch
failovermethod=priority
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6

[epel-testing-debuginfo]
name=Extra Packages for Enterprise Linux 6 - Testing - $basearch - Debug
#baseurl=http://download.fedoraproject.org/pub/epel/testing/6/$basearch/debug
mirrorlist=https://mirrors.fedoraproject.org/metalink?repo=testing-debug-epel6&arch=$basearch
failovermethod=priority
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
gpgcheck=1

[epel-testing-source]
name=Extra Packages for Enterprise Linux 6 - Testing - $basearch - Source
#baseurl=http://download.fedoraproject.org/pub/epel/testing/6/SRPMS
mirrorlist=https://mirrors.fedoraproject.org/metalink?repo=testing-source-epel6&arch=$basearch
failovermethod=priority
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
gpgcheck=1
# rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt
```
* FFmpeg Download and Test
```sh
# yum install ffmpeg
# ffmpeg --help
# ffmpeg -i rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k -t 20 test.mp3
```
* Make Bash Script
```sh
# vi download_rtsp.sh
ffmpeg -i $4 -t $1 $3/$2.`date "+%Y%m%d.%H%M"`.mp3
# 
```
* Create Crontab Job
```sh
# crontab -e
59 14 * * 0-5 /home/eng/english/download_rtsp.sh 1230 lipeng /home/eng/english rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k
39 14 * * 0-5 /home/eng/english/download_rtsp.sh 1230 eareng /home/eng/english rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k
39 15 * * 0-5 /home/eng/english/download_rtsp.sh 1230 poweng /home/eng/english rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k
59 15 * * 0-5 /home/eng/english/download_rtsp.sh 6630 moreng /home/eng/english rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k
59 17 * * 0-5 /home/eng/english/download_rtsp.sh 1230 lipeng /home/eng/english/backup rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k
39 19 * * 0-5 /home/eng/english/download_rtsp.sh 1230 eareng /home/eng/english/backup rtsp://ebsandroid.ebs.co.kr/fmradiotablet500k/tablet500k
# service crond restart
```
