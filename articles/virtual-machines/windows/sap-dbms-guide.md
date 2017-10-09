---
title: "aaaSAP NetWeaver en máquinas virtuales de Azure: Guía de implementación de DBMS | Documentos de Microsoft"
description: "SAP NetWeaver en máquinas virtuales de Azure: guía de implementación de DBMS"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver en máquinas virtuales Windows de Azure: guía de implementación de DBMS
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
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
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md 
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md 
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Esta guía forma parte de documentación de hello sobre la implementación y la implementación de software SAP de hello en Microsoft Azure. Antes de leer esta guía, lea hello [Guía de implementación y planificación][planning-guide]. Este documento centra en implementación Hola de los distintos sistemas de administración de base de datos relacionales (RDBMS) y productos relacionados en combinación con SAP máquinas virtuales en Microsoft Azure (VM) con hello infraestructura de Azure como las capacidades de un servicio (IaaS).

Hola papel complementa Hola documentación de la instalación de SAP y las notas de SAP que representan recursos principales de Hola para las instalaciones e implementaciones de software SAP en correctos plataformas

## <a name="general-considerations"></a>Consideraciones generales
En este capítulo, se presentan consideraciones sobre ejecución de sistemas DBMS relacionados con SAP en máquinas virtuales de Azure. Hay algunas referencias toospecific los sistemas DBMS en este capítulo. En su lugar sistemas DBMS específicos de Hola se tratan en este documento, después de este capítulo.

### <a name="definitions-upfront"></a>Lista de definiciones
En el documento de hello utilizamos Hola términos siguientes:

* IaaS: infraestructura como servicio.
* PaaS: plataforma como servicio.
* SaaS: software como servicio.
* Componente de SAP: una aplicación de SAP individual, como ECC, BW, Solution Manager o EP.  Los componentes de SAP pueden basarse en tecnologías tradicionales, como ABAP o Java, o en una aplicación no basada en NetWeaver, como Business Objects.
* Entorno SAP: uno o más componentes SAP agrupan lógicamente tooperform una función empresarial, como desarrollo, QAS, aprendizaje, recuperación ante desastres o producción.
* Panorama SAP: Se refiere toohello todos activos de SAP en un cliente panorama de TI. Hola panorama SAP incluye todos los entornos de producción y no es de producción.
* Sistema SAP: combinación de Hola de capa de DBMS y la capa de aplicación de, por ejemplo, un sistema de desarrollo SAP ERP, sistema de prueba de SAP BW, sistema de producción de SAP CRM, etcetera. En Azure implementaciones no es compatible con toodivide estas dos capas entre local y Azure. Esto significa que un sistema SAP debe implementarse de forma local o en Azure, pero no en ambos. Sin embargo, puede implementar diferentes sistemas de Hola de un panorama SAP en Azure o de forma local. Por ejemplo, podría implementar los sistemas de desarrollo y prueba de SAP CRM hello en Azure pero Hola SAP CRM producción sistema local.
* Implementación solo en la nube: una implementación donde hello suscripción de Azure no está conectado a través de un sitio a sitio o ExpressRoute conexión toohello local la infraestructura de red. En la documentación habitual de Azure este tipo de implementaciones se denomina "implementaciones exclusivas en la nube". Máquinas virtuales implementadas con este método se tiene acceso a través de Internet de Hola y extremos públicos de Internet asignan toohello las máquinas virtuales en Azure. Hola Active Directory (AD) local y DNS no se extiende tooAzure en estos tipos de implementaciones. Por lo tanto, las máquinas virtuales de hello no forman parte de hello Active Directory local. Nota: Las implementaciones exclusivas en la nube se definen en este documento como infraestructuras de SAP completas ejecutadas exclusivamente en Azure sin extensión de Active Directory ni resolución de nombres desde la infraestructura local a la nube pública. Configuraciones solo en la nube no están compatible con sistemas de SAP de producción ni las configuraciones donde STMS de SAP u otros recursos locales tener toobe utiliza entre los sistemas SAP hospedados en Azure y recursos que se encuentran en local.
* Entre entornos: Describe un escenario donde las máquinas virtuales son implementado tooan suscripción de Azure que tiene el sitio a sitio, de varios sitio o conectividad de ExpressRoute entre datacenter(s) de hello local y Azure. En la documentación habitual de Azure, este tipo de implementaciones se denominan "escenarios entre locales". motivo de Hola de conexión de hello es tooextend dominios locales, Active Directory local y local DNS en Azure. Hola horizontal local es extendido toohello activos de Azure de suscripción de Hola. Con esta extensión, hello las máquinas virtuales puede formar parte del dominio local de Hola. Los usuarios de dominio del dominio local de hello pueden tener acceso a servidores de Hola y pueden ejecutar servicios en esas máquinas virtuales (por ejemplo, servicios de DBMS). Es posible la comunicación y resolución de nombres entre máquinas virtuales implementadas de forma local y en Azure. Esperamos que este escenario más común de hello toobe para la implementación de activos SAP en Azure. Para más información, consulte [este][vpn-gateway-cross-premises-options] artículo y [este][vpn-gateway-site-to-site-create] vínculo.

> [!NOTE]
> En sistemas de producción SAP, se admiten implementaciones entre locales de sistemas SAP donde las máquinas virtuales de Azure que ejecuten sistemas SAP pertenezcan a un dominio local. Las configuraciones entre locales se admiten para la implementación completa o parcial de infraestructuras de SAP en Azure. Incluso en ejecución completa panorama de SAP hello en Azure requiere tener esas máquinas virtuales que se va a parte del dominio local y anuncios. En versiones anteriores de documentación de hello hablamos sobre escenarios de TI híbrida, donde el término de Hola "Híbrido" se ha modificado en hechos de Hola que hay una conectividad entre entornos entre local y Azure. En este caso "Híbrido" también significa que las máquinas virtuales de hello en Azure forman parte de hello en Active Directory local.
>
>

Algunos documentos de Microsoft describen escenarios entre locales de un modo ligeramente distinto, en especial en configuraciones de DBMS de alta disponibilidad. Hola caso de hello SAP documentos relacionados, escenario de hello entre locales solo reduce toohaving un sitio a sitio o privado (ExpressRoute) conectividad y toohello hecho que el panorama de SAP de Hola se distribuye entre local y Azure.

### <a name="resources"></a>Recursos
Hello guías siguientes están disponibles para hello tema de las implementaciones de SAP en Azure:

* [SAP NetWeaver en Azure Virtual Machines (VMs): guía de planeación e implementación][planning-guide]
* [SAP NetWeaver en Azure Virtual Machines: guía de implementación][deployment-guide]
* [SAP NetWeaver en máquinas virtuales de Azure: guía de implementación de DBMS (este documento)][dbms-guide]
* [SAP NetWeaver en máquinas virtuales de Azure: guía de implementación de alta disponibilidad][ha-guide]

Hola siguiendo las notas de SAP está relacionadas toohello tema de SAP en Azure:

| Número de nota | Título |
| --- | --- |
| [1928533] |SAP Applications on Azure: Supported Products and Azure VM types (Aplicaciones de SAP en Azure: tipos de máquina virtual de Azure y productos compatibles) |
| [2015553] |SAP on Microsoft Azure: Support Prerequisites (SAP en Microsoft Azure: requisitos previos de compatibilidad) |
| [1999351] |Troubleshooting Enhanced Azure Monitoring for SAP (Solución de problemas de la supervisión mejorada de Azure para SAP) |
| [2178632] |Key Monitoring Metrics for SAP on Microsoft Azure (Métricas de supervisión clave para SAP en Microsoft Azure) |
| [1409604] |Virtualization on Windows: Enhanced Monitoring (Virtualización en Windows: supervisión mejorada) |
| [2191498] |SAP on Linux with Azure: Enhanced Monitoring (SAP en Linux con Azure: supervisión mejorada) |
| [2039619] |Hola de aplicaciones SAP en Microsoft Azure con base de datos de Oracle: admite productos y versiones |
| [2233094] |DB6: SAP Applications on Azure Using IBM DB2 for Linux, UNIX, and Windows - Additional Information (DB6: aplicaciones de SAP en Azure con IBM DB2 para Linux, UNIX y Windows: información adicional) |
| [2243692] |Linux on Microsoft Azure (IaaS) VM: SAP license issues (Linux y máquinas virtuales de Microsoft Azure (IaaS): problemas de licencia de SAP) |
| [1984787] |SUSE LINUX Enterprise Server 12: Installation notes (SUSE Linux Enterprise Server 12: notas de instalación) |
| [2002167] |Red Hat Enterprise Linux 7.x: Installation and Upgrade (Red Hat Enterprise Linux 7.x: instalación y actualización) |

Lea también hello [Wiki de SCN](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) que contiene todas las notas de SAP para Linux.

Debe tener conocimientos prácticos acerca de hello arquitectura de Microsoft Azure y cómo se implementan y opera máquinas virtuales de Microsoft Azure. Puede encontrar más información aquí <https://azure.microsoft.com/documentation/>.

> [!NOTE]
> Estamos **no** hablando de la plataforma Microsoft Azure como las ofertas de servicio (PaaS) de hello plataforma Microsoft Azure. Este documento es sobre la ejecución de máquinas virtuales en Microsoft Azure (IaaS) de un sistema de administración de bases de datos (DBMS) igual que ejecutaría Hola DBMS en su entorno local. Las funcionalidades de bases de datos de estas dos ofertas son muy diferentes y no deben combinarse. Consulte también: <https://azure.microsoft.com/services/sql-database/>.
>
>

Puesto que estamos analizando la IaaS, por lo general Hola Windows, Linux y DBMS la instalación y configuración son básicamente Hola igual que cualquier máquina virtual o una máquina sin sistema operativo se instala localmente. Sin embargo, hay algunas decisiones de implementación de administración de sistemas y arquitecturas que diferirán cuando se utilice el modelo IaaS. Hola de este documento sirve tooexplain Hola arquitectónicas y sistema de administración diferencias específicas que debe estar preparado para cuando utilice la IaaS.

En general, hello áreas generales de diferencia que se tratará en este documento son:

* Planear el diseño VM/VHD adecuado de Hola de tooensure de sistemas SAP tiene diseño del archivo de datos apropiados de Hola y puede lograr suficientes IOPS para la carga de trabajo.
* Consideraciones sobre redes al utilizar IaaS
* Toouse características de base de datos específica en el diseño de base de datos de pedido toooptimize Hola.
* Consideraciones sobre las operaciones de copia de seguridad y restauración en IaaS
* Uso de diferentes tipos de imágenes para tareas de implementación
* Alta disponibilidad en IaaS de Azure

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Estructura de una implementación de RDBMS
En orden, siga este capítulo, es necesario toounderstand lo que se presenta en [esto] [ deployment-guide-3] capítulo de hello [Guía de implementación][deployment-guide]. Conocimiento sobre Hola distintos Series de máquinas virtuales y sus diferencias y las diferencias del estándar de Azure y almacenamiento Premium deben comprender y se conoce antes de leer este capítulo.

Hasta marzo de 2015, discos duros virtuales de Azure que contienen un sistema operativo estaba limitado too127 GB de tamaño. Esta limitación se eliminó en marzo de 2015 (para más información, consulte <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/>). Desde allí en discos duros virtuales contenedor sistema de operativo Hola puede haber Hola mismo tamaño como cualquier otro disco duro virtual. No obstante, se prefiere una estructura de implementación donde hello sistema operativo, eventual archivos binarios SAP y DBMS son independientes de los archivos de base de datos de Hola. Por lo tanto, esperamos que sistemas SAP que se ejecutan en máquinas virtuales de Azure tendrá Hola base virtual (o VHD) instalada con sistema operativo de hello, base de datos administración los ejecutables del sistema y los ejecutables de SAP. Hola datos del DBMS y los archivos de registro se almacenados en el almacenamiento de Azure (Standard o Premium almacenamiento) en archivos VHD aparte y adjunta como imagen de sistema operativo Azure original VM de discos lógicos toohello.

Depende de aprovechar Azure estándar o Premium almacenamiento (por ejemplo, mediante el uso de Hola DS-series o GS-series las máquinas virtuales) se están otras cuotas en Azure que se documentan [aquí][virtual-machines-sizes]. Al planificar sus VHD de Azure, necesitará toofind Hola mejor equilibrio en las cuotas de Hola para siguiente hello:

* número de Hola de archivos de datos.
* número de Hola de discos duros virtuales que contienen archivos de Hola.
* cuotas de IOPS de Hola de un solo disco duro virtual.
* rendimiento de datos de Hola por VHD.
* número de Hola de posibles de discos duros virtuales adicionales por tamaño de máquina virtual.
* Hello general rendimiento de almacenamiento una máquina virtual puede proporcionar.

Azure aplicará una cuota de IOPS por unidad de VHD. Estas cuotas son diferentes para los VHD hospedados en el almacenamiento estándar y premium de Azure. Las latencias de E/S también será muy diferentes entre dos tipos de almacenamiento Hola con almacenamiento Premium entregar factores mejor latencias de E/S. Cada uno de los diferentes tipos de VM hello tiene un número limitado de discos duros virtuales que es capaz de tooattach. Otra restricción consiste en que solo determinados tipos de máquinas virtuales pueden utilizar Azure Premium Storage. Esto significa la decisión de Hola para un determinado tipo de máquina virtual podría no solo está determinado por hello CPU y requisitos de memoria, sino también por hello IOPS, requisitos de rendimiento de disco y latencia que normalmente se escalan con número de Hola de discos duros virtuales u Hola tipo de discos de almacenamiento Premium. Especialmente con almacenamiento Premium tamaño Hola de un disco duro virtual también puede determinarse por número de Hola de e/s por segundo y el rendimiento que necesita toobe logra por cada disco duro virtual.

hecho de Hola Hola tasa de IOPS general, número de Hola de VHD montados y Hola tamaño de hello VM estén todos relacionados, puede provocar una configuración de un toobe de sistema SAP diferente de su implementación local de Azure. límites de IOPS de Hola por LUN son normalmente configurables en las implementaciones locales. Mientras que con el almacenamiento de Azure esos límites son fijos o como en almacenamiento Premium depende de tipo de disco de Hola. Por lo que con las implementaciones locales vemos configuraciones del cliente de los servidores de base de datos que se están utilizando muchos volúmenes diferentes para los ejecutables especiales como SAP y Hola DBMS o volúmenes especiales para bases de datos temporales o espacios de tabla. Dichos sistemas local una vez movida tooAzure podría dar lugar tooa residuos de ancho de banda IOPS potencial al desperdiciar un VHD para ejecutables o bases de datos que no tienen que realizar alguna o no una gran cantidad de e/s por segundo. Por lo tanto, en máquinas virtuales de Azure recomendamos que ejecutables SAP y DBMS Hola instalarse en el disco de hello SO si es posible.

Hello selección de ubicación de archivos de base de datos de Hola y archivos de registro y tipo de Hola de almacenamiento de Azure utilizado, se debería definir IOPS, latencia y requisitos de rendimiento. En orden toohave suficientes IOPS para el registro de transacciones de hello, podría ser forzada tooleverage varios discos duros virtuales para registro de transacciones de Hola de archivo o usen un disco de almacenamiento Premium de mayor tamaño. En este caso podría simplemente compilar un RAID de software (por ejemplo, grupo de almacenamiento de Windows para Windows o MDADM y LVM (Administrador de discos lógicos) para Linux) con discos duros virtuales que contendrá el registro de transacciones de Hola Hola.

- - -
> ![Windows][Logo_Windows] Windows
>
> Unidad D:\ en una máquina virtual de Azure es una unidad no persistente que está respaldada por algunos discos locales en el nodo de proceso de Azure de Hola. Dado que es no persistente, esto significa que cualquier contenido de toohello los cambios realizados en la unidad D:\ Hola se pierde cuando Hola VM se reinicia. Por "cambios", nos referimos a los archivos guardados, los directorios creados, las aplicaciones instaladas, etc.
>
> ![Linux][Logo_Linux] Linux
>
> Las máquinas virtuales de Linux Azure automáticamente montar una unidad en/mnt/Resource que es una unidad no persistente respaldada por discos locales de nodo de proceso de Azure Hola. Dado que es no persistente, esto significa que cualquier toocontent los cambios realizados en/mnt/Resource se pierden cuando se reinicia la VM de Hola. Por "cambios", nos referimos a los archivos guardados, los directorios creados, las aplicaciones instaladas, etc.
>
>

- - -
Dependiente de hello series de máquinas virtuales de Azure, los discos locales de Hola de Hola proceso mostrar diferentes el rendimiento del nodo que se pueden clasificar como:

* A0-A7: rendimiento muy limitado. No se puede usar para un recurso que no sea un archivo de paginación de Windows.
* A8-A11: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie D: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie DS: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie G: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie GS: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.

Las instrucciones anteriores están aplicando los tipos de VM toohello certificados con SAP. Hola series de máquinas virtuales con excelente IOPS y el rendimiento son aptos para aprovechar algunas características de DBMS, como tempdb o espacio de tabla temporal.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Almacenamiento en caché de máquinas virtuales y VHD
Cuando creamos esos discos/discos duros virtuales a través del portal de Hola o cuando montamos cargado tooVMs de discos duros virtuales, podemos elegir si el tráfico de hello E/S entre hello VM y los discos duros virtuales ubicados en el almacenamiento de Azure se almacenan en caché. Azure Standard Storage and Azure Premium Storage utilizan dos tecnologías diferentes para este tipo de almacenamiento en caché. En ambos casos, Hola propia caché se disco realizarían en hello usan mismas unidades por hello disco temporal (D:\ en Windows) o/mnt/Resource en Linux de hello máquina virtual.

Almacenamiento de Azure estándar Hola posibles tipos de caché son:

* Sin almacenamiento en caché
* Almacenamiento en caché de lectura
* Almacenamiento en caché de lectura y escritura

En orden tooget coherente y determinista el rendimiento, debería establecer Hola almacenamiento en caché en el almacenamiento de Azure estándar para todos los discos duros virtuales que contiene **DBMS relacionados con archivos de datos, archivos de registro y too'NONE de espacio de tabla '**. Hola almacenamiento en caché de hello VM puede permanecer no tiene valor predeterminado de Hola.

Almacenamiento de Azure Premium existe Hola siguientes opciones de almacenamiento en caché:

* Sin almacenamiento en caché
* Almacenamiento en caché de lectura

Recomendación para el almacenamiento de Azure Premium es tooleverage **almacenamiento en caché para archivos de datos de lectura** de base de datos SAP de Hola y seleccione **ningún almacenamiento en caché para VHD de los archivos de registro de hello**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>RAID de software
Como ya se ha indicado anteriormente, necesitará toobalance Hola número de IOPS necesarios para los archivos de base de datos de hello en número de Hola de hello y discos duros virtuales que se puede configurar número máximo de IOPS proporcionará una VM de Azure por VHD o almacenamiento Premium disco tipo. La manera más fácil toodeal con carga de IOPS en discos duros virtuales de hello es toobuild una RAID de software a través de Hola diferentes discos duros virtuales. A continuación, colocar una cantidad de archivos de datos de SAP DBMS hello en hello que LUN se extraen de RAID de software de Hola. Depende de los requisitos de hello que conviene tooconsider Hola uso de almacenamiento Premium también desde dos hello, tres discos diferentes de almacenamiento Premium proporcionan mayor cuota de IOPS de discos duros virtuales en función de almacenamiento estándar. Además, Hola significativos mejor latencia de E/S proporciona almacenamiento Premium de Azure.

Esto mismo aplica toohello el registro de transacciones de distintos sistemas de DBMS Hola. Con muchos de ellos limitarse a agregar más archivos de registro de transacciones no se soluciona porque los sistemas DBMS Hola escribir en uno de los archivos de hello en uno solo. Si se necesitan mayores tasas de e/s por segundo que un almacenamiento en función del estándar solo puede entregar el disco duro virtual, puede crear bandas en varios discos duros de virtuales de almacenamiento estándar o puede usar un tipo de disco de almacenamiento Premium mayor que, más allá de los mayores tasas de e/s por segundo, también ofrece factores menor latencia de escritura de hello I / Sistema operativo en el registro de transacciones de Hola.

Estas son las situaciones experimentadas en las implementaciones de Azure que se favorecerían si se emplea software RAID:

* El registro de transacciones y el de rehacer necesitan más IOPS que lo que ofrece Azure para un solo VHD. Tal y como se mencionó anteriormente, esto puede solucionarse creando un LUN en varios VHD que utilicen software RAID.
* E/S cargas de trabajo distribución desigual sobre Hola diferentes archivos de datos de base de datos SAP de Hola. En tales casos, uno puede experimentar un archivo de datos que se alcanza la cuota de hello en su lugar a menudo. Mientras que otros archivos de datos no obtienen incluso cerrar toohello cuota de IOPS de un solo disco duro virtual. En este tipo hello casos solución más fácil es toobuild una LUN en varios discos duros virtuales con un software RAID.
* No sabe qué Hola exacta E/S cargas de trabajo por cada archivo de datos es y solo aproximadamente saber qué Hola es de carga de trabajo de e/s por segundo de hello DBMS general. Toodo más fácil es toobuild un LUN con hello ayuda de un software RAID. suma de Hola de cuotas de varios discos duros virtuales detrás de este LUN, a continuación, debe cumplir Hola conocida IOPS velocidad.

- - -
> ![Windows][Logo_Windows] Windows
>
> Se recomienda usar Windows Server 2012 o espacios de almacenamiento superior, ya que es más eficaz que la funcionalidad de creación de secciones de versiones anteriores de Windows. Ten en cuenta que puede ser necesario toocreate Hola grupos de almacenamiento de Windows y espacios de almacenamiento mediante comandos de PowerShell cuando se usa Windows Server 2012 como sistema operativo. comandos de PowerShell de Hello pueden encontrarse aquí <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> Sólo MDADM y LVM (Administrador de discos lógicos) son compatible toobuild una RAID de software en Linux. Para obtener más información, lea Hola siguientes artículos:
>
> * [Configuración de RAID de software en Linux][virtual-machines-linux-configure-raid] (para MDADM)
> * [Configuración del LVM en una máquina virtual Linux en Azure][virtual-machines-linux-configure-lvm]
>
>

- - -
Consideraciones para aprovechar la serie de máquinas virtuales que suelen ser capaz de toowork con almacenamiento Premium de Azure son:

* Las peticiones de las latencias de E/S que cierre toowhat SAN/NAS dispositivos entregar.
* Petición proporcionar una mejor latencia de E/S que la que puede proporcionar Azure Standard Storage.
* Mayor tasa de IOPS por máquina virtual que la que podría obtenerse con varios VHD de almacenamiento estándar en un determinado tipo de máquina virtual.

Desde Hola almacenamiento de Azure subyacente replica a cada nodos de almacenamiento de disco duro virtual tooat tres mínimos, RAID 0 se puede utilizar la creación de bandas simple. No hay ninguna necesidad tooimplement RAID 5 o RAID 1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Almacenamiento de Microsoft Azure
Microsoft almacenará el almacenamiento de Azure Hola VM base (con SO) y discos duros virtuales o BLOBs de nodos de almacenamiento independientes tooat 3 mínimos. Al crear una cuenta de almacenamiento, se ofrece una opción de protección, tal y como se muestra aquí:

![Replicación geográfica habilitada para la cuenta de almacenamiento de Azure][dbms-guide-figure-100]

Replicación almacenamiento de Azure Local (redundancia local) proporciona niveles de protección contra la pérdida de datos debido a errores de tooinfrastructure que pocos clientes pueden permitirse toodeploy. Como se indicó anteriormente hay 4 opciones diferentes con una quinta parte que se va a una variación de uno de hello en primer lugar tres. Si las analizamos más detenidamente, podemos distinguir:

* **Almacenamiento con redundancia local (LRS) premium**: Azure Premium Storage ofrece compatibilidad con discos de alto rendimiento y latencia baja para máquinas virtuales con cargas de trabajo intensivas de E/S. Hay 3 réplicas de datos de hello en hello mismo centro de datos de Azure de una región de Azure. Hello copias estará en diferentes dominios de error y actualización (para conceptos, vea [esto] [ planning-guide-3.2] capítulo Hola [Guía de planificación][planning-guide]). En el caso de una réplica de datos de Hola que salen de servicio debido a error de nodo de almacenamiento de tooa o error de disco, una nueva réplica se genera automáticamente.
* **Almacenamiento redundante local (LRS)**: en este caso, hay 3 réplicas de datos de hello en hello mismo centro de datos de Azure de una región de Azure. Hello copias estará en diferentes dominios de error y actualización (para conceptos, vea [esto] [ planning-guide-3.2] capítulo Hola [Guía de planificación][planning-guide]). En el caso de una réplica de datos de Hola que salen de servicio debido a error de nodo de almacenamiento de tooa o error de disco, una nueva réplica se genera automáticamente.
* **Almacenamiento con redundancia geográfica (GRS)**: en este caso, hay una replicación asincrónica que se alimenta el papel más 3 réplicas de datos de hello en otra región de Azure que se encuentra en la mayoría de casos de hello en Hola misma región geográfica (por ejemplo, Europa del Norte y oeste Europa). Esta opción generará 3 réplicas adicionales, por lo que habrá 6 réplicas en total. Una variación de este es una adición donde se pueden usar datos de hello en región de Azure replicada Hola geográfica para su lectura (acceso de lectura con redundancia geográfica).
* **La zona de almacenamiento redundante (ZRS)**: en este caso réplicas Hola 3 de hello datos permanecen en Hola la misma región de Azure. Como se explica en [esto] [ planning-guide-3.1] capítulo de hello [Guía de planificación] [ planning-guide] una región de Azure puede ser un número de centros de datos cerca unas de otras. En caso de hello de LRS réplicas Hola se reparte Hola distintos centros de datos que hacen que una región de Azure.

Puede encontrar más información [aquí][storage-redundancy].

> [!NOTE]
> Para las implementaciones de DBMS, no se recomienda el uso de Hola de almacenamiento con redundancia geográfica
>
> La replicación geográfica de Azure Storage es asincrónica. Replicación de discos duros virtuales individuales montado tooa sola máquina virtual no están sincronizadas en el paso de bloqueo. Por lo tanto, no son archivos DBMS tooreplicate adecuado que se distribuyen en diferentes discos duros virtuales o se implementa con un software RAID basada en varios discos duros virtuales. El software de DBMS requiere que el almacenamiento en disco persistente Hola se sincronice con precisión en LUN diferentes y subyacentes discos/discos duros virtuales/ejes. El software de DBMS utiliza diversos toosequence mecanismos actividades de escritura de E/S y un DBMS informará de que el almacenamiento en disco Hola dirigida por la replicación de hello está dañado si estas varían incluso en unos pocos milisegundos. Por lo tanto, si realmente desea una configuración de base de datos con una base de datos que se extienda a través de varios discos duros virtuales con replicación geográfica, dicha replicación debe realizar con los medios de la base de datos y la funcionalidad de toobe. No se debe depender de replicación geográfica del almacenamiento Azure tooperform este trabajo.
>
> problema de Hello es más sencillo tooexplain con un sistema de ejemplo. Supongamos que tiene un sistema SAP cargado en Azure con 8 discos duros virtuales que contienen archivos de datos de hello DBMS más un disco duro virtual que lo contiene Hola transacción archivo de registro. Cada uno de estos 9 VHD tendrá datos escritos toothem en un método coherente según toohello DBMS, si se escriben los archivos de registro de transacciones o datos toohello datos de Hola.
>
> En orden tooproperly replicar geográficamente Hola datos y mantener una imagen de la base de datos coherente, el contenido de Hola de los nueve VHD habría toobe replicación geográfica en operaciones de hello orden exacto Hola E/S ejecutados contra Hola nueve VHD diferentes. Sin embargo, la replicación geográfica del almacenamiento de Azure no permite toodeclare dependencias entre los discos duros virtuales. Esto significa que no sabe replicación geográfica del almacenamiento de Azure de Microsoft sobre el hecho de Hola que el contenido de hello en estos nueve VHD diferentes están relacionado tooeach otra y que los cambios de datos de hello son coherentes solo cuando se replican Hola orden hello en operaciones de E/S ha ocurrido en todos los discos duros virtuales Hola 9.
>
> Además de posibilidades alta que imágenes de replicación geográfica de hello en el escenario de hello proporcionan una imagen de la base de datos coherente, también hay una reducción del rendimiento que se muestra con almacenamiento con redundancia geográfica que graves puede afectar al rendimiento. En resumen, no utilice este tipo de redundancia de almacenamiento para las cargas de trabajo de tipo DBMS.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Asignación de VHD en cuentas de almacenamiento del servicio de máquina virtual de Azure
Las cuentas de almacenamiento de Azure se usan con fines administrativos y presentan algunas limitaciones. Mientras que las limitaciones de hello varían si hablamos de una cuenta de almacenamiento de Azure estándar o una cuenta de almacenamiento Premium de Azure. Hola exacta capacidades y limitaciones se enumeran [aquí][storage-scalability-targets]

Modo estándar para almacenamiento de Azure que es importante toonote hay un límite en hello IOPS por cuenta de almacenamiento (en la fila que contiene 'Velocidad Total de solicitudes' [artículo hello][storage-scalability-targets]). Además, hay un límite inicial de 100 cuentas de almacenamiento por suscripción de Azure (a partir de julio de 2015). Por lo tanto, se recomienda toobalance IOPS de máquinas virtuales entre varias cuentas de almacenamiento al usar el almacenamiento de Azure estándar. Asimismo, lo ideal es que una sola máquina virtual utilice una cuenta de almacenamiento, si es posible. Por consiguiente, si hablamos de implementaciones de DBMS donde cada VHD que se hospeda en Azure Standard Storage puede alcanzar su límite de cuota, solo se deben implementar entre 30 y 40 VHD por cuenta de almacenamiento de Azure que utilice Azure Standard Storage. En hello otra parte, si aprovechar almacenamiento Premium de Azure y desea toostore volúmenes de base de datos grande, es posible que un problema en términos de IOPS. No obstante, una cuenta de Azure Premium Storage es mucho más restrictiva en lo que respecta al volumen de datos que una cuenta de Azure Standard Storage. Como resultado, solo se puede implementar un número limitado de discos duros virtuales dentro de una cuenta de almacenamiento de Azure Premium antes de alcanzar el límite de volumen de datos de Hola. En la reflexión de hello final de una cuenta de almacenamiento de Azure como una "SAN Virtual" tiene capacidades limitadas en IOPS y capacidad. Como resultado, tarea hello sigue siendo, como las implementaciones locales, diseño de hello toodefine de hello discos duros virtuales de diferentes sistemas SAP Hola sobre Hola diferentes 'dispositivos SAN imaginarios' o cuentas de almacenamiento de Azure.

Para Azure no se recomienda toopresent almacenamiento de tooa de cuentas de almacenamiento diferente de almacenamiento estándar única VM si es posible.

Mientras que el uso de Hola DS o GS-series de máquinas virtuales de Azure es posible toomount discos duros virtuales de cuentas de almacenamiento de Azure estándar y cuentas de almacenamiento Premium. Casos de uso como escribir copias de seguridad en almacenamiento estándar habían respaldado discos duros virtuales, mientras que los datos de DBMS y archivos de registro en almacenamiento Premium vienen toomind donde puede aprovecharse dicho almacenamiento heterogénea.

Basándose en las implementaciones de clientes y pruebas too40 aproximadamente 30 discos duros virtuales que contiene archivos de datos de la base de datos y archivos de registro se pueden aprovisionar en una cuenta de almacenamiento estándar de Azure único con un rendimiento aceptable. Tal y como se mencionó anteriormente, limitación de Hola de una cuenta de almacenamiento de Azure Premium es capacidad de datos de hello toobe es probable que puede contener y no IOPS.

Como con SAN dispositivos locales, uso compartido requiere algunos supervisión en orden tooeventually detectar cuellos de botella en una cuenta de almacenamiento de Azure. Hola extensión de supervisión de Azure para SAP y Hola Portal de Azure son herramientas que pueden ser utilizado toodetect ocupados cuentas de almacenamiento de Azure que pueden estar proporcionando poco óptimo rendimiento de E/S.  Si se detecta esta situación, se recomienda toomove ocupado máquinas virtuales tooanother cuenta de almacenamiento de Azure. Consulte toohello [Guía de implementación] [ deployment-guide] para obtener más información sobre cómo tooactivate Hola SAP hospedar las capacidades de supervisión.

Otro artículo donde se resumen los procedimientos recomendados para Azure Standard Storage y las cuentas de Azure Standard Storage se puede encontrar aquí <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Mover implementa las VM de DBMS desde el almacenamiento de Azure estándar tooAzure almacenamiento Premium
Descubrimos bastante algunos escenarios donde desea que como cliente toomove una VM implementada estándar del almacenamiento de Azure en almacenamiento Premium de Azure. Esto no es posible sin mover físicamente los datos de Hola. Hay objetivo de Hola de tooachieve de varias maneras:

* Podría copiar simplemente todos los VHD, el VHD base y los VHD de datos en una nueva cuenta de Azure Premium Storage. Muy a menudo número Hola de discos duros virtuales que eligió en el almacenamiento de Azure estándar no debido a hechos de hello precisó de volumen de datos de Hola. Pero necesitan que muchos discos duros virtuales debido a Hola e/s por segundo. Ahora que mover tooAzure almacenamiento Premium podría ir con forma menos tooachieve discos duros virtuales Hola algunas rendimiento de e/s por segundo. Dado el hecho de Hola que almacenamiento de Azure estándar se paga por hello usa datos y no el tamaño de disco nominal hello, número de Hola de discos duros virtuales no importa realmente en términos de costos. Sin embargo, con el almacenamiento de Azure Premium, pagaría por tamaño de disco nominal de Hola. Por lo tanto, la mayoría de los clientes de hello pruebe con tookeep Hola número de discos duros virtuales de Azure en almacenamiento Premium a Hola número tooachieve necesarios Hola IOPS rendimiento necesario. Por lo tanto, la mayoría de los clientes deciden en forma de Hola de un simple 1:1 copia.
* Si aún no lo ha hecho, monte un solo VHD que pueda contener una copia de seguridad de la base de datos de SAP. Después de la copia de seguridad de hello, desmontar todos los discos duros virtuales incluida copia Hola VHD del contenedor Hola y Hola de copia base VHD y Hola VHD con copia de seguridad de hello en una cuenta de almacenamiento Premium de Azure. A continuación, implemente Hola que VM en función de Hola base VHD y montaje Hola VHD con copia de seguridad de Hola. Ahora cree adicional Premium almacenamiento discos vacíos para hello VM base de datos de uso toorestore hello en. Esto se da por supuesto que Hola DBMS permite toochange toohello datos y registro de archivos de las rutas de acceso como parte del proceso de restauración de Hola.
* Otra posibilidad es una variación del proceso anterior hello, donde se copia VHD de copia de seguridad de hello en almacenamiento Premium de Azure y adjuntar contra una VM que implementaron e instalaron recientemente.
* posibilidad cuarto Hola elegiría cuando haya necesitados número de hello toochange de archivos de datos de la base de datos. En ese caso, realizaría una copia del sistema homogéneo de SAP mediante procesos de exportación e importación. Coloque los archivos de exportación en un disco duro virtual que se copia en una cuenta de almacenamiento de Azure Premium y adjuntarlo tooa VM que usar procesos de importación de toorun Hola. Los clientes usar esta posibilidad principalmente cuando lo deseen número de hello toodecrease de archivos de datos.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Implementación de máquinas virtuales para SAP en Azure
Microsoft Azure ofrece varias maneras de toodeploy las máquinas virtuales y discos de asociados. Por tanto, es muy importante toounderstand diferencias de Hola, ya preparativos de hello las máquinas virtuales pueden variar según en forma de Hola de implementación. En general, ponemos atención a los escenarios de hello descritos en hello siguientes capítulos.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Implementación de una máquina virtual de hello Azure Marketplace
Le gusta tootake Microsoft o entidad 3rd proporciona imágenes de hello Azure Marketplace toodeploy la máquina virtual. Una vez implementada la máquina virtual en Azure, siga Hola mismas instrucciones y herramientas tooinstall Hola software SAP en la máquina virtual como lo haría en un entorno local. Para la instalación de software de SAP de hello en hello VM de Azure, SAP y Microsoft recomienda tooupload y almacenan medios de instalación de SAP de hello en discos duros virtuales de Azure o toocreate una VM de Azure funciona como un servidor de archivos' ' que contiene todos los Hola necesarios SAP medios de instalación.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Implementación de máquinas virtuales con una imagen generalizada específica del cliente
Debido a requisitos de revisión de toospecific en lo que respecta tooyour sistema operativo o versión DBMS, imágenes Hola proporcionado en hello Azure Marketplace no pueden ajustarla a sus necesidades. Por lo tanto, tendrá que toocreate una máquina virtual mediante su propia imagen de VM de SO o DBMS 'private' que se puede implementar varias veces con posterioridad. tooprepare una imagen 'privada' para la duplicación, Hola que SO debe estar generalizado en hello local de máquina virtual. Consulte toohello [Guía de implementación] [ deployment-guide] para obtener más información acerca de cómo toogeneralize una máquina virtual.

Si ya ha instalado contenido de SAP en la VM local (especialmente para sistemas de 2 niveles), puede adaptar la configuración del sistema SAP Hola después de implementación de Hola de hello Azure VM a través de la instancia de hello cambiar el nombre de procedimiento admite Hola aprovisionamiento de Software de SAP Administrador (Nota de SAP [1619720]). En caso contrario, puede instalar software SAP de hello más tarde después de la implementación de Hola de hello VM de Azure.

A partir de contenido de base de datos de hello usados por hello aplicación SAP, puede generar contenido Hola nuevo mediante una instalación de SAP o puede importar el contenido a Azure mediante el uso de un disco duro virtual con una copia de seguridad de base de datos DBMS o mediante el aprovechamiento de las capacidades de hello DBMS toodirectly copia de seguridad en el almacenamiento de Azure de Microsoft. En este caso, puede preparar VHD con datos del DBMS de hello y registrar archivos locales y, a continuación, importarlos como discos en Azure. Pero la transferencia de Hola de datos DBMS que se está cargando desde local tooAzure funcionaría en los discos VHD que necesitan toobe preparado local.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Mover una máquina virtual de tooAzure local con un disco no generalizado
Planee toomove un sistema SAP específico desde local tooAzure (elevar y cambiar). Esto puede hacerse mediante la carga de hello VHD que contiene Hola SO, Hola archivos binarios SAP y los archivos binarios DBMS eventuales más Hola discos duros virtuales con archivos de datos y registro de hello de hello DBMS tooAzure. En opuesto tooscenario #2 anterior, mantener Hola hostname, SID de SAP y las cuentas de usuario SAP en hello Azure VM tal y como se configuraron en el entorno local de Hola. Por lo tanto, no es necesario generalizar la imagen de Hola. En este caso se aplicará sobre todo en escenarios entre entornos donde una parte del programa Hola panorama de SAP se ejecuta en local y los elementos en Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Alta disponibilidad y recuperación ante desastres con máquinas virtuales de Azure
Azure ofrece Hola siguiendo las funcionalidades de alta disponibilidad (HA) y recuperación ante desastres (DR) que se aplican los componentes toodifferent que se utilizaría para las implementaciones de SAP y DBMS

### <a name="vms-deployed-on-azure-nodes"></a>Máquinas virtuales implementadas en nodos de Azure
Hola plataforma de Azure no ofrece características como la migración en vivo de máquinas virtuales implementadas. Esto significa que si hay mantenimiento necesario en un clúster de servidor en el que se implementa una máquina virtual, Hola VM debe tooget detenerse y reiniciarse. El mantenimiento de Azure se realiza utilizando los llamados "dominios de actualización" de los clústeres de servidores. Solo se mantiene a la vez un único dominio de actualización. Durante un reinicio habrá una interrupción del servicio mientras Hola que VM se apaga, realizando el mantenimiento y reinicia la máquina virtual. Sin embargo, la mayoría de los proveedores DBMS proporciona funcionalidad de alta disponibilidad y recuperación ante desastres que reinicia rápidamente servicios del DBMS hello en otro nodo si el nodo principal de hello no está disponible. Hello plataforma Azure ofrece funcionalidad toodistribute máquinas virtuales, almacenamiento y otros servicios de Azure a través de dominios de actualización tooensure que prevé errores de infraestructura o de mantenimiento solo afectarán a un pequeño subconjunto de máquinas virtuales o servicios.  Con una planificación cuidadosa es infraestructuras de posibles tooachieve disponibilidad niveles comparables tooon local.

Conjuntos de disponibilidad de Microsoft Azure son una agrupación lógica de máquinas virtuales o servicios que garantizan que las máquinas virtuales y otros servicios son distribuida toodifferent error y dominios de actualización dentro de un clúster de forma que solo habría un apagado de nodo en cualquier momento en el tiempo (lectura [esto] [ virtual-machines-manage-availability] artículo para obtener más detalles).

Necesita toobe configurado según su fin al implementarse las máquinas virtuales tal como se muestra aquí:

![Definición de conjunto de disponibilidad para configuraciones de alta disponibilidad de DBMS][dbms-guide-figure-200]

Si queremos toocreate configuraciones de alta disponibilidad de las implementaciones de DBMS (independientes de hello individuales HA de DBMS funcionalidad usada), las VM de DBMS Hola tendría que:

* Agregar toohello de máquinas virtuales de hello misma red Virtual de Azure (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* También debe estar Hello las máquinas virtuales de la configuración de alta disponibilidad de Hola Hola misma subred. Resolución de nombres entre diferentes subredes de hello no es posible en las implementaciones que solo en la nube, la resolución IP solo funcionará. Al utilizar la conectividad ExpressRoute de sitio a sitio para las implementaciones entre locales, ya deberá haber establecida una red con al menos una subred. Resolución de nombres se hará según toohello local las directivas de AD y la infraestructura de red.

[comment]: <> (MSSedusch TODO Test if still true in ARM)

#### <a name="ip-addresses"></a>Direcciones IP
Se recomienda encarecidamente toosetup hello las máquinas virtuales para las configuraciones de alta disponibilidad de una manera flexible. Confiar en el asociado de HA de IP direcciones tooaddress Hola dentro de la configuración de alta disponibilidad de hello no es confiable en Azure, a menos que se utilizan direcciones IP estáticas. Hay dos conceptos de apagado en Azure:

* Apagado a través del Portal de Azure o Azure PowerShell cmdlet Stop-AzureRmVM: en este caso Hola Máquina Virtual obtiene cierre y desasigne. Su cuenta de Azure ya no se le cobrará por esta máquina virtual para que hello únicos gastos que se le cobrará son para el almacenamiento de hello usa. Sin embargo, si dirección IP privada de Hola de interfaz de red de hello no es estático, se libera la dirección IP de hello y no se garantiza que esa interfaz de red de hello Obtiene la dirección IP antigua Hola asigna nuevo después del reinicio del programa Hola a máquina virtual. Realizar Hola apagado a través del Portal de Azure de Hola o automáticamente hará que la cancelación de la asignación mediante una llamada a Stop-AzureRmVM. Si no desea que uso AzureRmVM Stop - StayProvisioned de la máquina de hello toodeallocat
* Si apaga Hola máquina virtual desde un nivel de sistema operativo, Hola VM obtiene apagar y de asignación no se cancela. Sin embargo, en este caso, su cuenta de Azure todavía se cobrará por Hola de máquina virtual, a pesar del hecho de Hola que está apagada. En tal caso, hello asignación de tooa de dirección IP de hello VM detenida permanecerá intacta. Cerrando Hola VM desde dentro no automáticamente forzará la cancelación de la asignación.

Incluso en escenarios entre locales, de forma predeterminada un apagado y la cancelación de la asignación significan una desasignación del programa Hola a direcciones IP de Hola de máquina virtual, incluso si las directivas locales en la configuración de DHCP son diferentes.

* Hello excepción es si uno asigna una interfaz de red estática de tooa dirección IP como se describe [aquí][virtual-networks-reserved-private-ip].
* En tal caso dirección IP de hello permanece fija mientras no se elimina la interfaz de red de Hola.

> [!IMPORTANT]
> En orden tookeep Hola toda implementación simple y fácil de administrar, desactive la recomendación es toosetup Hola Hola colaborar en una configuración de HA de DBMS o recuperación ante desastres en Azure de forma que hay una resolución de nombres funciona entre Hola implicadas diferentes máquinas virtuales de las máquinas virtuales.
>
>

## <a name="deployment-of-host-monitoring"></a>Implementación de funcionalidades de supervisión de hosts
Para el uso productivo de las aplicaciones SAP en máquinas virtuales de Azure, SAP requiere host tooget Hola capacidad que datos de supervisión de hosts físicos que Hola ejecutan Hola máquinas virtuales de Azure. Se requiere un nivel de revisión específico del agente de host de SAP que permita esta funcionalidad en SAPOSCOL y el agente de host de SAP. nivel de revisión exacto de Hola se documenta en la nota de SAP [1409604].

Para obtener detalles de hello con respecto a la implementación de componentes que proporcionan los host datos tooSAPOSCOL y HostAgent de SAP y Hola administración del ciclo de vida de esos componentes, consulte toohello [Guía de implementación][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Detalles tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>IaaS de SQL Server
A partir de Microsoft Azure, puede migrar fácilmente aplicaciones existentes de SQL Server depende de la plataforma de Windows Server tooAzure máquinas virtuales. SQL Server en una máquina Virtual permite tooreduce Hola costo total de propiedad de implementación, administración y mantenimiento de aplicaciones empresariales al migrar fácilmente estas tooMicrosoft aplicaciones Azure. Con SQL Server en una máquina Virtual de Azure, los administradores y desarrolladores todavía pueden usar Hola mismas herramientas de desarrollo y administración que están disponibles en local.

> [!IMPORTANT]
> Tenga en cuenta que no estamos analizando Microsoft Azure SQL Database, que es una plataforma como una oferta de servicio de hello plataforma Microsoft Azure. análisis de Hello en este documento es sobre la ejecución de producto de SQL Server de hello tal y como se le conoce para las implementaciones locales en máquinas virtuales de Azure, Hola sacar provecho de infraestructura como una capacidad de servicio de Azure. Las funcionalidades de bases de datos de estas dos ofertas son diferentes y no deben combinarse. Consulte también: <https://azure.microsoft.com/services/sql-database/>.
>
>

Se recomienda encarecidamente tooreview [esto] [ virtual-machines-sql-server-infrastructure-services] documentación antes de continuar.

Hola siguientes piezas de secciones de partes de la documentación de hello en el vínculo de hello anterior se agregan y se ha mencionado. Se describen de forma más detallada algunos conceptos y se mencionan consideraciones sobre SAP. Sin embargo, se recomienda encarecidamente toowork en la documentación de hello sobre primero antes de leer la documentación específica de SQL Server de Hola.

Debe conocer información específica sobre SQL Server en IaaS antes de continuar:

* **Acuerdo de Nivel de Servicio de máquina virtual**: hay un Acuerdo de Nivel de Servicio para Virtual Machines que se ejecuta en Azure que puede encontrarse aquí: <https://azure.microsoft.com/support/legal/sla/>.  
* **Soporte para versiones de SQL**: para los clientes de SAP, prestamos soporte para SQL Server 2008 R2 y posteriores en las máquinas virtuales de Microsoft Azure. No se prestará soporte para versiones anteriores. Revise esta [declaración de soporte](https://support.microsoft.com/kb/956893) general para más información. Tenga en cuenta que, a rasgos generales, Microsoft también presta soporte para SQL Server 2008. Sin embargo, debido a la funcionalidad toosignificant para SAP que se introdujo con SQL Server 2008 R2, SQL Server 2008 R2 es la versión mínima de Hola para SAP. Tenga en cuenta que SQL Server 2012 y 2014 se amplió con una integración más profunda en el escenario de IaaS de hello (por ejemplo, realizar copias de seguridad directamente frente al almacenamiento de Azure). Por lo tanto, se restringen este tooSQL papel Server 2012 y 2014 con su nivel de revisión más reciente de Azure.
* **Soporte para características de SQL**: se presta soporte para la mayoría de las características de SQL Server en las máquinas virtuales de Microsoft Azure, aunque con algunas excepciones. **No se presta soporte para los clústeres de conmutación por error de SQL Server que usan discos compartidos**.  Las tecnologías distribuidas, como la creación de reflejo de base de datos, los grupos de disponibilidad AlwaysOn, la replicación, el trasvase de registros y Service Broker, se admiten en una única región de Azure. SQL Server AlwaysOn también se admite entre diferentes regiones, como se documenta aquí:  <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Hola de revisión [declaración de soporte técnico](https://support.microsoft.com/kb/956893) para obtener más detalles. Un ejemplo de cómo toodeploy que se muestra una configuración de AlwaysOn en [esto] [ virtual-machines-workload-template-sql-alwayson] artículo. Asimismo, consulte Hola prácticas recomendadas documentadas [aquí][virtual-machines-sql-server-infrastructure-services]
* **El rendimiento de SQL**: se está seguros de que Microsoft Azure máquinas virtuales hospedadas realizará muy bien en las ofertas de virtualización de nube pública de comparación tooother, pero los resultados individuales pueden variar. Consulte [este][virtual-machines-sql-server-performance-best-practices] artículo.
* **Uso de imágenes de Azure Marketplace**: toodeploy de manera más rápida de hello una nueva máquina virtual de Azure de Microsoft es toouse una imagen de hello Azure Marketplace. Hay imágenes en hello Azure Marketplace que contienen SQL Server. imágenes de Hello SQL Server ya está instalado no se puede utilizar inmediatamente para las aplicaciones de SAP NetWeaver. motivo de Hello es la intercalación predeterminada del servidor SQL de Hola se instala dentro de esas imágenes y no la intercalación del Hola requeridos por los sistemas SAP NetWeaver. En Ordenar toouse dichas imágenes, compruebe los pasos de hello documentados en el capítulo [utilizando un servidor SQL Server imágenes fuera de Microsoft Azure Marketplace hello][dbms-guide-5.6].
* Para más información, consulte [Precios de Azure](https://azure.microsoft.com/pricing/) . Hola [Guía de administrador de licencias de SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) y [Guía de administrador de licencias de SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) también son un recurso importante.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Directrices de configuración de SQL Server para SAP relacionadas con las instalaciones de SQL Server en máquinas virtuales de Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Recomendaciones sobre la estructura de máquina virtual y VHD para SAP relacionadas con las implementaciones de SQL Server
Con arreglo a la descripción general de hello, se encuentra o se instala en unidad del sistema Hola de disco duro virtual base de la máquina virtual de hello ejecutables de SQL Server (la unidad C:\).  Normalmente, la mayoría de las bases de datos del sistema de SQL Server de hello no se utiliza en un nivel alto por carga de trabajo de SAP NetWeaver. Por lo tanto, hello las bases de datos de SQL Server (master, msdb y model) pueden permanecer en hello también la unidad C:\. Una excepción podría ser tempdb, que en caso de hello de algunos SAP ERP y todas las cargas de trabajo de BW, podría requerir mayor volumen de datos o volumen de operaciones de E/S que no cabe en hello de la VM original. En estos sistemas, debe realizarse Hola pasos:

* Mover toohello de los archivos de datos de tempdb primarios Hola misma unidad lógica que los archivos de datos principal de Hola de base de datos SAP de Hola.
* Agregue cualquier tooeach de archivos de datos de tempdb adicionales del programa Hola a otras unidades lógicas que contiene un archivo de datos de la base de datos de usuario SAP de Hola.
* Agregar Hola tempdb logfile toohello unidad lógica que contiene el archivo de registro de hello usuario de base de datos.
* **Exclusivamente para los tipos VM que usan SSD local** en datos de tempdb del nodo de proceso de Hola y registro de archivos podrían estar colocados en hello unidad D:\. No obstante, puede ser recomendable toouse varios archivos de datos de tempdb. Tenga en cuenta los volúmenes de unidad D:\ son diferentes en función de hello tipo de máquina virtual.

Estas configuraciones permiten tempdb tooconsume más espacio de unidad del sistema hello es capaz de tooprovide. En el tamaño correcto de tempdb de orden toodetermine hello, se pueden comprobar los tamaños de tempdb de hello en los sistemas existentes que se ejecutan de forma local. Además, dicha configuración permitiría a números de IOPS frente a tempdb que no se pueden proporcionar con la unidad del sistema Hola. De nuevo, sistemas que se ejecutan en local pueden cargas de trabajo de toomonitor usa E/S frente a tempdb para que pueda obtener los números de IOPS de hello espera toosee en tempdb.

Una configuración de máquina virtual que ejecuta SQL Server con una base de datos SAP y donde se colocan los datos de tempdb y el archivo de registro de tempdb en la unidad D:\ de hello sería:

![Configuración de referencia de máquinas virtuales IaaS de Azure en SAP][dbms-guide-figure-300]

Tenga en cuenta que esa unidad D:\ hello tiene distintos tamaños depende Hola tipo de máquina virtual. Dependiente de requisito de tamaño de Hola de tempdb podrían ser datos de tempdb de toopair forzada y archivos de registro con hello la base de datos de SAP y archivos de registro en casos donde la unidad D:\ es demasiado pequeño.

#### <a name="formatting-hello-vhds"></a>Dar formato a discos duros virtuales de Hola
Para hello tamaño de bloque NTFS para discos duros virtuales que contiene datos de SQL Server y de registro de SQL Server los archivos deben estar 64K. No hay ningún Hola de tooformat necesidad unidad D:\. ya que este proceso se ha realizado previamente.

En orden toomake seguro de que hello restauración o la creación de bases de datos no inicializan los archivos de datos de hello al poner ceros en contenido de Hola de archivos de hello, uno debe asegurarse de que se está ejecutando el servicio de SQL Server de Hola Hola usuario contexto tiene un permiso determinado. Normalmente, los usuarios del grupo de administrador de Windows hello tienen estos permisos. Si Hola servicio SQL Server se ejecuta en el contexto de usuario de Hola de usuario de administrador distinto de Windows, deberá tooassign ese derecho de usuario 'Realizar tareas de mantenimiento del volumen' hello de usuario.  Ver detalles de hello en este artículo de Microsoft Knowledge Base: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Impacto de la compresión de las bases de datos
En configuraciones donde el ancho de banda de E/S puede convertirse en un factor restrictivo, todas las medidas que reduzca las IOPS podrían ayudar a cargas de trabajo de toostretch Hola puede ejecutar en un escenario IaaS como Azure. Por lo tanto, si no ha hecho todavía, aplicar compresión de página de SQL Server se recomienda por SAP y Microsoft antes de cargar una SAP existente tooAzure las bases de datos.

Hola recomendación tooperform compresión de base de datos antes de cargar tooAzure viene dada por dos motivos:

* cantidad de Hola de toobe de datos cargado es menor.
* duración de Hello de la ejecución de la compresión de hello es más corta, suponiendo que uno puede utilizar hardware más fuerte con más CPU o mayor ancho de banda de E/S o menos latencia de E/S en local.
* Los tamaños de base de datos más pequeños podrían provocar los costos que no requiere herramientas para la asignación de disco

La compresión de las bases de datos funciona también correctamente en las máquinas virtuales de Azure de la misma forma que en local. Para obtener más detalles sobre cómo toocompress una base de datos de SAP SQL Server existente, visite: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>SQL Server 2014: almacenamiento de archivos directamente en Almacenamiento de blobs de Azure
SQL Server 2014 abre los archivos de base de datos de hello posibilidad toostore directamente en el almacén de blobs de Azure sin Hola "contenedor" de un disco duro virtual a su alrededor. Especialmente con el almacenamiento de Azure estándar o tipos VM más pequeños Esto habilita escenarios donde puede superar los límites de Hola de e/s por segundo que se pueden imponer un número limitado de discos duros virtuales que pueden ser tipos VM más pequeños toosome montada. Aunque esto funciona con las bases de datos de usuario, no lo hace con las de sistema de SQL Server. También funciona con los archivos de registro y de datos de SQL Server. Si desea que toodeploy un SAP SQL Server de base de datos en lugar de este modo, 'ajuste' en discos duros virtuales, tenga en cuenta los siguiente hello:

* Hola toobe de necesidades de cuenta de almacenamiento usada en Hola misma región de Azure como Hola uno que es hello toodeploy usado VM SQL Server se ejecuta en.
* Se aplican consideraciones enumeradas anteriormente en lo que respecta toodistribute discos duros virtuales a través de diferentes cuentas de almacenamiento de Azure para este método de también en las implementaciones. Significa Hola recuento de operaciones de E/S con límites de Hola de hello cuenta de almacenamiento de Azure.

[comment]: <> (MSSedusch TODO But this will use network bandwith and not storage bandwith, doesn't it?)

Los detalles acerca de este tipo de implementación se indican aquí: <https://msdn.microsoft.com/library/dn385720.aspx>.

En archivos de datos de orden toostore SQL Server directamente en almacenamiento Premium de Azure, deberá toohave un mínimo de SQL Server 2014 versión de revisión que se documenta aquí: <https://support.microsoft.com/kb/3063054>. Almacenar archivos de datos de SQL Server en almacenamiento de Azure estándar funciona con la versión de Hola publicada de SQL Server 2014. Sin embargo, muy mismas revisiones de hello contienen otra serie de correcciones que hacen uso directo Hola de almacenamiento de blobs de Azure para archivos de datos de SQL Server y las copias de seguridad más confiable. Por lo tanto, se recomienda toouse estas revisiones en general.

### <a name="sql-server-2014-buffer-pool-extension"></a>Extensión de grupo de búferes de SQL Server 2014
SQL Server 2014 introdujo una nueva característica denominada "extensión de grupo de búferes". Esta funcionalidad extiende el grupo de búferes de Hola de SQL Server que se mantiene en memoria con una caché de segundo nivel que esté respaldada por SSD local de un servidor o la máquina virtual. Esto permite tookeep un espacio de trabajo más grande de datos 'in memory'. Tooaccessing en comparación con acceso de almacenamiento de Azure estándar hello en extensión de hello del grupo de búferes de Hola que se almacena en las SSD locales de una VM de Azure es más rápido muchos factores.  Por lo tanto, aprovechando la unidad D:\ local de Hola de tipos VM de hello con excelente IOPS y el rendimiento podría ser un Hola de tooreduce de manera muy razonable IOPS cargar en el almacenamiento de Azure y mejorar drásticamente los tiempos de respuesta de las consultas. Esto sucede sobre todo cuando no se utiliza Premium Storage. En el caso de almacenamiento Premium y el uso de Hola de hello caché de lectura de Azure Premium en el nodo de proceso de hello, tal como se recomienda para los archivos de datos, no se esperan que ningún grandes diferencias. Razón es que las memorias caché (SQL Server Buffer Pool Extension y caché de lectura de almacenamiento Premium) utilizan discos locales de Hola Hola de nodos de ejecución.
Para más información sobre esta funcionalidad, consulte esta documentación: <https://msdn.microsoft.com/library/dn133176.aspx>.

### <a name="backuprecovery-considerations-for-sql-server"></a>Consideraciones de copia de seguridad y recuperación en SQL Server
Al implementar SQL Server en Azure, se debe revisar la metodología de copia de seguridad. Incluso si el sistema de hello no es un sistema productivo, base de datos SAP de hello hospedada por SQL Server debe hacer copia periódicamente. Puesto que el almacenamiento de Azure mantiene tres imágenes, una copia de seguridad ahora es menos importante en sentido toocompensating un bloqueo de almacenamiento. razón de prioridad de Hello para el mantenimiento de un plan de copia de seguridad y recuperación adecuado es mayor que compensar los errores lógicos/manuales al proporcionar capacidades de recuperación de tiempo. Por lo que el objetivo de hello es tooeither usar copias de seguridad toorestore Hola base de datos nuevo tooa determinado punto en tiempo o toouse Hola copias de seguridad en Azure tooseed otro sistema mediante la copia de base de datos existente de Hola. Por ejemplo, podría transferir desde una instalación de sistema de 3 niveles 2 niveles SAP configuración tooa de hello mismo sistema mediante la restauración de una copia de seguridad.

Hay tres maneras diferentes toobackup SQL Server tooAzure almacenamiento:

1. SQL Server 2012 CU4 y la dirección URL tooa de forma nativa copia de seguridad de bases de datos de mayor can. Esto se detalla en el blog de hello [nueva funcionalidad de las mejoras de copia de seguridad y restauración de SQL Server 2014 – parte 5 –](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Consulte el capítulo [SQL Server 2012 SP1 CU4 y versiones posteriores][dbms-guide-5.5.1].
2. TooSQL anterior de las versiones de SQL Server 2012 CU4 puede usar un tooa de toobackup de funcionalidad de redirección VHD y básicamente avanzar la secuencia de escritura de hello hacia una ubicación de almacenamiento de Azure que se ha configurado. Consulte el capítulo [SQL Server 2012 SP1 CU3 y versiones anteriores][dbms-guide-5.5.2].
3. método final Hello es tooperform un comando de toodisk de copia de seguridad convencional de SQL Server en un dispositivo de disco VHD.  Esto es idéntico toohello patrón de implementación de local y no se describe en detalle en este documento.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 y versiones posteriores
Esta funcionalidad permite el almacenamiento de blobs de copia de seguridad tooAzure toodirectly. Sin este método, deben realizar backup tooother discos duros virtuales de Azure que consumiría capacidad de disco duro virtual e IOPS. idea Hello es básicamente lo siguiente:

 ![Uso de copias de seguridad de SQL Server 2012 tooMicrosoft BLOB de almacenamiento de Azure][dbms-guide-figure-400]

ventaja de Hello en este caso es que no es necesario las copias de seguridad de SQL Server de toospend discos duros virtuales toostore en. Por lo que tiene menos discos duros virtuales asignados y ancho de banda completo Hola de VHD IOPS se puede utilizar para los archivos de datos y de registro. Tenga en cuenta que el tamaño máximo de Hola de una copia de seguridad es limitado tooa máximo de 1 TB tal como se describe en la sección "Limitaciones" de hello en este artículo: <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. Si el tamaño de copia de seguridad de hello, a pesar de usar compresión de copia de seguridad de SQL Server supera 1 TB de tamaño, Hola funcionalidad descrita en el capítulo [SQL Server 2012 SP1 CU3 y versiones anteriores] [ dbms-guide-5.5.2] en este documento debe toobe utiliza.

[Documentación relacionada con](https://msdn.microsoft.com/library/dn449492.aspx) que describen la restauración de Hola de bases de datos de copias de seguridad en el almacén de blobs de Azure recomienda no toorestore directamente desde el almacén de blobs de Azure si las copias de seguridad de hello es > 25 GB. recomendación de Hello en este artículo simplemente se basa en las consideraciones de rendimiento y no debido a restricciones de toofunctional. Por lo tanto, pueden aplicarse distintas condiciones en cada caso.

Puede encontrar documentación sobre cómo configurar y utilizar este tipo de copia de seguridad en [este](https://msdn.microsoft.com/library/dn466438.aspx) tutorial.

Un ejemplo de hello secuencia de pasos que se puede leer [aquí](https://msdn.microsoft.com/library/dn435916.aspx).

Automatizar las copias de seguridad, es de toomake mayor importancia seguro de que los BLOB de Hola para cada copia de seguridad tienen nombres diferentes. De lo contrario, se sobrescribirán y se interrumpe la cadena de restauración de Hola.

En orden no toomix las cosas entre los distintos tipos de copias de seguridad de hello 3, es aconsejable toocreate diferentes contenedores cuenta de almacenamiento de hello usada para las copias de seguridad. contenedores de Hello podrían ser por VM solo o por tipo de copia de seguridad y la máquina virtual. Hola esquema podría verse como:

 ![Usar copias de seguridad de SQL Server 2012 tooMicrosoft BLOB de almacenamiento de Azure – contenedores diferentes en la cuenta de almacenamiento independiente][dbms-guide-figure-500]

En el ejemplo de Hola anteriormente, hello las copias de seguridad no se realizará en el mismo almacenamiento de información de la cuenta donde hello de Hola se implementan máquinas virtuales. Sería una nueva cuenta de almacenamiento específicamente para las copias de seguridad de Hola. Dentro de las cuentas de almacenamiento de hello, habría diferentes contenedores creados con una matriz de tipo hello de hello y copia de seguridad de nombre de máquina virtual. Dicha segmentación le resultará más fáciles tooadministrate hello las copias de seguridad de hello diferentes máquinas virtuales.

BLOBs de Hola se escriben directamente hello las copias de seguridad, no se agregan toohello recuento de hello discos duros virtuales de una máquina virtual. Por lo tanto, uno podría maximizar máximo de Hola de VHD montados de hello determinado VM SKU para datos de Hola y archivo de registro de transacciones y todavía ejecutar una copia de seguridad en un contenedor de almacenamiento.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 y versiones anteriores
Hola primer paso que debe realizar en orden tooachieve una copia de seguridad directamente frente al almacenamiento de Azure sería toodownload Hola msi que está vinculado demasiado[esto](https://www.microsoft.com/download/details.aspx?id=40740) artículo KBA.

Descargue el archivo de instalación de hello x64 y documentación de Hola. archivo Hello va a instalar un programa llamado: 'Copia de seguridad de Microsoft SQL Server tooMicrosoft herramienta de Azure'. Leer documentación de Hola de producto de hello exhaustivamente.  herramienta de Hello funciona básicamente de hello siguiente forma:

* De hello lado de SQL Server, se define una ubicación de disco de copia de seguridad de SQL Server de hello (no use la unidad D:\ de Hola para esto).
* Hola herramienta le permitirá toodefine reglas que pueden ser usado toodirect diferentes tipos de contenedores de almacenamiento de Azure de toodifferent de las copias de seguridad.
* Una vez que las reglas de hello, herramienta de hello redirigirá secuencia de escritura de Hola de hello tooone copia de seguridad de los discos duros virtuales/discos de hello toohello ubicación de almacenamiento de Azure que se definió anteriormente.
* Hola herramienta dejará un pequeño archivo stub de unos pocos KB de tamaño en hello VHD/disco que se ha definido para hello SQL Server copia de seguridad. **Este archivo debe dejarse en la ubicación de almacenamiento de Hola, ya que es necesario toorestore nuevo desde el almacenamiento de Azure.**
  * Si ha perdido el archivo de código auxiliar de hello (por ejemplo, debido a la pérdida Hola del medio de almacenamiento que contiene el archivo de código auxiliar de hello) y ha elegido la opción de Hola de copia de seguridad tooa cuenta de almacenamiento de Azure de Microsoft, puede recuperar el archivo de código auxiliar de Hola a través del almacenamiento de Azure de Microsoft por descargarlo del contenedor de almacenamiento de hello en el que se coloca. A continuación debería colocar el archivo de código auxiliar de hello en una carpeta en el equipo local de Hola donde hello herramienta es configurado toohello toodetect y la carga mismo contenedor con hello misma contraseña de cifrado si se usa el cifrado con la regla original Hola.

Esto significa que el esquema de hello tal y como se describió anteriormente para las versiones más recientes de SQL Server se puede colocar en su lugar, así como para las versiones de SQL Server que no se permite una dirección directa de una ubicación de almacenamiento de Azure.

Este método no debe usarse con las versiones más recientes de SQL Server que admiten copias de seguridad nativas en Almacenamiento de Azure. Las excepciones están donde las limitaciones de copia de seguridad nativa de hello en Azure están bloqueando la ejecución de copia de seguridad nativa en Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Otras bases de datos de SQL Server de toobackup de posibilidades
Otras bases de datos de toobackup posibilidades es tooa de discos duros virtuales adicional tooattach VM que usan las copias de seguridad de toostore en. En tal caso necesitaría toomake seguro de que ese Hola discos duros virtuales no se ejecutan completa. Si ese es el caso de hello, necesitaría toounmount Hola VHD y por lo tanto toospeak 'archivo' y reemplácelo por un nuevo VHD vacío. Si dejan de funcionar esa ruta de acceso, es conveniente tookeep estos discos duros virtuales en diferentes cuentas de almacenamiento de Azure de Hola que Hola discos duros virtuales con archivos de base de datos de Hola.

Una segunda posibilidad es toouse una máquina virtual grande que puede tener muchos discos duros virtuales conectados. Por ejemplo, D14 con 32 VHD. Utilice toobuild de espacios de almacenamiento un entorno flexible donde puede crear recursos compartidos que se utilizan, a continuación, como destinos de copia de seguridad para distintos servidores DBMS Hola.

También puede consultar algunos procedimientos recomendados [aquí](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) .

#### <a name="performance-considerations-for-backupsrestores"></a>Consideraciones de rendimiento sobre copias de seguridad y restauraciones
Como en las implementaciones sin sistema operativo, rendimiento de la copia de seguridad/restauración depende de cuántos volúmenes pueden leerse en paralelo y qué rendimiento Hola de estos volúmenes podría ser. Además, Hola consumo de CPU utilizado por la compresión de copia de seguridad puede desempeñan un papel importante en las máquinas virtuales con solo los subprocesos de CPU de too8. Por lo tanto, se pueden asumir los siguientes puntos:

* Hello menos Hola número de discos duros virtuales utiliza archivos de datos de toostore hello, Hola Hola cuanto menor sea el rendimiento global en la lectura.
* Hola menor número de Hola de subprocesos de CPU en hello VM, Hola más graves repercusiones de Hola de compresión de copia de seguridad.
* Hello menos toowrite destinos (BLOB o VHD) Hola copia de seguridad en, Hola menor rendimiento Hola.
* Hola Hola menor tamaño de máquina virtual, Hola menor Hola rendimiento cuota de almacenamiento escribir y leer desde el almacenamiento de Azure. Independientemente de si las copias de seguridad de Hola se almacenan directamente en el Blob de Azure o si se almacenan en discos duros virtuales que nuevo se almacenan en Blobs de Azure.

Cuando se usa un BLOB de almacenamiento de Microsoft Azure como destino de copia de seguridad de hello en las versiones más recientes, están restringidas toodesignating solo una dirección URL de destino para cada copia de seguridad específica.

Pero cuando se usa hello 'copia de seguridad de Microsoft SQL Server tooMicrosoft herramienta de Azure' en las versiones anteriores, puede definir más de un destino de archivo. Con más de un destino, puede escalar la copia de seguridad de Hola y Hola rendimiento de copia de seguridad de hello es mayor. A continuación, esto resultaría en varios archivos así como en hello cuenta de almacenamiento de Azure. En nuestras pruebas, mediante varios destinos de archivo puede lograr un rendimiento Hola lo que se podría lograr con las extensiones de copia de seguridad de hello definitivamente implementadas desde SQL Server 2012 SP1 CU4 en. También no estén bloqueado por límite de 1TB de hello como en la copia de seguridad nativa de hello en Azure.

Sin embargo, tenga en cuenta, rendimiento de hello también es dependiente de ubicación de Hola de hello cuenta de almacenamiento de Azure que use para copia de seguridad de Hola. Una idea podría ser la cuenta de almacenamiento de hello toolocate en una región diferente de hello en que las máquinas virtuales se ejecutan. Por ejemplo, podría ejecutar la configuración de máquina virtual de hello en Europa occidental, pero colocar Hola cuenta de almacenamiento que usa tooback contra en Norte de Europa. Que por supuesto, tendrá efecto en el rendimiento de copia de seguridad de Hola o toogenerate no es probable que un rendimiento de 150MB/s como parece toobe posible en casos donde Hola almacenamiento de destino y Hola máquinas virtuales se ejecutan en hello mismo centro de datos regional.

#### <a name="managing-backup-blobs"></a>Gestión de blobs de copia de seguridad
Hay un copias de seguridad de requisito toomanage Hola por su cuenta. Puesto que la expectativa de hello es que se creará muchos blobs mediante la ejecución de las copias de seguridad del registro de transacciones con frecuencia, administración de esos blobs puede fácilmente sobrecargar Hola Portal de Azure. Por lo tanto, es recomendable tooleverage un explorador de almacenamiento de Azure. Hay varias buenas noticias disponibles los que pueden ayudar a toomanage una cuenta de almacenamiento de Azure

* Microsoft Visual Studio con Azure SDK instalado (<https://azure.microsoft.com/downloads/>)
* Explorador de Microsoft Azure Storage (<https://azure.microsoft.com/downloads/>)
* Herramientas de terceros

[comment]: <> (Todavía no se admite en ARM)
[comment]: <> (#### Azure VM backup)
[comment]: <> (Pueden que las máquinas virtuales de hello sistema SAP se copia mediante la funcionalidad de copia de seguridad de máquina Virtual de Azure. Copia de seguridad de máquina Virtual de Azure se introdujo al principio de año de hello 2015 y al mismo tiempo es un método estándar toobackup una máquina virtual completa en Azure. Copia de seguridad de Azure almacena las copias de seguridad de hello en Azure y permite una restauración de una máquina virtual de nuevo.)
[comment]: <> (Máquinas virtuales de las bases de datos de ejecución pueden ser copia de seguridad de forma coherente si admite de sistemas DBMS Hola Hola Windows VSS Volume Shadow Copy Service < https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> como SQL Server. Por lo mediante copia de seguridad de máquina virtual de Azure puede ser un tooa de tooget de manera que pueda restaurar copia de seguridad de una base de datos SAP. Sin embargo, tenga en cuenta que no se pueden realizar restauraciones de bases de datos a un momento dado con esta funcionalidad. Por lo tanto, la recomendación de hello es tooperform copias de seguridad de bases de datos con la funcionalidad DBMS en lugar de depender de copia de seguridad de máquina virtual de Azure.)
[comment]: <> (tooget familiarizado con copia de seguridad de máquina Virtual de Azure, empiece aquí < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Usar una imagen de SQL Server fuera de hello Microsoft Azure Marketplace
Microsoft ofrece VM en hello Azure Marketplace que ya contienen versiones de SQL Server. Para los clientes de SAP que requieren licencias para SQL Server y Windows, esto podría ser una necesidad de Hola de portada de oportunidad toobasically de licencias al activar máquinas virtuales con SQL Server ya instalado. En orden toouse este tipo de imágenes para SAP, Hola después consideraciones necesita toobe realizado:

* versiones de Hello SQL Server no son evaluación adquieren costos mayores que simplemente una VM 'Solo de Windows' implementada de Azure Marketplace. Consulte estos artículos toocompare: <https://azure.microsoft.com/pricing/details/virtual-machines/> y <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* Solo se pueden usar las versiones de SQL Server compatibles con SAP, como SQL Server 2012.
* intercalación de Hola Hola instancia de SQL Server que se instala en máquinas virtuales de Hola que se ofrecen en hello Azure Marketplace no es intercalación Hola SAP NetWeaver requiere toorun de instancia de SQL Server de Hola. Puede cambiar la intercalación de hello aunque con instrucciones Hola Hola pasos de la sección.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Cambiar Hola intercalación de SQL Server de una máquina virtual de Microsoft Windows y SQL Server
Puesto que las imágenes de SQL Server de hello en hello Azure Marketplace no se configuran de intercalación de hello toouse y es necesario para las aplicaciones de SAP NetWeaver, debe toobe cambia inmediatamente después de la implementación de Hola. Para SQL Server 2012, esto puede hacerse con hello lo siguiente en cuanto hello máquina virtual se ha implementado y un administrador puede toolog en hello implementa VM:

* Abra una ventana de comandos de Windows como administrador.
* Cambiar directorio de hello tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Ejecutar el comando hello: Setup.exe /QUIET/Action = REBUILDDATABASE/instancename = MSSQLSERVER /SQLSYSADMINACCOUNTS =`<local_admin_account_name`>/SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> es la cuenta de hello que se definió como cuenta de administrador de hello al implementar hello VM para hello primera vez a través de la Galería de Hola.

proceso de Hello solo debería tardar unos minutos. En orden toomake seguro si Hola paso terminó con el resultado correcto de hello, lleve a cabo Hola pasos:

* Abra SQL Server Management Studio.
* Abra una ventana de consulta.
* Ejecute hello comando sp_helpsort en la base de datos maestra de hello SQL Server.

resultado de Hello deseado debe ser similar:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Si este no es el resultado de hello, DETENGA la implementación de SAP e investigue por qué comando de instalación de hello no funcionaron según lo previsto. Implementación de aplicaciones de SAP NetWeaver en la instancia de SQL Server con distintas páginas de códigos de SQL Server de Hola mencionada anteriormente es **no** compatible.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>Alta disponibilidad de SQL Server para SAP en Azure
Como se mencionó anteriormente en este documento, no hay ningún almacenamiento de toocreate compartido posibilidad que es necesario para el uso de Hola de funcionalidad de alta disponibilidad de SQL Server más antigua de Hola. Esta funcionalidad instala dos o más instancias de SQL Server en un clúster de conmutación por error de servidor de Windows (WSFC) con un disco compartido para las bases de datos de usuario de hello (y finalmente tempdb). Se trata de método de hello mucho tiempo estándar de alta disponibilidad que también es compatible con SAP. Dado que Azure no admite el almacenamiento compartido, no se pueden realizar configuraciones de alta disponibilidad de SQL Server con una configuración de clúster de disco compartido. Sin embargo, muchos otros métodos de alta disponibilidad sigue siendo posible y se describen en las secciones siguientes de Hola.

[comment]: <> (Artículo sigue siendo tooASM de referencia)
[comment]: <> (Antes de leer tecnologías de hello específicas distintas de alta disponibilidad utilizables para SQL Server en Azure, hay un excelente documento que proporciona más detalles y punteros [[[[aquí] Virtual-Machines-SQL-Server-High-Availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>Trasvase de registros de SQL Server
Uno de los métodos de Hola de alta disponibilidad (HA) es el trasvase de registros de SQL Server. Si las máquinas virtuales de hello participa en la configuración de alta disponibilidad de hello tienen funciona la resolución de nombres, no hay ningún problema y el programa de instalación de hello en Azure no será diferente de cualquier configuración que se hace de forma local. No se recomienda toorely en sólo la resolución de IP. En lo que respecta toosetting seguridad de trasvase de registros y principios de hello alrededor de trasvase de registros, consulte en esta documentación:

<https://technet.microsoft.com/library/ms187103.aspx>

En orden tooreally lograr cualquier alta disponibilidad, es necesario toodeploy Hola máquinas virtuales que están dentro de este tipo una toobe de configuración de trasvase de registros dentro de Hola mismo conjunto de disponibilidad de Azure.

#### <a name="database-mirroring"></a>Creación de reflejo de la base de datos
Creación de reflejo de base de datos compatible con SAP (consulte la nota de SAP [965908]) se basa en la definición de un asociado de conmutación por error en la cadena de conexión de SAP Hola. Para los casos de hello entre entornos, suponemos que Hola dos máquinas virtuales están en hello mismo dominio y que se ejecuten instancias de SQL Server de hello dos de contexto de usuario de hello en son los usuarios de dominio y dispone de suficientes privilegios en instancias de SQL Server de hello dos implicados. Por lo tanto, el programa de instalación de Hola de creación de reflejo de base de datos de Azure no se diferencia entre una instalación típica de local/configuración.

Como de las implementaciones que solo en la nube, el método más sencillo de Hola es toohave otro dominio de la instalación en Azure toohave esas VM de DBMS (y VM de SAP dedicadas idealmente) dentro de un dominio.

Si un dominio no es posible, uno puede usar certificados para base de datos de hello extremos de creación de reflejo tal y como se describe aquí: <https://technet.microsoft.com/library/ms191477.aspx>

Un tutorial tooset telefónico Database Mirroring en Azure puede encontrarse aquí: <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>AlwaysOn
Como AlwaysOn es compatible con SAP local (vea la nota de SAP [1772688]), es compatible toobe utilizado en combinación con SAP en Azure. Hola hecho de que no pueda toocreate compartido discos en Azure no significa que uno no puede crear una configuración de clúster de conmutación por error de Windows Server (WSFC) de AlwaysOn entre diferentes máquinas virtuales. Sólo significa que no tiene Hola posibilidad toouse un disco compartido como un quórum en configuración de clúster de Hola. Por lo tanto, puede crear una configuración de AlwaysOn WSFC en Azure y simplemente no seleccionar tipo de quórum de hello, que utiliza el disco compartido. Hello entorno Azure esas máquinas virtuales se implementan en se debe resolver Hola máquinas virtuales por su nombre y hello las máquinas virtuales debe estar en hello mismo dominio. Lo mismo ocurre con las implementaciones entre locales y exclusivas de Azure. Hay algunas consideraciones especiales respecto a implementar Hola escucha de grupo de disponibilidad de SQL Server (no toobe confundirse con hello conjunto de disponibilidad de Azure) puesto que Azure no permite en este momento toosimply crear un objeto AD/DNS como sea posible en local. Por lo tanto, algunos pasos de instalación diferente son necesarios tooovercome Hola un comportamiento específico de Azure.

Estas son algunas de las consideraciones que hay que tener en cuenta al usar un agente de escucha de grupo de disponibilidad:

* Uso de un agente de escucha del grupo de disponibilidad solo es posible con Windows Server 2012 o Windows Server 2012 R2 como sistema operativo invitado de VM de Hola. Para Windows Server 2012 necesita toomake seguro de que se aplique esta revisión: <https://support.microsoft.com/kb/2854082>
* Para Windows Server 2008 R2 esta revisión no existe y AlwaysOn tendría toobe usa Hola igual manera que la creación de reflejo de base de datos mediante la especificación de un asociado de conmutación por error en la cadena de conexión de hello (mediante Hola SAP default.pfl parámetro dbs/mss/server: consulte la nota de SAP [965908]).
* Cuando usa un agente de escucha del grupo de disponibilidad, las máquinas virtuales de base de datos de hello necesario toobe conectado tooa dedicado equilibrador de carga. La resolución de nombres en las implementaciones que solo nube requeriría en todas las máquinas virtuales de un sistema SAP (servidores de aplicaciones, servidor DBMS y (A) servidor SCS) están en Hola misma red virtual o requeriría de un mantenimiento de hello SAP capa de aplicación del archivo etc\host de hello en orden tooget Hola nombres de las VM de VM de SQL Server de hello resuelto. En orden tooavoid que Azure asigne nuevas direcciones IP en casos donde ambas máquinas virtuales a propósito están cerrados, se deben asignar direcciones IP estáticas toohello interfaces de red de esas máquinas virtuales en la configuración de AlwaysOn hello (definición de una dirección IP estática se describe en [esto] [ virtual-networks-reserved-private-ip] artículo)

[comment]: <> (Blogs anteriores)
[comment]: <> (&lt;https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx&gt;, &lt;https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx&gt;)
* Hay pasos especiales necesarios cuando la creación de la configuración de clúster WSFC Hola donde clúster Hola necesita una dirección IP especial asignada, ya que Azure con su funcionalidad actual podría asignar el nombre del clúster Hola Hola la misma dirección IP que el clúster de Hola Hola nodos se crea en. Esto significa que un paso manual debe ser realizada tooassign otro clúster de toohello de dirección IP.
* Hola agente de escucha del grupo de disponibilidad va toobe creado en Azure con los puntos de conexión de TCP/IP que se asignan a las máquinas virtuales de toohello ejecutan Hola réplicas principales y secundarias del grupo de disponibilidad de Hola.
* Puede haber una necesidad toosecure estos extremos con ACL.

[comment]: <> (Blog antiguo PENDIENTE)
[comment]: <> (Hola pasos detallados y la necesidad de instalar una configuración de AlwaysOn en Azure se realizan de mejor manera cuando se lleva a través de hello tutorial disponible [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Preconfigurado AlwaysOn el programa de instalación a través de la Galería de Azure Hola < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (La creación de un agente de escucha del grupo de disponibilidad se describe mejor en [este][virtual-machines-windows-classic-ps-sql-int-listener] tutorial)
[comment]: <> (Los puntos de conexión de red de protección con ACL se explican mejor aquí:)
[comment]: <> (*    &lt;https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/&gt;)
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx&gt; )
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx&gt;)  
[comment]: <> (*    &lt;https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx&gt;)

Es posible toodeploy un grupo de disponibilidad AlwaysOn de SQL Server a través de diferentes regiones de Azure también. Esta funcionalidad aprovechan la conectividad de hello Azure VNet a Vnet ([detalles más][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Blog antiguo PENDIENTE)
[comment]: <> (instalación de Hola de grupos de disponibilidad AlwaysOn de SQL Server en este escenario se describe aquí: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Resumen de alta disponibilidad de SQL Server en Azure
Dados los hechos de Hola que el almacenamiento de Azure es proteger el contenido de hello, hay una menor tooinsist motivo en una imagen de reserva activa. Esto significa que el escenario de alta disponibilidad necesita tooonly protegerse contra Hola casos siguientes:

* Falta de disponibilidad de hello VM como un todo debido toomaintenance en clúster de servidores de hello en Azure u otras razones
* Problemas de software en la instancia de SQL Server de Hola
* Protección contra el error manual donde se eliminan los datos y se necesita realizar una recuperación a un momento dado

Examinando las tecnologías de asociación puede argumentar que los primeros dos casos de Hola pueden estar cubiertos por la creación de reflejo de base de datos o AlwaysOn, mientras que el tercer caso de hello solo puede cubrir mediante el trasvase de registros.

Necesitará toobalance Hola instalación más compleja de AlwaysOn, tooDatabase comparado de creación de reflejo, con las ventajas de Hola de AlwaysOn. Estas ventajas son las siguientes:

* Réplicas secundarias legibles
* Copias de seguridad de las réplicas secundarias
* Mejor escalabilidad
* Más de una réplica secundaria legible

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Resumen general de SQL Server para SAP en Azure
En esta guía se ofrecen muchas recomendaciones: le sugerimos que la lea más de una vez antes de planear la implementación de Azure. En general, no obstante, ser seguro hello toofollow superiores DBMS generales diez en puntos concretos de Azure:

[comment]: <> (2.3 higher throughput than what? ¿Que un disco duro virtual?)
1. Usar Hola última versión DBMS, como SQL Server 2014, que tiene Hola mayoría de las ventajas de Azure. Para SQL Server, se trata de SQL Server 2012 SP1 CU4 que incluiría la característica de Hola de copia de seguridad del almacenamiento de Azure. Sin embargo, junto con SAP le recomendamos al menos hello o SQL Server 2012 SP2 y SQL Server 2014 SP1 CU1 CU más reciente.
2. Planee cuidadosamente su panorama del sistema SAP en el diseño del archivo de datos de Azure toobalance hello y las restricciones de Azure:
   * No tiene demasiados discos duros virtuales, pero tiene suficiente tooensure puede alcanzar sus IOPS necesarias.
   * Recuerde que los valores de E/S también están limitados por cuenta de Azure Storage y que las cuentas de Storage están limitadas en cada suscripción de Azure ([más información][azure-subscription-service-limits]).
   * Solo seccione a través de los discos duros virtuales si necesita tooachieve un mayor rendimiento.
3. No instalar nunca software o ponga todos los archivos que se requieren la persistencia en hello unidad D:\ según sea no es permanente y nada en esta unidad se perderá en un reinicio de Windows.
4. No utilice el almacenamiento en caché de VHD de Azure para el almacenamiento estándar de Azure.
5. No utilice cuentas de almacenamiento con replicación geográfica de Azure.  Use la redundancia local para las cargas de trabajo de DBMS.
6. Usar datos de base de datos de la solución de su proveedor DBMS HA/DR de tooreplicate.
7. Use siempre la resolución de nombres, no confíe exclusivamente en las direcciones IP.
8. Use la compresión de base de datos más alto de hello posibles. Para SQL Server es la compresión de página.
9. Tenga cuidado al usar imágenes de SQL Server de hello Azure Marketplace. Si usas Hola SQL Server uno, debe cambiar la intercalación de la instancia de hello antes de instalar cualquier sistema SAP NetWeaver en él.
10. Instalar y configurar Hola supervisión de Host de SAP para Azure como se describe en [Guía de implementación][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Detalles tooSAP ASE en Windows
A partir de Microsoft Azure, puede migrar fácilmente su tooAzure de aplicaciones SAP ASE máquinas virtuales existente. SAP ASE en una máquina Virtual permite tooreduce Hola costo total de propiedad de implementación, administración y mantenimiento de aplicaciones empresariales al migrar fácilmente estas tooMicrosoft aplicaciones Azure. Con SAP ASE en una máquina Virtual de Azure, los desarrolladores y administradores la pueden seguir usando Hola mismas herramientas de desarrollo y administración que están disponibles en local.

Hay un SLA para hello máquinas virtuales de Azure que puede encontrarse aquí: <https://azure.microsoft.com/support/legal/sla>

Se está seguros de que Microsoft Azure máquinas virtuales hospedadas realizará muy bien en las ofertas de virtualización de nube pública de comparación tooother, pero los resultados individuales pueden variar. Ajustar el tamaño de los números de SAPS de hello diferentes SAP certificado SKU de la máquina virtual se proporcionará en una nota de SAP independiente de SAP [1928533].

Las instrucciones y las recomendaciones de uso de toohello de tener en cuenta de almacenamiento de Azure, la implementación de máquinas virtuales de SAP o la supervisión de SAP se aplican toodeployments de SAP ASE junto con las aplicaciones de SAP como se indica a lo largo de hello primeros cuatro capítulos de este documento.

### <a name="sap-ase-version-support"></a>Compatibilidad de versiones de SAP ASE
Actualmente, SAP admite la versión 16.0 de SAP ASE para poder utilizarse con productos de SAP Business Suite. Todas las actualizaciones para el servidor de SAP ASE o toobe de controladores JDBC y ODBC utiliza con SAP Business Suite productos se proporcionan únicamente a través de Hola SAP Service Marketplace en: <https://support.sap.com/swdc>.

Como para las instalaciones locales, descargar las actualizaciones para el servidor de SAP ASE de Hola o hello JDBC y controladores ODBC directamente desde sitios Web de Sybase. Para obtener información detallada sobre las revisiones que se pueden usar con los productos de SAP Business Suite en locales y máquinas virtuales de Azure vea Hola siguiendo las notas de SAP:

* [1590719]
* [1973241]

Información general sobre la ejecución de SAP Business Suite en SAP ASE puede encontrarse en hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Instrucciones de configuración de SAP ASE para SAP relacionadas con las instalaciones de SAP ASE en máquinas virtuales de Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Estructura de hello SAP ASE implementación
Con arreglo a la descripción general de hello, se encuentra o se instala en unidad del sistema Hola de disco duro virtual base de la máquina virtual de hello ejecutables de SAP ASE (la unidad c:\). Normalmente, la mayoría de hello SAP ASE herramientas del sistema ni las bases de datos no realmente aprovecha rígida cargas de trabajo de SAP NetWeaver. Hola, por tanto, sistema y las bases de datos de herramientas (master, model, saptools, sybmgmtdb, sybsystemdb) pueden permanecer en hello C:\drive.

Una excepción podría ser Hola base de datos temporal que contiene todas las tablas de trabajo y las tablas temporales creadas por SAP ASE, que en el caso de algunos SAP ERP y todas las cargas de trabajo de BW podría requerir mayor volumen de datos o volumen de operaciones de E/S que no cabe en hello original VHD de base de la máquina virtual (la unidad c:\).

Función hello versión de SAPInst/SWPM utiliza sistema de hello tooinstall, base de datos de hello podría contener:

* Una única tempdb de SAP ASE que se crea al instalar SAP ASE
* Una tempdb de SAP ASE creado mediante la instalación de SAP ASE y un saptempdb adicional creados por hello rutina de instalación de SAP
* Una tempdb de SAP ASE creado mediante la instalación de SAP ASE y un tempdb adicional que se ha creado manualmente (por ejemplo, después de la nota de SAP [1752266]) requisitos de toomeet ERP/BW tempdb específico

En el caso de ERP específica o todas las cargas de trabajo de BW tiene sentido, en tooperformance de tener en cuenta, dispositivos de tempdb tookeep Hola de hello además crean tempdb (SWPM o manualmente) en una unidad distinta C:\. Si no existe ningún tempdb adicional, se recomienda toocreate uno (Nota de SAP [1752266]).

Para este tipo hello sistemas se deben realizar los pasos siguientes para hello además creado tempdb:

* Mover Hola primera tempdb toohello primer dispositivo de base de datos SAP de Hola
* Agregar tooeach de dispositivos de tempdb de discos duros virtuales que contiene un dispositivo de base de datos SAP de Hola Hola

Esta tooeither de tempdb de configuración permite consumir más espacio de unidad del sistema hello es capaz de tooprovide. Como referencia se pueden comprobar los tamaños de dispositivo de tempdb de hello en los sistemas existentes que se ejecutan de forma local. O bien, dicha configuración permitiría a números de IOPS frente a tempdb que no se pueden proporcionar con la unidad del sistema Hola. Vuelva a sistemas que se ejecutan en local pueden toomonitor usa E/S cargas de trabajo en tempdb.

Nunca colocar los dispositivos de SAP ASE en hello unidad D:\ de hello máquina virtual. Esto también aplica toohello tempdb, incluso si los objetos de hello mantienen en tempdb Hola solo son temporales.

#### <a name="impact-of-database-compression"></a>Impacto de la compresión de las bases de datos
En configuraciones donde el ancho de banda de E/S puede convertirse en un factor restrictivo, todas las medidas que reduzca las IOPS podrían ayudar a cargas de trabajo de toostretch Hola puede ejecutar en un escenario IaaS como Azure. Por lo tanto, se recomienda encarecidamente toomake seguro de que se use la compresión de SAP ASE antes de cargar una tooAzure de base de datos SAP existente.

compresión de Hello recomendación tooperform antes de cargar tooAzure si ya no está implementado viene dada por varias razones:

* cantidad de Hola de tooAzure toobe carga de datos es inferior
* duración de Hola de ejecución de la compresión de hello es más corta, suponiendo que uno puede utilizar hardware más fuerte con más CPU o mayor ancho de banda de E/S o menos latencia de E/S en local
* Los tamaños de base de datos más pequeños podrían provocar los costos que no requiere herramientas para la asignación de disco

La compresión de datos y de LOB funciona en una máquina virtual hospedada en máquinas virtuales de Azure del mismo modo a como lo hace en un entorno local. Para obtener más detalles sobre cómo usar toocheck si ya está en la compresión en un ASE de SAP existente base de datos Compruebe la nota de SAP [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Uso de instancias de base de datos de DBACockpit toomonitor
Para los sistemas SAP que usan SAP ASE como plataforma de base de datos, es accesible como ventanas de explorador integrado en transacciones DBACockpit o como Webdynpro hello DBACockpit. Sin embargo Hola toda la funcionalidad de supervisión y administrar base de datos de Hola está disponible en la implementación de Webdynpro Hola de hello DBACockpit.

Como con local sistemas que tienen varios pasos necesario tooenable utilizada por la implementación de Webdynpro Hola de hello DBACockpit toda la funcionalidad de SAP NetWeaver. Siga la nota de SAP [1245200] tooenable Hola uso de webdynpros y generar Hola los necesarios. Cuando las instrucciones siguientes de Hola Hola anteriormente notas con que también configurará Hola Administrador de comunicación de Internet (icm) junto Hola toobe de puertos que se utilizan para las conexiones http y https. configuración predeterminada de Hola para http tiene el siguiente aspecto:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

y los vínculos de hello generados en transacciones DBACockpit tendrá un aspecto similar toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

En función de si y cómo Hola Hola de host de máquina Virtual de Azure sistema SAP está conectado a través de sitio a sitio, varios sitios o ExpressRoute (implementación entre locales) necesita toomake seguro de que ICM está usando un nombre de host completo que se puede resolver en hello equipo que va a probar tooopen Hola DBACockpit desde. Vea la nota de SAP [773830] toounderstand cómo determina ICM Hola nombre de host completo según los parámetros de perfil y parámetro de conjunto icm/host_name_full explícitamente si es necesario.

Si ha implementado Hola VM en un escenario solo en la nube sin conectividad entre entornos entre local y Azure, deberá toodefine una dirección IP pública y un domainlabel. formato de Hola de nombre DNS público de Hola de hello VM, a continuación, tendrá un aspecto similar al siguiente:

> `<custom domainlabel`&gt;.`<azure region`&gt;.cloudapp.azure.com
>
>

Obtener más detalles relacionados con puede encontrarse el nombre DNS de toohello [aquí][virtual-machines-azurerm-versus-azuresm].

Hola SAP perfil parámetro icm/host_name_full toohello nombre DNS del vínculo de Hola de hello Azure VM puede ser similar de la configuración:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

En este caso necesita toomake olvide:

* Agregar reglas de entrada toohello grupo de seguridad de red en hello Portal de Azure para los puertos TCP/IP de hello usa toocommunicate con ICM
* Agregue una configuración de Firewall de Windows de las reglas de entrada toohello para hello toocommunicate de puertos que usa TCP/IP con hello ICM

Para importa automáticamente de todas las correcciones disponibles, se recomienda tooperiodically aplicar versión SAP de hello corrección colección nota de SAP tooyour aplicables:

* [1558958]
* [1619967]
* [1882376]

Encontrará más información acerca de la cabina de DBA para SAP ASE Hola siguiendo las notas de SAP:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Consideraciones de copia de seguridad y recuperación para SAP ASE
Al implementar SAP ASE en Azure, debe revisar la metodología de copia de seguridad. Incluso si el sistema de hello no es un sistema productivo, base de datos SAP de hello hospeda SAP ASE debe hacer copia periódicamente. Puesto que el almacenamiento de Azure mantiene tres imágenes, una copia de seguridad ahora es menos importante en sentido toocompensating un bloqueo de almacenamiento. Hello razón principal para el mantenimiento de un plan de copia de seguridad y restauración correcta es mayor que compensar los errores lógicos/manuales al proporcionar capacidades de recuperación de tiempo. Por lo que el objetivo de hello es tooeither usar copias de seguridad toorestore Hola base de datos nuevo tooa determinado punto en tiempo o toouse Hola copias de seguridad en Azure tooseed otro sistema mediante la copia de base de datos existente de Hola. Por ejemplo, podría transferir desde una instalación de sistema de 3 niveles 2 niveles SAP configuración tooa de hello mismo sistema mediante la restauración de una copia de seguridad.

Copia de seguridad y restaurar una base de datos en Azure funciona Hola misma manera que lo hace en local. Consulte las notas de SAP

* [1588316]
* [1585981]

para obtener más información sobre la creación de configuraciones de volcado y la programación de copias de seguridad. Según las necesidades que se puede configurar y estrategia de base de datos y registro de volcados de memoria toodisk en uno de hello existente discos duros virtuales o agregar un disco duro virtual adicional para copia de seguridad de Hola.  riesgo de pérdida de datos en caso de error es Hola que tooreduce recomienda toouse un disco duro virtual donde no se encuentra ningún dispositivo de base de datos.

Además de compresión de datos y de LOB, SAP ASE también ofrece compresión de copias de seguridad. toooccupy menos espacio con la base de datos de Hola y de registro de volcados de memoria, se recomienda la compresión de copia de seguridad de toouse. Consulte la nota de SAP [1588316] para más información. Comprimir copia de seguridad de hello también es fundamental tooreduce cantidad de Hola de toobe de datos transferido si tiene previsto copias de seguridad de toodownload o discos duros virtuales que contiene la copia de seguridad volcados de hello local tooon de máquina Virtual de Azure.

No utilice la unidad D:\ como destino de los volcados de bases de datos o registros.

#### <a name="performance-considerations-for-backupsrestores"></a>Consideraciones de rendimiento sobre copias de seguridad y restauraciones
Como en las implementaciones sin sistema operativo, rendimiento de la copia de seguridad/restauración depende de cuántos volúmenes pueden leerse en paralelo y qué rendimiento Hola de estos volúmenes podría ser. Además, Hola consumo de CPU utilizado por la compresión de copia de seguridad puede desempeñan un papel importante en las máquinas virtuales con solo los subprocesos de CPU de too8. Por lo tanto, se pueden asumir los siguientes puntos:

* Hello menos Hola número de discos duros virtuales utilizar dispositivos de base de datos de toostore hello, hello Hola cuanto menor sea el rendimiento global en la lectura
* Hola menor número de Hola de subprocesos de CPU en hello VM, Hola más graves repercusiones de Hola de compresión de copia de seguridad
* Hola de copia de seguridad en Hello menos toowrite destinos (directorios de Stripe, discos duros virtuales), Hola menor rendimiento Hola

número de hello tooincrease de destinos toowrite toothere son dos opciones que pueden ser usar/combinan según sus necesidades:

* Creación de bandas volumen de destino de copia de seguridad de hello en varios discos duros virtuales montados en el rendimiento IOPS de orden tooimprove hello en ese volumen seccionado
* Crear una configuración de volcado en nivel de SAP ASE que usa más de un destino directory toowrite Hola volcado de memoria para

Anteriormente ya se trató en esta guía la sección de un volumen en varios VHD montados. Para obtener más información sobre el uso de varios directorios en la configuración de volcado de memoria de SAP ASE hello, consulte la documentación de toohello en sp_config_dump de procedimiento almacenado que es configuración de volcado de memoria de hello toocreate usado en hello [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Recuperación ante desastres con máquinas virtuales de Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replicación de datos con el servidor de replicación SAP Sybase
Con hello ASE de SAP de servidor de replicación de Sybase (SRS) de SAP proporciona una ubicación solución en espera semiactiva tootransfer base de datos las transacciones tooa está lejos de la forma asincrónica.

instalación de Hola y el funcionamiento de SRS funciona así funcionalmente en una máquina virtual hospedada en servicios de máquinas virtuales de Azure que lo hace en local.

Se ha previsto incluir ASE HADR a través de SAP Replication Server en una de las próximas versiones. Se someterá a pruebas con las plataformas de Microsoft Azure y se publicará para estas mismas en cuanto esté disponible.

## <a name="specifics-toosap-ase-on-linux"></a>Detalles tooSAP ASE en Linux
A partir de Microsoft Azure, puede migrar fácilmente su tooAzure de aplicaciones SAP ASE máquinas virtuales existente. SAP ASE en una máquina Virtual permite tooreduce Hola costo total de propiedad de implementación, administración y mantenimiento de aplicaciones empresariales al migrar fácilmente estas tooMicrosoft aplicaciones Azure. Con SAP ASE en una máquina Virtual de Azure, los desarrolladores y administradores la pueden seguir usando Hola mismas herramientas de desarrollo y administración que están disponibles en local.

Para implementar máquinas virtuales de Azure es importante tooknow Hola SLA oficiales que encontrará aquí: <https://azure.microsoft.com/support/legal/sla>

En la nota de SAP [1928533], se proporcionará información de tamaño de SAP y una lista de SKU para máquinas virtuales certificada por SAP. Se pueden encontrar documentos adicionales sobre el ajuste de tamaño de SAP para máquinas virtuales de Azure aquí <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> y aquí <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>.

Las instrucciones y las recomendaciones de uso de toohello de tener en cuenta de almacenamiento de Azure, la implementación de máquinas virtuales de SAP o la supervisión de SAP se aplican toodeployments de SAP ASE junto con las aplicaciones de SAP como se indica a lo largo de hello primeros cuatro capítulos de este documento.

Hello siguientes notas SAP dos incluyen información general sobre ASE en Linux y ASE en hello en la nube:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Compatibilidad de versiones de SAP ASE
Actualmente, SAP admite la versión 16.0 de SAP ASE para poder utilizarse con productos de SAP Business Suite. Todas las actualizaciones para el servidor de SAP ASE o toobe de controladores JDBC y ODBC utiliza con SAP Business Suite productos se proporcionan únicamente a través de Hola SAP Service Marketplace en: <https://support.sap.com/swdc>.

Como para las instalaciones locales, descargar las actualizaciones para el servidor de SAP ASE de Hola o hello JDBC y controladores ODBC directamente desde sitios Web de Sybase. Para obtener información detallada sobre las revisiones que se pueden usar con los productos de SAP Business Suite en locales y máquinas virtuales de Azure vea Hola siguiendo las notas de SAP:

* [1590719]
* [1973241]

Información general sobre la ejecución de SAP Business Suite en SAP ASE puede encontrarse en hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Instrucciones de configuración de SAP ASE para SAP relacionadas con las instalaciones de SAP ASE en máquinas virtuales de Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Estructura de hello SAP ASE implementación
Con arreglo a la descripción general de hello, archivos ejecutables de SAP ASE se deben encontrar o instalados en el sistema de archivos de raíz de Hola de hello VM (/sybase). Normalmente, la mayoría de hello SAP ASE herramientas del sistema ni las bases de datos no realmente aprovecha rígida cargas de trabajo de SAP NetWeaver. Hola, por tanto, sistema y las bases de datos de herramientas (master, model, saptools, sybmgmtdb, sybsystemdb) pueden permanecer en el sistema de archivos de raíz de hello así.

Una excepción podría ser Hola base de datos temporal que contiene todas las tablas de trabajo y las tablas temporales creadas por SAP ASE, que en el caso de algunos SAP ERP y todas las cargas de trabajo de BW podría requerir mayor volumen de datos o volumen de operaciones de E/S que no cabe en hello original Disco del sistema operativo de la máquina virtual.

Función hello versión de SAPInst/SWPM utiliza sistema de hello tooinstall, base de datos de hello podría contener:

* Una única tempdb de SAP ASE que se crea al instalar SAP ASE
* Una tempdb de SAP ASE creado mediante la instalación de SAP ASE y un saptempdb adicional creados por hello rutina de instalación de SAP
* Una tempdb de SAP ASE creado mediante la instalación de SAP ASE y un tempdb adicional que se ha creado manualmente (por ejemplo, después de la nota de SAP [1752266]) requisitos de toomeet ERP/BW tempdb específico

En el caso de ERP específica o todas las cargas de trabajo de BW tiene sentido, en tooperformance de tener en cuenta, dispositivos de tempdb tookeep Hola de hello además crean tempdb (SWPM o manualmente) en un sistema de archivos independiente que puede representarse mediante un disco de datos de Azure único o una RAID de Linux expansión de varios discos de datos de Azure. Si no existe ningún tempdb adicional, se recomienda toocreate uno (Nota de SAP [1752266]).

Para este tipo hello sistemas se deben realizar los pasos siguientes para hello además creado tempdb:

* Mover Hola primera tempdb directory toohello primer sistema de archivos de base de datos SAP de Hola
* Agregar tooeach de directorios de tempdb de discos duros virtuales que contiene un sistema de archivos de base de datos SAP de Hola Hola

Esta tooeither de tempdb de configuración permite consumir más espacio de unidad del sistema hello es capaz de tooprovide. Como referencia se pueden comprobar los tamaños de directorios de tempdb de hello en los sistemas existentes que se ejecutan de forma local. O bien, dicha configuración permitiría a números de IOPS frente a tempdb que no se pueden proporcionar con la unidad del sistema Hola. Vuelva a sistemas que se ejecutan en local pueden toomonitor usa E/S cargas de trabajo en tempdb.

Nunca colocar los directorios de SAP ASE en/mnt o/mnt/Resource de hello máquina virtual. Esto también aplica toohello tempdb, incluso si objetos Hola mantienen en tempdb Hola solo son temporales porque/mnt o/mnt/Resource es un espacio temporal de máquina virtual de Azure predeterminado que no es persistente. Pueden encontrar más detalles acerca de hello espacio temporal de máquina virtual de Azure en [este artículo][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Impacto de la compresión de las bases de datos
En configuraciones donde el ancho de banda de E/S puede convertirse en un factor restrictivo, todas las medidas que reduzca las IOPS podrían ayudar a cargas de trabajo de toostretch Hola puede ejecutar en un escenario IaaS como Azure. Por lo tanto, se recomienda encarecidamente toomake seguro de que se use la compresión de SAP ASE antes de cargar una tooAzure de base de datos SAP existente.

compresión de Hello recomendación tooperform antes de cargar tooAzure si ya no está implementado viene dada por varias razones:

* cantidad de Hola de tooAzure toobe carga de datos es inferior
* duración de Hola de ejecución de la compresión de hello es más corta, suponiendo que uno puede utilizar hardware más fuerte con más CPU o mayor ancho de banda de E/S o menos latencia de E/S en local
* Los tamaños de base de datos más pequeños podrían provocar los costos que no requiere herramientas para la asignación de disco

La compresión de datos y de LOB funciona en una máquina virtual hospedada en máquinas virtuales de Azure del mismo modo a como lo hace en un entorno local. Para obtener más detalles sobre cómo usar toocheck si ya está en la compresión en un ASE de SAP existente base de datos Compruebe la nota de SAP [1750510]. Consulte también la nota de SAP [2121797] para más información sobre la compresión de bases de datos.

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Uso de instancias de base de datos de DBACockpit toomonitor
Para los sistemas SAP que usan SAP ASE como plataforma de base de datos, es accesible como ventanas de explorador integrado en transacciones DBACockpit o como Webdynpro hello DBACockpit. Sin embargo Hola toda la funcionalidad de supervisión y administrar base de datos de Hola está disponible en la implementación de Webdynpro Hola de hello DBACockpit.

Como con local sistemas que tienen varios pasos necesario tooenable utilizada por la implementación de Webdynpro Hola de hello DBACockpit toda la funcionalidad de SAP NetWeaver. Siga la nota de SAP [1245200] tooenable Hola uso de webdynpros y generar Hola los necesarios. Cuando las instrucciones siguientes de Hola Hola anteriormente notas con que también configurará Hola Administrador de comunicación de Internet (icm) junto Hola toobe de puertos que se utilizan para las conexiones http y https. configuración predeterminada de Hola para http tiene el siguiente aspecto:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
>
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
>
>

y los vínculos de hello generados en transacciones DBACockpit tendrá un aspecto similar toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

En función de si y cómo Hola Hola de host de máquina Virtual de Azure sistema SAP está conectado a través de sitio a sitio, varios sitios o ExpressRoute (implementación entre locales) necesita toomake seguro de que ICM está usando un nombre de host completo que se puede resolver en hello equipo que va a probar tooopen Hola DBACockpit desde. Vea la nota de SAP [773830] toounderstand cómo determina ICM Hola nombre de host completo según los parámetros de perfil y parámetro de conjunto icm/host_name_full explícitamente si es necesario.

Si ha implementado Hola VM en un escenario solo en la nube sin conectividad entre entornos entre local y Azure, deberá toodefine una dirección IP pública y un domainlabel. formato de Hola de nombre DNS público de Hola de hello VM, a continuación, tendrá un aspecto similar al siguiente:

> `<custom domainlabel`&gt;.`<azure region`&gt;.cloudapp.azure.com
>
>

Obtener más detalles relacionados con puede encontrarse el nombre DNS de toohello [aquí][virtual-machines-azurerm-versus-azuresm].

Hola SAP perfil parámetro icm/host_name_full toohello nombre DNS del vínculo de Hola de hello Azure VM puede ser similar de la configuración:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

En este caso necesita toomake olvide:

* Agregar reglas de entrada toohello grupo de seguridad de red en hello Portal de Azure para los puertos TCP/IP de hello usa toocommunicate con ICM
* Agregue una configuración de Firewall de Windows de las reglas de entrada toohello para hello toocommunicate de puertos que usa TCP/IP con hello ICM

Para importa automáticamente de todas las correcciones disponibles, se recomienda tooperiodically aplicar versión SAP de hello corrección colección nota de SAP tooyour aplicables:

* [1558958]
* [1619967]
* [1882376]

Encontrará más información acerca de la cabina de DBA para SAP ASE Hola siguiendo las notas de SAP:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Consideraciones de copia de seguridad y recuperación para SAP ASE
Al implementar SAP ASE en Azure, debe revisar la metodología de copia de seguridad. Incluso si el sistema de hello no es un sistema productivo, base de datos SAP de hello hospeda SAP ASE debe hacer copia periódicamente. Puesto que el almacenamiento de Azure mantiene tres imágenes, una copia de seguridad ahora es menos importante en sentido toocompensating un bloqueo de almacenamiento. Hello razón principal para el mantenimiento de un plan de copia de seguridad y restauración correcta es mayor que compensar los errores lógicos/manuales al proporcionar capacidades de recuperación de tiempo. Por lo que el objetivo de hello es tooeither usar copias de seguridad toorestore Hola base de datos nuevo tooa determinado punto en tiempo o toouse Hola copias de seguridad en Azure tooseed otro sistema mediante la copia de base de datos existente de Hola. Por ejemplo, podría transferir desde una instalación de sistema de 3 niveles 2 niveles SAP configuración tooa de hello mismo sistema mediante la restauración de una copia de seguridad.

Copia de seguridad y restaurar una base de datos en Azure funciona Hola misma manera que lo hace en local. Consulte las notas de SAP

* [1588316]
* [1585981]

para obtener más información sobre la creación de configuraciones de volcado y la programación de copias de seguridad. Según las necesidades que se puede configurar y estrategia de base de datos y registro de volcados de memoria toodisk en uno de hello existente discos duros virtuales o agregar un disco duro virtual adicional para copia de seguridad de Hola.  riesgo de pérdida de datos en caso de error es Hola que tooreduce recomienda toouse un disco duro virtual donde no se encuentra ningún directorio o archivo de base de datos.

Además de compresión de datos y de LOB, SAP ASE también ofrece compresión de copias de seguridad. toooccupy menos espacio con la base de datos de Hola y de registro de volcados de memoria, se recomienda la compresión de copia de seguridad de toouse. Consulte la nota de SAP [1588316] para más información. Comprimir copia de seguridad de hello también es fundamental tooreduce cantidad de Hola de toobe de datos transferido si tiene previsto copias de seguridad de toodownload o discos duros virtuales que contiene la copia de seguridad volcados de hello local tooon de máquina Virtual de Azure.

No use/mnt espacio temporal de máquina virtual de Azure de Hola o/mnt/Resource como destino de volcado de memoria de base de datos o de registro.

#### <a name="performance-considerations-for-backupsrestores"></a>Consideraciones de rendimiento sobre copias de seguridad y restauraciones
Como en las implementaciones sin sistema operativo, rendimiento de la copia de seguridad/restauración depende de cuántos volúmenes pueden leerse en paralelo y qué rendimiento Hola de estos volúmenes podría ser. Además, Hola consumo de CPU utilizado por la compresión de copia de seguridad puede desempeñan un papel importante en las máquinas virtuales con solo los subprocesos de CPU de too8. Por lo tanto, se pueden asumir los siguientes puntos:

* Hello menos Hola número de discos duros virtuales utilizar dispositivos de base de datos de toostore hello, hello Hola cuanto menor sea el rendimiento global en la lectura
* Hola menor número de Hola de subprocesos de CPU en hello VM, Hola más graves repercusiones de Hola de compresión de copia de seguridad
* Hola de copia de seguridad en Hello menos toowrite destinos (Linux software RAID, discos duros virtuales), Hola menor rendimiento Hola

número de hello tooincrease de destinos toowrite toothere son dos opciones que pueden ser usar/combinan según sus necesidades:

* Creación de bandas volumen de destino de copia de seguridad de hello en varios discos duros virtuales montados en el rendimiento IOPS de orden tooimprove hello en ese volumen seccionado
* Crear una configuración de volcado en nivel de SAP ASE que usa más de un destino directory toowrite Hola volcado de memoria para

Anteriormente ya se trató en esta guía la sección de un volumen en varios VHD montados. Para obtener más información sobre el uso de varios directorios en la configuración de volcado de memoria de SAP ASE hello, consulte la documentación de toohello en sp_config_dump de procedimiento almacenado que es configuración de volcado de memoria de hello toocreate usado en hello [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Recuperación ante desastres con máquinas virtuales de Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replicación de datos con el servidor de replicación SAP Sybase
Con hello ASE de SAP de servidor de replicación de Sybase (SRS) de SAP proporciona una ubicación solución en espera semiactiva tootransfer base de datos las transacciones tooa está lejos de la forma asincrónica.

instalación de Hola y el funcionamiento de SRS funciona así funcionalmente en una máquina virtual hospedada en servicios de máquinas virtuales de Azure que lo hace en local.

En este momento no se admite ASE HADR a través de SAP Replication Server. Puede probar con y publicado para plataformas de Microsoft Azure en hello futuras.

## <a name="specifics-toooracle-database-on-windows"></a>Detalles tooOracle base de datos en Windows
Desde mediados de 2013, el software de Oracle es compatible con toorun de Oracle en Microsoft Windows Hyper-V y Azure. Lea este artículo tooget obtener más detalles sobre la compatibilidad general de Hola de Windows Hyper-V y Azure Oracle: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Después de la compatibilidad general de hello, escenario específico de Hola de aplicaciones de SAP que aprovechan las bases de datos de Oracle se admite también. Se denominan los detalles en esta parte del documento de Hola.

### <a name="oracle-version-support"></a>Compatibilidad de versiones de Oracle
Todos los detalles acerca de las versiones de Oracle y las versiones correspondientes de sistema operativo que se admiten para ejecutar SAP en Oracle en máquinas virtuales de Azure puede encontrarse en hello después de la nota de SAP [2039619]

Se puede encontrar información general sobre la ejecución de SAP Business Suite en Oracle en SCN: <https://scn.sap.com/community/oracle>.

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instrucciones de configuración de Oracle para instalaciones de SAP en máquinas virtuales de Azure
#### <a name="storage-configuration"></a>Configuración de almacenamiento
Solo se admiten versiones de Oracle de solo una versión que usen discos con formato NTFS. Todos los archivos de base de datos deben almacenarse en el sistema de archivos NTFS de hello en función de los discos VHD. Estos discos duros virtuales están montado toohello máquina virtual de Azure y se basan en el almacenamiento de blobs de página de Azure (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Las unidades de red o los recursos compartidos remotos como los servicios de archivos de Azure:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

**NO** son compatibles con los archivos de bases de datos de Oracle.

Usar discos duros virtuales de Azure basado en almacenamiento de blobs de página de Azure, hello las instrucciones realizadas en este documento en el capítulo [almacenamiento en caché para las máquinas virtuales y discos duros virtuales] [ dbms-guide-2.1] y [almacenamiento de Microsoft Azure] [ dbms-guide-2.3] aplicar toodeployments con hello base de datos de Oracle.

Como se explicó anteriormente en "parte general del documento de Hola" Hola, existen cuotas en el rendimiento IOPS para discos duros virtuales de Azure. las cuotas de Hello exacto se según el tipo de máquina virtual de hello usan. Dispone de una lista con los tipos de máquina virtual y sus cuotas [aquí][virtual-machines-sizes].

tooidentify Hola admite tipos de VM de Azure, consulte la nota tooSAP [1928533]

Como la cuota de IOPS actual de Hola por disco cumple los requisitos de hello, es posible toostore todos los archivos de base de datos de hello en una sola monta el VHD de Azure.

Si se requieren más de IOPS, se recomienda encarecidamente toouse ventana Storage Pools (solo disponible en Windows Server 2012 y versiones posteriores) o la creación de bandas para Windows 2008 R2 toocreate un dispositivo lógico grande en varios discos VHD montados de Windows. Consulte también el capítulo [RAID de software][dbms-guide-2.2] de este documento. Este enfoque simplifica el espacio en disco Hola Hola administración toomanage sobrecarga y evita el esfuerzo de hello toomanually distribuir archivos a través de varios discos duros virtuales montados.

#### <a name="backup--restore"></a>Copia de seguridad y restauración
Para copia de seguridad o restaurar la funcionalidad, Hola SAP BR * Tools para Oracle se admite en Hola mismo forma como en Hyper-V y sistemas operativos Windows Server estándar. Oracle Recovery Manager (RMAN) también se admite para toodisk de las copias de seguridad y restauración desde el disco.

#### <a name="high-availability"></a>Alta disponibilidad
[comment]: <> (vínculo hace referencia tooASM)
Oracle Data Guard se admite con fines de alta disponibilidad y recuperación ante desastres. Encontrará los detalles en [esta][virtual-machines-windows-classic-configure-oracle-data-guard] documentación.

#### <a name="other"></a>Otros
Todos los demás temas generales como conjuntos de disponibilidad de Azure y SAP supervisión de aplicaciones se aplican tal como se describe en hello tres primeros capítulos de este documento para las implementaciones de máquinas virtuales con hello base de datos de Oracle.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Características específicas para la base de datos de SAP MaxDB en Windows hello
### <a name="sap-maxdb-version-support"></a>Compatibilidad de versiones de SAP MaxDB
SAP actualmente admite SAP MaxDB versión 7.9 para su uso con productos basados en SAP NetWeaver en Azure. Todas las actualizaciones para el servidor de SAP MaxDB o toobe de controladores JDBC y ODBC utiliza con productos basados en SAP NetWeaver se proporcionan únicamente a través de hello SAP Service Marketplace en <https://support.sap.com/swdc>.
Se puede encontrar información general sobre la ejecución de SAP NetWeaver en SAP MaxDB en <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Versiones de Microsoft Windows y tipos de máquina virtual de Azure admitidos para SAP MaxDB DBMS
toofind Hola admite la versión de Microsoft Windows para SAP MaxDB DBMS en Azure, vea:

* [Matriz de disponibilidad de productos (PAM) SAP][sap-pam]
* Nota de SAP [1928533]

Se recomienda encarecidamente la versión más reciente de hello toouse del sistema operativo de hello Microsoft Windows, que es Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Documentación de SAP MaxDB disponible
Encontrará la lista de hello actualizado de documentación de SAP MaxDB Hola después de la nota de SAP [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instrucciones de configuración de SAP MaxDB para instalaciones de SAP en máquinas virtuales de Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Configuración de almacenamiento
Prácticas recomendadas de almacenamiento de Azure para SAP MaxDB siguen las recomendaciones generales Hola mencionadas en el capítulo [estructura de una implementación de RDBMS][dbms-guide-2].

> [!IMPORTANT]
> Al igual que otras bases de datos, SAP MaxDB también dispone de archivos de datos y de registro. Sin embargo, en la terminología de SAP MaxDB término correcto de hello es "volumen" (no "archivo"). Por ejemplo, existen volúmenes de datos y de registro de SAP MaxDB. No los confunda con los volúmenes de disco del sistema operativo.
>
>

En resumen, deberá hacer lo siguiente:

* Establecer la cuenta de almacenamiento de Azure de Hola que contiene volúmenes de datos y de registro a los MaxDB de SAP hello (es decir, archivos) demasiado**almacenamiento redundante Local (LRS)** según se haya especificado en el capítulo [almacenamiento de Microsoft Azure] [ dbms-guide-2.3].
* Ruta de acceso de E/S de hello independiente para volúmenes de datos de SAP MaxDB (es decir, archivos) de la ruta de acceso de E/S de Hola para volúmenes de registro (es decir, archivos). Esto significa que los volúmenes de datos de SAP MaxDB (es decir, archivos) tienen toobe instalado en una unidad lógica y los volúmenes de registro de SAP MaxDB (es decir, archivos) tienen toobe instalado en otra unidad lógica.
* Establecer Hola adecuadamente los archivos de caché para cada blob de Azure, dependiendo de si se usa para los volúmenes de datos o de registro de SAP MaxDB (es decir, archivos) y si se usa el estándar de Azure o almacenamiento de Azure Premium, tal como se describe en el capítulo [almacenamiento en caché para las máquinas virtuales] [ dbms-guide-2.1].
* Como la cuota de IOPS actual de Hola por disco cumple los requisitos de hello, es posible toostore todos los volúmenes de datos de hello en un solo VHD montados de Azure y también almacenan todos los volúmenes de registro de base de datos en otro VHD de Azure montada único.
* Si se necesitan más IOPS o espacio, se recomienda encarecidamente toouse Microsoft ventana Storage Pools (solo disponible en Microsoft Windows Server 2012 y versiones posteriores) o Microsoft Windows creación de bandas para Microsoft Windows 2008 R2 toocreate un dispositivo lógico de gran tamaño a través de varios discos VHD montados. Consulte también el capítulo [RAID de software][dbms-guide-2.2] de este documento. Este enfoque simplifica el espacio en disco Hola Hola administración toomanage sobrecarga y evita el trabajo de Hola de distribuir manualmente archivos entre varios discos duros virtuales montados.
* Para los requisitos de e/s por segundo más altos de hello, puede usar el almacenamiento de Azure Premium, que está disponible en la serie DS y GS-series las máquinas virtuales.

![Configuración de referencia de máquinas virtuales IaaS de Azure para SAP MaxDB DBMS][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Copia de seguridad y restauración
Al implementar SAP MaxDB en Azure, debe revisar la metodología de copias de seguridad. Incluso si el sistema de hello no es un sistema productivo, base de datos SAP de hello hospeda MaxDB de SAP debe hacer copia periódicamente. Puesto que Azure Storage guarda tres imágenes, ahora una copia de seguridad tiene menos relevancia en cuanto a la protección del sistema contra errores de almacenamiento y más relevancia en cuanto a errores operativos o administrativos. Hello razón principal para mantener una copia de seguridad correcta y el plan de restauración es por lo que puede compensar errores lógicos o manuales al proporcionar capacidades de recuperación a un punto en el momento. Por lo que es el objetivo de hello tooeither utilice copias de seguridad toorestore Hola base de datos tooa determinado punto en tiempo o toouse Hola copias de seguridad en Azure tooseed otro sistema mediante la copia de base de datos existente de Hola. Por ejemplo, podría transferir desde una instalación de sistema de 3 niveles 2 niveles SAP configuración tooa de hello mismo sistema mediante la restauración de una copia de seguridad.

Copia de seguridad y restaurar una base de datos en hello Azure funciona la misma manera que lo hace para sistemas locales, por lo que puede usar MaxDB de SAP estándar herramientas, que se describen en uno de los documentos de documentación de SAP MaxDB Hola de copia de seguridad/restauración aparecen en la nota de SAP [767598 ].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Consideraciones de rendimiento para copias de seguridad y restauraciones
Como en las implementaciones sin sistema operativo, el rendimiento de copia de seguridad y restauración es depende de cuántos volúmenes pueden leerse en paralelo y Hola rendimiento de esos volúmenes. Además, Hola consumo de CPU utilizado por la compresión de copia de seguridad puede desempeñar un papel importante en las máquinas virtuales con too8 subprocesos de CPU. Por lo tanto, se pueden asumir los siguientes puntos:

* Hola menor número de Hola de dispositivos de base de datos de VHD en uso toostore hello, Hola Hola general menor rendimiento de lectura
* Hola menor número de Hola de subprocesos de CPU en hello VM, Hola más graves repercusiones de Hola de compresión de copia de seguridad
* Hola menos destinos (directorios de Stripe, discos duros virtuales) toowrite Hola copia de seguridad, menor rendimiento de Hola Hola

número de hello tooincrease de destino es toowrite a, hay dos opciones que puede utilizar, posiblemente en combinación, dependiendo de sus necesidades:

* Dedicar volúmenes distintos a copias de seguridad
* Creación de bandas volumen de destino de copia de seguridad de hello en varios discos duros virtuales montados en el rendimiento IOPS de orden tooimprove hello en ese volumen de discos con bandas
* Disponer de dispositivos de discos lógicos dedicados distintos para:
  * Volúmenes (archivos) de copia de seguridad de SAP MaxDB
  * Volúmenes de datos de SAP MaxDB
  * Volúmenes de registros de SAP MaxDB

Ya se trató en el capítulo [RAID de software][dbms-guide-2.2] de este documento la sección de un volumen en varios discos duros virtuales montados.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Otros
También se aplican todos los demás temas generales como la supervisión de conjuntos de disponibilidad de Azure o SAP como se describe en hello tres primeros capítulos de este documento para las implementaciones de máquinas virtuales con la base de datos de SAP MaxDB Hola.
Otra configuración específica de SAP MaxDB son máquinas virtuales tooAzure transparente y se describen en distintos documentos aparecen en la nota de SAP [767598 ] y en estas notas SAP:

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Detalles de SAP liveCache en Windows
### <a name="sap-livecache-version-support"></a>Compatibilidad de versiones de SAP liveCache
La versión mínima de SAP liveCache que las máquinas virtuales de Azure admiten es **SAP LC/LCAPPS 10.0 SP 25**, incluida **liveCache 7.9.08.31** y **LCA-Build 25**, publicadas en **EhP 2 para SAP SCM 7.0** y en versiones posteriores.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Versiones de Microsoft Windows y tipos de máquina virtual de Azure admitidos para SAP liveCache DBMS
versión de Microsoft Windows hello admite toofind para liveCache SAP en Azure, vea:

* [Matriz de disponibilidad de productos (PAM) SAP][sap-pam]
* Nota de SAP [1928533]

Se recomienda encarecidamente la versión más reciente de hello toouse del sistema operativo de hello Microsoft Windows, que es Microsoft Windows 2012 R2.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instrucciones de configuración de SAP liveCache para instalaciones de SAP en máquinas virtuales de Azure
#### <a name="recommended-azure-vm-types"></a>Tipos de máquina virtual de Azure recomendadas
Como SAP liveCache es una aplicación que realiza cálculos muy grandes, cantidad de Hola y velocidad de CPU y RAM tiene una influencia importante en el rendimiento de liveCache SAP.

Para los tipos de máquina virtual de Azure Hola compatibles con SAP (Nota de SAP [1928533]), todos los recursos de CPU virtuales asignan toohello VM están respaldados por recursos dedicados de CPU físicos de hipervisor de Hola. No existe aprovisionamiento en exceso (y, por tanto, tampoco existe competencia por los recursos de CPU).

De forma similar, para todos los tipos de instancia virtual de Azure compatibles con SAP, memoria VM de hello es memoria física asignada de 100% toohello – en exceso (compromiso), por ejemplo, no se utiliza.

Desde esta perspectiva se recomienda encarecidamente toouse Hola nueva serie D o la máquina virtual de Azure de la serie DS (en combinación con el almacenamiento de Azure Premium) tipo, porque tienen procesadores más rápidos de 60% de Hola una serie. Para la carga máxima de memoria RAM y CPU de hello, puede usar serie G y máquinas virtuales de GS-series (en combinación con el almacenamiento de Azure Premium) con un procesador más reciente de Intel® Xeon® de hello E5 v3 familia, que tiene dos veces de memoria hello y cuatro veces Hola estado sólido almacenamiento en disco (SSD) de hello D / DS-series.

#### <a name="storage-configuration"></a>Configuración de almacenamiento
Como liveCache SAP se basa en tecnología de SAP MaxDB, todos Hola almacenamiento de Azure prácticas recomendadas mencionadas para SAP MaxDB en el capítulo [configuración de almacenamiento] [ dbms-guide-8.4.1] también son válidas para SAP liveCache.

#### <a name="dedicated-azure-vm-for-livecache"></a>Máquina virtual de Azure dedicada para liveCache
Como SAP liveCache usa de forma intensiva potencia de cálculo, para el uso productivo se recomienda encarecidamente toodeploy en una máquina Virtual de Azure dedicado.

![Máquina virtual de Azure dedicada para liveCache para un caso de uso productivo][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Copia de seguridad y restauración
Copia de seguridad y restauración, incluidas las consideraciones de rendimiento, ya se describe en capítulos de SAP MaxDB relevantes hello [de copia de seguridad y restauración] [ dbms-guide-8.4.2] y [consideraciones de rendimiento de copia de seguridad y restaurar][dbms-guide-8.4.3].

#### <a name="other"></a>Otros
Ya se describen todos los demás temas generales en hello pertinentes de SAP de MaxDB [esto] [ dbms-guide-8.4.4] capítulo.

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Características específicas para el servidor de contenido de SAP en Windows hello
Hola servidor de contenido de SAP es un contenido de toostore componente independiente basado en servidor, como documentos electrónicos en formatos diferentes. Hola servidor de contenido de SAP proporcionada por el desarrollo de la tecnología y es toobe usa todas las aplicaciones para las aplicaciones de SAP. Se instala en un sistema independiente. Contenido típico es aprendizaje material y la documentación del almacén de información o dibujos técnicos que se origina en hello mySAP PLM sistema de administración de documentos.

### <a name="sap-content-server-version-support"></a>Compatibilidad de versiones de SAP Content Server
SAP actualmente admite:

* **SAP Content Server** con la versión **6.50 (y superior)**
* **SAP MaxDB versión 7.9**
* **Microsoft IIS (Internet Information Server) versión 8.0 (y versiones posterior)**

Se recomienda encarecidamente versión más reciente de hello toouse del servidor de contenido de SAP, lo cual en tiempo de presentación de la escritura de este documento es **6.50 SP4**y la versión más reciente de Hola de **Microsoft IIS 8.5**.

Compruebe hello más reciente admitido versiones de servidor de contenido de SAP y Microsoft IIS en hello [matriz de disponibilidad de producto (PAM) de SAP][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Tipos de máquina virtual de Azure y Microsoft Windows admitidos con SAP Content Server
toofind out versión admitida de Windows para el servidor de contenido de SAP en Azure, vea:

* [Matriz de disponibilidad de productos (PAM) SAP][sap-pam]
* Nota de SAP [1928533]

Se recomienda encarecidamente versión más reciente de hello toouse de Microsoft Windows, lo cual en tiempo de presentación de la escritura de este documento es **Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instrucciones de configuración de SAP Content Server para las instalaciones de SAP en máquinas virtuales de Azure
#### <a name="storage-configuration"></a>Configuración de almacenamiento
Si configura los archivos de toostore de servidor de contenido de SAP en base de datos de SAP MaxDB hello, el almacenamiento de Azure todos los mejores prácticas recomendación mencionado para SAP MaxDB en el capítulo [configuración de almacenamiento] [ dbms-guide-8.4.1] también son válido para el escenario de servidor de contenido de SAP de Hola.

Si configura los archivos de toostore de servidor de contenido de SAP en el sistema de archivos de hello, es recomendable toouse una unidad lógica exclusiva. Uso de espacios de almacenamiento permite tooalso aumente el tamaño de disco lógico y el rendimiento de e/s por segundo, como se describe en el capítulo [RAID de Software][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>Ubicación de SAP Content Server
Servidor de contenido de SAP tiene toobe implementado en hello misma región de Azure y red virtual de Azure donde se implementa Hola sistema SAP. Son toodecide libre si desea que la misma máquina virtual que se ejecuta el sistema SAP de Hola Hola a toodeploy componentes de servidor de contenido de SAP en una VM de Azure dedicada o en.

![Máquina virtual de Azure dedicada para SAP Content Server][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Ubicación del SAP Cache Server
Hola servidor de caché de SAP es un componente basado en servidor adicional tooprovide obtienen acceso a too(cached) documentos localmente. Hola servidor de caché de SAP se almacena en memoria caché los documentos de Hola de un servidor de contenido de SAP. Se trata de tráfico de red de toooptimize si los documentos tienen toobe más de una vez recuperado desde distintas ubicaciones. por regla general Hello es que ese servidor de caché de SAP de hello tiene toobe toohello físicamente cerrar cliente que tiene acceso a Hola servidor de caché de SAP.

Dispone de dos opciones:

1. **Cliente es un sistema SAP de back-end** si un sistema SAP de back-end está configurado tooaccess servidor de contenido de SAP, dicho sistema SAP es un cliente. Como el sistema SAP y el servidor de contenido de SAP se implementan en hello misma región de Azure: Hola mismo centro de datos de Azure: son físicamente cerrar tooeach otro. Por lo tanto, no hay ningún toohave necesidad de un servidor de caché dedicado de SAP. Hola de acceso de clientes (Explorador de GUI de SAP o web) de interfaz de usuario de SAP sistema SAP directamente y hello SAP sistema recupera documentos de hello servidor de contenido de SAP.
2. **Cliente es un explorador de web local** Hola servidor de contenido de SAP puede ser configurado toobe hello web explorador obtener acceso directamente. En este caso, un explorador web que se ejecutan en local es un cliente de hello servidor de contenido de SAP. Centro de datos local y el centro de datos de Azure se colocan en diferentes ubicaciones físicas (lo ideal es que cerrar tooeach otros). El centro de datos local es tooAzure conectado a través de Azure VPN de sitio a sitio o ExpressRoute. Aunque ambas opciones ofrecen tooAzure de conexión de red VPN segura, conexión de red de sitio a sitio no ofrece un SLA de ancho de banda y la latencia de red entre el centro de datos de hello en local y Hola centro de datos de Azure. toospeed la toodocuments de acceso, puede hacer uno de hello siguientes:
   1. Instalar servidor de caché de SAP locales, cierre el Explorador de web local toohello (opción [esto] [ dbms-guide-900-sap-cache-server-on-premises] figura)
   2. Configurar ExpressRoute de Azure, que ofrece una conexión de red dedicada de alta velocidad y baja latencia entre el centro de datos local y el centro de datos de Azure.

![Opción tooinstall el servidor de caché de SAP local][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Copia de seguridad y restauración
Si configura toostore los archivos del servidor de contenido de SAP hello en la base de datos de SAP MaxDB hello, consideraciones de procedimiento y el rendimiento de copia de seguridad/restauración Hola ya se describen en el capítulo de SAP MaxDB [de copia de seguridad y restauración] [ dbms-guide-8.4.2] y el capítulo [consideraciones de rendimiento de copia de seguridad y restauración][dbms-guide-8.4.3].

Si configura toostore los archivos del servidor de contenido de SAP hello en el sistema de archivos de hello, una opción es tooexecute manual copia de seguridad y restauración de estructura de archivo completo de Hola donde se encuentran los documentos de Hola. TooSAP similar MaxDB copia de seguridad/restauración, es recomendable toohave un volumen de disco dedicado para el propósito de copia de seguridad.

#### <a name="other"></a>Otros
Otras opciones específicas del servidor de contenido de SAP son máquinas virtuales tooAzure transparente y se describen en varios documentos y las notas de SAP:

* <https://service.sap.com/contentserver>
* Nota de SAP [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Detalles tooIBM DB2 para LUW en Windows
Con Microsoft Azure, puede migrar fácilmente la aplicación SAP existente que se ejecuta en IBM DB2 para las máquinas virtuales de tooAzure Linux, UNIX y Windows (LUW). Con SAP en IBM DB2 para LUW, programadores y administradores la pueden seguir usando Hola mismas herramientas de desarrollo y administración que están disponibles en local.
Información general sobre la ejecución de SAP Business Suite en IBM DB2 para LUW puede encontrarse en Hola red de comunidad de SAP (SCN) en <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Para más información y actualizaciones de SAP en DB2 para LUW en Azure, consulte la nota de SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>IBM DB2 para Linux, UNIX y compatibilidad de versiones de Windows
SAP en IBM DB2 para LUW en los servicios de máquina virtual de Microsoft Azure es compatible a partir de la versión 10.5 de DB2.

Para obtener información sobre productos SAP y tipos de VM de Azure, consulte tooSAP Nota [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Instrucciones de configuración de IBM DB2 para Linux, UNIX y Windows para instalaciones de SAP en máquinas virtuales de Azure
#### <a name="storage-configuration"></a>Configuración de almacenamiento
Todos los archivos de base de datos deben almacenarse en el sistema de archivos NTFS de hello en función de los discos VHD. Estos discos duros virtuales son toohello montada VM de Azure y se basan en el almacenamiento de blobs de página de Azure (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Cualquier tipo de unidades de red o recursos compartidos remotos como Hola después de servicios de archivos de Azure es **no** admite archivos de base de datos:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Si usas discos duros virtuales de Azure basado en almacenamiento de blobs de página de Azure, hello las instrucciones realizadas en este documento en el capítulo [estructura de una implementación de RDBMS] [ dbms-guide-2] también se aplican toodeployments con hello IBM DB2 para LUW Base de datos.

Como se explicó anteriormente en "parte general del documento de Hola" Hola, existen cuotas en el rendimiento IOPS para discos duros virtuales de Azure. las cuotas exacto de Hola dependen de Hola VM tipo utilizado. Dispone de una lista con los tipos de máquina virtual y sus cuotas [aquí][virtual-machines-sizes].

Como Hola actual cuota IOPS por disco es suficiente, es posible toostore en que Hola a todos los archivos de base de datos una sola monta VHD de Azure.

Para obtener un rendimiento consideraciones aludir toochapter "seguridad y rendimiento consideraciones para la base de datos de directorios de datos" en guías de instalación de SAP.

Como alternativa, puede usar grupos de almacenamiento de Windows (solo disponible en Windows Server 2012 y versiones posteriores) o creación de bandas de Windows para Windows 2008 R2 como se describe en el capítulo [RAID de Software] [ dbms-guide-2.2] de este documento toocreate una gran dispositivo lógico a través de varios discos VHD montados.
En los discos de Hola que contiene las rutas de acceso de almacenamiento de hello DB2 para los directorios de SAP y saptmp, debe especificar un tamaño de sector de disco físico de 512 KB. Al utilizar grupos de almacenamiento de Windows, debe crear Hola grupos de almacenamiento manualmente a través de la interfaz de línea de comandos mediante el parámetro hello "-LogicalSectorSizeDefault". Para más información, consulte <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Copia de seguridad y restauración
funcionalidad de copia de seguridad/restauración de Hello en IBM DB2 para LUW se admite en Hola igual forma que en Hyper-V y sistemas operativos Windows Server estándar.

Debe asegurarse de seguir una estrategia establecida de copias de seguridad de bases de datos válida.

Como en las implementaciones sin sistema operativo, rendimiento de la copia de seguridad/restauración depende de cuántos volúmenes pueden leerse en paralelo y podría ser qué rendimiento Hola de esos volúmenes. Además, Hola consumo de CPU utilizado por la compresión de copia de seguridad puede desempeñan un papel importante en las máquinas virtuales con solo los subprocesos de CPU de too8. Por lo tanto, se pueden asumir los siguientes puntos:

* Hello menos Hola número de discos duros virtuales utilizar dispositivos de base de datos de toostore hello, hello Hola cuanto menor sea el rendimiento global en la lectura
* Hola menor número de Hola de subprocesos de CPU en hello VM, Hola más graves repercusiones de Hola de compresión de copia de seguridad
* Hola menos destinos (directorios de Stripe, discos duros virtuales) toowrite Hola copia de seguridad, menor rendimiento de Hola Hola

número de Hola de tooincrease de toowrite de destinos para, dos opciones pueden ser usar/combinan según sus necesidades:

* Creación de bandas volumen de destino de copia de seguridad de hello en varios discos duros virtuales montados en el rendimiento IOPS de orden tooimprove hello en ese volumen seccionado
* Con más de un destino directory toowrite Hola copia de seguridad para

#### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidad y recuperación ante desastres
Microsoft Cluster Server (MSCS) no es compatible.

La alta disponibilidad y la recuperación ante desastres (HADR) de DB2 sí son compatibles. Si dispone de máquinas virtuales de Hola de configuración de alta disponibilidad de hello funciona la resolución de nombres, el programa de instalación de hello en Azure no es diferente de cualquier instalación que se hace de forma local. No se recomienda toorely en sólo la resolución de IP.

No utilice la replicación geográfica de Tienda de Azure. Para obtener más información, consulte toochapter [almacenamiento de Microsoft Azure] [ dbms-guide-2.3] y el capítulo [alta disponibilidad y recuperación ante desastres con máquinas virtuales de Azure] [ dbms-guide-3].

#### <a name="other"></a>Otros
Todos los demás temas generales como conjuntos de disponibilidad de Azure y SAP supervisión de aplicaciones se aplican tal como se describe en hello tres primeros capítulos de este documento para las implementaciones de máquinas virtuales con IBM DB2 para LUW así.

Consulte también toochapter [generales de SQL Server para SAP en Azure resumen][dbms-guide-5.8].
