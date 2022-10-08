pipeline {

    agent any

    stages {
        stage("environment preparation"){
            steps {
                sh "pwd"
                sh "ls"
                sh "echo ${USER}"
                sh "df -h"
                sh "curl ifconfig.co"
                sh "echo testing"
            }
        }

        stage("connect to deploy server"){

            environment { 
                SSH_CRED = credentials('deploy-test-pem')
                REM_USER = "{USER}"
            }

            steps {
                //=============== THIRD APPROACH
                script {
                    sh """
                    #!/bin/bash
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@ec2-52-25-213-88.us-west-2.compute.amazonaws.com << EOF
                    curl ifconfig.co/ip
                    df -h
                    # Update system repos
                    echo -e "\n Updating package repositories.."
                    sudo apt update -y

                    # Install Apache
                    echo -e "\n Installing Apache.."
                    sudo apt-get install apache2 -y 

                    # UFW firewall
                    echo -e "\n add the HTTP and HTTPS services to the UFW firewall.."
                    sudo ufw allow "Apache Full" 

                    # Install PHP
                    echo -e "\n installing PHP.."
                    sudo apt install php libapache2-mod-php php-mysql -y 

                    # Check PHP installation
                    echo -e "\n checking that PHP installation was successful.."
                    php -v
                    
                    # Create directory for new domain
                    echo -e "\n creating directory for new domain.."
                    sudo mkdir /var/www/example.com
                    
                    # assign onwernship
                    echo -e "\n creating directory for new domain.."
                    sudo chown -R $USER:$USER /var/www/example.com
                    
                    # Create a configuration file for apache
                    echo -e "\n creating configuration file for apache to use.."
                    sudo touch /etc/apache2/sites-available/example.conf
                    sudo chown -R $USER:$USER /etc/apache2/sites-available/example.com.conf
                    
                    # Configure conf file
                    echo -e "\n Configuring conf file.."
                    sudo touch /etc/apache2/sites-available/example.com.conf
                    sudo chown -R $USER:$USER /etc/apache2/sites-available/example.com.conf
                    echo "<VirtualHost *:80>
                    ServerName example.com
                    ServerAlias www.example.com
                    ServerAdmin webmaster@localhost
                    DocumentRoot /var/www/example.com
                    ErrorLog ${APACHE_LOG_DIR}/error.log
                    CustomLog ${APACHE_LOG_DIR}/access.log combined
                    </VirtualHost>" > /etc/apache2/sites-available/example.com.conf
                    
                    
                    # Enable configuration file
                    echo -e "\n enabling configuration file.."
                    sudo a2ensite example.com
                    sudo a2dissite 000-default
                    sudo apache2ctl configtest
                    sudo systemctl reload apache2
                    
                    
                    # create root index file
                    echo -e "\n creating root index file.."
                    touch /var/www/example.com/index.html
                    touch nano /var/www/example.com/about.php
                    
                    #add the contents to the files created
                    echo -e "\n creating html index file.."
                    echo "<html>
                    <head>
                    <title>example.com</title>
                    </head>
                    <body>
                    <h1>Hello World!</h1>
                    <p>This is the landing page of <strong>example.com</strong>.</p>
                    </body>
                    </html>" > /var/www/example.com/index.html
                    
                    #add the contents to the files created
                    echo -e "\n LAMP Script installed successfully.."
                    exit
                    << EOF
                    """
                }

                // ============== SECOND APPROACH
                
                // script {
                //     def remote = [
                //         name: 'ubuntu', 
                //         host: 'ec2-35-92-93-35.us-west-2.compute.amazonaws.com', 
                //         user: 'ubuntu', 
                //         identityFile: "$SSH_CRED", 
                //         identity: "$SSH_CRED", 
                //         password: "$SSH_CRED", 
                //         allowAnyHosts: true,
                //         knownHosts: SSH_CRED
                //     ]
                    
                //     sshCommand remote: remote, command: "df -h"
                //     sshCommand remote: remote, command: "curl ifconfig.co"
                // }

                // ===========FIRST APPROACH 
                // sh "pwd"
                // sh 'echo "SSH private key is located at $SSH_CRED"'
                
                // // sh "ssh -i $SSH_CRED -tt -o StrictHostKeyChecking=no ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com"
                // sh 'ssh -i $SSH_CRED -t ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com $remoteCommands'
                
            }
        }
    }
}