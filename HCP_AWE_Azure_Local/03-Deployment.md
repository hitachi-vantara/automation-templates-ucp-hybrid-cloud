## Content Table

-   [01-Introduction](.\01-Introduction.md)
-   [02-Technical_Deep_Dive](.\02-Technical_Deep_Dive.md)
-   [03-Deployment](.\03-Deployment.md)   <----This doc
-   [04-Conclusion](.\04-Conclusion.md)
-   [05-All_in_One](.\05-All_in_One.md)


## Deployment of HCP Anywhere Enterprise with HCP for Cloud Scale

This section provides concise guides on deploying HCP Anywhere
Enterprise Portal and Edge Filers, along with considerations for
networking and integrating HCP for Cloud Scale. By following these
steps, you can ensure a smooth and successful installation of the HCP
Anywhere Enterprise solution.

### Prerequisites

Before beginning the deployment process, ensure that you have the
following:

1.  Access to the Azure portal and an active Azure subscription

2.  Access to an Azure Local environment (if deploying on Azure Local)

3.  Appropriate permissions to create and manage resources in your Azure
    and Azure Local environments. A few examples of resources required
    (work with the respective Azure Admins, not an exhaustive list
    below):

-   Allocate public facing IP address.

-   Key Vault Administrator role.

-   Manage network Security Groups.

1.  HCP Anywhere Enterprise Portal and Edge Filer images obtained from
    HCP Anywhere Enterprise support

### Obtaining HCP Anywhere Enterprise Images

To deploy HCP Anywhere Enterprise Portal and Edge Filers, <u>you'll need
to acquire the necessary images from HCP Anywhere Enterprise
support</u>. The specific images required depend on your deployment
target:

#### For Installing HCP AWE Portal on Azure

-   Request the following image files from **HCP Anywhere Enterprise
    support**:

    -   CentOS-HCP-AWE-Portal-Image-x-y-z-OS-disk.vhd (OS disk image)

    -   CentOS-HCP-AWE-Portal-Image-x-y-z-Data-Disk.vhd (Data disk
        image)

#### For Installing HCP AWE Portal and Edge Filer on Azure Local

-   Request the Hyper-V based \*.vhd file for the HCP Anywhere
    Enterprise Portal and Edge Filer from HCP Anywhere Enterprise
    support.

#### Storing and Uploading HCP Anywhere Enterprise Images

Once you have obtained the necessary images, follow these steps to store
and upload them:

1.  Store copies of the image files on your self-managed storage for
    backup purposes.

2.  Upload the images to the proper location based on your deployment
    target:

    -   **Azure Blob Storage**:

        -   Create a new storage account in the Azure portal (or use an
            existing one).

        -   Create a new container within the storage account.

        -   Upload the HCP Anywhere Enterprise Portal and Edge Filer
            image files to the container.

        -   Or use **AzCopy.exe** with the command AzCopy.exe cp
            "&lt;source\_uri&gt;" "&lt;destination\_uri&gt;" for all the
            VHD files.

    -   **Azure Compute Gallery (Recommended for Azure deployment)**:

        -   Create a new Compute Gallery in the Azure portal.

        -   Add
            the CentOS-HCP-AWE-Portal-Image-x-y-z-OS-disk.vhd and CentOS-HCP-AWE-Portal-Image-x-y-z-Data-Disk.vhd files
            as image definitions within the gallery.

    -   **USB Stick (Optional – for air-gapped environment)**:

        -   Copy the Hyper-V based HCP Anywhere Enterprise Portal and
            Edge Filer image files to a USB stick for manual transfer to
            your Azure Local environment in the field.

### Installing HCP Anywhere Enterprise Portal on Azure

#### Warning

-   Do not clone an existing/running HCP Anywhere Enterprise Portal as
    template for installation. Always use the provided VHD template
    file.

#### Installation Workflow

1.  **Option 1: Create a Portal Instance with VHD image in Azure Compute
    Gallery** :

    -   Follow the steps on the documentation of Azure Compute Gallery
        for creating “Specialized” VM
        (<https://learn.microsoft.com/en-us/azure/virtual-machines/vm-specialized-image-version?tabs=portal%2Ccli2%2Ccli3%2Ccli4%2Cportal5>).

2.  **Option 2: Create a Portal Instance with VHD image in Azure Blob
    Storage** :

    -   In Azure, go to the Images service and click Create.

    -   Fill in the basics: Resource group (with premium storage), Name,
        Region, OS type (Linux), VM generation (Gen 1), and Storage blob
        URI for the OS VHD file.

    -   Add the data disk VHD file as a data disk.

    -   Select Premium SSD for both disks.

    -   Review and create the image.

    -   From the Images service, select the created HCP AWE Portal image
        and click Create VM.

    -   Configure the VM settings: Resource group, Virtual machine name,
        Region, Size (based on requirements), Authentication type
        (Password), Username, and Password.

    -   Set inbound rules to include HTTPS (443).

    -   On the Disks tab, create and attach a new disk for the archive
        storage if it's a primary or replication server. Use Premium SSD
        and set Host caching to Read/write.

    -   Review and create the VM.

3.  **Configure Network Settings**:

    -   After VM deployment, note/configure the Public IP address.

    -   Add necessary inbound and outbound port rules as per HCP AWE's
        requirements.

4.  **Logging in and Configuring the Server**:

    -   SSH into the server using the root user and the initial, default
        password (ctera321), then change the password.

    -   Identify the disk for the archive pool using **fdisk -l**.

    -   Create the archive pool with **portal-storage-util.sh**
        **create\_db\_archive\_pool &lt;Device&gt;**.

    -   Start HCP AWE Portal services with **portal-manage.sh start**.

5.  **Set a Default Gateway** (if needed):

    -   Run **echo
        "GATEWAY=&lt;****default\_gateway\_ip\_address&gt;****" &gt;
        /****etc/****sysconfig/network** and restart the network service
        with **service network restart**.

### Installing HCP Anywhere Enterprise Portal on Azure Local (Hyper-V)

#### Warning

-   Do not clone an existing/running HCP Anywhere Enterprise Portal as
    template for installation. Always use the provided VHD template
    files.

#### Installation Workflow (as **Non-Arc VM**)

-   Non-Arc VMs on Azure Local are managed using **traditional
    on-premises tools** and local access controls, while Arc VMs
    leverage Azure’s management tools.

##### Create a Portal Instance in Hyper-V:

-   Open the Azure Local management interface:

    1.  Option 1: Use Windows Admin Center

    2.  Option 2: Use PowerShell

    3.  Option 3: Use Windows Admin Center on Azure portal (if your
        Azure Local cluster is registered with Azure and WAC on Azure
        enabled)  
        <img src=".\attachments\/media/image13.png"
        style="width:3in;height:2.17in"
        alt="A screenshot of a computer Description automatically generated" />

-   Specify storage locations for the VM and its data pool disk.
    (**Note**: a Portal VM requires running both the provided OS and
    Data VHD files as a set. To add additional storage aside from the
    default Data partition, check **step 2**.)

-   Finish the wizard and start the virtual machine.

##### **Configure Additional Storage** (for primary and replication servers):

-   Right-click the VM and go to Settings.

-   Add a new hard drive under the IDE Controller, selecting VHDX format
    and dynamically expanding disk type.

-   Specify the size (**minimum 200GB, recommended 2% of expected global
    file system size**).

##### Log in to the Server to Create the Archive Pool:

-   Connect to the VM (default password: ctera321) and change the
    password.

-   Identify the disk for the archive pool using **fdisk -l**.

-   Create the archive pool with **portal-storage-util.sh**
    **create\_db\_archive\_pool &lt;Device&gt;**.

-   Start HCP AWE Portal services with **portal-manage.sh start**.

##### Configure Network Settings:

-   By default, DHCP is used. For production, a static IP is
    recommended.

-   Use **nmtui** to configure network settings, including setting a
    static IP, default gateway, and DNS servers.

-   Restart the network service with **service network restart** for
    changes to take effect.

##### Configuring a Default Gateway (if needed):

-   Run **echo "GATEWAY=&lt;****default\_gateway\_ip\_address&gt;****"
    &gt; /****etc/****sysconfig/network**.

-   Restart the network service.

#### Installation Workflow (as **Arc VM** – Option 1)

-   This option (Option 1) is highly manual and **not preferred** due to
    the current Azure Portal’s support for Arc VM on Azure Local.
    However, the procedure includes valuable skills that can assist with
    the ongoing management of HCP Anywhere Enterprise on Azure Local.

-   Arc VMs on Azure Local utilize Azure’s management tools and security
    features for a unified management experience across on-premises and
    cloud environments. However, the OS partition of the Portal VM is
    immutable, and only basic Arc VM features are used, without Guest
    Management enabled.  
    <img src=".\attachments\/media/image14.png"
    style="width:4in;height:2.65641in"
    alt="A screenshot of a computer Description automatically generated" />

-   The Azure Portal UI does not support deploying Gen1 Linux VMs, which
    our images are based on. Therefore, we must partially use the ARM
    template method for deployment.

-   The procedure below will begin with copying the Portal OS and Data
    VHD files from your Azure Storage Account to your Azure Local
    cluster’s CSV (cluster shared volume), allowing you to create the
    Portal VM using these images later.

##### Load the OS and Data VHD files onto Azure Local as “VM Image”

-   **Prerequisite**:

    1.  Basic understanding of ARM (Azure Resource Manager) template
        operations.

    2.  The Portal OS and Data VHD files are already uploaded to an
        Azure Storage Account that you have access to and permission to
        share.

    3.  Understand how to generate SAS Links (example shown using
        Microsoft Azure Storage Explorer below) and save the SAS links
        of the OS and Data VHD files to a place that you can access
        later  
        <img src=".\attachments\/media/image15.png"
        style="width:4in;height:3.80043in"
        alt="A screenshot of a computer Description automatically generated" />

-   Use ARM template to deploy the “VM Images”:

    1.  Use “**Deploy a customer template**” service on Azure Portal  
        <img src=".\attachments\/media/image16.png"
        style="width:3in;height:1.33641in"
        alt="A screenshot of a computer Description automatically generated" />

    2.  Choose “**Build your own template in the editor**”

    3.  Copy the example ARM template below, paste into UI on Azure, and
        click “Save”


```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "apiVersion": {
            "type": "string"
        },
        "customLocationId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "osImageName": {
            "type": "string"
        },
        "dataImageName": {
            "type": "string"
        },
        "osType": {
            "type": "string"
        },
        "osImagePath": {
            "type": "securestring"
        },
	"dataImagePath": {
            "type": "securestring"
        },
        "hyperVGeneration": {
            "type": "string"
        }
    },
    "resources": [
        {
            "apiVersion": "[parameters('apiVersion')]",
            "extendedLocation": {
                "name": "[parameters('customLocationId')]",
                "type": "CustomLocation"
            },
            "location": "[parameters('location')]",
            "name": "[parameters('osImageName')]",
            "properties": {
                "osType": "[parameters('osType')]",
                "hyperVGeneration": "[parameters('hyperVGeneration')]",
                "imagePath": "[parameters('OSImagePath')]"
            },
            "tags": {},
            "type": "microsoft.azurestackhci/galleryimages"
        },
		        {
            "apiVersion": "[parameters('apiVersion')]",
            "extendedLocation": {
                "name": "[parameters('customLocationId')]",
                "type": "CustomLocation"
            },
            "location": "[parameters('location')]",
            "name": "[parameters('dataImageName')]",
            "properties": {
                "osType": "[parameters('osType')]",
                "hyperVGeneration": "[parameters('hyperVGeneration')]",
                "imagePath": "[parameters('dataImagePath')]"
            },
            "tags": {},
            "type": "microsoft.azurestackhci/galleryimages"
        }
    ]
}

```


<img src=".\attachments\/media/image17.png"
style="width:6.3in;height:6.13644in"
alt="A screenshot of a computer program Description automatically generated" />  
Figure – Save the template after you have pasted the content

1.  Fill in the parameters:  
    <img src=".\attachments\/media/image18.png"
    style="width:3in;height:4.20389in" />

    1.  **Resource Group**: New or Existing group

    2.  **Region**: The region where your Azure Local cluster and the
        **Custom Location** (see below) are located.

    3.  **API Version**: Use “2023-09-01-preview”

    4.  **Custom Location ID**: Each Azure Local Cluster comes with a
        Custom Location ID, which you can find it by hunting down to the
        resource and click into the JSON View like this  
        <img src=".\attachments\/media/image19.png"
        style="width:4in;height:1.55632in" />  
        Where you can also find the “**location**” parameter

    5.  **Location**: The same as “Region” but needs to be entered again
        using the corresponding code found in the **Custom Location**
        JSON View.

    6.  **OS Image Name**: A name you will recognize for the OS VHD

    7.  **Data Image Name**: A name you will recognize for the Data VHD

    8.  **OS Type**: Enter “Linux”

    9.  **OS Image Path**: Paste the SAS Link of the OS VHD image you
        generated previously

    10. **Data Image Path**: Paste the SAS Link of the Data VHD image
        you generated previously

    11. **Hyper V Generation**: Enter “**V1**” (must be “**V1**” for Gen
        1 image).

    12. **Note 1** – This template is a working example. Experienced ARM
        users can easily customize as they see fit.

    13. **Note 2** – ARM templates can be created to deploy all the
        resources needed for the Portal VM on your Azure Local cluster;
        this advanced topic will be covered in a later section of this
        document.

2.  Click “**Review + Create**” after filling in the parameters

3.  If no error alerts showing up, click “**Create**” and wait the
    process to finish

4.  The copying time depends on the internet speed at the location of
    the Azure Local

5.  After the successful ARM deployment, you can find the images in “VM
    images” section of your Azure Local cluster  
    <img src=".\attachments\/media/image20.png"
    style="width:3in;height:2.09103in"
    alt="A screenshot of a computer Description automatically generated" />

##### Create a Portal VM Instance from Azure Portal:

-   **Note**: Advanced users can use PowerShell / Az CLI / ARM templates
    to create the Portal VM instance. Below only shows deployment using
    Azure Portal

-   **Prerequisite**:

    1.  Ensure the VM images are uploaded to the cluster and accessible

    2.  Ensure there are “Logical networks” created and configured on
        the cluster for the VM usage

-   “**Create VM**” in the Azure Local UI on Azure  
    <img src=".\attachments\/media/image21.png"
    style="width:3in;height:2.84171in"
    alt="A screenshot of a computer Description automatically generated" />

-   Fill in the parameters for the VM:

    1.  Choose the Subscription and Resource Group where your VM will be

    2.  Enter unique “**Virtual machine name**”

    3.  Skip “**Custom location**” and “**Virtual machine kind**” as
        they are assigned automatically when you create the Arc VM from
        the UI

    4.  Choose “Standard” for “**Security type**”

    5.  For “**Storage path**”, you can select either option based your
        preference

    6.  For “**Image**”, choose the OS image you uploaded previously

    7.  Enter the desired capacities for “**Virtual processor count**”
        and “**Memory (MB)**”

    8.  Use “Static” for “**Memory type**”

    9.  Uncheck “**Enable guest management**” since the OS partition is
        immutable  
        <img src=".\attachments\/media/image22.png"
        style="width:3in;height:0.71827in"
        alt="A screenshot of a computer Description automatically generated" />

    10. (Optional) Fill in “**VM proxy configuration**” if you want to
        use a proxy. Details are not covered here

    11. For “**Root user**” section, enter dummy values since the OS
        partition is immutable

-   For “**Add new disk to Arc VM**” -- The Data disk uploaded
    previously **cannot** attach to the Arc VM directly. We should skip
    this step.

-   Add network interface  
    <img src=".\attachments\/media/image23.png"
    style="width:3in;height:1.44663in" />

-   (Optional) Add Tags

-   Finally, create the Arc VM. This step will generate a Private key
    PEM file. **You don’t have to keep it since the OS partition is
    immutable**. This step will take about **20** minutes to complete VM
    creation and Azure Arc registration.

-   Finish the wizard and start the virtual machine.

-   At this point, there is no Data Disk attached to the Arc VM yet.

-   Finally, stop the Portal VM.

##### Create the Data Disk and Attach to the Arc VM

-   The steps in this section are the most complex and require careful
    attention. This complexity arises from the current limitations of
    the Azure Portal and Azure REST API in supporting Arc VM disks.

-   Therefore, in this section, we will first create a Dummy Data Disk,
    replace the Dummy Data Disk with a copy of the Data VHD, attach it
    to the Arc VM, and finally test if the Arc VM is functioning
    properly.

-   Create a Dummy Data Disk via ARM template

    1.  Due to Azure Portal only supporting creating a Data Disk in VHDX
        format, we use ARM template to create a Dummy Data Disk in VHD
        format.

    2.  Use “**Deploy a customer template**” service on Azure Portal and
        “**Build your own template in the editor**”

    3.  Use a template like below or customize it based your needs:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "customLocationId": {
      "type": "string"
    },
    "location": {
      "type": "string"
    },
    "vmName": {
      "type": "string"
    }
  },
  "resources": [
	{
      "type": "Microsoft.AzureStackHCI/virtualHardDisks",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('vmName'), '-data')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "diskFileFormat": "vhd",
        "diskSizeGB": 60,
        "dynamic": false,
        "hyperVGeneration": "V1"
      }
    }
  ]
}
```


1.  Fill in the parameters (details not provided) then Deploy:  
    <img src=".\attachments\/media/image24.png"
    style="width:3in;height:2.76378in" />

2.  Verify Deployment by checking “Disks” resources:  
    <img src=".\attachments\/media/image25.png"
    style="width:3in;height:3.31929in"
    alt="A screenshot of a computer Description automatically generated" />

-   Replace the Dummy Data Disk with a copy of the Data VHD. The steps
    are

    1.  Copy the ACL information from the Dummy Data Disk.

    2.  Remove the Dummy Data Disk.

    3.  Copy the Portal Data VHD to the location of the deleted Dummy
        Data Disk, ensuring it has the same name.

    4.  Apply the previously copied ACL information to the Portal Data
        Disk

```powershell
\# Step 0: Find the path to the Dummy Data Disk VHD file. It resides in
Cluster Storage. Example:
C:\ClusterStorage\UserStorage\_2\e254bb98922eeec\PortalDemo2-data-&lt;subscription\_id&gt;-&lt;resource
group\_name&gt;.vhd

\# Step 1: Copy the ACL information from the Dummy Data Disk

$acl = Get-Acl -Path "C:\Path\To\DummyDataDisk.vhd"

\# Step 2: Remove the Dummy Data Disk

Remove-Item -Path "C:\Path\To\DummyDataDisk.vhd" -Force

\# Step 3: Copy the Portal Data VHD to the location of the deleted Dummy
Data Disk, ensuring it has the same name

Copy-Item -Path "C:\Path\To\PortalDataVHD.vhd" -Destination
"C:\Path\To\DummyDataDisk.vhd"

\# Step 4: Apply the previously copied ACL information to the Portal
Data Disk

Set-Acl -Path "C:\Path\To\DummyDataDisk.vhd" -AclObject $acl
```
-   Attach The Portal Data VHD to the Arc VM

    1.  Get familiar with Azure CLI. Details are not provided here.

    2.  Use “az stack-hci-vm disk attach” to attach the Portal Data VHD
        to the Portal VM
```powershell
az stack-hci-vm disk attach \\

--resource-group "your-resource-group" \\

--vm-name "your-vm-name" \\

--disks "your-disk"

\# If error occurs due to the incompatible version of “stack-hci-vm”,
use commands below to install the needed version:

az extension remove --name stack-hci-vm

az extension add --name stack-hci-vm --version
&lt;the-compatible-version&gt;
```
-   Test if the Arc VM is functioning

    1.  Go to the Portal VM resource page

    2.  Check if the data disk shows up  
        <img src=".\attachments\/media/image26.png"
        style="width:3in;height:1.89784in"
        alt="A screenshot of a computer Description automatically generated" />

    3.  Start the Portal VM (we stopped it earlier) and wait until the
        VM “Status” shows “Running

##### **Configure Additional Storage** (for primary and replication servers):

-   Add new disk  
    <img src=".\attachments\/media/image27.png"
    style="width:3in;height:2.29167in"
    alt="A screenshot of a computer Description automatically generated" />

-   Add a new hard drive under the IDE Controller, selecting dynamically
    provisioning type with minimum **200GB**, recommended **2%** of
    expected global file system size.  
    <img src=".\attachments\/media/image28.png"
    style="width:3in;height:1.82857in"
    alt="A screenshot of a computer Description automatically generated" />

-   Save the configuration to create the disk  
    <img src=".\attachments\/media/image29.png"
    style="width:3in;height:1.08716in"
    alt="A screenshot of a computer Description automatically generated" />

-   Wait until the disk is created and the VM is updated  
    <img src=".\attachments\/media/image30.png"
    style="width:3in;height:2.18493in"
    alt="A screenshot of a computer Description automatically generated" />

##### Log in to the Server to Create the Archive Pool:

-   **IMPORTANT:** Although the Portal VM has an assigned IP address,
    its networking setup is not yet complete. To connect, use either a
    locally set up Windows Admin Center (WAC) or WAC on Azure. For this
    example, we will use WAC on Azure.

-   Connect to the WAC on Azure from the Azure Local UI  
    <img src=".\attachments\/media/image31.png"
    style="width:3in;height:2.14359in"
    alt="A screenshot of a computer Description automatically generated" />

-   Find the Portal VM  
    <img src=".\attachments\/media/image32.png"
    style="width:3in;height:2.15833in"
    alt="A screenshot of a computer Description automatically generated" />

-   Enter the VM’s UI and Connect  
    <img src=".\attachments\/media/image33.png"
    style="width:3in;height:2.58034in"
    alt="A screenshot of a computer Description automatically generated" />

-   Enter the credentials that can manage the VM on the local cluster.
    This is typically a legitimate network login.  
    <img src=".\attachments\/media/image34.png"
    style="width:3in;height:1.73526in"
    alt="A screenshot of a computer Description automatically generated" />

-   Log in to the VM using the default credentials (username: root,
    password: ctera321), and then change the password.  
    <img src=".\attachments\/media/image35.png"
    style="width:3in;height:1.12127in"
    alt="A screenshot of a computer Description automatically generated" />

-   Identify the disk for the archive pool using **fdisk -l**.

-   Create the archive pool with **portal-storage-util.sh
    create\_db\_archive\_pool &lt;Device&gt;**.  
    <img src=".\attachments\/media/image36.png"
    style="width:4in;height:2.59017in"
    alt="A screenshot of a computer screen Description automatically generated" />

-   Start HCP AWE Portal services with **portal-manage.sh start**.  
    <img src=".\attachments\/media/image37.png"
    style="width:4in;height:0.39188in" />

##### Configure Network Settings:

-   During the previous step of creating a Portal VM, an IP address was
    assigned to the VM. Locate this IP address in the Azure Portal
    before proceeding.

-   Use **nmtui** to configure network settings, including setting a
    static IP, default gateway, and DNS servers.

-   Restart the network service with **service network restart** for
    changes to take effect.

#### Installation Workflow (as **Arc VM** – Option 2)

-   This option (Option 2) is **preferred** and has less steps than
    Option 1. This option heavily utilizes ARM template, covering the
    step 1, 2, and partial 3 in Option 1, reducing manual works. This
    option deploys several resources, with dependencies configured, at
    once.

##### Deploy a Portal VM instance with all the required resources in a single ARM template

-   **Prerequisites**:

    1.  Ensure the VM images are uploaded to the cluster and accessible

    2.  Ensure there are “Logical networks” created and configured on
        the cluster for the VM usage

    3.  Ensure you have created a dummy Key pair that the dummy public
        key can be used as “Key Data” parameter. You can use OpenSSL to
        create or other tools convenient to use.

    4.  **IMPORTANT** – The ARM template example below includes
        hardcoded parameters for processors and memory sizes. Adjust
        these (in the “**hardwareProfile**” key ) based on your
        requirements or create additional input parameters.

-   Use ARM template to deploy all the resources at once:

    1.  Use “**Deploy a customer template**” service on Azure Portal  
        <img src=".\attachments\/media/image16.png"
        style="width:3in;height:1.33641in"
        alt="A screenshot of a computer Description automatically generated" />

    2.  Choose “**Build your own template in the editor**”

    3.  Copy the example ARM template below, paste into UI on Azure, and
        click “Save”

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "customLocationId": {
      "type": "string"
    },
    "location": {
      "type": "string"
    },
    "osImageName": {
      "type": "string"
    },
	"osImagePath": {
      "type": "securestring"
    },
	"dataImageName": {
      "type": "string"
    },
	"dataImagePath": {
      "type": "securestring"
    },
    "vmName": {
      "type": "string"
    },
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    },
    "securityType": {
      "type": "string"
    },
    "keyData": {
      "type": "securestring"
    },
    "logicNetworkId": {
      "type": "string"
    },
    "logicNetworkGateway": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "microsoft.azurestackhci/galleryimages",
      "apiVersion": "2023-09-01-preview",
      "name": "[parameters('osImageName')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "osType": "Linux",
        "hyperVGeneration": "V1",
        "imagePath": "[parameters('osImagePath')]"
      },
      "tags": {}
    },
	{
      "type": "microsoft.azurestackhci/galleryimages",
      "apiVersion": "2023-09-01-preview",
      "name": "[parameters('dataImageName')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "osType": "Linux",
        "hyperVGeneration": "V1",
        "imagePath": "[parameters('dataImagePath')]"
      },
      "tags": {}
    },
    {
      "type": "Microsoft.HybridCompute/machines",
      "apiVersion": "2023-06-20-preview",
      "name": "[parameters('vmName')]",
      "kind": "HCI",
      "location": "[parameters('location')]",
      "identity": {
        "type": "SystemAssigned"
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/networkInterfaces",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('vmName'), '-nic')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "ipConfigurations": [
          {
            "name": "[concat(parameters('vmName'), '-nic')]",
            "properties": {
              "gateway": "[parameters('logicNetworkGateway')]",
              "subnet": {
                "id": "[parameters('logicNetworkId')]"
              }
            }
          }
        ]
      }
    },
	{
      "type": "Microsoft.AzureStackHCI/virtualHardDisks",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('vmName'), '-data')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "diskFileFormat": "vhd",
        "diskSizeGB": 60,
        "dynamic": false,
        "hyperVGeneration": "V1"
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/VirtualMachineInstances",
      "apiVersion": "2023-09-01-preview",
      "name": "default",
      "scope": "[concat('Microsoft.HybridCompute/machines/', parameters('vmName'))]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "dependsOn": [
        "[resourceId('Microsoft.HybridCompute/machines', parameters('vmName'))]",
        "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('vmName'), '-nic'))]",
        "[resourceId('microsoft.azurestackhci/galleryimages', parameters('osImageName'))]",
		"[resourceId('microsoft.azurestackhci/galleryimages', parameters('dataImageName'))]",
		"[resourceId('Microsoft.AzureStackHCI/virtualHardDisks', concat(parameters('vmName'), '-data'))]"
      ],
      "properties": {
        "osProfile": {
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]",
          "computerName": "[parameters('vmName')]",
          "linuxConfiguration": {
            "provisionVMAgent": false,
            "provisionVMConfigAgent": false,
            "ssh": {
              "publicKeys": [
                {
                  "keyData": "[parameters('keyData')]",
                  "path": "[concat('/home/', parameters('adminUsername'), '/.ssh/authorized_keys')]"
                }
              ]
            },
            "disablePasswordAuthentication": false
          }
        },
        "hardwareProfile": {
          "vmSize": "Default",
          "processors": 4,
          "memoryMB": 8192
        },
        "storageProfile": {
		  "dataDisks": [
		    {
              "id": "[resourceId('Microsoft.AzureStackHCI/virtualHardDisks', concat(parameters('vmName'), '-data'))]"
            }
		  ],
          "imageReference": {
            "id": "[resourceId('microsoft.azurestackhci/galleryimages', parameters('osImageName'))]"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('vmName'), '-nic'))]"
            }
          ]
        }
      }
    }
  ]
}

```


4.  Fill in the parameters:  
    <img src=".\attachments\/media/image38.png"
    style="width:3in;height:4.6535in" />

    1.  **Resource Group**: New or Existing group

    2.  **Region**: The region where your Azure Local cluster and the
        **Custom Location** (see below) are located.

    3.  **Custom Location ID**: Each Azure Local Cluster comes with a
        Custom Location ID, which you can find it by hunting down to the
        resource and click into the JSON View like this  
        <img src=".\attachments\/media/image19.png"
        style="width:4in;height:1.55632in"
        alt="A screenshot of a computer Description automatically generated" />  
        Where you can also find the “**location**” parameter

    4.  **Location**: The same as “Region” but needs to be entered again
        using the corresponding code found in the **Custom Location**
        JSON View.

    5.  **OS Image Name**: A name you will recognize for the OS VHD

    6.  **OS Image Path**: Paste the SAS Link of the OS VHD image you
        generated previously

    7.  **Data Image Name**: A name you will recognize for the Data VHD

    8.  **Data Image Path**: Paste the SAS Link of the Data VHD image
        you generated previously

    9.  **VM Name**: The name of the Portal VM instance to be created

    10. **Admin Username**: This can be **any dummy username**, not to
        be used, to satisfy Azure Rest API requirements

    11. **Admin Password**: This can be **any dummy password**, not to
        be used, to satisfy Azure Rest API requirements

    12. **Security Type**: Enter “Standard”

    13. **Key Data**: Enter the dummy public key generated previously

    14. **Logic Network ID**: The resource ID that you can acquire in
        the JSON view of the logic network resource

    15. **Logic Network Gateway**: The gateway IP to be supplied to the
        Portal VM’s NIC

    16. **Note** – This template is a working example. Experienced ARM
        users can easily customize as they see fit.

5.  Click “**Review + Create**” after filling in the parameters

6.  If no error alerts showing up, click “**Create**” and wait the
    process to finish

7.  Check if the Portal VM and related resources are created and running

8.  Stop the Portal VM

##### Replace the Dummy Data Disk

-   Replace the Dummy Data Disk with a copy of the Data VHD. The steps
    are

    1.  Copy the ACL information from the Dummy Data Disk.

    2.  Remove the Dummy Data Disk.

    3.  Copy the Portal Data VHD to the location of the deleted Dummy
        Data Disk, ensuring it has the same name.

    4.  Apply the previously copied ACL information to the Portal Data
        Disk
    
    5. Start the Portal VM.
```powershell
# Step 0: Find the path to the Dummy Data Disk VHD file. It resides in
Cluster Storage. Example:
C:\ClusterStorage\UserStorage\_2\e254bb98922eeec\PortalDemo2-data-&lt;subscription\_id&gt;-&lt;resource
group\_name&gt;.vhd

# Step 1: Copy the ACL information from the Dummy Data Disk

$acl = Get-Acl -Path "C:\Path\To\DummyDataDisk.vhd"

# Step 2: Remove the Dummy Data Disk

Remove-Item -Path "C:\Path\To\DummyDataDisk.vhd" -Force

# Step 3: Copy the Portal Data VHD to the location of the deleted Dummy
Data Disk, ensuring it has the same name

Copy-Item -Path "C:\Path\To\PortalDataVHD.vhd" -Destination
"C:\Path\To\DummyDataDisk.vhd"

# Step 4: Apply the previously copied ACL information to the Portal
Data Disk

Set-Acl -Path "C:\Path\To\DummyDataDisk.vhd" -AclObject $acl

# Step 5: Start the Portal VM.
```


##### Follow Step 4 to 6 in Option 1

-   **Note 1**: Step 4 to 6 is the common steps that can be used in
    Option 2

-   **Note 2**: Experienced ARM template users can include “Additional
    Storage” in the ARM template to further simplify the deployment
    process

#### Add Storage Nodes for HCP AWE Portal

This procedure is standard for all Portal Installation Workflows.

1.  **Log in to the Server**:

    -   For NFS storage nodes, log in to the server as **root** using
        SSH.

2.  **Create an NFS Mount Folder**:

    -   On the server, create a folder specifically for the NFS mount.

3.  **Mount the NFS Storage Node**:

    -   Run the following script on each server (except the preview
        server):

    -   portal-mount.sh mount\_storage\_node NFS\_IP:/NFS\_FOLDER

**Note**: Replace NFS\_IP with the IP address of the NFS mount point
and NFS\_FOLDER with the name of the folder created on the NFS server.

4.  **Access the Global Administration View**:

    -   In the HCP AWE Portal, navigate to **Main &gt; Storage
        Nodes** in the navigation pane.

5.  **Add or Edit a Storage Node**:

    -   Either add a new storage node by clicking **New Storage Node
        or** edit an existing one by clicking the node’s name.

    -   Enter the generic details for the storage node (applicable to
        all types).

    -   Depending on the storage node type (e.g., Amazon S3, Azure Blob,
        Hitachi HCP, etc.), complete the additional fields specific to
        that type.

#### Add HCP for Cloud Scale as Storage Nodes for HCP AWE Portal

This procedure is standard for all Portal Installation Workflows.

-   Log in to the “Admin” portal and select “Administration” context and
    click the “Storage Nodes”. Then click the “New Storage Node” to
    initiate the wizard.

<img src=".\attachments\/media/image39.png"
style="width:5in;height:3.41346in" />

<img src=".\attachments\/media/image40.png"
style="width:6.5in;height:3.39583in" />

-   Change the first dropdown “Type:” to Amazon S3. This will change the
    wizard UI as seen in the next screenshot.

<img src=".\attachments\/media/image41.png"
style="width:5.17433in;height:4.5625in" />

-   Provide the required fields

    -   Your access key and secret access key can be generated from the
        HCP CS Console.

<img src=".\attachments\/media/image42.png"
style="width:6.5in;height:1.09375in" />

-   Once completed, you will see the S3 bucket has successfully
    connected:

<img src=".\attachments\/media/image43.png"
style="width:6.5in;height:0.94792in" />

#### Additional Notes

-   For backup, block-storage-level snapshots are an option, but they
    have limitations regarding point-in-time recovery and data loss on
    failure.

-   For detailed network configuration, including static routes and DHCP
    settings, refer to the **nmtui** tool and the provided network
    service commands.

### Installing HCP Anywhere Enterprise Edge Filer on Azure Local (Hyper-V) 

#### Warning

-   Do not clone an existing/running HCP Anywhere Enterprise Edge Filer
    at template for installation. Always use the provided VHD template
    file.

#### Installation Workflow (as Non-Arc VM)

##### Create a Portal Instance in Hyper-V:

-   Open the Azure Local management interface:

    1.  Option 1: Use Windows Admin Center

    2.  Option 2: Use PowerShell

    3.  Option 3: Use Windows Admin Center on Azure portal (if your
        Azure Local cluster is registered with Azure and WAC on Azure
        enabled)  
        <img src=".\attachments\/media/image13.png"
        style="width:3in;height:2.17in"
        alt="A screenshot of a computer Description automatically generated" />

-   Create a new virtual machine with the following specifications:

    1.  Generation: 1

    2.  Memory: Assign the default startup memory recommended by the
        wizard

    3.  Virtual Processors: Adjust based on the HCP AWE Edge Filer
        license (see step 3)

    4.  Network Adapter: Connected to the appropriate virtual switch

    5.  Hard Disk: Attach the HCP AWE Edge Filer VHD file provided by
        HCP Anywhere Enterprise Support

##### Configure the Virtual Machine:

-   Attach an additional virtual hard disk to the VM for storing data:

    -   Format: VHDX

    -   Disk Type: Fixed size (recommended for performance) or
        Dynamically expanding

    -   Size: According to your license and needs (20% of the Portal
        Global Name Space recommended)

##### Set Virtual Processors:

-   Adjust the number of virtual processors based on the HCP AWE Edge
    Filer license:

    1.  EV16: up to 4 processors

    2.  EV32: up to 8 processors

    3.  EV64: up to 16 processors

    4.  EV128: up to 32 processors

    5.  EV256: up to 64 processors

##### Start the Virtual Machine:

-   Power on the Edge Filer VM to proceed with the initial setup.

#### Installation Workflow (as **Arc VM**)

-   Unlike illustrated in the Installation Workflows for Portal VM, this
    only describes how to deploy the Edge Filer VM using one ARM
    template. Users can break it down to separate deployments of the
    different resources as needed.

##### Deploy an Edge Filer VM instance with all the required resources in a single ARM template

-   **Prerequisites**:

    1.  Ensure the VM images are uploaded to the cluster and accessible

    2.  Ensure there are “Logical networks” created and configured on
        the cluster for the VM usage

    3.  Ensure you have created a dummy Key pair that the dummy public
        key can be used as “Key Data” parameter. You can use OpenSSL to
        create or other tools convenient to use.

    4.  **IMPORTANT** – The ARM template example below includes
        hardcoded parameters for processors and memory sizes. Adjust
        these (in the “**hardwareProfile**” key) based on your
        requirements or create additional input parameters.



-   Use ARM template to deploy all the resources at once:

    1.  Use “**Deploy a customer template**” service on Azure Portal  
        <img src=".\attachments\/media/image16.png"
        style="width:3in;height:1.33641in"
        alt="A screenshot of a computer Description automatically generated" />

    2.  Choose “**Build your own template in the editor**”

    3.  Copy the example ARM template below, paste into UI on Azure, and
        click “Save”

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "customLocationId": {
      "type": "string"
    },
    "location": {
      "type": "string"
    },
    "imageName": {
      "type": "string"
    },
    "imagePath": {
      "type": "securestring"
    },
    "name": {
      "type": "string"
    },
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    },
    "securityType": {
      "type": "string"
    },
    "keyData": {
      "type": "securestring"
    },
	"logicNetworkId": {
      "type": "string"
    },
	"logicNetworkGateway": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "microsoft.azurestackhci/galleryimages",
      "apiVersion": "2023-09-01-preview",
      "name": "[parameters('imageName')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "osType": "Linux",
        "hyperVGeneration": "V1",
        "imagePath": "[parameters('imagePath')]"
      },
      "tags": {}
    },
    {
      "type": "Microsoft.HybridCompute/machines",
      "apiVersion": "2023-06-20-preview",
      "name": "[parameters('name')]",
      "kind": "HCI",
      "location": "[parameters('location')]",
      "identity": {
        "type": "SystemAssigned"
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/networkInterfaces",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('name'), '-nic')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "ipConfigurations": [
          {
            "name": "[concat(parameters('name'), '-nic')]",
            "properties": {
              "gateway": "[parameters('logicNetworkGateway')]",
              "subnet": {
                "id": "[parameters('logicNetworkId')]"
              }
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/VirtualMachineInstances",
      "apiVersion": "2023-09-01-preview",
      "name": "default",
      "scope": "[concat('Microsoft.HybridCompute/machines/', parameters('name'))]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "dependsOn": [
        "[resourceId('Microsoft.HybridCompute/machines', parameters('name'))]",
        "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('name'), '-nic'))]",
        "[resourceId('microsoft.azurestackhci/galleryimages', parameters('imageName'))]"
      ],
      "properties": {
        "osProfile": {
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]",
          "computerName": "[parameters('name')]",
          "linuxConfiguration": {
            "provisionVMAgent": false,
            "provisionVMConfigAgent": true,
            "ssh": {
              "publicKeys": [
                {
                  "keyData": "[parameters('keyData')]",
                  "path": "[concat('/home/', parameters('adminUsername'), '/.ssh/authorized_keys')]"
                }
              ]
            },
            "disablePasswordAuthentication": false
          }
        },
        "hardwareProfile": {
          "vmSize": "Default",
          "processors": 4,
          "memoryMB": 8192
        },
        "storageProfile": {
          "imageReference": {
            "id": "[resourceId('microsoft.azurestackhci/galleryimages', parameters('imageName'))]"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('name'), '-nic'))]"
            }
          ]
        }
      }
    }
  ]
}

```


4.  Fill in the parameters:  
    <img src=".\attachments\/media/image44.png"
    style="width:3in;height:4.05224in"
    alt="A screenshot of a computer Description automatically generated" />

    1.  **Resource Group**: New or Existing group

    2.  **Region**: The region where your Azure Local cluster and the
        **Custom Location** (see below) are located.

    3.  **Custom Location ID**: Each Azure Local Cluster comes with a
        Custom Location ID, which you can find it by hunting down to the
        resource and click into the JSON View like this  
        <img src=".\attachments\/media/image19.png"
        style="width:4in;height:1.55632in"
        alt="A screenshot of a computer Description automatically generated" />  
        Where you can also find the “**location**” parameter

    4.  **Location**: The same as “Region” but needs to be entered again
        using the corresponding code found in the **Custom Location**
        JSON View.

    5.  **Image Name**: A name you will recognize for the EF VHD

    6.  **Image Path**: Paste the SAS Link of the EF VHD image you
        generated previously

    7.  **Name**: The name of the Edge Filer VM instance to be created

    8.  **Admin Username**: This can be **any dummy username**, not to
        be used, to satisfy Azure Rest API requirements

    9.  **Admin Password**: This can be **any dummy password**, not to
        be used, to satisfy Azure Rest API requirements

    10. **Security Type**: Enter “Standard”

    11. **Key Data**: Enter the dummy public key generated previously

    12. **Logic Network ID**: The resource ID that you can acquire in
        the JSON view of the logic network resource

    13. **Logic Network Gateway**: The gateway IP to be supplied to the
        Portal VM’s NIC

    14. **Note** – This template is a working example. Experienced ARM
        users can easily customize as they see fit.

5.  Click “**Review + Create**” after filling in the parameters

6.  If no error alerts showing up, click “**Create**” and wait the
    process to finish

7.  Check if the Edge Filer VM and related resources are created and
    running

8.  Stop the Edge Filer VM

##### Configure the Virtual Machine:

-   Attach an additional virtual hard disk to the VM for storing data as
    needed:

    -   Format: VHDX

    -   Disk Type: Fixed size (recommended for performance) or
        Dynamically expanding

    -   Size: According to your license and needs (20% of the Portal
        Global Name Space recommended)

-   Perform the action using the Azure Portal after creating the EF VM,
    or define additional resources in the ARM template before creating
    the EF VM.

##### Start the Virtual Machine:

-   Power on the Edge Filer VM to proceed with the initial setup.

#### Initial Network Configuration

This procedure is standard for all Portal Installation Workflows.

-   **For DHCP**:

    -   Log in to the VM console using the username **setup** with no
        password.

    -   The DHCP-assigned IP address will be displayed on the console.

-   **For Static IP**:

    -   Access the VM console and log in as above.

    -   Navigate to Network settings and select Static IP mode.

    -   Enter the required network details: static IP, netmask, default
        gateway, and DNS server IPs.

    -   Confirm the settings with OK.

#### Additional Notes

-   Ensure that the virtual network and subnet for the HCP AWE Edge
    Filer VM are properly configured in Azure Local.

-   Configure the necessary inbound and outbound firewall rules for the
    HCP AWE Edge Filer based on the communication requirements.

-   Follow best practices for securing and managing your virtual
    machines, such as regularly applying updates, configuring backup and
    disaster recovery, and monitoring resource utilization.

### Recommendation: Deployments with Azure Resource Manager templates

Azure Resource Manager (ARM) templates are JSON files that declaratively
define the infrastructure and configuration of Azure resources. They
allow you to create, update, and delete resources consistently and
repeatedly. ARM templates consist of parameters for customization,
variables for reusability, resources for specifying the desired state of
infrastructure, and outputs for returning important information after
deployment.

To deploy an ARM template, you use Azure PowerShell, Azure CLI, or the
Azure portal, providing the template file and required parameters. ARM
validates the template, creates a deployment plan, and provisions the
specified resources in the target Azure subscription and resource group.
ARM templates enable infrastructure as code, consistency across
environments, modularity, and extensibility, making it easier to
automate the provisioning and management of Azure resources.

#### Core Concepts

-   **ARM Templates Overview:** This is the foundational starting point
    to understanding the concept behind ARM
    templates. <https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview>

-   **ARM Templates Structure & Syntax:** Dive deeper into how to
    compose ARM templates and the elements
    within. <https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-syntax>

Below is an example of deploying HCP Anywhere Enterprise Edge Filer
using ARM templates on Azure (not on Azure Local). The workflow would as
well apply to deployments for HCP Anywhere Enterprise Portal. In order
to leverage Azure Resource Manager, a <u>template</u> is required. The
easiest method to create a template is to navigate to <u>an existing
successful deployment</u> and downloading the template.

<img src=".\attachments\/media/image45.png"
style="width:6.5in;height:2.125in" />

Select the deployment you would like to create a template from:

In this example, we will create a template from an HCP AWE Edge filer we
previously deployed via Azure Portal.

<img src=".\attachments\/media/image46.png"
style="width:6.5in;height:4.82292in" />

Once you click the deployment, navigate to the “Template” option and
click “Download”.

<img src=".\attachments\/media/image47.png"
style="width:6.5in;height:3.78125in" />

The download will provide you with two files.

1.  Template file – contains the configuration information of the VM.

2.  Parameter file – contains some of the unique parameters for the VM.
    You can modify this file to reflect changes you want to make to the
    new VM.

From the machine you wish to deploy from, install the required Azure
PowerShell Module:
```powershell
Install-Module -Name Az -Repository PSGallery -Force
```
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th>Install-Module -Name Az -Repository PSGallery -Force</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

Run the following commands to connect to your Azure account:
```powershell
Connect-AzAccount
```


Run the following command to set the context to your subscription:
```powershell
Set-AzContext SubscriptionName
```

A simple PowerShell script below will create a new resource group and
deploy a VM in the resource group.
```powershell
$resourceGroupName = Read-Host -Prompt "Enter a resource group name that is used to generate resource" 

New-AzResourceGroup -Name $resourceGroupName -Location "Central US"

$templateFile = Read-Host -Prompt "Enter the template file path and file name"
$parameterFile = Read-Host -Prompt "Enter the parameter file path and file name"

New-AzResourceGroupDeployment -Name DeployLocalTemplate -ResourceGroupName $resourceGroupName -TemplateFile $templateFile -TemplateParameterFile $parameterFile -verbose

```


This will trigger the deployment of the template:

<img src=".\attachments\/media/image48.png"
style="width:6.5in;height:4.03542in" />

Once the VM is deployed, the parameters will be configured from our
parameters file:

<img src=".\attachments\/media/image49.png"
style="width:6.5in;height:5.875in" />

Your deployment is complete, and you can now validate that the VM is up
and running:

<img src=".\attachments\/media/image50.png"
style="width:6.5in;height:3.61458in" />

We navigate to the public IP Assigned and see the Edge filer **webui**
is running.

<img src=".\attachments\/media/image51.png"
style="width:6.5in;height:3.58333in" />

### Connect Edge Filers with Portal

This section explains the process to connect an Edge Filer to the
Portal.

1.  Create your portal admin account.

-   Connect to the Admin Portal and switch context to your portal
    instance. In our screen shots, our context is “Test-portal”.

-   Click New User and fill out the required fields. The ‘Role’ should
    be “Read/Write Administrator”.

<img src=".\attachments\/media/image52.png"
style="width:4.77344in;height:4.9315in" />

#### Click Save and your new user is created.

<img src=".\attachments\/media/image53.png"
style="width:6.5in;height:2.42708in" />

-   Open a new browser tab and navigate to the Services Portal this time
    and validate that your login is working as expected.

<img src=".\attachments\/media/image54.png"
style="width:5.9375in;height:3.20833in" />

1.  Connect your Edge Filer to Portal.

#### Log in to your Edge Filer instance. You will be presented with the setup up wizard. 

<img src=".\attachments\/media/image55.png"
style="width:4.92708in;height:3.96882in" />

-   Enter the Portal IP.

-   Enter the credentials of the account created in the previous step.

-   Complete the rest of the wizard and your edge filer is connected to
    the portal. You can validate that it is visible in the Portal under
    “Devices”.

<img src=".\attachments\/media/image56.png"
style="width:4.98958in;height:4.35417in" />

### **Important: Additional Considerations on Networking and Firewall Settings**

When checking for network connectivity issues where traffic goes through
a firewall, verify if the firewall is configured to ‘reject’ or ‘deny’
traffic to port **995**. A firewall with a setting of ‘reject’ traffic
might let TCP sessions be established before stopping any application
traffic after the session is created. **This can make it seem like port
995 traffic is passing through the firewall when it is not.**