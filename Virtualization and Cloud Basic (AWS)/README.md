AWS Cloud Basic 

#### 1. Read the terms of Using the[  AWS Free Tier  ](https://docs.aws.amazon.com/en_us/awsaccountbilling/latest/aboutv2/billing-free-tier.html)and the ability to control their own costs.
#### 2. [Register  with AWS  ](https://portal.aws.amazon.com/billing/signup?redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start)(first priority) or alternatively, you can request access to courses  in[  AWS ](https://aws.amazon.com/training/awsacademy/member-list/) [Academy  ](https://aws.amazon.com/training/awsacademy/member-list/)if you are currently a student of[  certain University.](https://aws.amazon.com/training/awsacademy/member-list/)
#### 3. Find the[  hands-on tutorials  ](https://aws.amazon.com/ru/getting-started/hands-on/?awsf.getting-started-category=category%23compute&amp;awsf.getting-started-content-type=content-type%23hands-on&amp;?e=gs2020&amp;p=gsrc&amp;awsf.getting-started-level=*all)and[  AWS Well-Architected Labs  ](https://www.wellarchitectedlabs.com/)for  your AWS  needs. Explore list of step-by-step tutorials for deferent  category. Use, repeat as  many as you  can and have fun))
#### 4. Register and pass courses on[  AWS Educate.](https://www.awseducate.com/) Filter by checking Topic Cloud Computing and Foundational Level. Feel free to pass more. 

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Virtualization%20and%20Cloud%20Basic%20(AWS)/Docs/AWS-educate-screen.png">
</p>

#### 5. Register and pass free courses  on[  AWS Skillbuilder](https://explore.skillbuilder.aws/learn). AWS Cloud  Practitioner Essentials: Core Services, AWS Cloud  Practitioner Essentials: Cloud Concepts. Try AWS Cloud  Quest: Cloud Practitioner. 

<p align="center">
  <img src="">
</p>

#### 6. Pass free courses on[  Amazon  qwiklabs ](https://amazon.qwiklabs.com/)

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Virtualization%20and%20Cloud%20Basic%20(AWS)/Docs/quicklabs-screen.png">
</p>

#### 7. Review[  Getting  Started  with  Amazon  EC2.](https://aws.amazon.com/ec2/getting-started/?nc1=h_ls)  Log  Into  Your  AWS  Account,  Launch,  Configure,  Connect and Terminate Your Instance. Do not use Amazon Lightsail. It is recommended to use the t2 or t3.micro instance and the CentOS operating system. 

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Virtualization%20and%20Cloud%20Basic%20(AWS)/Docs/7-point.png">
</p>

#### 8. Create a snapshot of  your instance to keep as a backup.

__[Amazon EC2 backup and recovery with snapshots and AMIs](https://docs.aws.amazon.com/prescriptive-guidance/latest/backup-recovery/ec2-backup.html)__

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Virtualization%20and%20Cloud%20Basic%20(AWS)/Docs/8-point-Snapshot.png">
</p>

#### 9. Create and attach a Disk_D (EBS) to your instance to add more storage space. Create and save some file on Disk_D.

[Make an Amazon EBS volume available for use on Linux](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html)

```console
# Login to your ec2 instance and list the available disks using the following command.
lsblk

# Format the volume to the ext4 filesystem using the following command.
sudo mkfs -t ext4 /dev/xvdf

# Create a directory of your choice to mount our new ext4 volume.
sudo mkdir /mnt/Disc_D

# Mount the volume to “Disc_D” directory using the following command.
sudo mount /dev/xvdf /mnt/Disc_D

# Check the disk space to validate the volume mount.
df -h

# Create file on Disk_D
sudo sh -c "echo EPAM University Programs - AWS > /mnt/Disk_D/file2.txt"
cat /mnt/Disk_D/file2.txt

# To unmount the volume, use the unmount command as shown below..
umount /dev/xvdf
```

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Virtualization%20and%20Cloud%20Basic%20(AWS)/Docs/9-point-1.png">
</p>

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Virtualization%20and%20Cloud%20Basic%20(AWS)/Docs/9-point-2.png">
</p>

#### 10. Launch the second instance from backup.

__[Restoring from an Amazon EBS snapshot or an AMI](https://docs.aws.amazon.com/prescriptive-guidance/latest/backup-recovery/restore.html)

> Follow these steps to restore a volume to an earlier point-in-time backup by using the console:
> - On the Amazon EC2 console, on the Elastic Block Store menu, choose Snapshots.
> - Search for the snapshot that you want to restore, and select it.
> - Choose Actions, and then choose Create Volume.
> - Create the new volume in the same Availability Zone as your EC2 instance.
> - On the Amazon EC2 console, select the instance.
> - In the instance details, make note of the device name that you want to replace in the Root device entry or Block Devices entries.
> - Attach the volume. The process differs for root volumes and non-root volumes.
<p align="center">
  <img src="">
</p>

> For root volumes:
> - Stop the EC2 instance.
> - On the EC2 Elastic Block Store Volumes menu, select the root volume that you want to replace.
> - Choose Actions, and then choose Detach Volume.
> - On the EC2 Elastic Block Store Volumes menu, select the new volume.
> - Choose Actions, and then choose Attach Volume.
> - Select the instance that you want to attach the volume to, and use the same device name that you noted earlier.
<p align="center">
  <img src="">
</p>


