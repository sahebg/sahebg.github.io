---
layout: post
title: "How to Change Service Fabric replicator log size and drive"
modified:   2017-11-17
categories: [ComputerSceince]
tags: [Azure, Service Fabric, Local Cluster, Replicator Log, Windows]
sitemap:
    priority: 0.7
    changefreq: 'monthly'
    lastmod: 2017-11-17T11:49:30-05:00
image:
    feature: /Azure/servicefabric.JPG
---
Installing Service Fabric SDK and creating a local cluster takes huge space. The replicator log itself allocates 8GB of disk space.
Here is a solution to change the Replicator Log size and even change the Drive of Local Cluster, so that you never needs to worry about space at any 
latter point of time.


- Go to path where Azure SDK/ Service Fabric Manager is installed. Usually @ C:\Program Files\Microsoft SDKs\Service Fabric

![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric1.JPG)
- Then go inside ClusterSetup/NonSecure/OneNode or FiveNode based on for which you like to change the configuration. In case
you have Secure setup then you need to go inside ClusterSetup/Secure. By default its created in NonSecure.
- Inside that folder you will see a file named ClusterManifestTemplate.json. This is the file which generates the ClusterManifest.xml during Cluster creation.
- Before making any changes into the file, for safer side please make a copy of the original. Now do the changes as mentioned below :
    - To change only the size of Replicator log : add a subsection for KtlLogger in fabricsettings section
    
      {
		"name": "KtlLogger",
		"parameters": [
		  {
          "name": "SharedLogSizeInMB",
          "value": "1024"
		  }
        ]
	  },
	  
	Note that minimum value is : 1024. You can make it 1024 or its integer multiples. 
	This should look like this after change. Make sure Curly braces and Commas are correctly closed.
	
   	 ![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric2.JPG)
    
    - To change the drive itself for Local Cluster : edit the Setup subsection in fabricsettings section.Replace %systemdrive% 	    to the drive where you want to keep your Cluster. Mine looks like this: 
    
        "name": "Setup",
        "parameters": [
          {
            "name": "FabricDataRoot",
            "value": "F:\\SfDevCluster\\Data"
          },
          {
            "name": "FabricLogRoot",
            "value": "F:\\SfDevCluster\\Log"
          }
        ]
	
        ![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric3.JPG)

#### You can even do both the changes, as I have done. This should look like this after the change.
![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric4.JPG) 

- Now we need to re-create the cluster. To do that Right Click on the Servcie Fabric Cluster Manager -> Remove Local Cluster. It will take some time. Get a coffee or something !

![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric5.JPG) 

- When its removed you will see an option for  Servcie Fabric Cluster Manager -> Setup Local Cluster -> 1 Node  or 5 Node as per your requirement.
In case you want 5 Node Cluster then you must also change FiveNode ClusterManifestTemplate.json file as well, as mentioned in ealier setup.
![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric6.JPG)

Thats it ! Now you should the required changes and no more problem about C Drive getting full by replicatorsharedlog file.
Next time whenever you build an Application into Service Fabric you will see Replicator log generated but of size you have mentioned.
![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric7.JPG)

Also, you can always verify wheather your template changes has reflected or not in the ClusterManifest.xml file, which is located in side SfDevCluster/Data folder.
![_config.yml]({{ site.baseurl }}/images/Azure/servicefabric8.JPG)

Hope this helps. Please comment below in case of any problem found during running the code or any other doubts.
