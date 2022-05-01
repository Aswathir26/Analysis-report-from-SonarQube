# Analysis-report-from-SonarQube

 # Analysis report from SonarQube Deployed in AKS

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
    
Step 3: Do SAST with a project repo by following the steps given in sinarqube 



**Step 2: Get analysis report of SonarQube Output**

Step 1: Download and install CNES Report plugin jar file

- Click here to download jar file for plugin:

https://github.com/cnescatlab/sonar-cnes-report/releases/download/4.0.0/sonar-cnes-report-4.0.0.jar

ref:https://github.com/cnescatlab/sonar-cnes-report/releases


Step 2: copy jar file to sonarqube plugin directory from local system:

kubectl cp < jar name > < pod name >:< path of plugin directory >

      $ kubectl cp sonar-cnes-report-4.0.0.jar sonarqube-7cb949bc84-8ztw2:/opt/bitnami/sonarqube/extensions/plugins/
  
Step 3: Restart sonarqube

Step 4: get the help about cnesreport:

java -jar < jar name > -h

     $ java -jar sonar-cnes-report-4.0.0.jar -h
  
Step 5: export sonarqube output:

    
java -jar sonar-cnes-report-4.0.0.jar -p < projectkey > -t < token >

      $ java -jar sonar-cnes-report-4.0.0.jar -p TE-DevOps_javunit -t 005ac6a16120ff82e05c779888d3848dbb497e70
  
  Give ls command to view the reports 
  
Step 6: Copy report to local system:

kubectl cp < pod name >:< path of file >/< file > < file >
    
    $ kubectl cp sonarqube-7cb949bc84-8ztw2:/opt/bitnami/sonarqube/extensions/plugins/2022-04-28-java-maven-junit-helloworld-analysis-report.docx report1.docx



Step 7: Convert exported report to PDF file 
