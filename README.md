    
<h2>learn-ansible</h2>
<br/>
<b>YAML</b> 
   <ul> <li> it is easier to read and write </li></ul>
<b>YAML Basics</b>
   <p> 
        <ul> 
            <li> --- shows the begining of YAML anything above that line shout not be parsed as YAML </li>
            <li> every item in the list is a list of key/value pairs, commonly known as hash or a dictionary </li>
            <li>we should learn how to write list and dictionaries </li>
            <li>need to be careful about the white space. it matters!!! </li>
        <ul>
    </p>
<p> <b> example 1 </b> </p>

<div>
    <pre>
        --- 
        # list of car manufacturers --> this is a comment starts with "#" 
        cars
          - Maruthi
          - Honda
          - Audi
    </pre>
</div>
<b>example 2 </b>
<div>
    <pre>
        ---
        # type of car model produced by each manufacturers 
        cars
          - Marthi
            Model: Ciaz
            colour: red
            price: 10L
            engine: hybrid
    </pre>
</div
<div>
    <h2> Install Ansibe in Centos 7 </h2>
    <pre>
        yum install -y epel-release
        yum install -y ansible
    </pre>
    <h2> Check the version of the Ansible </h2>
    <pre>
        ansible --version
    </pre>
    <h2> Create and add host key to enable password less login</h2>
    <pre>
        ssh-keygen -t rsa -b 4096
        ssh-copy-id root@192.168.100.160 # replace the ip with your own ip
    </pre>
    <h2> Configure the host file in /etc/ansible/hosts </h2>
    <pre>
        [webservers] # webserver group 
        webserver1 ansible_ssh_host=192.168.100.160
        webserver2 ansible_ssh_host=192.168.100.161
        webserver3.example.com 
        192.168.100.162        
        #create your ungrouped hosts like this
        ftpserver1.example.com
        192.168.100.163
    </pre>
    <h2> Check the connectivity with the hosts </h2>
    <pre>
        # it will ping all the nodes
        # Note it is not the network ping
            # -m module name
        ansible -m ping all 
        # ping a single node
        ansible -m ping webserver1
    </pre>
    <pre>
        # output of single node ping
        webserver1 | SUCCESS => {
            "changed": false, 
            "ping": "pong"
        }
    </pre> 
    <h2> List all the modules </h2>
    <pre>
        ansible-doc -l # list all the available modules in the system
        ansible-doc -l | grep copy # search a particular module
        ansible-doc copy # provide the complete sysntax and examples
    </pre>       
</div>
<div>
    <h2>Gathering Facts</h2>         
    <pre>
        ansible webserver1 -m setup
        # extract the facts form webserver1
    </pre>
</div>
<div>
    <p><b>Simple playbook to install apache webserver</b></p>
    <a href="apache.yml">First apache playbook</a><hr>
    <b> Check the syntax of the playbook before playing</b>
    <pre>
        ansible-playbook --syntax-check /etc/ansible/playbooks/apache.yml         
    </pre>
    <b> Run a playbook</b>
    <pre>
        ansible-playbook apache.yml
    </pre>
    <p>Note: Sometimes above palybook will not install apache if there is a libselinux-python package dependency if you have a minimal installation of Centos7</p>
    <p><b>Simple playbook to install apache webserver by checking the dependency</b></p>
    <a href="apache1.yml">First apache playbook with dependency checking</a>
</div>

