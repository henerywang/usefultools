# usefultools
## html to pdf
> https://wkhtmltopdf.org/downloads.html

## centos samba install
* yum -y install samba samba-client
* vim smb.conf
> [global]
> 
> workgroup = WORKGROUP
> 
> server string = Samba Server %v
> 
> netbios name = centos
> 
> security = user
> 
> map to guest = bad user
> 
> dns proxy = no
> 
> #============================ Share Definitions ============================== 
> 
> [samba]
> 
> path = /home/samba
> 
> browsable =yes
> 
> writable = yes
> 
> guest ok = yes
> 
> read only = no

* chmod -R 777 samba
* chmod -R nobody:nobody samba
* chcon -t samba_share_t samba
* systemctl restart smb nmb


## centos sshd install
* yum install openssh*
* systemctl enable sshd 
* systemctl start sshd
* service firewalld stop
