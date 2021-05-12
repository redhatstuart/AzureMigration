Before the Hands on lab
![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Before the Java application on JBoss EAP/RHEL migration lab
</div>

<div class="MCWHeader2">
Before the hands-on lab setup guide
</div>

<div class="MCWHeader3">
April 2021
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2021 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Java on JBoss EAP/RHEL application migration before the hands-on lab setup guide](#line-of-business-application-migration-before-the-hands-on-lab-setup-guide)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
    - [Task 1: Deploy the on-premises environment](#task-1-deploy-the-on-premises-environment)
    - [Task 2: Verify the on-premises environment](#task-2-verify-the-on-premises-environment)

<!-- /TOC -->

# Java on JBoss EAP/RHEL application migration before the hands-on lab setup guide 

## Requirements

1. You will need Owner or Contributor permissions for an Azure subscription to use in the lab.

2. Your subscription must have sufficient unused quota to deploy the VMs used in this lab. To check your quota:

    - Log in to the Azure portal, select **All services** then **Subscriptions**. Select your subscription, then choose **Usage + quotas**.
  
    - From the **Select a provider** drop-down, select **Microsoft.Compute**.
  
    - From the **All service quotas** drop down, select **Standard DSv3 Family vCPUs**, **Standard FSv2 Family vCPUs** and **Total Regional vCPUs**.
  
    - From the **All locations** drop down, select the location where you will deploy the lab.
  
    - From the last drop-down, select **Show all**.
  
    - Check that the selected quotas have sufficient unused capacity:
  
        - Standard DSv3 Family vCPUs: **at least 8 vCPUs**.
  
        - Standard FSv2 Family vCPUs: **at least 6 vCPUs**.

        - Total Regional vCPUs: **at least 14 vCPUs**.

    > **Note:** If you are using an Azure Pass subscription, you may not meet the vCPU quotas above. In this case, you can still complete the lab, by taking the following steps:

     >- Deploy the 'on-premises' environment (see below) in a different Azure region to the Azure VMs created during migration. With this change, you will only need 8 Total Regional vCPUs. Migration will take a little longer since data must be transferred between regions.
        
     >- Use a different VM tier instead of FSv2 for the migrated VMs (for example, DSv2 or DSv3). However, you cannot change the tier of the DSv3 VM, since this tier is required for the nested virtualization support used to implement the 'on-premises' environment.

## Before the hands-on lab

Duration: 60 minutes

### Task 1: Deploy the on-premises environment

1. Deploy the template **azuredeploy.json** to a new resource group. This template deploys a virtual machine running Red Hat Enterprise Linux with 3 nested VMs. This comprises the 'on-premises' environment which you will assess and migrate during this lab.

    You can deploy the template by selecting the 'Deploy to Azure' button below. You will need to create a new resource group. The suggested resource group name to use is **CovidVaccineDataHostRG**. You will also need to select a location close to you to deploy the template to. Then choose **Review + create** 
    NOTE: You will need to scroll down to Admin Password and create the password. The workshop is written with **demo!pass123** as the password.
Click **Create**. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fcloudworkshop.blob.core.windows.net%2Fline-of-business-application-migration%2Fsept-2020%2FSmartHotelHost.json" target="_blank">![Button to deploy the CovidVaccineDataHost template to Azure.](images/BeforeTheHOL/deploy-to-azure.png "Deploy the CovidVaccineDataHost template to Azure")</a>

    > **Note:** The template will take around 6-7 minutes to deploy. Once template deployment is complete, you will need to begin an Azure Migration to the point of downloading and deploying your migration appliance to your on-premises server. Without this step, the workshop will not work.

### Task 2: Verify the on-premises environment

1. Navigate to the **CovidVaccineDataHost** VM that was deployed by the template in the previous step.

2. Make a note of the public IP address.

3. Open a browser tab and navigate to **http://\<CovidVaccineDataHostIP-Address\>**. You should see the Covid Vaccine application, which is running on nested VMs within JBoss EAP and Red Hat Enterprise Linux on the CovidVaccineDataHost.

    ![Browser screenshot showing the Covid Vaccine Data application.](images/BeforeTheHOL/covid.png)

    > **Note:** If the Covid Vaccine application is not shown, wait 10 minutes and try again. It takes **at least 1 hour** from the start of template deployment. You can also check the CPU, network, and disk activity levels for the CovidVaccineDataHost VM in the Azure portal, to see if the provisioning is still active.

You should follow all steps provided *before* performing the Hands-on lab.
