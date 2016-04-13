## ansible-role-nginx-
Install Nginx on the web node and balance requests to the application nodes in a round-robin fashion

## Running Ansible against new instances

Used nginx playbook from  https://github.com/geerlingguy/ansible-role-nginx 

# Note: Niginx was installed on both web and app instances but configured to perform different tasks  as required for this task. 

# Nginx :
	- set variables { ansible/roles/nginx/defaults/main.yml}
		upstreams_servers:
		   - { server: ec2-52-51-6-126.eu-west-1.compute.amazonaws.com}    #  aws app server instance  FQDN  set manually  
		   - { server: ec2-52-50-17-184.eu-west-1.compute.amazonaws.com}
    
       - aws instance host names must contain WEB for webserver and APP for app  servers 
	  /ansible/roles/nginx/tasks/vhost.yml  apply diffrent vhost files per-server functionality base on the hostname having web or app 


# Test Result 
  	[root@web01 conf.d]# curl localhost
	i there, I'm served from application node hostname  app01 but on a diffrent instance IP "10.0.5.74" !
	[root@web01 conf.d]# curl localhost
	i there, I'm served from application node hostname  app01 but on a diffrent instance IP "10.0.4.241" !

I relaiased that my app instance has the same hostnames. you can tell the difference via the IP address. issues with my teraform templating. 

