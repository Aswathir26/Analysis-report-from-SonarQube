# Do SAST and download Analysis report from SonarQube through pipeline


**SAST**

Static application security testing (SAST), or static analysis, is a testing methodology that analyzes source code to find security vulnerabilities that make your organization’s applications susceptible to attack. SAST scans an application before the code is compiled.
 
**CNES Report Plugin**

By using CNES Report plugin we can export code analysis from a SonarQube server as a docx, xlsx, csv, markdown, and text files. This plugin is used in Sonarqube version 8.9.X LTS.

     $ git clone https://github.com/Aswathir26/Analysis-report-from-SonarQube.git


**Step 1: Deploy Sonarqube and Do SAST on a project**

Step 1: Create namespace

    $ kubectl create namespace sonarqube
    
Step 2: Deploy Sonarqube

    $ helm repo add bitnami https://charts.bitnami.com/bitnami
    $ helm install -f values.yaml sonarqube bitnami/sonarqube -n sonarqube
    
Step 3: Do SAST with a project repo by following the steps given in sonarqube 

Note : Use pipeline.yml (upto line number 36)



**Step 2: Install plugin**

USE SONARQUBE MARKETPLACE TO INSTALL CNES REPORT PLUGIN 

OR

Step 1: Download and install CNES Report plugin jar file

- Click here to download jar file for plugin:

https://github.com/cnescatlab/sonar-cnes-report/releases/download/4.1.1/sonar-cnes-report-4.1.1.jar

ref:https://github.com/cnescatlab/sonar-cnes-report/releases


Step 2: copy jar file to sonarqube plugin directory from local system:

kubectl cp < jar name > < pod name >:< path of plugin directory >

      $ kubectl cp sonar-cnes-report-4.1.1.jar sonarqube-7cb949bc84-8ztw2:/opt/bitnami/sonarqube/extensions/plugins/
      
note : Restart sonarqube


**Step 3: Download sonarqube analysis report and save it to pipeline artifact**

Run the full pipeline

then check pipeline artifact we can see reports there

download and Convert report to PDF file 
