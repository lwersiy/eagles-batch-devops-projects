The following are instructions for installing Apache Maven and Java 8 on an Amazon EC2 instance. These are required for the Amazon Neptune Signature Version 4 authentication samples.

## Steps To Install Apache Maven and Java 8 on your EC2 instance

1. Connect to your Amazon EC2 instance with an SSH client.

2. Install Apache Maven on your EC2 instance. First, enter the following to add a repository with a Maven package.

    ``sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo``

- Enter the following to set the version number for the packages.

    `sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo`
- Then you can use yum to install Maven.

    `sudo yum install -y apache-maven`
3. The Gremlin libraries require Java 8. Enter the following to install Java 8 on your EC2 instance.

    `sudo yum install java-1.8.0-devel`
4. Enter the following to set Java 8 as the default runtime on your EC2 instance.

    `sudo /usr/sbin/alternatives --config java`
- When prompted, enter the number for Java 8.

5. Enter the following to set Java 8 as the default compiler on your EC2 instance.

    `sudo /usr/sbin/alternatives --config javac`
- When prompted, enter the number for Java 8.

6. Verify your maven version
    `mvn -v`

### Project Preparation
7. Create the `.m2` directory in the home directory of your current user
    `mkdir ~/.m2`

8. Create the Settings file inside of the `~/.m2` directory
    `cd ~/.m2/`
    `mv demo/settings.xml ~/.m2/`

9. Install git
   'sudo yum install git -y'

10. clone git repository to remote repository
    'git clone https://github.com/lwersiy/eagles-batch-devops-projects.git'
    
12. List all git branches and checkout to the maven-nexus branch that contains our settings.xml and pom.xml files
    'git branch -a'
    'git checkout maven-nexus
    
14. Install tree in order to have a clear view of our directories and files
    'sudo yum install tree -y'

15. Chenge directory into the JavaWebApp and run the maven lifecycle commands depending on your use case
    'mvn validate'
    'mvn compile'
    'mvn test'
    'mvn package'
    'mvn verify'
    'mvn install

16. Launch and configure the maven nexus handshake before deploying, by following the steps below
- Sign in and change password to nexus server
- go to github and navigate into the settings.xml and pom.xml files located in the maven-nexus branch.
- update the ip address or the DNS host name. 
- the lines to update are the nexus-snapshot and the nexus-release-repo
- do thesame in the pom.xml file
- Commit these changes in the github and perform a git pull in you clone repository to see the updated changes.

15. move the updated settings.xml file to the ~/.m2 folder
    'mv settings.xml ~/.m2'

16. run mvn deploy to complete the maven lifecycle
    'mvn deploy'
