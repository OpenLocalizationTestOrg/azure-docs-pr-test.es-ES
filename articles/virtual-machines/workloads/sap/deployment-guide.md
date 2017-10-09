---
title: "implementación de máquinas virtuales para SAP NetWeaver aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo SAP toodeploy software en máquinas virtuales de Linux en Azure."
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 1c4f1951-3613-4a5a-a0af-36b85750c84e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.openlocfilehash: 42f1d8a3eff51e113729dbfe2848b67deaf06936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a>Implementación de Azure Virtual Machines para SAP NetWeaver
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP)
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md (Azure Virtual Machines deployment for SAP)
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md (Azure Virtual Machines planning and implementation for SAP)
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-managed-disks]:planning-guide.md#c55b2c6e-3ca1-4476-be16-16c81927550f (Managed Disks)
[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-os-disk-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk-md%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-2-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image-md%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image-md%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-windows-agent-user-guide]:../../windows/agent-user-guide.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Máquinas virtuales de Azure es la solución de Hola para organizaciones que necesitan recursos de proceso y almacenamiento, en un tiempo mínimo y sin ciclos de adquisición prolongados. Puede usar máquinas virtuales de Azure toodeploy clásico aplicaciones como aplicaciones basadas en SAP NetWeaver en Azure. Amplíe la confiabilidad y disponibilidad de una aplicación sin recursos locales adicionales. Azure Virtual Machines admite la conectividad entre locales, así que podrá integrar Azure Virtual Machines a los dominios locales, las nubes privadas y la infraestructura de sistema SAP de la organización.

En este artículo, trataremos las aplicaciones de SAP toodeploy pasos hello en máquinas virtuales (VM) en Azure, incluidas las opciones de implementación alternativas y solución de problemas. En este artículo se basa en información de hello en [máquinas virtuales de Azure planificación e implementación para SAP NetWeaver][planning-guide]. También complementa la documentación de la instalación de SAP y las notas de SAP, que son recursos principales de Hola para instalar e implementar el software SAP.

## <a name="prerequisites"></a>Requisitos previos
Configurar una máquina virtual de Azure para la implementación de software de SAP conlleva varios pasos y recursos. Antes de empezar, asegúrese de que se cumplen los requisitos previos de hello para la instalación de software SAP en máquinas virtuales en Azure.

### <a name="local-computer"></a>Equipo local
toomanage Windows o máquinas virtuales de Linux, puede usar un script de PowerShell y Hola portal de Azure. Para ambas herramientas, necesita un equipo local que ejecute Windows 7 o una versión posterior de Windows. Si desea toomanage solo máquinas virtuales de Linux y desea que un equipo Linux toouse para esta tarea, puede utilizar la CLI de Azure.

### <a name="internet-connection"></a>Conexión a Internet
toodownload y herramientas de ejecución hello y secuencias de comandos que son necesarios para la implementación de software SAP, debe estar conectado toohello Internet. Hola VM de Azure que ejecuta hello Azure extensión de supervisión mejorada para SAP también es necesario toohello de acceso a Internet. Si hello Azure VM es parte de una red virtual de Azure o de dominio local, asegúrese de que se establecen opciones de proxy correspondientes de hello, como se describe en [configurar el proxy de hello][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Suscripción de Microsoft Azure
Necesita una cuenta de Azure activa.

### <a name="topology-and-networking"></a>Topología y redes
Necesita toodefine topología de Hola y la arquitectura de hello implementación de SAP en Azure:

* Toobe de cuentas de almacenamiento de Azure usa
* Red virtual donde desea que el sistema SAP de hello toodeploy
* Toowhich de grupo de recursos que desea toodeploy Hola SAP sistema
* Región de Azure donde desea que el sistema SAP de hello toodeploy
* Configuración de SAP (dos o tres niveles)
* Tamaños de máquina virtual y el número de Hola de toobe de discos de datos adicionales montados toohello las máquinas virtuales
* Configuración de SAP Correction and Transport System (CTS)

Crear y configurar cuentas de almacenamiento de Azure (si es necesario) o redes virtuales de Azure antes de comenzar el proceso de implementación de software SAP de Hola. Para obtener información acerca de cómo toocreate y configurar estos recursos, consulte [máquinas virtuales de Azure planificación e implementación para SAP NetWeaver][planning-guide].

### <a name="sap-sizing"></a>Ajuste del tamaño de SAP
Saber Hola siguiente información para el ajuste de SAP:

* Proyectar la carga de trabajo SAP, por ejemplo, mediante el uso de la herramienta de SAP Quick Sizer de Hola y Hola SAP aplicación rendimiento estándar (SAPS) número
* Requiere consumo de memoria y recursos de CPU del sistema SAP de Hola
* Número de operaciones de entrada/salida (E/S) por segundo
* Ancho de banda de red que se requiere ante una eventual comunicación entre distintas máquinas virtuales en Azure
* Ancho de banda de red requerido entre hello sistema SAP implementado en Azure y recursos locales

### <a name="resource-groups"></a>Grupos de recursos
En el Administrador de recursos de Azure, puede usar toomanage de grupos de recursos todos los recursos de la aplicación hello en su suscripción de Azure. Para más información, consulte [Información general de Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Recursos

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Recursos de SAP
Cuando se está configurando la implementación de software SAP, necesita Hola SAP recursos siguientes:

* Nota de SAP [1928533], que incluye:
  * Lista de tamaños de máquina virtual de Azure que se admiten para la implementación de hello del software SAP.
  * Información importante sobre la capacidad para los tamaños de máquina virtual de Azure
  * Software de SAP admitido y combinaciones de sistema operativo y base de datos
  * Versión del kernel de SAP requerida para Windows y Linux en Microsoft Azure

* La nota de SAP [2015553] enumera los requisitos previos para las implementaciones de software de SAP admitidas por SAP en Azure.
* La nota de SAP [2178632] contiene información detallada sobre todas las métricas de supervisión notificadas para SAP en Azure.
* Nota de SAP [1409604] Hola necesario versión del agente de Host de SAP para Windows en Azure.
* Nota de SAP [2191498] Hola necesario versión del agente de Host de SAP para Linux en Azure.
* La nota de SAP [2243692] incluye información acerca de las licencias de SAP en Linux en Azure.
* La nota de SAP [1984787] incluye información general sobre SUSE Linux Enterprise Server 12.
* La nota de SAP [2002167] incluye información general sobre Red Hat Enterprise Linux 7.x.
* La nota de SAP [2069760] incluye información general sobre Oracle Linux 7.x.
* Nota de SAP [1999351] información adicional de solución de problemas de hello Azure extensión de supervisión mejorada para SAP.
* La nota de SAP [1597355] incluye información general sobre el espacio de intercambio para Linux.
* La página de [SCN de SAP en Azure](https://wiki.scn.sap.com/wiki/x/Pia7Gg) tiene noticias y una colección de recursos útiles.
* La [WIKI de la comunidad SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene todas las notas de SAP que se necesitan para Linux.
* Los cmdlets de PowerShell específicos de SAP y que forman parte de [Azure PowerShell][azure-ps].
* Los comandos de la CLI de Azure específicos de SAP y que forman parte de la [CLI de Azure][azure-cli].

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Recursos de Windows
Estos artículos de Microsoft se refieren a las implementaciones de SAP en Azure:

* [Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver][planning-guide]
* [Implementación de Azure Virtual Machines para SAP NetWeaver (este artículo)][deployment-guide]
* [Implementación de DBMS de Azure Virtual Machines para SAP NetWeaver][dbms-guide]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Escenarios de implementación de software de SAP en máquinas virtuales de Azure
Tiene varias opciones para implementar máquinas virtuales y sus discos asociados en Azure. Es diferencias de hello toounderstand importante entre las opciones de implementación, ya que podría seguir tooprepare pasos diferentes las máquinas virtuales para la implementación en función del tipo de implementación de Hola que elija.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Escenario 1: Implementar una máquina virtual desde hello Azure Marketplace para SAP
Puede usar una imagen proporcionada por Microsoft o por un tercero en hello Azure Marketplace toodeploy la máquina virtual. Hola Marketplace ofrece algunas imágenes de sistema operativo estándares de Windows Server y diferentes distribuciones de Linux. También puede implementar una imagen que incluya SKU del sistema de administración de base de datos (DBMS), por ejemplo, Microsoft SQL Server. Para más información sobre el uso de imágenes con SKU de DBMS, consulte [Implementación de DBMS de Azure Virtual Machines para SAP en NetWeaver][dbms-guide].

Hello diagrama de flujo siguiente muestra hello específico de SAP secuencia de pasos para implementar una máquina virtual desde hello Azure Marketplace:

![Diagrama de flujo de implementación de VM para los sistemas SAP mediante una imagen de máquina virtual de hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Crear una máquina virtual mediante Hola portal de Azure
toocreate de manera más fácil de Hello una nueva máquina virtual con una imagen de hello Azure Marketplace es mediante el uso de hello portal de Azure.

1.  Vaya demasiado<https://portal.azure.com/#create/hub>.  O bien, en hello Azure menús del portal, seleccione **+ nuevo**.
2.  Seleccione **proceso**y, a continuación, seleccione tipo hello de desea toodeploy de sistema operativo. Por ejemplo, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2) u Oracle Linux 7.2. vista de lista predeterminada de Hello no muestra que todos los sistemas operativos compatibles. Seleccione **ver todo** para obtener una lista completa. Para más información acerca de los sistemas operativos compatibles para la implementación de software de SAP, consulte la nota de SAP [1928533].
3.  En la página siguiente de hello, revise los términos y condiciones.
4.  Hola **seleccionar un modelo de implementación** , seleccione **el Administrador de recursos**.
5.  Seleccione **Crear**.

Hola asistente le guía a través de configuración de máquina virtual de hello requiere parámetros toocreate hello, además tooall necesario que los recursos, como interfaces de red y cuentas de almacenamiento. Algunos de estos parámetros son:

1. **Aspectos básicos**:
 * **Nombre**: nombre de hello del recurso de hello (nombre de máquina virtual de hello).
 * **Tipo de disco de máquina virtual**: seleccione el tipo de disco de hello del disco de SO Hola. Si desea toouse almacenamiento Premium para los discos de datos, se recomienda usar almacenamiento Premium para el disco del sistema operativo Hola así.
 * **Nombre de usuario y la contraseña** o **clave pública SSH**: escriba Hola nombre de usuario y contraseña de usuario de Hola que se crea durante el aprovisionamiento de Hola. Para una máquina virtual de Linux, puede escribir la clave de Shell seguro (SSH) pública Hola que usas toosign en toohello máquina.
 * **Suscripción**: seleccione suscripción Hola que desea toouse tooprovision Hola máquina virtual.
 * **Grupo de recursos**: nombre de Hola Hola del grupo de recursos para hello máquina virtual. Puede escribir cualquier nombre de Hola de un nombre nuevo de Hola o grupo de recursos de un grupo de recursos que ya existe.
 * **Ubicación**: donde toodeploy Hola nueva máquina virtual. Si desea que la red local de tooconnect Hola máquina virtual tooyour, asegúrese de que seleccionar ubicación de Hola de Hola de red virtual que se conecta la red local de Azure tooyour. Para más información, vea [Redes de Microsoft Azure][planning-guide-microsoft-azure-networking] en [Planeación e implementación de Azure Virtual Machines para SAP en NetWeaver][planning-guide].
2. **Tamaño**:

     Lea la nota de SAP [1928533] para ver una lista de los tipos de máquinas virtuales que se admiten. Asegúrese de que seleccionar el tipo correcto de VM de hello si desea toouse almacenamiento Premium de Azure. No todos los tipos de VM son compatibles con el Almacenamiento premium. Para más información, consulte [Almacenamiento: Microsoft Azure Storage y discos de datos][planning-guide-storage-microsoft-azure-storage-and-data-disks] y [Azure Premium Storage][planning-guide-azure-premium-storage] en [Planeación e implementación de Azure Virtual Machines para SAP en NetWeaver][planning-guide].

3. **Configuración**:
  * **Almacenamiento**
    * **Tipo de disco**: seleccione el tipo de disco de hello del disco de SO Hola. Si desea toouse almacenamiento Premium para los discos de datos, se recomienda usar almacenamiento Premium para el disco del sistema operativo Hola así.
    * **Usar discos administrados**: si desea toouse administrar discos, seleccione Sí. Para obtener más información acerca de los discos administrados, consulte el capítulo [discos administrados] [ planning-guide-managed-disks] en la Guía de planificación de Hola.
    * **Cuenta de almacenamiento**: seleccione una cuenta de almacenamiento o cree una. No todos los tipos de almacenamiento admiten la ejecución de aplicaciones SAP. Para más información sobre los tipos de almacenamiento, consulte [Microsoft Azure Storage][dbms-guide-2.3] en [Implementación de DBMS de Azure Virtual Machines para SAP en NetWeaver][dbms-guide].
  * **Red**
    * **Red virtual** y **subred**: toointegrate Hola virtual machine con la intranet, la red virtual seleccione Hola que es la red local de tooyour conectado.
    * **Dirección IP pública**: seleccione Hola dirección IP pública que se desea toouse, o especifica parámetros toocreate una nueva dirección IP pública. Puede usar la máquina virtual de un tooaccess de dirección IP pública a través de Internet de Hola. Asegúrese de que también crea una máquina red seguridad grupo toohelp un acceso seguro tooyour virtual.
    * **Grupo de seguridad de red**: para más información, consulte [Control del flujo de tráfico de red con grupos de seguridad de red][virtual-networks-nsg].
  * **Extensiones**: puede instalar extensiones de máquina virtual mediante la adición de implementación de toohello. No es necesario tooadd extensiones en este paso. las extensiones de Hello necesarias para la compatibilidad con SAP se instalan más adelante. Consulte el capítulo [configurar hello Azure extensión de supervisión mejorada para SAP] [ deployment-guide-4.5] en esta guía.
  * **Alta disponibilidad**: seleccione un conjunto de disponibilidad o escriba Hola parámetros toocreate la disponibilidad de un nuevo conjunto. Consulte [Conjuntos de disponibilidad de Azure][planning-guide-3.2.3] para más información.
  * **Supervisión**
    * **Diagnósticos de arranque**: puede seleccionar **Deshabilitar** para el diagnóstico de arranque.
    * **Diagnósticos del SO invitado**: puede seleccionar **Deshabilitar** para el diagnóstico de arranque.

4. **Resumen**:

  Revise las opciones seleccionadas y, a continuación, seleccione **Aceptar**.

La máquina virtual se implementa en el grupo de recursos de hello seleccionado.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Creación de una máquina virtual con una plantilla
Puede crear una máquina virtual mediante una de plantillas SAP de hello publicadas en hello [repositorio de GitHub de plantillas de inicio rápido de azure][azure-quickstart-templates-github]. También puede crear manualmente una máquina virtual mediante el uso de hello [portal de Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], o [CLI de Azure ][virtual-machines-linux-tutorial].

* [**Plantilla de configuración de dos niveles (solo una máquina virtual)** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]

  toocreate un sistema de dos niveles utilizando solo una máquina virtual, utilice esta plantilla.
* [**Plantilla de configuración de dos niveles (solo una máquina virtual): Managed Disks** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]

  toocreate un sistema de dos niveles con solo una máquina virtual y discos administrados, utilice esta plantilla.
* [**Plantilla de configuración de tres niveles (varias máquinas virtuales)** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]

  toocreate un sistema de tres niveles mediante el uso de varias máquinas virtuales, utilice esta plantilla.
* [**Plantilla de configuración de tres niveles (varias máquinas virtuales): Managed Disks** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]

  toocreate un sistema de tres niveles mediante el uso de varias máquinas virtuales y discos administrados, utilice esta plantilla.

Hola portal de Azure, escriba Hola parámetros de plantilla de hello siguientes:

1. **Aspectos básicos**:
  * **Suscripción**: plantilla de hello suscripción toouse toodeploy Hola.
  * **Grupo de recursos**: plantilla de hello recursos grupo toouse toodeploy Hola. Puede crear un nuevo grupo de recursos, o puede seleccionar un grupo de recursos existente en la suscripción de Hola.
  * **Ubicación**: donde toodeploy Hola plantilla. Si ha seleccionado un grupo de recursos existente, se utiliza la ubicación de Hola de ese grupo de recursos.

2. **Configuración**:
  * **Id. del sistema SAP**: Hola Id. de sistema de SAP (SID).
  * **Tipo de sistema operativo**: sistema operativo de Hola que desee toodeploy, por ejemplo, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2) y Oracle Linux 7.2.

    vista de lista de Hello no muestra que todos los sistemas operativos compatibles. Para más información acerca de los sistemas operativos compatibles para la implementación de software de SAP, consulte la nota de SAP [1928533].
  * **Tamaño del sistema SAP**: Hola tamaño de hello sistema SAP.

    número de Hola de nuevo sistema de SAPS Hola proporciona. Si no estás seguro de cuántos SAPS Hola sistema requiere, pregunte al socio de tecnología de SAP o integrador de sistema.
  * **Disponibilidad del sistema** (solo plantilla de tres niveles): Hola disponibilidad del sistema.

    Seleccione **HA** para una configuración en la que se puede realizar una instalación de alta disponibilidad. Se crean dos servidores de base de datos y dos servidores para ABAP SAP Central Services (ASCS).
  * **Tipo de almacenamiento** (solo plantilla de dos niveles): Hola tipo de almacenamiento toouse.

    En los sistemas grandes, se recomienda usar Azure Premium Storage. Para más información acerca de los tipos de almacenamiento, consulte estos recursos:
      * [Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194] (Uso de almacenamiento de SSD premium de Azure para la instancia de DBMS de SAP)
      * [Microsoft Azure Storage][dbms-guide-2.3] en [Implementación de DBMS de Azure Virtual Machines para SAP en NetWeaver][dbms-guide]
      * [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure][storage-premium-storage-preview-portal]
      * [Introducción tooMicrosoft almacenamiento de Azure][storage-introduction]
  * **Admin username** (Nombre de usuario de administrador) y **Admin password** (Contraseña de administrador): nombre de usuario y contraseña.
    Se crea un nuevo usuario, para iniciar sesión en la máquina virtual de toohello.
  * **New or existing subnet** (Subred nueva o existente): determina si es necesario crear una red virtual y una subred nuevas o si se debe usar una que ya exista. Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione **existente**.
  * **Id. de subred**: Id. de Hola de máquinas virtuales de hello subred Hola se conectará a. Seleccione subred Hola de su red privada virtual (VPN) o Azure ExpressRoute red virtual toouse tooconnect hello tooyour local red de máquina virtual. Id. de Hello normalmente se ve así: / Subscriptions /&lt;Id. de suscripción >/ResourceGroups /&lt;nombre del grupo de recursos > /providers/Microsoft.Network/virtualNetworks/&lt;nombre de red virtual > /subnets/&lt;nombre de subred >

3. **Términos y condiciones**:  
    Revise y acepte los términos legales Hola.

4.  Seleccione **Comprar**.

Hola agente de máquina virtual de Azure se implementa de forma predeterminada cuando se usa una imagen de hello Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Configuración de los valores de proxy
Según cómo esté configurada su red local, tendrá que tooset el proxy de hello en su máquina virtual. Si la máquina virtual está conectado tooyour red de local a través de VPN o ExpressRoute, Hola VM podría no ser capaz de tooaccess Hola Internet y no ser capaz de toodownload extensiones de hello necesario o recopilar datos de supervisión. Para obtener más información, consulte [configurar el proxy de hello][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Unión a un dominio (solo Windows)
Si la implementación de Azure es la instancia de Active Directory o DNS de local de tooan conectado a través de una conexión de VPN de sitio a sitio de Azure o ExpressRoute (Esto se denomina *entre entornos* en [planificación de máquinas virtuales de Azure y la implementación de SAP NetWeaver][planning-guide]), se espera que Hola VM se une a un dominio local. Para obtener más información acerca de las consideraciones para esta tarea, vea [unirse a un dominio local de tooan de máquina virtual (solo Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configuración de la supervisión
toobe seguro SAP admite configure Hola extensión de supervisión de Azure para SAP como se describe en su entorno [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5]. Comprobar los requisitos previos de hello para la supervisión de SAP y las versiones mínimas necesarias del Kernel de SAP y agente de Host de SAP, en recursos de hello enumerados en [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Comprobación de la supervisión
Compruebe si la supervisión funciona según lo descrito en [Comprobaciones y solución de problemas de configuración de la supervisión de extremo a extremo][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Pasos posteriores a la implementación
Después de crear VM de Hola y Hola máquina virtual se implementa, es necesario tooinstall Hola requiere componentes de software Hola VM. Debido a la secuencia de instalación de software/implementación hello en este tipo de implementación de máquina virtual, ya debe estar disponible, ya sea en Azure, en otra máquina virtual, o como un disco que se pueden adjuntar hello toobe de software instalado. O bien, considere la posibilidad de usar un escenario entre entornos, en qué conectividad toohello locales activos (recursos compartidos de instalación) recibe.

Después de implementar la VM en Azure, siga Hola mismo instrucciones y herramientas tooinstall Hola software SAP en su máquina virtual como se haría en un entorno local. tooinstall software SAP en una máquina virtual de Azure, tanto SAP y Microsoft recomiendan cargar y almacenar los medios de instalación de SAP de hello en discos duros virtuales de Azure o discos administrados o que cree una VM de Azure que funciona como un servidor de archivos que tiene todos los Hola requiere los medios de instalación de SAP.

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Escenario 2: Implementación de una máquina virtual con una imagen personalizada para SAP
Dado que diferentes versiones de un sistema operativo o DBMS tienen requisitos de revisión diferentes, imágenes de Hola que encuentre en hello Azure Marketplace podrían no cumplir sus necesidades. En su lugar, conviene toocreate una máquina virtual usando su propia imagen de VM de SO o DBMS, que puede implementar de nuevo más tarde.
Usar pasos diferentes toocreate una imagen privada para Linux que toocreate para Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> tooprepare una imagen de Windows que puede usar toodeploy varias máquinas virtuales, configuración de Windows hello (como SID de Windows y el nombre de host) se debe resumir o generalizado en hello VM en local. Puede usar [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo esto.
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare una imagen de Linux que se puede usar toodeploy en varias máquinas virtuales, algunos valores de configuración de Linux deben ser hello como abstracto o generalizado en máquina virtual local. Puede usar `waagent -deprovision` toodo esto. Para obtener más información, consulte [capturar una máquina virtual de Linux con Azure] [ virtual-machines-linux-capture-image] hello y [Guía de usuario del agente de Linux de Azure][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Puede preparar y crear una imagen personalizada y, a continuación, utilizarlo toocreate varias nuevas máquinas virtuales. Esto se describe en [Planeación e implementación de Azure Virtual Machines para SAP en NetWeaver][planning-guide]. Configurar la base de datos de contenido mediante el Administrador de aprovisionamiento de Software de SAP tooinstall un nuevo sistema SAP (restaura una copia de seguridad de base de datos desde un disco que está adjunto toohello virtual machine) o directamente restaurando una copia de seguridad de base de datos del almacenamiento de Azure, si el DBMS lo admite. Para más información, consulte [Implementación de DBMS de Azure Virtual Machines para SAP en NetWeaver][dbms-guide]. Si ya ha instalado un sistema SAP en la VM local (especialmente para los sistemas de dos niveles), puede adaptar la configuración del sistema SAP Hola después de la implementación de Hola de hello Azure VM mediante el procedimiento de cambiar el nombre de sistema de hello admitido aprovisionamiento de Software de SAP Administrador (Nota de SAP [1619720]). En caso contrario, puede instalar el software SAP Hola después de implementar Hola VM de Azure.

Hello diagrama de flujo siguiente muestra hello específico de SAP secuencia de pasos para implementar una máquina virtual desde una imagen personalizada:

![Diagrama de flujo de la implementación de máquinas virtuales para sistemas SAP con una imagen de máquina virtual de Marketplace privado][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Crear una máquina virtual mediante Hola portal de Azure
toocreate de manera más fácil de Hello una nueva máquina virtual desde una imagen de disco administrado consiste en usar Hola portal de Azure. Para obtener más información sobre cómo toocreate una imagen de disco administrar, leer [capturar una imagen administrada de una VM generalizada en Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)

1.  Vaya demasiado<https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>. O bien, en hello Azure menús del portal, seleccione **imágenes**.
2.  Imagen de disco administrado de hello seleccione desea toodeploy y haga clic en **crear VM**

Hola asistente le guía a través de configuración de máquina virtual de hello requiere parámetros toocreate hello, además tooall necesario que los recursos, como interfaces de red y cuentas de almacenamiento. Algunos de estos parámetros son:

1. **Aspectos básicos**:
 * **Nombre**: nombre de hello del recurso de hello (nombre de máquina virtual de hello).
 * **Tipo de disco de máquina virtual**: seleccione el tipo de disco de hello del disco de SO Hola. Si desea toouse almacenamiento Premium para los discos de datos, se recomienda usar almacenamiento Premium para el disco del sistema operativo Hola así.
 * **Nombre de usuario y la contraseña** o **clave pública SSH**: escriba Hola nombre de usuario y contraseña de usuario de Hola que se crea durante el aprovisionamiento de Hola. Para una máquina virtual de Linux, puede escribir la clave de Shell seguro (SSH) pública Hola que usas toosign en toohello máquina.
 * **Suscripción**: seleccione suscripción Hola que desea toouse tooprovision Hola máquina virtual.
 * **Grupo de recursos**: nombre de Hola Hola del grupo de recursos para hello máquina virtual. Puede escribir cualquier nombre de Hola de un nombre nuevo de Hola o grupo de recursos de un grupo de recursos que ya existe.
 * **Ubicación**: donde toodeploy Hola nueva máquina virtual. Si desea que la red local de tooconnect Hola máquina virtual tooyour, asegúrese de que seleccionar ubicación de Hola de Hola de red virtual que se conecta la red local de Azure tooyour. Para más información, vea [Redes de Microsoft Azure][planning-guide-microsoft-azure-networking] en [Planeación e implementación de Azure Virtual Machines para SAP en NetWeaver][planning-guide].
2. **Tamaño**:

     Lea la nota de SAP [1928533] para ver una lista de los tipos de máquinas virtuales que se admiten. Asegúrese de que seleccionar el tipo correcto de VM de hello si desea toouse almacenamiento Premium de Azure. No todos los tipos de VM son compatibles con el Almacenamiento premium. Para más información, consulte [Almacenamiento: Microsoft Azure Storage y discos de datos][planning-guide-storage-microsoft-azure-storage-and-data-disks] y [Azure Premium Storage][planning-guide-azure-premium-storage] en [Planeación e implementación de Azure Virtual Machines para SAP en NetWeaver][planning-guide].

3. **Configuración**:
  * **Almacenamiento**
    * **Tipo de disco**: seleccione el tipo de disco de hello del disco de SO Hola. Si desea toouse almacenamiento Premium para los discos de datos, se recomienda usar almacenamiento Premium para el disco del sistema operativo Hola así.
    * **Usar discos administrados**: si desea toouse administrar discos, seleccione Sí. Para obtener más información acerca de los discos administrados, consulte el capítulo [discos administrados] [ planning-guide-managed-disks] en la Guía de planificación de Hola.
  * **Red**
    * **Red virtual** y **subred**: toointegrate Hola virtual machine con la intranet, la red virtual seleccione Hola que es la red local de tooyour conectado.
    * **Dirección IP pública**: seleccione Hola dirección IP pública que se desea toouse, o especifica parámetros toocreate una nueva dirección IP pública. Puede usar la máquina virtual de un tooaccess de dirección IP pública a través de Internet de Hola. Asegúrese de que también crea una máquina red seguridad grupo toohelp un acceso seguro tooyour virtual.
    * **Grupo de seguridad de red**: para más información, consulte [Control del flujo de tráfico de red con grupos de seguridad de red][virtual-networks-nsg].
  * **Extensiones**: puede instalar extensiones de máquina virtual mediante la adición de implementación de toohello. No es necesario extensión tooadd en este paso. las extensiones de Hello necesarias para la compatibilidad con SAP se instalan más adelante. Consulte el capítulo [configurar hello Azure extensión de supervisión mejorada para SAP] [ deployment-guide-4.5] en esta guía.
  * **Alta disponibilidad**: seleccione un conjunto de disponibilidad o escriba Hola parámetros toocreate la disponibilidad de un nuevo conjunto. Consulte [Conjuntos de disponibilidad de Azure][planning-guide-3.2.3] para más información.
  * **Supervisión**
    * **Diagnósticos de arranque**: puede seleccionar **Deshabilitar** para el diagnóstico de arranque.
    * **Diagnósticos del SO invitado**: puede seleccionar **Deshabilitar** para el diagnóstico de arranque.

4. **Resumen**:

  Revise las opciones seleccionadas y, a continuación, seleccione **Aceptar**.

La máquina virtual se implementa en el grupo de recursos de hello seleccionado.
#### <a name="create-a-virtual-machine-by-using-a-template"></a>Creación de una máquina virtual con una plantilla
toocreate una implementación mediante el uso de una imagen de sistema operativo privada de hello portal de Azure, use uno de hello siguiendo las plantillas SAP. Estas plantillas se publican en hello [repositorio de GitHub de plantillas de inicio rápido de azure][azure-quickstart-templates-github]. También puede crear una máquina virtual manualmente con [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Plantilla de configuración de dos niveles (solo una máquina virtual)** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]

  toocreate un sistema de dos niveles utilizando solo una máquina virtual, utilice esta plantilla.
* [**Plantilla de configuración de dos niveles (solo una máquina virtual): imagen de Managed Disks** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]

  toocreate un sistema de dos niveles con solo una máquina virtual y una imagen de disco administrado, utilice esta plantilla.
* [**Plantilla de configuración de tres niveles (varias máquinas virtuales)** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]

  toocreate un sistema de tres niveles mediante varias máquinas virtuales o su propia imagen de sistema operativo, use esta plantilla.
* [**Plantilla de configuración de tres niveles (varias máquinas virtuales): imagen de Managed Disks** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]

  toocreate un sistema de tres niveles mediante varias máquinas virtuales o su propia imagen de sistema operativo y una imagen de disco administrado, utilice esta plantilla.

Hola portal de Azure, escriba Hola parámetros de plantilla de hello siguientes:

1. **Aspectos básicos**:
  * **Suscripción**: plantilla de hello suscripción toouse toodeploy Hola.
  * **Grupo de recursos**: plantilla de hello recursos grupo toouse toodeploy Hola. Puede crear un nuevo grupo de recursos o seleccione un grupo de recursos existente en la suscripción de Hola.
  * **Ubicación**: donde toodeploy Hola plantilla. Si ha seleccionado un grupo de recursos existente, se utiliza la ubicación de Hola de ese grupo de recursos.
2. **Configuración**:
  * **Id. del sistema SAP**: Hola identificador del sistema de SAP.
  * **Tipo de sistema operativo**: Hola tipo de sistema operativo que desee toodeploy (Windows o Linux).
  * **Tamaño del sistema SAP**: Hola tamaño de hello sistema SAP.

    número de Hola de nuevo sistema de SAPS Hola proporciona. Si no estás seguro de cuántos SAPS Hola sistema requiere, pregunte al socio de tecnología de SAP o integrador de sistema.
  * **Disponibilidad del sistema** (solo plantilla de tres niveles): Hola disponibilidad del sistema.

    Seleccione **HA** para una configuración en la que se puede realizar una instalación de alta disponibilidad. Se crean dos servidores de base de datos y dos servidores para ASCS.
  * **Tipo de almacenamiento** (solo plantilla de dos niveles): Hola tipo de almacenamiento toouse.

    En los sistemas grandes, se recomienda usar Azure Premium Storage. Para obtener más información acerca de los tipos de almacenamiento, vea Hola recursos siguientes:
      * [Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194] (Uso de almacenamiento de SSD premium de Azure para la instancia de DBMS de SAP)
      * [Microsoft Azure Storage][dbms-guide-2.3] en [Implementación de DBMS de Azure Virtual Machines para SAP en NetWeaver][dbms-guide]
      * [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure][storage-premium-storage-preview-portal]
      * [Introducción tooMicrosoft almacenamiento de Azure][storage-introduction]
  * **Imagen de usuario de URI de VHD** (solo plantilla de imagen de disco no administrado): Hola URI de imagen del SO privada Hola VHD como, por ejemplo, https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Cuenta de almacenamiento de imagen de usuario** (solo plantilla de imagen de disco no administrado): nombre de Hola de cuenta de almacenamiento de Hola donde se almacena imagen del sistema operativo privada hello, por ejemplo, &lt;accountname > en https://&lt;accountname >. BLOB.Core.Windows.NET/vhds/userimage.vhd.
  * **userImageId** (solo plantilla de imagen de disco administrado): Id. de imagen de disco administrado que desee toouse hello
  * **Nombre de usuario administrador** y **contraseña de administrador**: Hola username y password.

    Se crea un nuevo usuario, para iniciar sesión en la máquina virtual de toohello.
  * **New or existing subnet** (Subred nueva o existente): determina si es necesario crear una red virtual y una subred nuevas o si se debe usar una que ya exista. Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione **existente**.
  * **Id. de subred**: Id. de Hola de máquinas virtuales de hello subred toowhich Hola se conectará a. Seleccione la subred de hello de la VPN o ExpressRoute red virtual toouse tooconnect Hola máquina virtual tooyour en red local. Id. de Hello normalmente este aspecto:

    /subscriptions/&lt;id. de suscripción>/resourceGroups/&lt;nombre del grupo de recursos>/providers/Microsoft.Network/virtualNetworks/&lt;nombre de red virtual>/subnets/&lt;nombre de subred>

3. **Términos y condiciones**:  
    Revise y acepte los términos legales Hola.

4.  Seleccione **Comprar**.

#### <a name="install-hello-vm-agent-linux-only"></a>Instalar Hola agente de máquina virtual (solamente para Linux)
plantillas de hello toouse que se describe en la sección anterior de hello, Hola que ya se debe instalar el agente de Linux en la imagen de usuario de Hola o implementación de Hola se producirá un error. Descargue e instale Hola agente de máquina virtual en la imagen de usuario de hello tal y como se describe en [descargar, instalar y habilitar hello Azure VM Agent][deployment-guide-4.4]. Si no usa plantillas de hello, también puede instalar más adelante Hola agente de máquina virtual.

#### <a name="join-a-domain-windows-only"></a>Unión a un dominio (solo Windows)
Si la implementación de Azure es la instancia de Active Directory o DNS de local de tooan conectado a través de una conexión de VPN de sitio a sitio de Azure o ExpressRoute de Azure (Esto se denomina *entre entornos* en [máquinas virtuales de Azure planificación e implementación para SAP NetWeaver][planning-guide]), se espera que Hola VM se une a un dominio local. Para obtener más información acerca de las consideraciones para este paso, consulte [unirse a un dominio local de tooan de máquina virtual (solo Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configuración de los valores de proxy
Según cómo esté configurada su red local, tendrá que tooset el proxy de hello en su máquina virtual. Si la máquina virtual está conectado tooyour red de local a través de VPN o ExpressRoute, Hola VM podría no ser capaz de tooaccess Hola Internet y no ser capaz de toodownload extensiones de hello necesario o recopilar datos de supervisión. Para obtener más información, consulte [configurar el proxy de hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configuración de la supervisión
toobe seguro SAP admite configure Hola extensión de supervisión de Azure para SAP como se describe en su entorno [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5]. Comprobar los requisitos previos de hello para la supervisión de SAP y las versiones mínimas necesarias del Kernel de SAP y agente de Host de SAP, en recursos de hello enumerados en [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Comprobación de la supervisión
Compruebe si la supervisión funciona según lo descrito en [Comprobaciones y solución de problemas de configuración de la supervisión de extremo a extremo][deployment-guide-troubleshooting-chapter].


### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Escenario 3: Traslado de una máquina virtual local con un VHD no generalizado de Azure con SAP
En este escenario, puede planear toomove un sistema SAP específico desde una tooAzure del entorno local. Puede hacerlo mediante la carga de hello disco duro virtual que tiene Hola OS, archivos binarios SAP de hello, y finalmente Hola archivos binarios DBMS, además de hello discos duros virtuales con datos de Hola y archivos de registro de hello DBMS, tooAzure. A diferencia del escenario de Hola se describe en [escenario 2: implementar una máquina virtual con una imagen personalizada para SAP][deployment-guide-3.3], en este caso, mantener el nombre de host de hello, SID de SAP, y las cuentas de usuario SAP en hello Azure VM, porque estaban configurado en el entorno local de Hola. No es necesario toogeneralize Hola SO. Este escenario aplica a escenarios de toocross locales con mayor frecuencia donde una parte de hello panorama SAP ejecuta en local y una parte del mismo se ejecuta en Azure.

En este escenario, hello agente de máquina virtual es **no** instala automáticamente durante la implementación. Dado que hello Azure extensión de supervisión mejorada para SAP y agente de máquina virtual de hello son necesario toorun SAP NetWeaver en Azure, necesita ambos toodownload, instalar y habilitar componentes manualmente después de crear máquinas virtuales de Hola.

Para obtener más información acerca de hello agente de máquina virtual de Azure, vea Hola recursos siguientes.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Información general del agente de máquina virtual de Azure][virtual-machines-windows-agent-user-guide]
>
> ![Linux][Logo_Linux] Linux
>
> [Guía de usuario del agente de Linux de Azure][virtual-machines-linux-agent-user-guide]
>
>

- - -

Hola sigue diagrama de flujo muestra hello secuencia de pasos para mover una máquina virtual local mediante el uso de un VHD de Azure no generalizado:

![Diagrama de flujo de la implementación de máquinas virtuales para sistemas SAP mediante un disco de máquina virtual][deployment-guide-figure-400]

Si el disco de hello ya está cargado y definido en Azure (consulte [máquinas virtuales de Azure planificación e implementación para SAP NetWeaver][planning-guide]), realice las tareas de Hola se describen en hello junto secciones.

#### <a name="create-a-virtual-machine"></a>de una máquina virtual
toocreate una implementación con un disco de sistema operativo privado a través de hello portal de Azure, use la plantilla SAP de hello publicada en hello [repositorio de GitHub de plantillas de inicio rápido de azure][azure-quickstart-templates-github]. También puede crear una máquina virtual manualmente con PowerShell.

* [**Plantilla de configuración de dos niveles (solo una máquina virtual)** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]

  toocreate un sistema de dos niveles utilizando solo una máquina virtual, utilice esta plantilla.
* [**Plantilla de configuración de dos niveles (solo una máquina virtual): Managed Disks** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]

  toocreate un sistema de dos niveles con solo una máquina virtual y un disco administrado, utilice esta plantilla.

Hola portal de Azure, escriba Hola parámetros de plantilla de hello siguientes:

1. **Aspectos básicos**:
  * **Suscripción**: plantilla de hello suscripción toouse toodeploy Hola.
  * **Grupo de recursos**: plantilla de hello recursos grupo toouse toodeploy Hola. Puede crear un nuevo grupo de recursos o seleccione un grupo de recursos existente en la suscripción de Hola.
  * **Ubicación**: donde toodeploy Hola plantilla. Si ha seleccionado un grupo de recursos existente, se utiliza la ubicación de Hola de ese grupo de recursos.
2. **Configuración**:
  * **Id. del sistema SAP**: Hola identificador del sistema de SAP.
  * **Tipo de sistema operativo**: Hola tipo de sistema operativo que desee toodeploy (Windows o Linux).
  * **Tamaño del sistema SAP**: Hola tamaño de hello sistema SAP.

    número de Hola de nuevo sistema de SAPS Hola proporciona. Si no estás seguro de cuántos SAPS Hola sistema requiere, pregunte al socio de tecnología de SAP o integrador de sistema.
  * **Tipo de almacenamiento** (solo plantilla de dos niveles): Hola tipo de almacenamiento toouse.

    En los sistemas grandes, se recomienda usar Azure Premium Storage. Para obtener más información acerca de los tipos de almacenamiento, vea Hola recursos siguientes:
      * [Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194] (Uso de almacenamiento de SSD premium de Azure para la instancia de DBMS de SAP)
      * [Microsoft Azure Storage][dbms-guide-2.3] en [Implementación de DBMS de Azure Virtual Machines para SAP en NetWeaver][dbms-guide]
      * [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure][storage-premium-storage-preview-portal]
      * [Introducción tooMicrosoft almacenamiento de Azure][storage-introduction]
  * **URI de VHD de disco del sistema operativo** (solo plantilla de disco no administrado): Hola URI de disco de SO de privada de hello, por ejemplo, https://&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Identificador de disco administrado de disco del sistema operativo** (solo plantilla de disco administrado): Hola Id. de disco del sistema operativo de disco administrado hello, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN
  * **New or existing subnet** (Subred nueva o existente): determina si es necesario crear una red virtual y una subred nuevas o si se debe usar una que ya exista. Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione **existente**.
  * **Id. de subred**: Id. de Hola de máquinas virtuales de hello subred toowhich Hola se conectará a. Seleccione la subred de hello de la VPN o Azure ExpressRoute red virtual toouse tooconnect Hola máquina virtual tooyour en red local. Id. de Hello normalmente este aspecto:

    /subscriptions/&lt;id. de suscripción>/resourceGroups/&lt;nombre del grupo de recursos>/providers/Microsoft.Network/virtualNetworks/&lt;nombre de red virtual>/subnets/&lt;nombre de subred>

3. **Términos y condiciones**:  
    Revise y acepte los términos legales Hola.

4.  Seleccione **Comprar**.

#### <a name="install-hello-vm-agent"></a>Instalar agente de máquina virtual de Hola
Hola de hello toouse plantillas se describen en la sección anterior, hello agente de máquina virtual debe instalarse en el disco de SO de Hola o se producirá un error en la implementación de Hola. Descargue e instale Hola agente de máquina virtual en Hola de máquina virtual, como se describe en [descargar, instalar y habilitar hello Azure VM Agent][deployment-guide-4.4].

Si no usa plantillas de Hola que se describe en la sección anterior de hello, también puede instalar posteriormente Hola agente de máquina virtual.

#### <a name="join-a-domain-windows-only"></a>Unión a un dominio (solo Windows)
Si la implementación de Azure es la instancia de Active Directory o DNS de local de tooan conectado a través de una conexión de VPN de sitio a sitio de Azure o ExpressRoute (Esto se denomina *entre entornos* en [planificación de máquinas virtuales de Azure y la implementación de SAP NetWeaver][planning-guide]), se espera que Hola VM se une a un dominio local. Para obtener más información acerca de las consideraciones para esta tarea, vea [unirse a un dominio local de tooan de máquina virtual (solo Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configuración de los valores de proxy
Según cómo esté configurada su red local, tendrá que tooset el proxy de hello en su máquina virtual. Si la máquina virtual está conectado tooyour red de local a través de VPN o ExpressRoute, Hola VM podría no ser capaz de tooaccess Hola Internet y no ser capaz de toodownload extensiones de hello necesario o recopilar datos de supervisión. Para obtener más información, consulte [configurar el proxy de hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configuración de la supervisión
toobe seguro SAP admite configure Hola extensión de supervisión de Azure para SAP como se describe en su entorno [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5]. Comprobar los requisitos previos de hello para la supervisión de SAP y las versiones mínimas necesarias del Kernel de SAP y agente de Host de SAP, en recursos de hello enumerados en [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Comprobación de la supervisión
Compruebe si la supervisión funciona según lo descrito en [Comprobaciones y solución de problemas de configuración de la supervisión de extremo a extremo][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Actualizar configuración de supervisión de Hola para SAP
Actualizar configuración de supervisión de SAP de hello en cualquiera de hello los escenarios siguientes:
* equipo de Microsoft/SAP conjunto Hola extiende las capacidades de supervisión de Hola y solicita los contadores más o menos.
* Microsoft presenta una nueva versión de hello infraestructura subyacente de Azure que entrega los datos de supervisión de Hola y Hola extensión de supervisión mejorada de Azure para SAP necesidades toobe adaptar toothose cambios.
* Montar los discos de datos adicionales tooyour máquina virtual de Azure o se quita un disco de datos. En este escenario, actualizar la colección de Hola de datos relacionados con el almacenamiento. Cambiar la configuración mediante la adición o eliminación de puntos de conexión o mediante la asignación de IP direcciones tooa VM no afecta a configuración de supervisión de Hola.
* Cambia Hola tamaño de la máquina virtual de Azure, por ejemplo, de tamaño A5 tooany otro tamaño de máquina virtual.
* Agregar nueva tooyour de interfaces de red virtual de Azure.

tooupdate supervisión de configuración, Hola de actualización de supervisión de la infraestructura por hello siguiendo los pasos de [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment"></a>Tareas detalladas para la implementación de software de SAP
En esta sección se detallan los pasos para realizar tareas específicas en proceso de configuración e implementación de Hola.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Implementación de cmdlets de Azure PowerShell
1.  Vaya demasiado[descargas de Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  En **Herramientas de línea de comandos**, en **PowerShell**, seleccione **Instalación para Windows**.
3.  En el cuadro de diálogo Administrador de descargas de Microsoft hello, Hola Descargar archivo (por ejemplo, WindowsAzurePowershellGet.3f.3f.3fnew.exe), seleccione **ejecutar**.
4.  Seleccione toorun Microsoft Web Platform Installer (instalador de plataforma Web de Microsoft,) **Sí**.
5.  Se muestra una página como la siguiente:

  ![Página de instalación de cmdlets de Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Seleccione **instalar**y, a continuación, acepte los términos de licencia del Software de Microsoft de Hola.
7.  PowerShell se instala. Seleccione **finalizar** Asistente para la instalación de tooclose Hola.

Compruebe con frecuencia actualizaciones toohello cmdlets de PowerShell, que normalmente se actualiza mensualmente. Hola toocheck de manera más sencilla para las actualizaciones es hello toodo pasos de instalación, página de instalación de toohello que se muestra en el paso 5 anteriores. número de fecha y la versión de lanzamiento de Hola de cmdlets de Hola se incluye en la página de Hola que se muestra en el paso 5. A menos que se indique lo contrario en la nota de SAP [1928533] o nota de SAP [2015553], recomendamos que trabaje con la versión más reciente de Hola de cmdlets de PowerShell de Azure.

versión de hello toocheck de hello cmdlets de PowerShell de Azure que están instalados en el equipo, ejecute este comando de PowerShell:
```powershell
(Get-Module AzureRm.Compute).Version
```
resultado de Hello tiene el siguiente aspecto:

![Resultado de la comprobación de versión de los cmdlets de Azure PowerShell][deployment-guide-figure-600]
<a name="figure-6"></a>

Si Hola cmdlet de Azure versión instalada en el equipo es actual hello, primera página del Asistente para instalación de Hola de Hola indica mediante la adición de **(instalado)** toohello título del producto (consulte la siguiente captura de pantalla de hello). Los cmdlets de Azure PowerShell están actualizados. Asistente de instalación de hello tooclose, seleccione **Exit**.

![Página de instalación de cmdlets de PowerShell de Azure que indica que la versión más reciente Hola de cmdlets de PowerShell de Azure están instalados][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Implementación de la CLI de Azure
1.  Vaya demasiado[descargas de Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  En **herramientas de línea de comandos**, en **interfaz de línea de comandos de Azure**, seleccione hello **instalar** vínculo para su sistema operativo.
3.  En el cuadro de diálogo Administrador de descargas de Microsoft hello, Hola Descargar archivo (por ejemplo, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), seleccione **ejecutar**.
4.  Seleccione toorun Microsoft Web Platform Installer (instalador de plataforma Web de Microsoft,) **Sí**.
5.  Se muestra una página como la siguiente:

  ![Página de instalación de cmdlets de Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Seleccione **instalar**y, a continuación, acepte los términos de licencia del Software de Microsoft de Hola.
7.  La CLI de Azure está instalada. Seleccione **finalizar** Asistente para la instalación de tooclose Hola.

Comprobar frecuentemente si hay actualizaciones tooAzure CLI, que normalmente se actualiza mensualmente. Hola toocheck de manera más sencilla para las actualizaciones es hello toodo pasos de instalación, página de instalación de toohello que se muestra en el paso 5 anteriores.

versión de hello toocheck de CLI de Azure que está instalado en el equipo, ejecute este comando:
```
azure --version
```

resultado de Hello tiene el siguiente aspecto:

![Resultado de la comprobación de versión de CLI de Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Unirse a un dominio local de tooan VM (sólo Windows)
Si implementa máquinas virtuales de SAP en un escenario entre entornos, donde se han ampliado en local de Active Directory y DNS en Azure, se espera que las máquinas virtuales de hello va a unir a un dominio local. Hola pasos detallados tomar toojoin un dominio local de tooan VM y hello toobe software adicional necesario un miembro de un dominio local, varía en función del cliente. Por lo general, toojoin un tooan VM dominio local, es necesario software adicional de tooinstall, como software antimalware y copia de seguridad o software de supervisión.

En este escenario, también deberá toomake seguro de que si se fuerza la configuración de proxy de Internet cuando una máquina virtual une a un dominio en su entorno, Windows hello tiene cuenta de sistema Local (S-1-5-18) en la máquina virtual invitada Hola Hola misma configuración de proxy. opción más sencilla de Hello es proxy de hello tooforce mediante el uso de un dominio de la directiva de grupo, que se aplica toosystems en dominio Hola.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Descargar, instalar y habilitar Hola agente de máquina virtual de Azure
Para máquinas virtuales que se implementan a partir de una imagen de sistema operativo que no se ha generalizado (por ejemplo, una imagen que no se origina en la herramienta de preparación del sistema de Windows o sysprep, hello), necesitará toomanually descarga, instalación y Hola habilitar agente de máquina virtual de Azure.

Si implementa una máquina virtual desde hello Azure Marketplace, este paso no es necesario. Imágenes de hello Azure Marketplace ya tienen Hola agente de máquina virtual de Azure.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Descargar Hola agente de máquina virtual de Azure:
  1.  Descargar hello [paquete del instalador de agente de máquina virtual de Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Almacenar un paquete MSI de agente de VM Hola localmente en un servidor o equipo personal.
2.  Instalar Hola agente de máquina virtual de Azure:
  1.  Conectar toohello implementa la máquina virtual de Azure mediante el protocolo de escritorio remoto (RDP).
  2.  Abra una ventana del explorador de Windows hello VM y un directorio de destino Hola select para el archivo MSI de hello de hello agente de máquina virtual.
  3.  Arrastre el archivo de MSI del instalador de agente de VM de Azure de Hola desde el directorio de destino de toohello equipo local/servidor de agente de máquina virtual de hello en hello VM.
  4.  Haga doble clic en el archivo MSI de hello en hello máquina virtual.
3.  Para máquinas virtuales que son dominios locales tooon combinadas, asegúrese de que su posible configuración de proxy de Internet también aplica toohello cuenta de sistema Local de Windows (S-1-5-18) Hola de máquina virtual, tal y como se describe en [configurar el proxy de hello] [ deployment-guide-configure-proxy]. Hola agente de máquina virtual se ejecuta en este contexto y necesita toobe tooconnect capaz de tooAzure.

Interacción del usuario no es necesario tooupdate Hola agente de máquina virtual de Azure. Hola agente de máquina virtual se actualiza automáticamente y no requiere un reinicio de máquina virtual.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Usar hello sigue comandos tooinstall Hola agente de máquina virtual para Linux:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL) u Oracle Linux**

  ```
  sudo yum install WALinuxAgent
  ```

Si ya está instalado el agente de hello, hello tooupdate agente Linux de Azure, Hola pasos descritos en [Hola actualización agente Linux de Azure en una versión más reciente de máquina virtual toohello desde GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configurar el proxy de Hola
pasos de Hola que seguir a tooconfigure proxy de hello en Windows son diferentes de manera Hola que configurar a proxy hello en Linux.

#### <a name="windows"></a>Windows
Configuración de proxy debe estar configurada correctamente para hello tooaccess Hola Internet cuenta del sistema Local. Si la configuración de proxy no se establece con directiva de grupo, puede configurar Hola para hello cuenta de sistema Local.

1. Vaya demasiado**iniciar**, escriba **gpedit.msc**y, a continuación, seleccione **ENTRAR**.
2. Seleccione **Configuración del equipo** > **Plantillas administrativas** > **Componentes de Windows** > **Internet Explorer**. Asegúrese de que esa configuración hello **hacer proxy configuración por equipo (en lugar de por usuario)** está deshabilitado o no configurado.
3. En **el Panel de Control**, vaya demasiado**centro de redes y recursos compartidos** > **opciones de Internet**.
4. En hello **conexiones** ficha, seleccione hello **configuración de LAN** botón.
5. Desactive hello **detectar automáticamente la configuración** casilla de verificación.
6. Seleccione hello **utilizar un servidor proxy para su LAN** casilla de verificación y, a continuación, escriba la dirección de proxy de Hola y el puerto.
7. Seleccione hello **avanzadas** botón.
8. Hola **excepciones** cuadro, escriba la dirección IP de hello **168.63.129.16**. Seleccione **Aceptar**.

#### <a name="linux"></a>Linux
Configurar el proxy correcto de hello en archivo de configuración de Hola de hello agente invitado de Azure de Microsoft, que se encuentra en \\etcetera\\waagent.conf.

Hola de conjunto de parámetros siguientes:

1.  **HTTP proxy host** (Host de proxy HTTP). Por ejemplo, establecer demasiado**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **HTTP proxy port** (Puerto de proxy HTTP). Por ejemplo, establecer demasiado**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Reinicie el agente de Hola.

  ```
  sudo service waagent restart
  ```

Hola configuración del proxy en \\etcetera\\waagent.conf también se aplican las extensiones de VM de toohello necesario. Si desea que toouse Hola repositorios de Azure, asegúrese de que los repositorios de hello tráfico toothese no va a través de la intranet local. Si se creó definido por el usuario tooenable rutas tunelización forzada, asegúrese de que agrega una ruta que enruta los repositorios de tráfico toohello directamente toohello Internet y no a través de la conexión VPN de sitio a sitio.

* **SLES**

  También necesita tooadd rutas para direcciones IP de Hola se enumeran en \\etcetera\\regionserverclnt.cfg. Hello en la ilustración siguiente se muestra un ejemplo:

  ![Tunelización forzada][deployment-guide-figure-50]


* **RHEL**

  También necesita tooadd rutas para las direcciones IP de los hosts de Hola Hola se enumeran en \\etcetera\\yum.repos.d\\rhui equilibradores de carga. Para obtener un ejemplo, vea Hola anterior figura.

* **Oracle Linux**

  No hay ningún repositorio para Oracle Linux en Azure. Necesita tooconfigure sus propios repositorios para Oracle Linux o usar repositorios públicos Hola.

Para más información sobre las rutas definidas por el usuario, consulte [Rutas definidas por el usuario y reenvío IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configurar hello Azure extensión de supervisión mejorada para SAP
Si ha preparado Hola VM como se describe en [escenarios de implementación de máquinas virtuales para SAP en Azure][deployment-guide-3], hello Azure VM Agent esté instalado en la máquina virtual de Hola. Hola siguiente paso es toodeploy hello Azure extensión de supervisión mejorada para SAP, que está disponible en hello repositorio de extensión de Azure en centros de datos Azure Hola global. Para más información, consulte [Planeación e implementación de Azure Virtual Machines para SAP en NetWeaver][planning-guide-9.1].

Puede usar tooinstall PowerShell o CLI de Azure y configurar hello Azure extensión de supervisión mejorada para SAP. extensión de hello tooinstall en una VM Windows o Linux mediante el uso de un equipo Windows, vea [Azure PowerShell][deployment-guide-4.5.1]. extensión de hello tooinstall en una VM de Linux mediante el uso de un escritorio de Linux, consulte [CLI de Azure][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell para máquinas virtuales Linux y con Windows
tooinstall hello Azure extensión de supervisión mejorada para SAP mediante el uso de PowerShell:

1. Asegúrese de que ha instalado la versión más reciente de Hola Hola Azure del cmdlet de PowerShell. Para más información, consulte [Implementación de cmdlets de Azure PowerShell][deployment-guide-4.1].  
2. Ejecute hello siguiente cmdlet de PowerShell.
    Para ver la lista de entornos disponibles, ejecute `commandlet Get-AzureRmEnvironment`. Si desea que toouse global Azure, el entorno es **nube de Azure**. Si desea usar Azure en China, seleccione **AzureChinaCloud**.

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of hello environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

Después de escribir los datos de cuenta e identificar Hola máquina virtual de Azure, script de Hola implementa extensiones de hello necesaria y permite ofrecer características de hello necesario. Esto puede tardar varios minutos.
Para más información acerca de `Set-AzureRmVMAEMExtension`, consulte [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![Ejecución correcta del cmdlet de Azure específico de SAP Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Hola `Set-AzureRmVMAEMExtension` hace configuración todos Hola pasos tooconfigure de supervisión de host para SAP.

salida del script de Hola incluye Hola siguiente información:

* Confirmación de que se haya configurado un supervisión para el disco de SO de Hola y todos los discos de datos adicionales.
* a continuación dos mensajes de Hola para confirmar la configuración de Hola de las métricas de almacenamiento para una cuenta de almacenamiento específico.
* Una línea de salida proporciona el estado de Hola de actualización en Sí Hola de configuración de supervisión de Hola.
* Otra línea de salida se confirma que la configuración de Hola se ha implementado o actualizado.
* Hola última línea de salida es informativa. Muestra las opciones de configuración de supervisión de hello pruebas.
* toocheck que se han ejecutado correctamente todos los pasos de supervisión mejorada de Azure y esa Hola infraestructura de Azure proporciona los datos necesarios de hello, continuar con la comprobación de preparación de Hola para hello Azure extensión de supervisión mejorada para SAP, como se describe en [Comprobación de preparación para la supervisión mejorada de Azure para SAP][deployment-guide-5.1].
* Espere 15 a 30 minutos para los datos relevantes de diagnósticos de Azure toocollect Hola.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>CLI de Azure para máquinas virtuales de Linux
tooinstall hello Azure extensión de supervisión mejorada para SAP mediante Azure CLI:

1. Instalar Azure CLI 1.0, como se describe en [Install hello Azure CLI 1.0][azure-cli].
2. Inicie sesión con su cuenta de Azure:

  ```
  azure login
  ```

3. Cambiar el modo de tooAzure Resource Manager:

  ```
  azure config mode arm
  ```

4. Habilite la supervisión mejorada de Azure:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Compruebe que la extensión de supervisión mejorada de Azure de Hola está activo en hello VM de Linux de Azure. Compruebe si Hola archivo \\var\\lib\\AzureEnhancedMonitor\\PerfCounters existe. Si existe, en un símbolo del sistema, ejecute este comando toodisplay la información recopilada por hello supervisión mejorada de Azure:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

salida de Hello tiene el siguiente aspecto:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Comprobaciones y solución de problemas de supervisión de extremo a extremo
Después de haber implementado la VM de Azure y configurar la infraestructura de supervisión Azure relevante hello, compruebe si todos los componentes de Hola de hello extensión de supervisión mejorada de Azure funcionan del modo esperado.

Ejecutar comprobación de preparación de Hola para hello Azure extensión de supervisión mejorada para SAP como se describe en [comprobación de preparación para hello Azure extensión de supervisión mejorada para SAP][deployment-guide-5.1]. Si todos los resultados de la comprobación de la preparación son positivos y todos los contadores de rendimiento pertinentes son correctos, la supervisión de Azure se configuró correctamente. Puede proceder con la instalación de Hola de agente de Host de SAP como se describe en las notas de SAP hello en [recursos SAP][deployment-guide-2.2]. Si la comprobación de preparación de hello indica que faltan contadores, ejecute la comprobación de mantenimiento de Hola para hello infraestructura de supervisión de Azure, tal y como se describe en [comprobación de estado de configuración de la infraestructura de supervisión Azure] [ deployment-guide-5.2]. Para ver más opciones de solución de problemas, consulte [Solución de problemas de supervisión de Azure para SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Comprobación de preparación para hello Azure extensión de supervisión mejorada para SAP
Esta comprobación se asegura de que todas las métricas de rendimiento que aparecen dentro de una aplicación de SAP se proporcionan con hello subyacente de la infraestructura de supervisión de Azure.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Ejecutar comprobación de preparación de hello en una VM de Windows

1.  Inicie sesión en la máquina virtual de Azure toohello (una cuenta de administrador no es necesario utilizar).
2.  Abra una ventana de símbolo del sistema.
3.  En línea de comandos de hello, cambiar carpeta de instalación de toohello de directorio de Hola de hello Azure extensión de supervisión mejorada para SAP: C:\\paquetes\\complementos\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versión >\\quitar

  Hola *versión* en hello toohello de ruta de acceso puede variar la extensión de supervisión. Si puede ver carpetas para varias versiones de hello supervisión extensión en la carpeta de instalación de hello, compruebe la configuración de servicio de AzureEnhancedMonitoring Windows, hello hello y, a continuación, el conmutador toohello carpeta indicada como *tooexecutable de ruta de acceso* .

  ![Propiedades del servicio que se ejecuta hello Azure extensión de supervisión mejorada para SAP][deployment-guide-figure-1000]

4.  En el símbolo de hello, ejecute **azperflib.exe** sin ningún parámetro.

  > [!NOTE]
  > Azperflib.exe se ejecuta en un bucle y actualiza los contadores de hello recopilado cada 60 segundos. bucle de hello tooend, ventana de símbolo del sistema de hello cerrar.
  >
  >

Si no se está ejecutando hello que no está instalada la extensión de supervisión mejorada de Azure, o hello AzureEnhancedMonitoring servicio, extensión de hello no ha configurado correctamente. Para obtener información detallada acerca de cómo toodeploy Hola extensión, vea [Troubleshooting Hola infraestructura de supervisión de Azure para SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Compruebe la salida de hello de azperflib.exe
La salida del archivo azperflib.exe muestra todos los contadores de rendimiento de Azure para SAP rellenados. Final Hola de hello lista de contadores recopilados, un indicador de resumen y estado de mostrar el estado de Hola de supervisión de Azure.

![Salida de la comprobación del estado mediante la ejecución de azperflib.exe, que indica que no hay problemas][deployment-guide-figure-1100]
<a name="figure-11"></a>

Compruebe el resultado de hello devuelto para hello **total de contadores** salida, que se notifica como vacíos y para **estado**, como se muestra en hello anterior figura.

Interpretar los valores resultantes de hello como sigue:

| Valores del resultado de azperflib.exe | Estado de mantenimiento de la supervisión de Azure |
| --- | --- |
| **Llamadas a API: no disponible** | Contadores que no están disponibles pueden ser cualquier configuración de máquina virtual de toohello no es aplicable, o están. Consulte **Estado de mantenimiento**. |
| **Total de contadores: vacíos** |Hola siguiendo dos contadores de almacenamiento de Azure puede estar vacío: <ul><li>Storage Read Op Latency Server msec</li><li>Storage Read Op Latency E2E msec</li></ul>Todos los demás contadores deben tener valores. |
| **Estado de mantenimiento** |Solo es correcto si el estado del resultado muestra **Correcto**. |
| **Diagnóstico** |Información detallada sobre el estado de mantenimiento. |

Si hello **estado** valor no es **Aceptar**, siga las instrucciones de hello en [comprobación de estado de configuración de la infraestructura de supervisión Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Ejecutar comprobación de preparación de hello en una VM Linux

1.  Conectar toohello Máquina Virtual de Azure a través de SSH.

2.  Compruebe la salida de hello de hello extensión de supervisión mejorada de Azure.

  a.  Ejecute `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **Resultado esperado**: devuelve una lista de contadores de rendimiento. archivo hello no debe estar vacío.

 b. Ejecute `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **Resultado esperado**: devuelve una línea donde se error hello **ninguno**, por ejemplo, **3; config; Error; 0; 0; Ninguno; 0; 1456416792; tst-servercs;**

  c. Ejecute `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **Resultado esperado**: devuelve un resultado vacío o no existente.

Si hello comprobación anterior no fue correcta, ejecute estas comprobaciones adicionales:

1.  Asegúrese de que ese waagent Hola está instalado y habilitado.

  a.  Ejecute `sudo ls -al /var/lib/waagent/`

      **Resultado esperado**: enumera el contenido de hello del directorio de waagent Hola.

  b.  Ejecute `ps -ax | grep waagent`

   **Resultado esperado**: muestra una entrada similar a: `python /usr/sbin/waagent -daemon`

3.   Asegúrese de que ese Hola extensión de supervisión mejorada de Azure está instalado y ejecutándose.

  a.  Ejecute `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`

    **Resultado esperado**: enumera el contenido de hello del directorio de extensión de supervisión mejorada de Azure Hola.

  b. Ejecute `ps -ax | grep AzureEnhanced`

     **Resultado esperado**: muestra una entrada similar a: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. Instalar el agente de Host de SAP como se describe en la nota de SAP [1031096]y compruebe la salida de hello de `saposcol`.

  a.  Ejecute `/usr/sap/hostctrl/exe/saposcol -d`

  b.  Ejecute `dump ccm`

  c.  Compruebe si Hola **Virtualization_Configuration\Enhanced supervisión acceso** métrica es **true**.

Si ya tiene instalado un servidor de aplicaciones de SAP NetWeaver ABAP, abra la transacción ST06 y compruebe si la supervisión mejorada está habilitada.

Si alguna de estas comprobaciones producirá un error y para obtener información detallada acerca de cómo tooredeploy Hola extensión, vea [Troubleshooting Hola infraestructura de supervisión de Azure para SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Comprobación de estado de hello Azure configuración de infraestructura de supervisión
Si algunos de los datos de supervisión de hello no se entregan correctamente como se indica por prueba Hola se describe en [comprobación de preparación para la supervisión mejorada de Azure para SAP][deployment-guide-5.1], hello ejecute `Test-AzureRmVMAEMExtension` toocheck de cmdlet si hello supervisión hello extensión de supervisión para SAP e infraestructura de Azure está configurada correctamente.

1.  Asegúrese de que ha instalado la versión más reciente de Hola Hola Azure del cmdlet de PowerShell, tal y como se describe en [cmdlets de PowerShell de Azure implementar][deployment-guide-4.1].
2.  Ejecute hello siguiente cmdlet de PowerShell. Para obtener una lista de entornos disponibles, ejecute el cmdlet de hello `Get-AzureRmEnvironment`. toouse global Azure, seleccione hello **nube de Azure** entorno. Si desea usar Azure en China, seleccione **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Escriba los datos de la cuenta e identificar Hola máquina virtual de Azure.

  ![Página de entrada del cmdlet de Azure específico para SAP Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. configuración de Hola Hola script pruebas de la máquina virtual de hello seleccione.

  ![Resultado de la prueba correcta de hello infraestructura de supervisión de Azure para SAP][deployment-guide-figure-1300]

Asegúrese de que todos los resultados de la comprobación del estado de mantenimiento sean **OK**. Si no se muestran algunas comprobaciones **Aceptar**, ejecute el cmdlet de actualización Hola tal y como se describe en [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5]. Espere 15 minutos y repita Hola comprobaciones se describen en [comprobación de preparación para la supervisión mejorada de Azure para SAP] [ deployment-guide-5.1] y [comprobación de estado de configuración de infraestructura de supervisión de Azure] [deployment-guide-5.2]. Si las comprobaciones de hello siguen indican un problema con algunos o todos los contadores, vea [Troubleshooting Hola infraestructura de supervisión de Azure para SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Solución de problemas de hello infraestructura de supervisión de Azure para SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] No aparecen contadores de rendimiento de Azure
Hola servicio de AzureEnhancedMonitoring Windows recopila métricas de rendimiento en Azure. Si el servicio de hello no se instaló correctamente o si no se está ejecutando en la máquina virtual, no se puede recopilar ninguna métrica de rendimiento.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>directorio de instalación de Hola de hello extensión de supervisión mejorada de Azure está vacío

###### <a name="issue"></a>Problema
directorio de instalación de Hello C:\\paquetes\\complementos\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versión >\\lista está vacía.

###### <a name="solution"></a>Solución
extensión de Hello no está instalada. Determine si se trata de un problema de proxy (como se describió anteriormente). Tendrá que toorestart máquina de Hola o vuelva a ejecutar hello `Set-AzureRmVMAEMExtension` script de configuración.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>El servicio de supervisión mejorada de Azure no existe

###### <a name="issue"></a>Problema
Hola servicio AzureEnhancedMonitoring Windows no existe.

La salida de Azperflib.exe produce un error:

![La ejecución de azperflib.exe indica que no se está ejecutando el servicio de Hola de hello extensión de supervisión mejorada de Azure para SAP][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Solución
Si no existe el servicio de hello, hello Azure extensión de supervisión mejorada para SAP no se instaló correctamente. Implementar la extensión de hello mediante el uso de pasos de hello descritos para su escenario de implementación en [escenarios de implementación de máquinas virtuales para SAP en Azure][deployment-guide-3].

Después de implementar la extensión de hello, después de una hora, vuelva a comprobar si los contadores de rendimiento de Azure Hola se proporcionan en hello VM de Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Servicio de supervisión mejorada existe, pero se produce un error toostart

###### <a name="issue"></a>Problema
Hola servicio AzureEnhancedMonitoring Windows existe y está habilitada, pero se produce un error toostart. Para obtener más información, compruebe el registro de eventos de aplicación Hola.

###### <a name="solution"></a>Solución
configuración de Hello es incorrecta. Reinicie Hola supervisión extensión para Hola de máquina virtual, como se describe en [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Faltan algunos contadores de rendimiento de Azure
Hola servicio de AzureEnhancedMonitoring Windows recopila métricas de rendimiento en Azure. servicio de Hello obtiene datos de varios orígenes. Algunos datos de configuración se recopilan localmente, y algunas métricas de rendimiento se leen de Diagnósticos de Azure. Contadores de almacenamiento se utilizan desde su registro en el nivel de suscripción de almacenamiento de Hola.

Si la solución de problemas mediante el uso de nota de SAP [1999351] no resuelva el problema de hello, vuelva a ejecutar hello `Set-AzureRmVMAEMExtension` script de configuración. Es posible que tenga toowait hora porque no se pueden crear contadores de análisis o diagnóstico de almacenamiento inmediatamente después de que se habiliten. Si persiste el problema de hello, abre un mensaje de compatibilidad del cliente SAP en hello componente BC-OP-NT-AZR para Windows o BC-OP-LNX-AZR para una máquina virtual Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] No aparecen contadores de rendimiento de Azure
Un demonio recopila las métricas de rendimiento en Azure. Si no se está ejecutando el daemon de hello, no se puede recopilar ninguna métrica de rendimiento.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>directorio de instalación de Hola de hello extensión de supervisión mejorada de Azure está vacío

###### <a name="issue"></a>Problema
directorio de Hello \\var\\lib\\waagent\\ no tiene un subdirectorio para hello extensión de supervisión mejorada de Azure.

###### <a name="solution"></a>Solución
extensión de Hello no está instalada. Determine si se trata de un problema de proxy (como se describió anteriormente). Tendrá que toorestart máquina de Hola o vuelva a ejecutar hello `Set-AzureRmVMAEMExtension` script de configuración.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Faltan algunos contadores de rendimiento de Azure
Un demonio recopila las métricas de rendimiento en Azure, y obtiene datos de varios orígenes. Algunos datos de configuración se recopilan localmente, y algunas métricas de rendimiento se leen de Diagnósticos de Azure. Contadores de almacenamiento proceden de registros de hello en su suscripción de almacenamiento.

Para ver una lista completa y actualizada de los problemas conocidos, consulte la nota de SAP [1999351], que contiene información adicional sobre la solución de problemas de la supervisión mejorada de Azure para SAP.

Si la solución de problemas mediante el uso de nota de SAP [1999351] no resuelva el problema de hello, vuelva a ejecutar hello `Set-AzureRmVMAEMExtension` script de configuración como se describe en [configurar hello Azure extensión de supervisión mejorada para SAP][deployment-guide-4.5]. Puede que tenga toowait durante una hora porque no se pueden crear contadores de análisis o diagnóstico de almacenamiento inmediatamente después de que se habiliten. Si persiste el problema de hello, abre un mensaje de compatibilidad del cliente SAP en hello componente BC-OP-NT-AZR para Windows o BC-OP-LNX-AZR para una máquina virtual Linux.
