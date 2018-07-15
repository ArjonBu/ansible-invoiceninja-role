InvoiceNinja is an open source billing platform used mostly by freelancers and small businesses. I am a big supporter of open source software and that’s the reason I have written this role.

InvoiceNinja requires PHP, MySQL/MatiaDB and a webserver. Installing the software manually is easy.

1. Download the zip file from https://download.invoiceninja.com
2. Upload the code to your server
3. Setup the database
4. Configure the web server
5. Configure the application for your usecase

To update the app you just need to copy over the latest code. The app tracks the current version in a file called version.txt, if it notices a change it loads /update to run the database migrations.

But who has time to manually install and update a software nowadays?! We can always use an automation tool like Ansible to do the job for us.

My role does the following steps:

1. Copies the Nginx virtual host template filled with your configurations.
2. Downloads the latest zip file from https://download.invoiceninja.com and unzips it to the domain root directory.
3. Copies the .env template file with all our configurations.
4. Creates the MariaDB database and user.
5. Fixes the permissions for the software files.
6. Restarts Nginx to reload the configuration.

Note: The role copies the Nginx config files to /etc/nginx/vhosts so you need to add 'include /etc/nginx/vhosts/*.conf;' to your nginx.conf file. 
 
My role does not:

- Install Nginx
- Install MariaDB

They will be added as separate roles in the future.

> playbook.yml:
~~~~
---
- name: Install InvoiceNinja
  hosts: all
  become: true
  roles: 
    - ansible-invoicecinja-role
~~~~

[Arjon Bujupi](https://a.bujupi.me)

PS: If you are looking for a freelancer to manage InvoiceNinja for your business, there is a contact section on my homepage https://a.bujupi.me 😉