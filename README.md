Dynamic Inventory

1. To work with a Dynamic Inventory we have to download  https://github.com/ansible-collections/community.aws/tree/main/scripts/inventory ec2.py and ec2.ini from an official repo.

```
shown ansadmin (folder to give copy permissions)

 scp -i ./Ansible.pem / ~/Desktop/ec2.ini ansadmin@ec2-x-xx-xx-xxx.compute-1.amazonaws.com:/home/ansadmin/ans_dev

```

2. Save the files to your ansible dir in the engine.

3. Install boto (to run py files)
  ```
  pip2 install boto

  ``` 
