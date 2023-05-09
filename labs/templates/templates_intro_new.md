## Lab Title: Using Templates to Create Configuration Files

### Lab Objective:
In this lab, you will learn how to use Ansible's template module to create configuration files based on a template file and variables. You will create a template file and use it to generate a configuration file on a Windows host.
Sure thing! Here's a lab guide on how to create an Ansible template and playbook to configure a Windows IIS web.config file:

## Prerequisites

Before you begin, you'll need:

- A Windows Server 2022 workstation with Git, Visual Studio Code, and PuTTY preinstalled.
- A GitHub account.
- Basic knowledge of Git and GitHub.
- Basic knowledge of IIS and web.config files.
- A basic understanding of Ansible.

## Step 1: Clone the repository

If you have not already done so, you need to clone the ansible-working repository to your Windows Server 2022 workstation. Follow these steps:

1. Open Git Bash or your preferred terminal application.
2. Navigate to the directory where you want to store your repository.
3. Run the following command to clone the repository:

```
git clone https://github.com/your-username/ansible-working.git
```

Note: Replace "your-username" with your GitHub username.

## Step 2: Create the Ansible playbook

Now it's time to create the Ansible playbook that will use the template to configure the web.config file. Follow these steps:

1. In Visual Studio Code.
2. Click the "Explorer" icon on the left sidebar.
5. Right-click on the root folder of your `ansible-working repo and choose "New File".
6. Name the file `configure.yml`.
7. Copy and paste the following code into `configure.yml`:

```
- name: Configure web.config for SQL connection string
  hosts: all
  vars:
    ip_address: 10.0.0.1
    database_name: mydatabase
    db_username: sqluser
    db_password: Pa$$w0rd
  tasks:
    - name: Create web.config file
      template:
        src: templates/web.config.j2
        dest: c:/inetpub/wwwroot/web.config
```

This playbook will use the `template` module to generate the web.config file from a Jinja2 template.

## Step 3: Create the Ansible template

Next, you need to create the Jinja2 template that will be used to generate the web.config file. Follow these steps:

1. In Visual Studio Code, 
2. In Explorer pane right-click on the `ansible-working` folder
3. Select `New Folder`
4. Enter `templates` as the folder name.
5. Right click on the `templates` folder
6. Choose "New File".
7. Name the file `web.config.j2`.
8. Copy and paste the following code into `web.config.j2`:

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <appSettings>
    <add key="sqlConnectionString" value="Server={{ ip_address }};Database={{ database_name }};User ID={{ db_username }};Password={{ db_password }};"/>
  </appSettings>
</configuration>
```

This template includes a configuration option to update the database connection string including:

- Server ip address
- Database name
- Database user name
- Database password

## Step 4: Run the playbook

Now that you've created the playbook and template, it's time to run the playbook to configure the web.config file. Follow these steps:

1. Open a PuTTY session and connect to your Ansible control host.
2. Navigate to the directory where you cloned your repository in Step 2.
3. Run the following command to pull the latest changes from the GitHub repository:

```
git pull
```

4. Run the following command to run the playbook:

```
ansible-playbook configure.yml
```

This command will execute the `configure.yml` playbook, which will generate the `web.config` file using the `web.config.j2` template and place it in the `C:\inetpub\wwwroot` directory on all hosts in the `all` group.

## Conclusion

In this lab, you learned how to create an Ansible playbook and template to configure a Windows IIS web.config file. You created a GitHub repository to store your playbook and template, used Visual Studio Code to edit your files, and used PuTTY to pull your changes to your Ansible control host and run the playbook. By following these steps, you can easily automate the configuration of your web.config file across multiple hosts, saving you time and effort.
