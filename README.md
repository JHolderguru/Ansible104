Dynamic Inventory

1. To work with a Dynamic Inventory we have to download  https://raw.githubusercontent.com/ansible/ansible/stable-1.9/plugins/inventory/ec2.py
https://raw.githubusercontent.com/ansible/ansible/stable-1.9/plugins/inventory/ec2.ini ec2.py and ec2.ini from an official repo.

```
shown ansadmin (folder to give copy permissions)

 scp -i ./Ansible.pem / ~/Desktop/ec2.ini ansadmin@ec2-x-xx-xx-xxx.compute-1.amazonaws.com:/home/ansadmin/ans_dev

```

2. Save the files to your ansible dir in the engine.
  ```
    chmod 755 ec2.py
    chmod 755 ec2.ini

  ```

3. Install boto (to run py files)
  ```
  pip2 install boto

  ``` 

4. Assign Ansible AWS role to instance - ec2full
  ```
  #list all ec2 inventry
  ./ec2.py 
  #Working with a region
  ansible -i ec2.py us-east-1a -m ping  
  #Working with ec2
  ansible -i ec2.py ec2 -m ping
  ```




