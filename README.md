
# *(POC) SLES Image build using packer (vsphere-ISO - Alternate for VirtualBox build)*

## _Prerequisite:_

* **Packer version (currently working)** : 1.6.0 

* **Working DHCP server on the subnet  :** need a MAC address hardcoded*  
	*Note: In our current environement **__restricting DHCP offer to only above MAC__**


* **Files required :**  
├── autoinst.xml		      : Passed as a boot option for automated install (AutoYast)  
└── vsphere-sles12sp3.json	: Required for packer build (Builder, provisioner, ...)  

* **ISO :** Make sure the operating system ISO is availabe on the Vcenter you want to build, (path is required for the Json file)  

* **VMware details requied for Json:**  
  * vcenter_server: "vCenterName"  
  * cluster: "ClusterName"  
  * datastore: "DataStoreName"  
  * host: "EsxHostname"  
  * username: "UserWithCredentialsToCreateVM" with ROLE "Inject USB HID scan codes"  


### How to build ?  
  * From the linux system where packer is available run : packer build vsphere-sles12sp3.json    

### *Tips :*  
  * Validate the Json before starting build		: packer validate vsphere-sles12sp3.json  
  * Detailed build log                     		: PACKER_LOG=1 packer build vsphere-sles12sp3.json  
  * Debug mode build (Interactive)			: packer build -debug vsphere-sles12sp3.json  


### Error observed due to insufficeint ROLE in VMware :  
  * Build 'vsphere-iso' errored: error typing a boot command: ServerFaultCode: Permission to perform this operation was denied.    
  * _(**Solution :** Make sure username used in Json has the ROLE [Inject USB HID scan codes])_    
  

### Successfull (VMDK image) Build tested in below environement :  
  - [x] VMware   
  - [x] CCloud   
  - [x] Azure  
  - [x] Google (GCP) - Tested on 14th Dec,2020  


### ~~~Pending environement to test:~~~  
  - [ ] ~~~Google (GCP)  - Initial test failed, driver issue~~~  


### Further images to build and test upon successfull testing in above environements:
  - [x] sles12sp3
  - [ ] sles12sp5
  - [ ] sles15  
  
