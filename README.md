APAC Destinasia Travel Rules Demo
=================================
Step 1: AppDev on Cloud Suite
-----------------------------
This demo is to install JBoss BRMS with Destinasia Travel discount rules in the Cloud based on leveraging any Red Hat OpenShift container based platform, such as:

 - [Red Hat Container Platform (OCP)](https://github.com/redhatdemocentral/ocp-install-demo)
  
It delivers a fully functioning containerized JBoss BRMS installation.


Step 2: Install JBoss BRMS on OpenShift
---------------------------------------
1. First ensure you have an OpenShift container based installation, such as one of the following installed first:

  - [OCP Install Demo](https://github.com/redhatdemocentral/ocp-install-demo)

  - or your own OpenShift installation.

2. [Download and unzip this demo.](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/archive/master.zip)

3. Download JBoss EAP & JBoss BRMS, add to installs directory (see installs/README).

4. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges:
```
   # The installation needs to be pointed to a running version
   # of OpenShift, so pass an IP address such as:
   #
   $ ./init.sh 192.168.99.100  # example for OCP.
```

Now log in to JBoss BRMS and start developing containerized rules projects (the address will be generated by the init script):

  - [http://apac-destinasia-rules-demo.192.168.99.100.xip.io/business-central](http://apac-destinasia-rules-demo.10.1.2.2.xip.io/business-central) ( u:erics / p:jbossbrms1! )


Step 3: Ansible Playbooks for Automated Service Deployment on OpenShift
-----------------------------------------------------------------------
See instructions for [Ansible Playbooks Service Deployment](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/support/playbooks/deploy-ocp-services/README.md) to deploy:

1. Rules from container JBoss BRMS to xPaaS Decision Server

2. .Net service to container

3. Java service to xPaaS EAP Server

4. PHP service to container

5. Fuse service to xPaaS Integration Server


Notes
-----
This project can be installed on any OpenShift platform, such as the OpenShift Container Platform. It's possible to install it on any available installation by pointing this installer to an OpenShift IP address:
```
  $ ./init.sh IP
```

If for any reason the installation breaks or you want a new JBoss BRMS installation, just remove the project apac-destinasia-rules-demo entry in the OpenShift console and re-run the installation.

Should your local network DNS not handle the resolution of the above address, giving you page not found errors, you can apply the following to your local hosts file:

```
$ sudo vi /etc/hosts

# add host for OCP demo resulution
192.168.99.100   apac-destinasia-rules-demo.192.168.99.100.xip.io 
```

The rule test you find in the project is BROKEN... guess what, you need to fix that! Hint for the fix is that the flights are all
APAC destinations, but the test uses an unknown destination for the rules. Can you fix it?

To clone a repository in the running container, the following actions would need to occur from a developer's machine.

1. Execute port forwarding through the OpenShift CLI. This will open a tunnel between the developer's machine and the pod through the OpenShift API pod proxy. The command window will block while the session is open:

   ```
   # Read-write access to repo on port 8001.
   #
   $ oc port-forward $(oc get pod -l=deploymentconfig=destinasia-rules-demo --template='{{ range .items }} {{ .metadata.name }} {{ end }}') 9418:9418
   ```

2. Clone the repository. In another window, clone the remote repository:

   ```
   # Read access to repo on port 9418.
   #
   $ git clone git://localhost:9418/destinasia 
   ```


Supporting Articles
-------------------
- [App Dev in the Cloud: How To Run JBoss BRMS in a Container](http://www.schabell.org/2016/12/appdev-cloud-howto-run-jboss-brms-in-container.html)

- [Real App Dev in the Cloud with JBoss BRMS Install Demo](http://www.schabell.org/2016/03/real-appdev-in-cloud-jboss-brms-install-demo.html)


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.1 - JBoss BRMS 6.4.0, JBoss EAP 7.0.0 with Destinasia Travel discount rules running on any given OpenShift installation and port forwarding for git repo access configured.

- v1.0 - JBoss BRMS 6.4.0, JBoss EAP 7.0.0 with Destinasia Travel discount rules running on any given OpenShift installation.

![Logo](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/docs/demo-images/destinasia-logo.png)

![Pods](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/docs/demo-images/destinasia-brms-pods.png)

![Rules](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/docs/demo-images/destinasia-travel-discount-rules.png)

![Deployments](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/docs/demo-images/destinasia-services-builds.png)

![Builds](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/docs/demo-images/destinasia-services-builds.png)

![Cloud Suite](https://github.com/redhatdemocentral/apac-destinasia-rules-demo/blob/master/docs/demo-images/rhcs-arch.png)
