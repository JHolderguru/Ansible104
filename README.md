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

5. Lauching a new instance.
 create an image from one of your nodes....then the configuration has andamin user with exchanged keys.


6. Implenting our Dynamic inventory
    vi dynamic_inventory
```
 #!/bin/python
import sys
try:
   import boto3
except Exception as e:
   print(e)
   print("Please rectify exception and then try again")
   sys.exit(1)

```
   have execution permissions --> chmod +X 

7. Assign the right IAM role to be able to run the python script.
   Python script to get our instances using tags
    ```
    #!/bin/python2
import sys
try:
   import boto3
except Exception as e:
   print(e)
   print("Please rectify exception and then try again")
   sys.exit(1)

def get_hosts(ec2_ob, fv):
   f={"Name":"tag:Env"  ,  "Values":  [fv]}
   hosts=[]
   for each_in in ec2_ob.instances.filter(Filters=[f]):
       #print(each_in.private_ip_address)
        hosts.append(each_in.private_ip_address)
   return hosts
def main():
   ec2_ob=boto3.resource("ec2","us-east-1")
   db_group=get_hosts(ec2_ob, 'db')
   server=get_hosts(ec2_ob, 'server')
   all_group={ 'db' : db_group, 'server' : server }
   print (all_group)
   return None


if __name__ == "__main__":
   main()


    ```
   
 





