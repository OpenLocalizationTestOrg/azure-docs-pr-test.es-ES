---
title: "aaaSAP NetWeaver en máquinas virtuales de Azure: planificación e implementación | Documentos de Microsoft"
description: "SAP NetWeaver en máquinas virtuales de Azure: guía de planeación e implementación"
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 2b58a419-c892-4722-8cb6-2f8beef4430c
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53d63240760282b409f7e9412e8240689bcbcc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--planning-and-implementation-guide"></a>SAP NetWeaver en máquinas virtuales Windows de Azure: guía de planeamiento e implementación
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
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

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

[getting-started-windows-classic]:classic/sap-get-started.mdsap-dbms-guide.md
[getting-started-windows-classic-dbms]:classic/sap-get-started.mdsap-dbms-guide.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/sap-get-started.mdsap-dbms-guide.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/sap-get-started.mdsap-dbms-guide.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/sap-get-started.mdsap-dbms-guide.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/sap-get-started.mdsap-dbms-guide.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
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
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#step-2-create-vm-image
[virtual-machines-windows-capture-image]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../virtual-machines-windows-create-vm-generalized.md
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

Microsoft Azure permite que los recursos de proceso y almacenamiento de tooacquire de empresas en un tiempo mínimo sin ciclos de adquisición prolongados. Máquinas virtuales de Azure permiten a las compañías toodeploy aplicaciones clásicas, como las aplicaciones en Azure basadas en SAP NetWeaver y extender su confiabilidad y disponibilidad sin tener más recursos de forma local. Servicios de máquinas virtuales de Azure también admite la conectividad entre entornos, qué tooactively de empresas permite integrar máquinas virtuales de Azure en sus dominios locales, sus nubes privadas y su panorama del sistema SAP.
Estas notas del producto describen aspectos básicos de hello Máquina Virtual de Microsoft Azure y proporciona un tutorial de consideraciones de planificación e implementación para las instalaciones de SAP NetWeaver en Azure y por lo tanto debe Hola documento tooread antes de iniciar implementaciones reales de SAP NetWeaver en Azure.
Hola papel complementa Hola documentación de la instalación de SAP y las notas de SAP que representan recursos principales de Hola para las instalaciones e implementaciones de software SAP en correctos plataformas.

## <a name="summary"></a>Resumen
Informática en la nube es un término ampliamente utilizado que está adquiriendo cada vez más importancia en hello sector de TI, desde las pequeñas empresas de las organizaciones toolarge y multinacional.

Microsoft Azure es la plataforma de servicios de nube de Microsoft que ofrece una amplia gama de nuevas posibilidades de Hola. Ahora los clientes están toorapidly puede aprovisionar y eliminación aprovisionar aplicaciones como un servicio en nube de hello, por lo que no son tootechnical limitado o restricciones presupuestarias. En lugar de invertir tiempo y presupuesto en infraestructura de hardware, las empresas pueden centrarse en la aplicación hello, procesos empresariales y sus ventajas para los clientes y los usuarios.

Con los servicios de máquinas virtuales de Microsoft Azure, Microsoft ofrece una completa plataforma de infraestructura como servicio (IaaS). Las aplicaciones de basadas en SAP NetWeaver son compatibles en las máquinas virtuales de Azure (IaaS). Estas notas del producto describen cómo tooplan e implementar SAP NetWeaver aplicaciones basan en Microsoft Azure como plataforma de Hola de elección.

documento en Hello sí se centrará en dos aspectos principales:

* Hola primera parte describe dos patrones de implementación admitidos para las aplicaciones basadas en SAP NetWeaver en Azure. También describe el control general de Azure desde el punto de vista de las implementaciones de SAP.
* Hola segunda parte detalla la implementación Hola dos escenarios diferentes descritos en la primera parte de Hola.

Para obtener recursos adicionales, consulte el capítulo [Recursos][planning-guide-1.2] de este documento.

### <a name="definitions-upfront"></a>Lista de definiciones
En el documento de hello utilizamos Hola términos siguientes:

* IaaS: infraestructura como servicio.
* PaaS: plataforma como servicio.
* SaaS: software como servicio.
* ARM: Azure Resource Manager.
* Componente de SAP: una aplicación de SAP individual, como ECC, BW, Solution Manager o EP.  Los componentes de SAP pueden basarse en tecnologías tradicionales, como ABAP o Java, o en una aplicación no basada en NetWeaver, como Business Objects.
* Entorno SAP: uno o más componentes SAP agrupan lógicamente tooperform una función empresarial, como desarrollo, QAS, aprendizaje, recuperación ante desastres o producción.
* Panorama SAP: Se refiere toohello todos activos de SAP en un cliente panorama de TI. Hola panorama SAP incluye todos los entornos de producción y no es de producción.
* Sistema SAP: combinación de Hola de capa de DBMS y la capa de aplicación de, por ejemplo, un sistema de desarrollo SAP ERP, sistema de prueba de SAP BW, sistema de producción de SAP CRM, etcetera... En Azure implementaciones no es compatible con toodivide estas dos capas entre local y Azure. Esto significa que un sistema SAP debe implementarse de forma local o en Azure, pero no en ambos. Sin embargo, puede implementar diferentes sistemas de Hola de un panorama SAP en Azure o de forma local. Por ejemplo, podría implementar los sistemas de desarrollo y prueba de SAP CRM hello en Azure pero Hola SAP CRM producción sistema local.
* Implementación solo en la nube: una implementación donde hello suscripción de Azure no está conectado a través de un sitio a sitio o ExpressRoute conexión toohello local la infraestructura de red. En la documentación habitual de Azure este tipo de implementaciones se denomina "implementaciones exclusivas en la nube". Máquinas virtuales implementadas con este método se tiene acceso a través de Hola a internet y una dirección IP pública o un DNS público el nombre asignado toohello las máquinas virtuales en Azure. Para Microsoft Windows hello local de Active Directory (AD) y DNS no se extiende tooAzure en estos tipos de implementaciones. Por lo tanto, las máquinas virtuales de hello no forman parte de hello Active Directory local. Ocurre lo mismo en implementaciones de Linux en las que se usa, por ejemplo, OpenLDAP y Kerberos.

> [!NOTE]
> Las implementaciones exclusivas en la nube se definen en este documento como infraestructuras de SAP completas ejecutadas exclusivamente en Azure sin extensión de Active Directory/OpenLDAP ni resolución de nombres desde la infraestructura local a la nube pública. Configuraciones solo en la nube no están compatible con sistemas de SAP de producción ni las configuraciones donde STMS de SAP u otros recursos locales tener toobe utiliza entre los sistemas SAP hospedados en Azure y recursos que se encuentran en local.
>
>

* Entre entornos: Describe un escenario donde las máquinas virtuales son implementado tooan suscripción de Azure que tiene el sitio a sitio, de varios sitio o conectividad de ExpressRoute entre datacenter(s) de hello local y Azure. En la documentación habitual de Azure, este tipo de implementaciones se denominan "escenarios entre locales". motivo de Hello para la conexión de hello es tooextend dominios, locales en Active Directory local / OpenLDAP locales y en DNS en Azure. Hola horizontal local es extendido toohello activos de Azure de suscripción de Hola. Con esta extensión, hello las máquinas virtuales puede formar parte del dominio local de Hola. Los usuarios de dominio del dominio local de hello pueden tener acceso a servidores de Hola y pueden ejecutar servicios en esas máquinas virtuales (por ejemplo, servicios de DBMS). Es posible la comunicación y resolución de nombres entre máquinas virtuales implementadas de forma local y en Azure. Se trata de escenario de hello en que esperamos que toobe la mayoría de los activos SAP implementados.  Para más información, consulte [este][vpn-gateway-cross-premises-options] artículo y [este][vpn-gateway-site-to-site-create] vínculo.

> [!NOTE]
> En sistemas de producción SAP, se admiten implementaciones entre locales de sistemas SAP donde las máquinas virtuales de Azure que ejecuten sistemas SAP pertenezcan a un dominio local. Las configuraciones entre locales se admiten para la implementación completa o parcial de infraestructuras de SAP en Azure. Incluso en ejecución completa panorama de SAP hello en Azure requiere tener las máquinas virtuales que se va a parte del dominio local y anuncios / OpenLDAP. En versiones anteriores de documentación de hello hablamos sobre escenarios de TI híbrida, donde el término de Hola "Híbrido" se ha modificado en hechos de Hola que hay una conectividad entre entornos entre local y Azure. Además, hechos Hola ese Hola máquinas virtuales en Azure forman parte de Hola en Active Directory local / OpenLDAP.
>
>

Algunos documentos de Microsoft describen escenarios entre locales de un modo ligeramente distinto, en especial en configuraciones de DBMS de alta disponibilidad. Hola caso de hello SAP documentos relacionados, escenario de hello entre locales solo reduce toohaving un sitio a sitio o privado (ExpressRoute) hello y conectividad hecho que el panorama de SAP de Hola se distribuye entre local y Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Recursos
Hello siguientes guías adicionales están disponibles para hello tema de las implementaciones de SAP en Azure:

* [SAP NetWeaver en Azure Virtual Machines: guía de planeamiento e implementación (este documento)][planning-guide]
* [SAP NetWeaver en Azure Virtual Machines: guía de implementación][deployment-guide]
* [SAP NetWeaver en Azure Virtual Machines: guía de implementación de DBMS][dbms-guide]
* [SAP NetWeaver en máquinas virtuales de Azure: guía de implementación de alta disponibilidad][ha-guide]

> [!IMPORTANT]
> Dondequiera que se use posible un toohello de vínculo que hace referencia la Guía de instalación de SAP (referencia InstGuide-01, consulte <http://service.sap.com/instguides>). Cuando se trata de requisitos previos de toohello y el proceso de instalación, guías de instalación de hello SAP NetWeaver siempre debe leer detenidamente, como en este documento solo cubre tareas específicas para sistemas de SAP NetWeaver instalados en una máquina Virtual de Microsoft Azure.
>
>

Hola siguiendo las notas de SAP está relacionadas toohello tema de SAP en Azure:

| Número de nota | Título |
| --- | --- |
| [1928533] |SAP Applications on Azure: Supported Products and Sizing (Aplicaciones SAP en Azure: productos y tamaños compatibles) |
| [2015553] |SAP on Microsoft Azure: Support Prerequisites (SAP en Microsoft Azure: requisitos previos de compatibilidad) |
| [1999351] |Troubleshooting Enhanced Azure Monitoring for SAP (Solución de problemas de la supervisión mejorada de Azure para SAP) |
| [2178632] |Key Monitoring Metrics for SAP on Microsoft Azure (Métricas de supervisión clave para SAP en Microsoft Azure) |
| [1409604] |Virtualization on Windows: Enhanced Monitoring (Virtualización en Windows: supervisión mejorada) |
| [2191498] |SAP on Linux with Azure: Enhanced Monitoring (SAP en Linux con Azure: supervisión mejorada) |
| [2243692] |Linux on Microsoft Azure (IaaS) VM: SAP license issues (Linux y máquinas virtuales de Microsoft Azure (IaaS): problemas de licencia de SAP) |
| [1984787] |SUSE LINUX Enterprise Server 12: Installation notes (SUSE Linux Enterprise Server 12: notas de instalación) |
| [2002167] |Red Hat Enterprise Linux 7.x: Installation and Upgrade (Red Hat Enterprise Linux 7.x: instalación y actualización) |

Lea también hello [Wiki de SCN](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) que contiene todas las notas de SAP para Linux.

En [este artículo][azure-subscription-service-limits-subscription] se exponen las limitaciones generales predeterminadas y el límite máximo de suscripciones de Azure.

## <a name="possible-scenarios"></a>Escenarios posibles
SAP se considera a menudo una de las aplicaciones de misión crítica de hello en empresas. arquitectura de Hola y las operaciones de estas aplicaciones principalmente es muy complejo y es importante asegurar que se cumplen los requisitos de disponibilidad y rendimiento.

Por lo tanto las empresas tienen toothink cuidadosamente sobre qué aplicaciones se pueden ejecutar en un entorno de nube pública, independiente del proveedor de nube de hello elegido.

La lista siguiente muestra los posibles tipos de sistemas para la implementación de aplicaciones basadas en SAP NetWeaver en entornos de nube pública:

1. Sistemas de producción de tamaño medio
2. Sistemas de desarrollo
3. Sistemas de pruebas
4. Sistemas de prototipos
5. Sistemas de aprendizaje y de demostración

En orden toosuccessfully implementar sistemas SAP en IaaS de Azure o IaaS en general, resulta diferencias significativas de hello toounderstand importante entre las ofertas de Hola de subcontratantes o proveedores tradicionales y las ofertas de IaaS. Mientras que Hola tradicional subcontratista o adaptará la carga de trabajo de infraestructura (tipo de red, almacenamiento y servidor) toohello toohost desea que un cliente, en su lugar se responsabilidad toochoose Hola carga de trabajo adecuada del cliente de hello para las implementaciones de IaaS.

Como primer paso, los clientes necesitan hello tooverify siguientes elementos:

* Hola SAP admite tipos de VM de Azure
* productos/versiones compatibles de Hello SAP en Azure
* Hola admite versiones de SO y DBMS para hello que versiones específicas de SAP en Azure
* Rendimiento de SAPS proporcionado por diferentes SKU de Azure

Hello respuestas toothese preguntas pueden leerse en la nota de SAP [1928533].

Como segundo paso, las limitaciones de recursos y ancho de banda de Azure necesitan toobe en comparación con tooactual consumo de recursos de sistemas locales. Por lo tanto, los clientes necesidad toobe familiarizado con distintas capacidades de Hola de Hola tipos de Azure compatibles con SAP en el área de Hola de:

* Recursos de CPU y memoria de diferentes tipos de máquina virtual
* Ancho de banda de IOPS de diferentes tipos de máquina virtual
* Funcionalidades de red de diferentes tipos de máquina virtual

Se puede encontrar la mayoría de los datos [aquí][virtual-machines-sizes].

Tenga en cuenta que Hola límites mencionados en el vínculo de hello anterior son límites superiores. No significa que limita Hola para cualquiera de los recursos de hello, por ejemplo, se pueden proporcionar e/s por segundo en todas las circunstancias. Sin embargo, las excepciones de Hello son recursos de CPU y memoria de Hola de un tipo de máquina virtual elegido. Para los tipos VM de hello compatibles con SAP, los recursos de CPU y memoria de Hola están reservados y como tal están disponibles en cualquier momento en el tiempo para el consumo en hello máquina virtual.

plataforma de Microsoft Azure Hello como otras plataformas de IaaS es una plataforma de varios inquilinos. Esto significa que el almacenamiento, la red y otros recursos se comparten entre los inquilinos. Lógica de limitación y cuota inteligente es tooprevent usado uno inquilino afectando al rendimiento de Hola de otro inquilino (vecino) de manera drástica. Aunque lógica en Azure intentos tookeep varianzas en plataformas pequeñas y muy compartidas de ancho de banda experimentó suelen toointroduce mayores variaciones en la disponibilidad de recursos/ancho de banda que muchos clientes es tooin usado sus implementaciones locales. Como resultado, puede tener diferentes niveles de ancho de banda en lo que respecta de E/S de almacenamiento o toonetworking (volumen Hola así como la latencia) de toominute minuto. probabilidad de Hola que un sistema SAP en Azure podría experimentar variaciones más grandes que en un sistema local debe toobe tener en cuenta.

Un último paso es tooevaluate requisitos de disponibilidad. Esto puede suceder, ese Hola subyacente de la infraestructura de Azure requiere tooget actualizado y hosts de hello ejecutando toobe de máquinas virtuales que se reinicia. En ese caso, estas máquinas virtuales también se cerrarán y reiniciarán. sincronización de Hola de dicho mantenimiento se realiza durante el horario comercial de no es esencial para una región determinada pero ventana potencial de hello de unas pocas horas durante el cual se producirá un reinicio es relativamente amplia. Hay varias tecnologías en hello plataforma Windows Azure que se puede configuran toomitigate algunos o todos de hello afectan de dichas actualizaciones. Hola a futuras mejoras de la plataforma Azure, aplicación de SAP y DBMS son diseñado el impacto de hello toominimize de estos reinicios.

En orden toosuccessfully implementar un sistema SAP en Azure, hello local SAP sistemas sistema operativo, base de datos y aplicaciones de SAP debe aparecen en hello matriz de compatibilidad de Azure de SAP, caben dentro de Hola Hola de recursos puede proporcionar la infraestructura de Azure y que puede trabajar con hello que ofrece disponibilidad ofertas de Microsoft Azure. A medida que se identifican esos sistemas, necesita toodecide en uno de hello siguiendo dos escenarios de implementación.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Solo en la nube: las implementaciones de máquina Virtual en Azure sin dependencias de hello local red de cliente
![Implementación de una sola máquina virtual con un escenario de demostración o aprendizaje de SAP en Azure][planning-guide-figure-100]

Este escenario es típico de aprendizajes o sistemas de demostración, donde todos los componentes de Hola de SAP y el software de SAP no se instalan dentro de una sola máquina virtual. No se admiten sistemas de producción de SAP en este escenario de implementación. En general, este escenario cumple Hola según los requisitos:

* Hola las propias máquinas virtuales son accesibles a través de la red pública de Hola. Conectividad de red directa para aplicaciones de Hola que se ejecutan dentro de hello las máquinas virtuales toohello red de cualquier empresa Hola propietaria Hola demostraciones o aprendizajes el contenido local o cliente hello no es necesario.
* En el caso de varias máquinas virtuales que representan los aprendizajes Hola o escenario de demostración, resolución de nombres y las comunicaciones de red debe toowork entre máquinas virtuales de Hola. Pero las comunicaciones entre el conjunto de Hola de máquinas virtuales tienen toobe aislada para que se pueden implementar varios conjuntos de máquinas virtuales en paralelo sin interferencias.  
* Conectividad a Internet es necesaria para el inicio de sesión de hello usuario final tooremote en toohello que las máquinas virtuales hospedadas en Azure. Función de sistema operativo de invitado de hello, se usa servicios de Terminal/RDS o VNC/ssh tooaccess Hola VM tooeither completar tareas de aprendizaje de Hola o realizar demostraciones de Hola. Si los puertos SAP como 3200, 3300 y 3600 también se pueden exponer instancia de la aplicación hello SAP puede tener acceso desde cualquier escritorio conectado Internet.
* Hola sistemas SAP (y VM(s)) representan un escenario independiente en Azure que solo requiere conectividad a internet pública para el acceso de usuario final y no requiere un tooother conexión máquinas virtuales en Azure.
* SAPGUI y un explorador se instala y ejecuta directamente en hello máquina virtual.
* Se requiere un restablecimiento rápido de un estado original de toohello de máquina virtual y una nueva implementación de ese estado original otra vez.
* En caso de hello de demostración y los escenarios de aprendizaje que se materializan en varias máquinas virtuales, un Active Directory / servicio OpenLDAP o DNS es necesario para cada conjunto de máquinas virtuales.

![Representación de un escenario de demostración o aprendizaje por parte de un grupo de VM en un servicio en la nube de Azure][planning-guide-figure-200]

Es importante tookeep en cuenta que Hola máquinas virtuales en cada uno de hello establece toobe necesidad de implementar en paralelo, donde se Hola nombres de las VM en cada conjunto de Hola Hola igual.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>entre entornos de implementación de una o varias máquinas virtuales de SAP en Azure con el requisito de Hola de que se integra totalmente en la red local de Hola
![VPN con conectividad de sitio a sitio (entre locales)][planning-guide-figure-300]

Este es un escenario entre locales con numerosos patrones de implementación posibles. Puede ser descrita como simplemente como si se ejecutaran algunas partes de hello SAP horizontal local y otras partes de hello panorama de SAP en Azure. Todos los aspectos del hecho de Hola que parte de los componentes SAP Hola se ejecutan en Azure deben ser transparentes para los usuarios finales. Hola, por tanto, el sistema de corrección de transporte de SAP (STMS), la comunicación de RFC, impresión, seguridad (como SSO), etc. funcionarán sin inconvenientes para sistemas SAP hello en Azure. Pero también describe el escenario entre entornos de hello un escenario donde panorama de SAP de hello completa se ejecuta en Azure con el dominio del cliente de Hola y DNS se ampliaron en Azure.

> [!NOTE]
> Se trata de un escenario de implementación de Hola que se admite para ejecutar los sistemas SAP productivos.
>
>

Lectura [este artículo] [ vpn-gateway-create-site-to-site-rm-powershell] para obtener más información acerca de cómo tooconnect tooMicrosoft Azure de red local

> [!IMPORTANT]
> Cuando hablamos escenarios entre entornos entre las implementaciones de clientes de Azure y local, ponemos atención a la granularidad de Hola de sistemas SAP completos. Los casos que *no admiten* escenarios entre locales son los siguientes:
>
> * La ejecución de varias capas de aplicaciones SAP en diferentes métodos de implementación. Por ejemplo, ejecuta Hola DBMS capa local, pero la capa de aplicación de SAP de hello en máquinas virtuales implementadas como VM de Azure o viceversa.
> * Combinar algunos componentes de una capa SAP en Azure y otras en medios locales. Por ejemplo, dividir las instancias de nivel de aplicación de SAP de hello entre locales y máquinas virtuales de Azure.
> * No se admite la distribución de máquinas virtuales que ejecuten instancias SAP de un sistema en varias regiones de Azure.
>
> motivo de Hola para estas restricciones es requisito de Hola para una red de alto rendimiento de una latencia muy baja dentro de un sistema SAP, especialmente entre instancias de la aplicación hello y capa de DBMS Hola de un sistema SAP.
>
>

### <a name="supported-os-and-database-releases"></a>Versiones de bases de datos y sistemas operativos compatibles
* Este artículo incluye una lista del software de servidor de Microsoft compatible con los servicios de Azure Virtual Machine: <http://support.microsoft.com/kb/2721672>.
* La nota de SAP [1928533]indica las versiones de sistemas operativos y de bases de datos admitidos en los servicios de máquinas virtuales de Azure con software SAP.
* La nota de SAP [1928533]muestra las aplicaciones y versiones de SAP compatibles con los servicios de máquinas virtuales de Azure.
* Sólo imágenes de 64 bits son compatible toorun como VM invitadas en Azure para escenarios SAP. Por ello, solo se admiten aplicaciones y bases de datos de SAP de 64 bits.

## <a name="microsoft-azure-virtual-machine-services"></a>Servicios de máquinas virtuales de Microsoft Azure
plataforma de Microsoft Azure Hello es una nube a escala de internet plataforma services había hospeda y opera en datos de Microsoft centros. plataforma de Hello incluye servicios de máquinas virtuales de hello Microsoft Azure (infraestructura como servicio o IaaS) y un conjunto de plataforma como capacidades de un servicio (PaaS).

Hola plataforma Windows Azure reduce la necesidad de Hola de tecnología inicial y compras de infraestructura. Esta característica simplifica el mantenimiento y operativo aplicaciones proporcionando toohost de proceso y almacenamiento a petición, escalar y administrar aplicaciones web y aplicaciones conectadas. Administración de la infraestructura es automatizada con una plataforma que está diseñada para lograr alta disponibilidad y escalado toomatch necesidades de uso con la opción de saludo de un modelo de precios de pago por uso dinámico.

![Posicionamiento de servicios de máquinas virtuales de Microsoft Azure][planning-guide-figure-400]

Con los servicios de máquina Virtual de Azure, Microsoft le permite tooAzure de imágenes de servidor personalizado toodeploy como instancias de IaaS (consulte la figura 4). Hola máquinas virtuales en Azure se basan en unidades de disco duro virtuales (VHD) de Hyper-V y son toorun capaz de distintos sistemas operativos como sistema operativo invitado.

Desde una perspectiva operacional, experiencias de hello que servicio de máquina Virtual de Azure ofrece similares como máquinas virtuales implementadas de forma local. Sin embargo, tiene Hola ventaja importante que no es necesario tooprocure, administrar y administrar la infraestructura de Hola. Los desarrolladores y administradores tienen control completo sobre la imagen de sistema operativo de hello en estas máquinas virtuales. Los administradores pueden iniciar sesión remotamente en esos mantenimiento tooperform de máquinas virtuales y solución de problemas de tareas, así como tareas de implementación de software. En toodeployment de tener en cuenta, Hola únicas restricciones son los tamaños de Hola y las capacidades de máquinas virtuales de Azure. Su configuración podría no ser tan granular como en el caso del entorno local. Hay una gran variedad de tipos de máquina virtual que combinan lo siguiente:

* Cantidad de vCPU
* Memoria
* Número de discos duros virtuales que se pueden conectar
* Anchos de banda de red y almacenamiento

tamaño de Hola y las limitaciones de diversos tamaños de distintas máquinas virtuales que ofrecen puede verse en una tabla de [este artículo][virtual-machines-sizes]

Hay diversas familias o series de máquinas virtuales. A partir de diciembre de 2015, puede distinguir Hola siguientes familias de máquinas virtuales:

* Tipos de máquinas virtuales A0-A7: no todos están certificados para SAP. Primera serie de máquinas virtuales en las que se introdujo IaaS de Azure.
* Tipos de máquinas virtuales A8-A11: instancias de procesos de alto rendimiento. Ejecución en distintos hosts con procesos de mejor rendimiento que otras máquinas virtuales de la serie A.
* Tipos de máquinas virtuales de la serie D: mejor rendimiento que A0-A7. No todos los tipos VM de hello están certificadas con SAP.
* Tipos de máquinas virtuales de serie DS: usar los mismos hosts como serie D, pero son tooAzure tooconnect capaz de almacenamiento Premium (consulte el capítulo [almacenamiento de Azure Premium] [ planning-guide-3.3.2] de este documento). De nuevo, no todos los tipos de máquinas virtuales están certificadas para SAP.
* Tipos de máquinas virtuales de la serie G: tipos de máquinas virtuales de memoria alta.
* Tipos de VM de GS-Series: similar serie G pero incluida Hola opción toouse almacenamiento Premium de Azure (consulte el capítulo [almacenamiento de Azure Premium] [ planning-guide-3.3.2] de este documento). Cuando se utilizan las máquinas virtuales de GS-Series como servidores de base de datos es obligatorio toouse almacenamiento Premium para los archivos de registro de transacciones y de datos de base de datos

Hola, puede encontrar misma configuración de CPU y memoria en otra serie de máquina virtual. No obstante, al examinar el rendimiento de rendimiento de Hola de estas máquinas virtuales fuera de series diferentes Hola podrían ser diferentes significativamente. A pesar de tener Hola misma configuración de CPU y memoria. Razón es que el hardware de servidor de host subyacente de hello en la introducción de Hola de diferentes tipos de VM Hola tenía las características de rendimiento diferentes.  Normalmente diferencia Hola se muestra en el rendimiento de la también se refleja en el precio de Hola de hello diferentes máquinas virtuales.

Tenga en cuenta que no todas las distintas series de máquinas virtuales se pueden ofrecer en cada uno de hello regiones de Azure (para las regiones de Azure consulte el capítulo siguiente). También hay que saber que no todas las máquinas virtuales o series de máquinas virtuales están certificadas para SAP.

> [!IMPORTANT]
> Para el uso de Hola de las aplicaciones basadas en SAP NetWeaver, solo Hola subconjunto de tipos de máquinas virtuales y las configuraciones incluidos en la nota de SAP [1928533] son compatibles.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Regiones de Azure
Microsoft permite toodeploy máquinas virtuales en lo que se denomina 'regiones de Azure'. Una región de Azure puede constar de uno o varios centros de datos próximos entre sí. Para la mayoría de hello las regiones geopolíticas en Hola a todos Microsoft tiene al menos dos regiones de Azure. Por ejemplo, en Europa hay una región de Azure "Europa del Norte" y otra "Europa Occidental". Estas dos regiones de Azure dentro de una región geopolíticas están separadas por una distancia considerable para que los casos de desastres naturales o técnicas no afectan a ambas regiones de Azure en hello misma región geopolíticos. Puesto que Microsoft constantemente está generando nuevas regiones de Azure en distintas regiones geopolíticas globalmente, número de Hola de estas regiones crezca de manera constante y a partir de diciembre de 2015 alcanzado el número de Hola de 20 regiones de Azure con otras regiones anunciadas ya. Como un cliente puede implementar los sistemas SAP en estas regiones, incluidos Hola dos regiones de Azure en China. Actual seguridad toodate obtener información sobre las regiones de Azure, vea este sitio Web: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Hola concepto de máquina Virtual de Microsoft Azure
Microsoft Azure ofrece una infraestructura como un toohost de solución de servicio (IaaS) máquinas virtuales con funcionalidades similares como una solución de virtualización local. Es capaz de toocreate máquinas virtuales desde dentro de hello Portal de Azure, PowerShell o CLI, que también ofrecen capacidades de implementación y administración.

Azure Resource Manager le permite tooprovision las aplicaciones utilizando una plantilla declarativa. En una plantilla, puede implementar varios servicios junto con sus dependencias. Usar hello mismo toorepeatedly plantilla implementar la aplicación durante cada fase del ciclo de vida de aplicación Hola.

Para obtener más información sobre las plantillas de ARM, consulte las siguientes referencias:

* [Implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y Hola CLI de Azure][virtual-machines-linux-cli-deploy-templates]
* [Administre máquinas virtuales con Azure Resource Manager y PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

Otra característica interesante es toocreate imágenes de capacidad de Hola de máquinas virtuales, lo cual permite hacer tooprepare determinado repositorios desde la cual están tooquickly capaz de implementan instancias de máquina Virtual que satisfacen sus necesidades.

Para obtener más información sobre la creación de imágenes de máquinas virtuales, consulte [este artículo (Windows)][virtual-machines-windows-capture-image] o [este otro (Linux)][virtual-machines-linux-capture-image].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Dominios de error
Dominios de error representan una unidad física de error, contenida en los centros de datos y, mientras que un disco físico o un bastidor puede considerarse un dominio de error de infraestructura física toohello muy estrechamente relacionados, no hay ninguna asignación directa de uno a uno entre dos Hola.

Cuando implemente varias máquinas virtuales como parte de un sistema SAP en los servicios de máquina Virtual de Microsoft Azure, puede influir en hello Azure Fabric Controller toodeploy su aplicación en diferentes dominios de error, con lo que se cumplen los requisitos de Hola Hola SLA de Microsoft Azure. Sin embargo, Hola distribución de los dominios de error a través de una unidad de escala de Azure (colección de cientos de nodos de proceso o nodos de almacenamiento y redes) o asignación de Hola de máquinas virtuales tooa dominio de error específico es algo sobre el que no tiene el control directo. En orden toodirect hello Azure fabric controlador toodeploy un conjunto de máquinas virtuales en diferentes dominios de error, deberá tooassign un toohello conjunto de disponibilidad de Azure máquinas virtuales durante la implementación. Para más información sobre los conjuntos de disponibilidad de Azure, consulte el capítulo [Conjuntos de disponibilidad de Azure][planning-guide-3.2.3] de este documento.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Dominios de actualización
Dominios de actualización representan una unidad lógica que le ayudan a toodetermine cómo una máquina virtual dentro de un sistema SAP, que consta de instancias SAP que se ejecutan en varias máquinas virtuales, se actualizará. Cuando se produce una actualización, Microsoft Azure pasa por proceso de Hola de actualización de estos dominios de actualización uno por uno. Al distribuir las máquinas virtuales en tiempo de implementación en diferentes dominios de actualización, se puede proteger parcialmente el sistema SAP frente a posibles tiempos de inactividad. En Ordenar tooforce toodeploy Azure hello las máquinas virtuales de un sistema SAP distribuidas en diferentes dominios de actualización, deberá tooset un atributo determinado durante la implementación de cada máquina virtual. Dominios de tooFault similar, una unidad de escala de Azure se divide en varios dominios de actualización. En orden toodirect hello Azure fabric controlador toodeploy un conjunto de máquinas virtuales en diferentes dominios de actualización, deberá tooassign un toohello conjunto de disponibilidad de Azure máquinas virtuales durante la implementación. Para más información sobre conjuntos de disponibilidad de Azure, consulte el capítulo [Conjuntos de disponibilidad de Azure][planning-guide-3.2.3] a continuación.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Conjuntos de disponibilidad de Azure
Máquinas virtuales de Azure en un conjunto de disponibilidad de Azure se distribuirán por hello controlador de tejido de Azure a través de diferentes dominios de error y actualización. Hola de distribución de hello en diferentes dominios de error y actualización sirve tooprevent que todas las máquinas virtuales de un sistema SAP desde el que se va a apagar en el caso de hello de mantenimiento de la infraestructura o un error dentro de un dominio de error. De forma predeterminada, las máquinas virtuales no forman parte de un conjunto de disponibilidad. participación de Hola de una máquina virtual en un conjunto de disponibilidad se define durante la implementación o más adelante mediante una reconfiguración y reimplementación de una máquina virtual.

concepto de hello toounderstand de forma de conjuntos de disponibilidad de Azure y Hola conjuntos de disponibilidad se relacionan tooFault y dominios de actualización, lea [este artículo][virtual-machines-manage-availability]

vea toodefine conjuntos de disponibilidad de ARM a través de una plantilla json [Hola las especificaciones de la api de rest](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) y busque "disponibilidad".

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Almacenamiento: Almacenamiento de Microsoft Azure y discos de datos
Las máquinas virtuales de Microsoft Azure usan varios tipos de almacenamiento. Al implementar SAP en los servicios de máquina Virtual de Azure es toounderstand importantes diferencias de hello entre estos dos tipos principales de almacenamiento:

* Almacenamiento volátil, no persistente.
* Almacenamiento persistente.

almacenamiento de Hello no persistente está directamente conectado toohello máquinas virtuales en ejecución y reside en hello nodos de proceso: almacenamiento de instancia local de hello (almacenamiento temporal). tamaño de Hello depende de tamaño de Hola de máquina Virtual elegida cuando inició la implementación de Hola Hola. Este tipo de almacenamiento es volátil y, por tanto, se ha inicializado Hola disco cuando se reinicia una instancia de la máquina Virtual. Normalmente, se encuentra el archivo de paginación de hello para el sistema operativo de Hola en este disco temporal.

- - -
> ![Windows][Logo_Windows] Windows
>
> En máquinas virtuales de Windows unidad temporal de Hola se monta como unidad D:\ en una VM implementada.
>
> ![Linux][Logo_Linux] Linux
>
> En las máquinas virtuales de Linux está montada como /mnt/Resource o /mnt. Para obtener información, consulte:
>
> * [¿Cómo tooAttach una máquina Virtual Linux tooa de disco de datos][virtual-machines-linux-how-to-attach-disk]
> * <http://blogs.msdn.com/b/mast/archive/2013/12/07/understanding-the-temporary-drive-on-windows-azure-virtual-machines.aspx>
>
>

- - -
unidad de Hello real es volátil porque se almacena en el propio servidor de host Hola. Si mueve Hola VM en una nueva implementación (por ejemplo, due toomaintenance en el host de Hola o apagado y reinicio) contenido Hola de unidad de Hola se pierde. Por lo tanto, no es una opción toostore cualquier dato importante en esta unidad. tipo de Hola de medios usados para este tipo de almacenamiento difiere entre las distintas series VM con características de rendimiento muy diferentes que, a partir de junio de 2015, el aspecto:

* A5-A7: rendimiento muy limitado. Solo se recomienda para el archivo de paginación.
* A8-A11: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie D: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie DS: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie G: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.
* Serie GS: características de rendimiento muy buenas con 10 000 IOPS y una tasa de más de 1 GB/seg.

Las instrucciones anteriores están aplicando los tipos de VM toohello certificados con SAP. Hola series de máquinas virtuales con excelente IOPS y el rendimiento son aptos para aprovechar algunas características de DBMS. Vea hello [Guía de implementación de DBMS] [ dbms-guide] para obtener más detalles.

Almacenamiento de Microsoft Azure proporciona niveles típicos hello y almacenamiento persistentes de protección y redundancia que se observan en el almacenamiento SAN. Discos basados en el almacenamiento de Azure son disco duro virtual (VHD) ubicado en servicios de almacenamiento de Azure Hola. Hola disco de SO local (C: Windows\, Linux / (/ dev/sda1)) se almacena en hello el almacenamiento de Azure y volúmenes/discos adicionales montado toohello VM también se almacenan allí demasiado.

Es posible tooupload un VHD existente desde el entorno local o crear algunos vacíos desde dentro de Azure y conectar esas máquinas virtuales toodeployed. Los discos duros virtuales se denominan discos de Azure.

Después de crear o cargar un disco duro virtual en el almacenamiento de Azure, es posible toomount y asociar esos tooan Máquina Virtual y toocopy existentes (desmontado) de disco duro virtual existentes.

Dado que esos discos duros virtuales son persistentes, los datos y las modificaciones no se pierden en los reinicios y nuevas instancias de la máquina virtual. Incluso si se elimina una instancia, estos discos duros virtuales mantienen seguros y pueden volver a implementar o en el caso de discos no son de SO pueden ser tooother montada las máquinas virtuales.

Dentro de Hola se puede configurar la red de los niveles de redundancia diferentes de almacenamiento de Azure:

* Nivel mínimo que se pueden seleccionar es 'redundancia local', que es equivalente toothree-réplica de datos de hello en hello mismo centro de datos de una región de Azure (consulte el capítulo [regiones de Azure][planning-guide-3.1]).
* Almacenamiento de redundancia de zona que repartirán imágenes Hola tres en distintos centros de datos dentro de Hola la misma región de Azure.
* Nivel de redundancia de forma predeterminada es la redundancia geográfica que replica de manera asincrónica el contenido de hello en otro imágenes 3 de los datos de hello en otra región de Azure que se hospeda en hello misma región geopolíticos.

Consulte también la tabla Hola encima de este artículo en las opciones de redundancia diferente de lo que respecta toohello: <https://azure.microsoft.com/pricing/details/storage/>

Obtener más información en tooAzure lo que respecta que almacenamiento puede encontrarse aquí:

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Almacenamiento de Azure estándar
Almacenamiento de Azure BLOB estándar era el tipo de Hola de almacenamiento disponible cuando se publicó IaaS de Azure. Se exigían cuotas de IOPS por cada disco duro virtual. Latencia experimentada no estaba en hello misma clase como dispositivos de SAN y NAS que normalmente se implementa para los sistemas SAP hospedan en local. No obstante, Hola almacenamiento de Azure estándar es suficiente para muchos cientos sistemas SAP mientras tanto implementados en Azure.

El almacenamiento de Azure estándar se cobra a Hola datos reales que se almacenan, volumen de Hola de transacciones de almacenamiento, transferencias de datos de salida y opción de redundancia elegido. Muchos discos duros virtuales se pueden crear en hello máximo 1 TB de tamaño, pero siempre y cuando los permanecen vacíos no hay ningún cargo. Si, a continuación, se llena un disco duro virtual de 100GB cada uno, se le cobrará para almacenar 100GB y no Hola Hola de tamaño nominal con que se llegó a crear VHD.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Almacenamiento premium de Azure
En abril de 2015, Microsoft presentó el almacenamiento Premium de Azure. Almacenamiento Premium se introdujo con hello objetivo tooprovide:

* Mejor latencia de E/S
* Mejor rendimiento
* Menor variabilidad de la latencia de E/S

Para ello, un lote de cambios se introdujeron de qué hello dos más importantes son:

* Uso de discos SSD en nodos de almacenamiento de Azure de Hola
* Hola a una nueva caché de lectura que esté respaldada por SSD local de un nodo de proceso de Azure

En opuesto donde no cambió las capacidades de almacenamiento de tooStandard depende del tamaño de Hola de hello (o disco VHD), almacenamiento Premium actualmente tiene 3 categorías de disco diferente que se muestran al final de Hola de este artículo antes de la sección de preguntas más frecuentes de hello: <https:/ /Azure.Microsoft.com/Pricing/Details/Storage/>

Verá que rendimiento VHD IOPS/VHD y el disco son dependientes de la categoría de tamaño de Hola de discos de Hola

Costo base en caso de hello de almacenamiento Premium no es un volumen de datos reales de hello almacenado en estos discos duros virtuales, pero la categoría de tamaño de Hola de tal un disco duro virtual, independientemente de la cantidad de Hola de datos de Hola que se almacenan en el disco duro virtual de Hola.

También puede crear discos duros virtuales en almacenamiento Premium que no se asigna directamente en categorías de tamaño de Hola que se muestra. Puede ser el caso de hello, especialmente cuando se copian los VHD de almacenamiento estándar en almacenamiento Premium. En tales casos se realiza una asignación toohello siguiente mayor almacenamiento Premium opción de disco.

Ten en cuenta que sólo determinadas series de máquinas virtuales pueden beneficiarse de hello almacenamiento Premium de Azure. A partir de diciembre de 2015, se trata de hello DS - y GS-series. Hola DS-series es básicamente Hola igual como serie D con la excepción de Hola que DS-series tiene capacidad de hello toomount almacenamiento Premium basados en máquinas virtuales además tooVHDs que se hospedan en el almacenamiento de Azure estándar. Lo mismo es válido para comparar de serie G tooGS-series.

Si va a retirar parte Hola de máquinas virtuales de hello DS-series en [este artículo] [ virtual-machines-sizes] , también se dará cuenta que no hay limitaciones de volumen de datos tooPremium almacenamiento VHD en la granularidad de Hola de nivel de máquina virtual de Hola. Diferentes DS-series o GS-series las máquinas virtuales también tienen diferentes limitaciones en lo que respecta toohello número de discos duros virtuales que se pueden montar. Estos límites se documentan en el artículo hello que también se ha mencionado anteriormente. Pero básicamente significa que si, por ejemplo, montar 32 x P30 discos/discos duros virtuales tooa DS14 máquina virtual no puede obtener 32 x el rendimiento máximo de un disco P30 Hola. En su lugar hello rendimiento máximo en el nivel de máquina virtual tal como se describe en el artículo Hola limitará el rendimiento.

Se puede encontrar más información sobre Premium Storage aquí: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>.

#### <a name="azure-storage-accounts"></a>Cuentas de almacenamiento de Azure
Al implementar servicios o máquinas virtuales en Azure, la implementación de discos duros virtuales e imágenes de máquinas virtuales debe estar organizada en unidades denominadas cuentas de almacenamiento de Azure. Al planear una implementación de Azure, necesita toocarefully tenga en cuenta las restricciones de Hola de Azure. En un lado de hello, hay un número limitado de cuentas de almacenamiento por suscripción de Azure. Aunque cada cuenta de almacenamiento de Azure puede contener un gran número de archivos de disco duro virtual, hay un límite fijo en hello total de IOPS por cuenta de almacenamiento. Al implementar cientos de máquinas virtuales de SAP con sistemas DBMS que crean importantes llamadas de E/S, es recomendable toodistribute alta VM de IOP DBMS entre varias cuentas de almacenamiento de Azure. Se debe tener cuidado no tooexceed Hola límite actual de las cuentas de almacenamiento de Azure por suscripción. Porque el almacenamiento es una parte vital de la implementación de la base de datos de Hola para un sistema SAP, este concepto se analiza con más detalle en hello ya hace referencia a [Guía de implementación de DBMS][dbms-guide].

Se puede encontrar más información sobre las cuentas de Azure Storage en [este artículo][storage-scalability-targets]. Leyendo este artículo, se dará cuenta de que existen diferencias en las limitaciones de hello entre cuentas de almacenamiento de Azure estándar y cuentas de almacenamiento Premium. Diferencias principales son Hola para un volumen de datos que se pueden almacenar dentro de una cuenta de almacenamiento de este tipo. En el almacenamiento estándar volumen hello es una magnitud mayor que con el almacenamiento Premium. En hello otro Hola lado cuenta de almacenamiento estándar graves está limitado en e/s por segundo (consulte la columna 'Velocidad Total de solicitudes'), mientras que Hola cuenta de almacenamiento de Azure Premium no tiene ninguna limitación de este tipo. Trataremos detalles y los resultados de estas diferencias al hablar de las implementaciones de Hola de sistemas SAP, especialmente los servidores DBMS de Hola.

Dentro de una cuenta de almacenamiento tiene contenedores diferentes toocreate de hello posibilidad con propósito de Hola de organizar y clasificar los diferentes discos duros virtuales. Estos contenedores son tooe.g utilizadas normalmente. Separe los discos duros virtuales de diferentes máquinas virtuales. Usar un único contenedor o varios contenedores en una sola cuenta de almacenamiento de Azure no influye en el rendimiento.

Dentro de Azure un nombre de disco duro virtual sigue Hola después de nomenclatura de conexión que necesita tooprovide un nombre único para hello VHD en Azure:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Como cadena Hola mencionados anteriormente debe identificar toouniquely Hola disco duro virtual que se almacena en almacenamiento de Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Redes de Microsoft Azure
Microsoft Azure ofrecerá una infraestructura de red que permite la asignación de Hola de todos los escenarios que deseamos toorealize con el software SAP. Hola capacidades son:

* Acceso de hello fuera toohello directamente las máquinas virtuales a través de servicios de Terminal Server de Windows o ssh/VNC
* Acceso tooservices y puertos específicos utilizados por aplicaciones dentro de hello las máquinas virtuales
* Comunicación interna y resolución de nombres entre un grupo de máquinas virtuales implementadas como máquinas virtuales de Azure
* Conectividad entre entornos entre hello red de Azure y red local del cliente
* Conectividad entre sitios de Azure y varias regiones de Azure o varios centros de datos

Se puede encontrar más información así: <https://azure.microsoft.com/documentation/services/virtual-network/>

Hay muchas posibilidades diferentes tooconfigure nombre de y resolución IP en Azure. En este documento, solo en la nube escenarios confían en hello predeterminados del uso de DNS de Azure (en contraste toodefining un servicio propio de DNS). También puede usarse un nuevo servicio DNS de Azure en lugar de configurar un servidor DNS propio. Se puede encontrar más información en [este artículo][virtual-networks-manage-dns-in-vnet] y en [esta página](https://azure.microsoft.com/services/dns/).

Para los escenarios de entre entornos confiamos en hechos de Hola que Hola local OpenLDAP/AD/DNS se ha ampliado a través de VPN o conexión privada tooAzure. Para determinados escenarios, como se indica a continuación, podría ser necesario toohave una réplica de AD/OpenLDAP instalada en Azure.

Redes y la resolución de nombres es una parte vital de la implementación de la base de datos de Hola para un sistema SAP, este concepto se analiza con más detalle en hello [Guía de implementación de DBMS][dbms-guide].

##### <a name="azure-virtual-networks"></a>Redes virtuales de Azure
Mediante la creación de una red Virtual de Azure puede definir el intervalo de direcciones de Hola de direcciones IP privadas Hola asignada por la funcionalidad de DHCP de Azure. En escenarios entre locales, intervalo de direcciones IP de hello definido todavía se asignarán mediante DHCP por Azure. Sin embargo, la resolución de nombres de dominio se realizará en local (suponiendo que las máquinas virtuales de hello forman parte de un dominio local) y, por lo que puede resolver direcciones más allá de los diferentes servicios de nube de Azure.

[comment]: <> (MSSedusch still needed? TAREAS originalmente a una red Virtual de Azure era enlazado tooan grupo de afinidad. Con el que una red Virtual en Azure tenemos restringido toohello unidad de escalado de Azure que Hola que obtuvo asigna el grupo de afinidad. Final de hello, esta red Virtual de hello están hecho era toohello restringido recursos disponibles en hello unidad de escalado de Azure. Desde entonces, esta situación ha cambiado y ahora las redes virtuales de Azure pueden abarcar varias unidades de escalado de Azure. Sin embargo, es necesario que las redes virtuales de Azure **NO** estén asociadas a grupos de afinidad en el momento de la creación. Ya hemos mencionado anteriormente que en toorecommendations opuesto año anterior, debe ** no aprovechar los grupos de afinidad de Azure ya **. Para más información, consulte <https://azure.microsoft.com/blog/regional-virtual-networks/>)

Cada máquina Virtual en Azure necesidades toobe conectado tooa red Virtual.

Se puede encontrar más información en [este artículo][resource-groups-networking] y en [esta página](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd lista de tareas no se pudo encontrar un artículo que incluye el tema de OpenLDAP Hola + ARM;)
[comment]: <> (MSSedusch &lt;https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL&gt;)

> [!NOTE]
> De forma predeterminada, una vez que se implementa una máquina virtual no se puede cambiar configuración de red Virtual de Hola. configuración de TCP/IP Hola debe quedar toohello servidor de DHCP de Azure. El comportamiento predeterminado es la asignación de IP dinámicas.
>
>

dirección MAC de Hola de tarjeta de red virtual de hello puede cambiar, por ejemplo, después de hello y cambie el tamaño de Windows o SO invitado de Linux recogerá la nueva tarjeta de red hello y utilizará automáticamente DHCP tooassign Hola IP y DNS direcciones en este caso.

##### <a name="static-ip-assignment"></a>Asignación de direcciones IP estáticas
Es posible tooassign fijada o direcciones IP reservadas tooVMs dentro de una red Virtual de Azure. Máquinas virtuales de Hola se ejecutan en una red Virtual de Azure abre una gran posibilidad tooleverage esta funcionalidad si es necesario o requerido para algunos escenarios. asignación de direcciones IP de Hello es válida en toda la existencia de Hola de hello VM, independientemente de si se está ejecutando Hola VM o apagado. Como resultado, deberá tootake Hola número total de máquinas virtuales (VM funcionamiento o detenidas) en cuenta al definir Hola intervalo de direcciones IP para hello red Virtual. dirección IP de Hello permanece asignada hasta que se elimine hello VM y su interfaz de red o hasta que la dirección IP de Hola se cancela la asignación nuevo. Para obtener más información, consulte [este artículo][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Varias NIC por máquina virtual
Se pueden definir varias tarjetas de interfaz de red virtual (vNIC) en una máquina virtual de Azure. Hola capacidad toohave varios vNICs podrá iniciar tooset la separación de tráfico de red donde p. ej. tráfico del cliente se enruta a través de un vNIC y tráfico de back-end se enruta a través de un segundo vNIC. Depende del tipo hello de la máquina virtual hay diferentes limitaciones en lo que respecta a número toohello de vNICs. En los artículos siguientes se indican los detalles, funcionalidades y restricciones:

* [Creación de una máquina virtual con varias NIC][virtual-networks-multiple-nics]
* [Implementación de varias máquinas virtuales de NIC con una plantilla][virtual-network-deploy-multinic-arm-template]
* [Implementación de máquinas virtuales con varias NIC mediante PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Implementar las máquinas virtuales de varias NIC con hello CLI de Azure][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Conectividad de sitio a sitio
Las máquinas virtuales de Azure tienen características entre locales, mientras que las instalaciones locales están vinculadas a una conexión VPN permanente y transparente. Es modelo de implementación SAP más común de toobecome esperado de hello en Azure. Hola, se supone que los procedimientos operacionales y procesos con instancias de SAP en Azure deben funcionar de forma transparente. Esto significa que debe ser capaz de tooprint fuera de estos sistemas así como usar hello tootransport de sistema de administración de transporte de SAP (TMS) cambia de un sistema de desarrollo en el sistema de prueba de tooa de Azure que está implementado de forma local. Se puede encontrar más documentación sobre la conectividad de sitio a sitio en [este artículo][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>Dispositivo de túnel VPN
En Ordenar toocreate una conexión de sitio a sitio (centro de datos de local datos center tooAzure), necesitará tooeither obtener y configurar un dispositivo VPN o utilizar enrutamiento y acceso remoto Service (RRAS) que se introdujo como un componente de software con Windows Server 2012.

* [Crear una red virtual con una conexión VPN de sitio a sitio mediante PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [Acerca de los dispositivos VPN para las conexiones VPN Gateway de sitio a sitio][vpn-gateway-about-vpn-devices]
* [Preguntas más frecuentes sobre VPN Gateway][vpn-gateway-vpn-faq]

![Conexión de sitio a sitio entre sistemas locales y Azure][planning-guide-figure-600]

Hola ilustración anterior muestra dos suscripciones de Azure tienen subrangos de direcciones IP reservadas para uso en redes virtuales en Azure. conectividad de Hola de hello local tooAzure de red se establece a través de VPN.

#### <a name="point-to-site-vpn"></a>VPN de punto a sitio
Point-to-site VPN requiere cada tooconnect del equipo cliente con su propia red privada virtual en Azure. Para escenarios SAP de Hola que estamos examinando, conectividad de punto a sitio no es práctico. Por lo tanto, no hay más referencias se proporcionará conectividad VPN de sitio a toopoint.

[comment]: <> (MSSedusch -- More information can be found here)
[comment]: <> (MShermannd TODO Link no longer valid; But ARM is anyway not supported - see next link below)
[comment]: <> (MSSedusch -- &lt;http://msdn.microsoft.com/library/azure/dn133798.aspx&gt;.)
[comment]: <> (TooSite MShermannd tareas punto que no se admite todavía con ARM)
[comment]: <> (MSSedusch -- &lt;https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/&gt;)

#### <a name="multi-site-vpn"></a>VPN de varios sitios
También en la actualidad, Azure ofrece conectividad de VPN de varios sitios de hello posibilidad toocreate para una suscripción de Azure. Anteriormente, una sola suscripción estaba limitado tooone conexión de VPN de sitio a sitio. Esta limitación desapareció con las conexiones VPN multisitio para suscripciones únicas. Esto hace posible tooleverage más de una región de Azure para una suscripción específica a través de las configuraciones entre entornos.

Para obtener documentación vea [este artículo][vpn-gateway-create-site-to-site-rm-powershell].

[comment]: <> (MShermannd TODO found no ARM docu link)

#### <a name="vnet-toovnet-connection"></a>TooVNet conexión de red virtual
Usar VPN de varios sitios, deberá tooconfigure una red Virtual de Azure independiente en cada una de las regiones de Hola. Sin embargo muy a menudo tienen requisitos de Hola que los componentes de software de hello en regiones diferentes Hola deben comunicarse entre sí. Lo ideal es que esta comunicación no se debería enrutar desde una región de Azure tooon local y desde ahí toohello otra región de Azure. tooshortcut, Azure ofrece Hola posibilidad tooconfigure una conexión de una red Virtual de Azure en tooanother de región una que red Virtual de Azure hospedada en otra región. Esta funcionalidad se denomina conexión de red virtual a red virtual. Se puede encontrar más información sobre esta funcionalidad aquí: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>TooAzure de conexión privada – ExpressRoute
Microsoft Azure ExpressRoute permite la creación de hello de conexiones privadas entre centros de datos de Azure y la infraestructura de local de cualquier cliente de Hola o en un entorno de ubicación compartida. ExpressRoute está disponible en varios proveedores de VPN de MPLS (conmutación por paquetes) u otros proveedores de servicios de red. Las conexiones ExpressRoute no pasan por hello Internet pública. Las conexiones ExpressRoute ofrecen mayor seguridad, más confiabilidad a través de varios circuitos paralelos, velocidades más rápidas y latencias más bajas que las típicas conexiones a través de Internet de Hola.

Se puede obtener más información sobre Azure ExpressRoute y su oferta aquí:

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

ExpressRoute permite varias suscripciones de Azure a través de un circuito ExpressRoute, como está documentado aquí

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Tunelización forzada en instalaciones entre locales
Para unirse a dominios de local a través de sitio a sitio, punto a sitio o ExpressRoute de las máquinas virtuales, debe toomake seguro de que se implemente también configuración de proxy de Internet de Hola para todos los usuarios de hello en esas máquinas virtuales también. De forma predeterminada, el software que se ejecuta en las VM o los usuarios que usen un Hola de tooaccess del explorador internet no pasan por el proxy de la empresa de hello, sino que se conectan directamente a través de Azure toohello internet. Pero la configuración de proxy de hello incluso no una solución al 100% toodirect Hola tráfico a través de proxy de la empresa de hello ya que es responsabilidad de toocheck de software y los servicios de proxy de Hola. Si el software que se ejecuta en hello VM no está haciendo que o un administrador modifica la configuración de hello, tráfico toohello Internet puede ser desviarse nuevo directamente a través de Azure toohello Internet.

En Ordenar tooavoid esto, puede configurar la tunelización forzada con conectividad de sitio a sitio entre local y Azure. Hello descripción detallada de la característica de tunelización forzada Hola se publica aquí <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Túnel forzado con ExpressRoute está habilitada por clientes que anuncian una ruta predeterminada a través de hello BGP de ExpressRoute sesiones de emparejamiento.

#### <a name="summary-of-azure-networking"></a>Resumen de las redes de Azure
Este capítulo contiene muchos puntos importantes sobre la red de Azure. Este es un resumen de los puntos principales de hello:

* Redes virtuales de Azure permite tooset de red de hello según tooyour propias necesidades
* Redes virtuales de Azure puede ser tooVMs de intervalos de dirección IP tooassign aprovechado o asignar tooVMs de direcciones IP fijas
* tooset un sitio a sitio o una conexión de punto a sitio necesita toocreate una red Virtual de Azure en primer lugar
* Una vez que se ha implementado una máquina virtual ya no es hello toochange posible que asignar toohello VM de red Virtual

### <a name="quotas-in-azure-virtual-machine-services"></a>Cuotas de los servicios de máquina virtual de Azure
Se necesita toobe borrar sobre hechos Hola dicho almacenamiento hello y la infraestructura de red se comparte entre máquinas virtuales que ejecutan una variedad de servicios de infraestructura de Azure de Hola. Y, al igual que en los centros de datos del cliente de hello, el aprovisionamiento es excesivo de algunos de los recursos de infraestructura de hello tiene lugar tooa grado. Hola plataforma Microsoft Azure utiliza disco, CPU, red y otros consumo de recursos de las cuotas toolimit hello y toopreserve un rendimiento constante y determinista.  Hola diferentes tipos de VM (A5, A6, etcetera) tienen diferentes cuotas para el número de Hola de discos, CPU, RAM y red.

> [!NOTE]
> Recursos de CPU y memoria de hello VM tipos compatibles con SAP se preasignan en nodos de host de Hola. Esto significa que una vez que se implementa Hola VM, recursos de hello en el host de hello estarán disponibles tal como se define por hello tipo de máquina virtual.
>
>

Al planificar y dimensionar SAP en soluciones de Azure Hola cuotas para cada tamaño de máquina virtual debe tener en cuenta.  se describen las cuotas de máquina virtual de Hello [aquí][virtual-machines-sizes].

cuotas de Hello descritas representan valores teóricos máximos de Hola.  límite de Hola de IOPS por VHD se puede lograr con IOs pequeños (8kb), pero posiblemente no puede lograr con IOs grandes (1Mb).  límite de IOPS de Hola se aplica en la granularidad de Hola de VHD únicos.

Siguiente árbol de decisión de hello puede usarse como un toodecide de árbol de decisión difícil si un sistema SAP se adapta a los servicios de máquinas virtuales de Azure y sus capacidades o si toobe configurado de forma distinta en el sistema de pedidos toodeploy hello en Azure, es necesario un sistema existente:

![Toodeploy de capacidad de toodecide de árbol de decisión SAP en Azure][planning-guide-figure-700]

**Paso 1**: Hola toostart de información más importante con es el requisito de SAPS de Hola para un sistema SAP determinado. requisitos de SAPS de Hello necesidad toobe separada en hello DBMS y elemento de aplicación de SAP de hello, incluso si Hola sistema SAP ya está implementado de forma local en una configuración de nivel 2. Para los sistemas existentes, Hola SAPS relacionados con hardware toohello en uso a menudo puede determinar o estimado se basa en las pruebas comparativas SAP existentes. resultados de Hola se pueden encontrar aquí: <http://global.sap.com/campaigns/benchmark/index.epx>.
Para los sistemas SAP recién implementados, debe haber pasado por un ejercicio de dimensionamiento que debería determinar los requisitos de sistema de Hola Hola.
Consulte también este blog y el documento adjunto para ver el ajuste de tamaño de SAP en Azure: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>.

**Paso 2**: para los sistemas existentes, Hola volumen de E/S y se deben medir las operaciones de E/S por segundo en el servidor DBMS Hola. Para los sistemas recién planificados, Hola ejercicio para el nuevo sistema de Hola de ajuste de tamaño también debe dar ideas aproximadas de los requisitos de E/S de hello en hello lado DBMS. Si no está seguro, deberá finalmente tooconduct una prueba de concepto.

**Paso 3**: requisito de SAPS Hola de comparación para hello proporciona DBMS servidor con hello SAPS Hola diferentes tipos de VM de Azure. información de Hello en SAP de diferentes tipos de máquina virtual de Azure Hola se documenta en la nota de SAP [1928533]. enfoque de Hello debe estar en hello VM de DBMS en primer lugar ya que capa de base de datos de hello es capa de hello en un sistema SAP NetWeaver que no se escala horizontalmente en la mayoría de Hola de implementaciones. En cambio, la capa de aplicación de SAP de Hola se puede escalar horizontalmente. Si ninguno de hello SAP admite tipos de VM de Azure pueden entregar los SAPS Hola necesario, no se puede ejecutar la carga de trabajo de Hola de sistema SAP de hello planeada en Azure. O bien deberá toodeploy Hola sistema local o necesitará volumen de carga de trabajo de toochange Hola Hola sistema.

**Paso 4**: Como se documenta [aquí][virtual-machines-sizes], Azure exige una cuota de E/S por segundo para cada VHD, al margen de si se usa almacenamiento estándar o premium. Dependiente de hello tipo de máquina virtual, número de Hola de discos duros virtuales que se pueden montar varía. Como resultado, puede calcular un número máximo de IOPS que se pueden lograr con cada uno de los diferentes tipos de VM Hola. Depende de la disposición de archivos de base de datos de hello, puede crear bandas toobecome un volumen de discos duros virtuales en el sistema operativo invitado de Hola. Sin embargo, si Hola volumen actual que tiene IOPS de un sistema SAP implementado supera los límites de hello calculado del tipo de máquina virtual más grande de Hola de Azure y si no hay ningún toocompensate oportunidad con más memoria, carga de trabajo de Hola de hello sistema SAP puede verse gravemente afectada. En tales casos, puede presionar un punto donde no se debe implementar sistema hello en Azure.

**Paso 5**: especialmente en SAP sistemas que están implementados localmente en configuraciones de 2 niveles, las posibilidades de hello son que el sistema de hello quizás sea necesario toobe configurado en Azure en una configuración de 3 niveles. En este paso, necesita toocheck si hay un componente de nivel de aplicación de SAP de Hola que no se puede escalar horizontalmente y que no se adaptaría a hello CPU y memoria recursos Hola otra oferta de tipos de máquina virtual de Azure. Si realmente hay un componente de ese tipo, sistema SAP de Hola y su carga de trabajo no se puede implementar en Azure. Pero si puede escalar horizontalmente Hola aplicación SAP se pueden implementar componentes en varias máquinas virtuales de Azure, sistema de hello en Azure.

**Paso 6**: si Hola DBMS y los componentes de capa de aplicación de SAP se pueden ejecutar en máquinas virtuales de Azure, configuración de hello debe toobe definido con respecto a:

* Número de máquinas virtuales de Azure
* Tipos de VM para componentes individuales de Hola
* Número de discos duros virtuales de VM de DBMS tooprovide suficientes IOPS

## <a name="managing-azure-assets"></a>Administración de activos de Azure
### <a name="azure-portal"></a>Portal de Azure
Hola Portal de Azure es uno de los tres implementaciones de máquina virtual de Azure toomanage de interfaces. tareas de administración básicas de Hello, como la implementación de máquinas virtuales entre varias imágenes, pueden realizarse a través de hello Portal de Azure. Además, creación de hello de cuentas de almacenamiento, redes virtuales y otros componentes de Azure también son Hola tareas Portal de Azure puede controlar muy bien. Sin embargo, la funcionalidad como cargar archivos VHD de local tooAzure o copiando un VHD en Azure son tareas que requieren herramientas de terceros o de administración a través de PowerShell o CLI.

![Portal de Microsoft Azure - información general sobre las máquinas virtuales][planning-guide-figure-800]

[comment]: <> (MSSedusch * &lt;https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/&gt;)
[comment]: <> (MSSedusch * &lt;https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/&gt;)

Tareas de administración y configuración de instancia de la máquina Virtual de hello son posibles desde Hola Portal de Azure.

Además de reiniciar y apagar una máquina Virtual puede también adjuntar, separar y crear discos de datos para la instancia de máquina Virtual de hello, instancia de hello toocapture para la preparación de imagen y configurar el tamaño de la instancia de la máquina Virtual de Hola Hola.

Hola Portal de Azure proporciona funcionalidad básica toodeploy y configurar las máquinas virtuales y muchos otros servicios de Azure. Sin embargo no toda funcionalidad disponible está cubierta por hello Portal de Azure. Hola Portal de Azure, no es posible tooperform tareas como:

* Cargar discos duros virtuales tooAzure
* Copiar máquinas virtuales

[comment]: <> (MShermannd TODO what about automation service for SAP VMs ? )
[comment]: <> (MSSedusch deployment of multiple VMs os meanwhile possible)
[comment]: <> (MSSedusch también cualquier tipo de automatización con respecto a la implementación no es posible con hello portal de Azure. Tareas como la implementación con guion de varias máquinas virtuales no es posible a través de hello Portal de Azure.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Administración mediante los cmdlets de Microsoft Azure PowerShell
Windows PowerShell es un marco eficaz y extensible que ha tenido una amplia adopción entre clientes que implementan un mayor número de sistemas en Azure. Después de la instalación de Hola de cmdlets de PowerShell en un escritorio, portátil o estación de administración dedicada, Hola cmdlets de PowerShell se puede ejecutar de forma remota.

Hola proceso tooenable un escritorio/portátil local para el uso de Hola de cmdlets de PowerShell de Azure y cómo tooconfigure los de Hola uso con hello Azure suscripciones se describe en [este artículo][powershell-install-configure].

También pueden encontrarse en pasos más detallados sobre cómo tooinstall, actualizar y configurar los cmdlets de PowerShell de Azure de hello [este capítulo de la Guía de implementación de hello][deployment-guide-4.1].

Experiencia del usuario hasta ahora ha sido que PowerShell (PS) es ciertamente Hola más eficaz herramienta toodeploy máquinas virtuales y toocreate personalizada de los pasos de implementación de Hola de máquinas virtuales. Todos los clientes de hello ejecutan instancias de SAP en Azure utilizan PS cmdlets toosupplement las tareas de administración que no Hola Portal de Azure o incluso están utilizando los cmdlets de PS exclusivamente toomanage sus implementaciones en Azure. Puesto que el recurso compartido de Azure cmdlets específicos de Hola Hola misma convención de nomenclatura como hello más de 2000 cmdlets relacionados de Windows, es una forma sencilla de tareas de Windows administradores tooleverage estos cmdlets.

Consulte el ejemplo aquí: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>.

[comment]: <> (MShermannd TODO describe new CLI command when tested )
Implementación de hello extensión de supervisión de Azure para SAP (consulte el capítulo [solución de supervisión de Azure para SAP] [ planning-guide-9.1] en este documento) solo es posible a través de PowerShell o CLI. Por lo tanto, es obligatorio toosetup y configurar PowerShell o CLI al implementar o administrar un sistema SAP NetWeaver en Azure.  

Como Azure ofrece más funcionalidad, nuevos cmdlets de PS va toobe agregado que requiere una actualización de los cmdlets de Hola. Por lo tanto, dificulta la Hola de sentido toocheck sitio de descargas de Azure de al menos una vez al mes de hello <https://azure.microsoft.com/downloads/> para una nueva versión de hello cmdlets. solo se instalará la nueva versión de Hello encima de la versión anterior de Hola.

Para ver una lista general de comandos de PowerShell relacionados con Azure, consulte aquí: <https://msdn.microsoft.com/library/azure/dn708514.aspx>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Administración a través de los comandos de CLI de Microsoft Azure
Para clientes que utilizan Linux y desea toomanage Azure Powershell de recursos no sea una opción. Microsoft ofrece la CLI de Azure como una alternativa.
Hola CLI de Azure proporciona un conjunto de código abierto, multiplataforma comandos para trabajar con hello plataforma de Azure. Hola CLI de Azure proporciona gran parte de la misma funcionalidad que se encuentra en hello portal de Azure de Hola.

Para obtener información acerca de la instalación, configuración y funcionamiento de los comandos tooaccomplish toouse CLI vea tareas de Azure

* [Instalar Hola CLI de Azure][xplat-cli]
* [Implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y Hola CLI de Azure][virtual-machines-linux-cli-deploy-templates]
* [Usar hello CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure][xplat-cli-azure-resource-manager]

Lea también el capítulo [CLI de Azure para máquinas virtuales Linux] [ deployment-guide-4.5.2] en hello [Guía de implementación] [ planning-guide] en cómo toouse CLI de Azure toodeploy hello Azure Extensión de supervisión para SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Toodeploy de maneras diferentes máquinas virtuales para SAP en Azure
En este capítulo aprenderá diferentes maneras de hello toodeploy una máquina virtual en Azure. En este capítulo también se tratan los procedimientos de preparación adicionales, así como la administración de VHD y máquinas virtuales en Azure.

### <a name="deployment-of-vms-for-sap"></a>Implementación de máquinas virtuales para SAP
Microsoft Azure ofrece varias maneras de toodeploy las máquinas virtuales y discos de asociados. Por tanto, es muy importante toounderstand diferencias de hello ya preparados de máquinas virtuales de hello pueden diferir según el método hello de implementación. En general, tomaremos un vistazo a Hola los escenarios siguientes:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Mover una máquina virtual de tooAzure local con un disco no generalizado
Planee toomove un sistema SAP específico desde tooAzure local. Esto puede realizarse mediante la carga de hello VHD que contiene Hola SO, Hola archivos binarios de los archivos binarios de SAP y DBMS más Hola discos duros virtuales con datos de Hola y archivos de registro de hello DBMS tooAzure. En cambio demasiado[escenario #2 siguiente][planning-guide-5.1.2], mantener el nombre de host de hello, SID de SAP y las cuentas de usuario SAP en hello Azure VM tal y como se configuraron en el entorno local de Hola. Por lo tanto, no es necesario generalizar la imagen de Hola. Vea capítulos [antes de mover una máquina virtual de tooAzure local con un disco no generalizado] [ planning-guide-5.2.1] de este documento para los pasos de preparación locales y la carga de máquinas virtuales no generalizado o discos duros virtuales tooAzure. Lea el capítulo [escenario 3: mover una máquina virtual de manera local mediante un VHD de Azure no generalizado con SAP] [ deployment-guide-3.4] en hello [Guía de implementación] [ deployment-guide]para obtener pasos detallados de la implementación de dicha imagen en Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Implementación de una máquina virtual con una imagen específica del cliente
Debido a toospecific los requisitos de revisión de la versión de SO o DBMS, imágenes de hello proporcionado en hello Azure Marketplace no podrían ajustarlo a sus necesidades. Por lo tanto, tendrá que toocreate una máquina virtual mediante su propia imagen de VM de SO o DBMS 'private' que se puede implementar varias veces con posterioridad. tooprepare una imagen 'privada' para la duplicación, Hola siguientes elementos tiene toobe considera:


[comment]: <> (MSSedusch &gt; See more details here :)
[comment]: <> (MShermannd TODO first link is about classic model. No se encontró un artículo del documento de Azure)
[comment]: <> (MSSedusch &gt; &lt;https://azure.microsoft.com/documentation/articles/virtual-machines-create-upload-vhd-windows-server/&gt;)
[comment]: <> (MSSedusch &gt; &lt;http://blogs.technet.com/b/blainbar/archive/2014/09/12/modernizing-your-infrastructure-with-hybrid-cloud-using-custom-vm-images-and-resource-groups-in-microsoft-azure-part-21-blain-barton.aspx&gt;)
- - -
> ![Windows][Logo_Windows] Windows
>
> Hola Windows Configuración (como SID de Windows y el nombre de host) debe ser resumir/generalizar en hello local de VM a través de comandos de sysprep de Hola.
>
>
> ![Linux][Logo_Linux] Linux
>
> Siga los pasos de Hola se describe en los siguientes artículos para [SUSE] [ virtual-machines-linux-create-upload-vhd-suse] o [Red Hat] [ virtual-machines-linux-redhat-create-upload-vhd] tooprepare toobe de un disco duro virtual cargado tooAzure.
>
>

- - -
Si ya ha instalado contenido de SAP en la VM local (especialmente para sistemas de 2 niveles), puede adaptar la configuración del sistema SAP Hola después de implementación de Hola de hello Azure VM a través de la instancia de hello cambiar el nombre de procedimiento admite Hola aprovisionamiento de Software de SAP Administrador (Nota de SAP [1619720]). Consulte los capítulos [preparación para la implementación de una máquina virtual con una imagen específica del cliente para SAP] [ planning-guide-5.2.2] y [cargar un VHD local tooAzure] [ planning-guide-5.3.2]de este documento para los pasos de preparación locales y la carga de un tooAzure generalizado de máquina virtual. Lea el capítulo [escenario 2: implementar una máquina virtual con una imagen personalizada para SAP] [ deployment-guide-3.3] en hello [Guía de implementación] [ deployment-guide] para obtener pasos detallados de implementar dicha imagen en Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Implementar una máquina virtual de hello Azure Marketplace
Le gustaría toouse Microsoft o 3ª parte que proporciona la imagen de máquina virtual de hello Azure Marketplace toodeploy la máquina virtual. Una vez implementada la máquina virtual en Azure, siga Hola Hola mismas instrucciones y herramientas tooinstall software SAP o DBMS en la máquina virtual como lo haría en un entorno local. Para obtener más descripción de la implementación, consulte el capítulo [escenario 1: implementar una máquina virtual de hello Azure Marketplace para SAP] [ deployment-guide-3.2] en hello [Guía de implementación de] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Preparación de máquinas virtuales con SAP para Azure
Antes de cargar las VM en Azure debe toomake seguro hello las máquinas virtuales y discos duros virtuales cumplan ciertos requisitos. Existen pequeñas diferencias según el método de implementación de Hola que se usa.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Preparación para mover una máquina virtual de tooAzure local con un disco no generalizado
Un método de implementación común es toomove una máquina virtual existente que se ejecuta un sistema SAP desde tooAzure local. Que VM Hola sistema SAP en hello VM debe simplemente ejecutarse en Azure mediante Hola el mismo nombre de host y muy probablemente Hola mismo SID de SAP. En este caso no debe generalizarse invitado Hola SO de VM para varias implementaciones. Si la red local de Hola se extendió hacia Azure (consulte el capítulo [entre entornos de implementación de una o varias máquinas virtuales de SAP en Azure con el requisito de Hola de que se integra totalmente en la red local de hello] [ planning-guide-2.2] en este documento), a continuación, incluso Hola mismas cuentas de dominio pueden usarse en hello VM puesto que se usaron antes de local.

Estos son los requisitos que se deben cumplir a la hora de preparar su propio disco de VM de Azure:

* Originalmente Hola VHD contenedor Hola operativo sistema podría tener un tamaño máximo de 127GB. Esta limitación se obtuvo elimina al final de Hola de marzo de 2015. Ahora hello VHD que contiene el sistema operativo de hello pueden funcionar too1TB tamaño como cualquier otra unidad de almacenamiento Azure hospedada VHD así.

[comment]: <> (MShermannd TODO tiene toocheck si CLI también convierte toostatic)
* Debe toobe Hola formato de disco duro virtual fijo. Los VHD dinámicos o en formato VHDx aún no se admiten en Azure. Los VHD dinámicos será toostatic convertir discos duros virtuales al cargar Hola VHD con los cmdlets de PowerShell o CLI
* Discos duros virtuales que están montado toohello VM y deben volver a montarse en toohello Azure VM necesidad toobe en un formato de disco duro virtual fijo también. Hello mismo límite de tamaño de disco del sistema operativo Hola aplica toodata discos también. Los VHD pueden tener un tamaño máximo de 1 TB. Los VHD dinámicos será toostatic convertir discos duros virtuales al cargar Hola VHD con los cmdlets de PowerShell o CLI
* Agregar se puede utilizar otra cuenta local con privilegios de administrador que se puede usar soporte técnico de Microsoft o que se pueda asignar como contexto para toorun de servicios y aplicaciones en hasta Hola que se implementa la VM y usuarios más adecuados.
* En caso de hello del uso de un escenario de implementación solo en la nube (consulte el capítulo [solo en la nube: las implementaciones de máquina Virtual en Azure sin dependencias de hello local red cliente] [ planning-guide-2.1] de este documentos) en combinación con este método de implementación, dominio cuentas podrían no funcionar una vez Hola disco de Azure se implementa en Azure. Esto es especialmente cierto para las cuentas que son servicios toorun usado como Hola DBMS o aplicaciones SAP. Por lo tanto, es necesario tooreplace estas cuentas de dominio con cuentas locales de VM y eliminar cuentas de dominio local de Hola Hola máquina virtual. Mantener los usuarios del dominio local en la imagen de máquina virtual de hello no es un problema cuando se implementa Hola VM en el escenario de hello entre entornos tal como se describe en el capítulo [entre entornos de implementación de una o varias máquinas virtuales de SAP en Azure con el requisito de Hola de que se va a totalmente integrado en la red local de hello] [ planning-guide-2.2] en este documento.
* Si las cuentas de dominio se usaron como inicios de sesión DBMS o los usuarios cuando se ejecuta el sistema hello en local y en esas máquinas virtuales deben toobe implementado en escenarios de solo en la nube, los usuarios de dominio de hello necesitan toobe eliminado. Necesita toomake seguro de que el administrador local de hello más otro usuario local de VM se agrega como un usuario de inicio de sesión en hello DBMS como administradores.
* Agregue otras cuentas locales como los que podrían ser necesarios para el escenario de implementación concreto de Hola.

- - -
> ![Windows][Logo_Windows] Windows
>
> En este escenario no generalización (sysprep) de hello VM es necesario tooupload e implementar Hola VM en Azure.
> Asegúrese de que la unidad D:\ no se esté usando. Configure el montaje automático para los discos conectados tal y como se describe en el capítulo [Configuración de montaje automático para discos conectados][planning-guide-5.5.3] del presente documento.
>
> ![Linux][Logo_Linux] Linux
>
> En este escenario no generalización (waagent-deprovision) del programa Hola a máquina virtual, es necesario tooupload e implementar Hola VM en Azure.
> Asegúrese de que no se usa /mnt/resource y de que todos los discos se montan mediante UUID. Para el disco de SO Hola Asegúrese de que entrada del cargador de arranque de hello también refleja montaje basada en el uuid de Hola.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Preparación para la implementación de una máquina virtual con una imagen específica del cliente para SAP
Los archivos VHD que contienen un SO generalizado también se almacenan en contenedores en cuentas de almacenamiento de Azure. Puede implementar una nueva máquina virtual de, una imagen de disco duro virtual haciendo referencia a Hola VHD como un disco duro virtual en los archivos de plantilla de implementación de origen tal como se describe en el capítulo [escenario 2: implementar una máquina virtual con una imagen personalizada para SAP] [ deployment-guide-3.3] de hello [Guía de implementación][deployment-guide].

Estos son los requisitos que se deben cumplir a la hora de preparar su propia imagen de VM de Azure:

* Originalmente Hola VHD contenedor Hola operativo sistema podría tener un tamaño máximo de 127GB. Esta limitación se obtuvo elimina al final de Hola de marzo de 2015. Ahora hello VHD que contiene el sistema operativo de hello pueden funcionar too1TB tamaño como cualquier otra unidad de almacenamiento Azure hospedada VHD así.

[comment]: <> (MShermannd TODO tiene toocheck si CLI también convierte toostatic)
* Debe toobe Hola formato de disco duro virtual fijo. Los VHD dinámicos o en formato VHDx aún no se admiten en Azure. Los VHD dinámicos será toostatic convertir discos duros virtuales al cargar Hola VHD con los cmdlets de PowerShell o CLI
* Discos duros virtuales que están montado toohello VM y deben volver a montarse en toohello Azure VM necesidad toobe en un formato de disco duro virtual fijo también. Hello mismo límite de tamaño de disco del sistema operativo Hola aplica toodata discos también. Los VHD pueden tener un tamaño máximo de 1 TB. Los VHD dinámicos será toostatic convertir discos duros virtuales al cargar Hola VHD con los cmdlets de PowerShell o CLI
* Puesto que todos los usuarios de dominio registrados como los usuarios de hello VM no existirán en un escenario solo en la nube de Hola (consulte el capítulo [solo en la nube: las implementaciones de máquina Virtual en Azure sin dependencias de hello local red cliente] [ planning-guide-2.1] de este documento), los servicios con ese dominio las cuentas podrían no funcionar una vez Hola imagen se implementa en Azure. Esto es especialmente cierto para las cuentas que son utilizados toorun servicios como DBMS o aplicaciones SAP. Por lo tanto, es necesario tooreplace estas cuentas de dominio con cuentas locales de VM y eliminar cuentas de dominio local de Hola Hola máquina virtual. Mantener los usuarios del dominio local en la imagen de máquina virtual de hello no podría ser un problema cuando Hola VM está implementada en hello escenario entre locales como se describe en el capítulo [entre entornos de implementación de una o varias máquinas virtuales de SAP en Azure con el requisito de Hola de se integra totalmente en la red local de hello] [ planning-guide-2.2] en este documento.
* Agregar se puede utilizar otra cuenta local con privilegios de administrador que se puede usar soporte técnico de Microsoft en las investigaciones de problemas o que se pueda asignar como contexto para toorun de servicios y aplicaciones en hasta Hola que se implementa la VM y usuarios más adecuados.
* En las implementaciones que solo en la nube y donde las cuentas de dominio se usaron como inicios de sesión DBMS o los usuarios cuando se ejecuta Hola sistema local, deben eliminarse los usuarios del dominio Hola. Necesita toomake seguro de que el administrador local de hello más otro usuario local de VM se agrega como un inicio de sesión o usuario de hello DBMS como administradores.
* Agregue otras cuentas locales como los que podrían ser necesarios para el escenario de implementación concreto de Hola.
* Si la imagen de hello contiene una instalación de SAP NetWeaver y es probable que el cambio de nombre de nombre de host de hello del nombre original de hello en el momento de Hola de hello implementación de Azure, es toocopy recomendada Hola versiones más recientes del DVD de administrador de aprovisionamiento de Software SAP de hello en plantilla de Hola. Esto le permitirá tooeasily uso Hola SAP siempre rename funcionalidad tooadapt Hola cambiar nombre de host o cambio Hola SID del sistema SAP dentro de Hola Hola implementa la imagen de máquina virtual en cuanto se inicia una nueva copia.

- - -
> ![Windows][Logo_Windows] Windows
>
> Asegúrese de que la unidad D:\ no se esté usando. Configure el montaje automático para los discos conectados tal y como se describe en el capítulo [Configuración de montaje automático para discos conectados][planning-guide-5.5.3] del presente documento.
>
> ![Linux][Logo_Linux] Linux
>
> Asegúrese de que no se usa /mnt/resource y de que todos los discos se montan mediante UUID. Hola SO disco Asegúrese entrada del cargador de arranque de hello también refleja montaje basada en el uuid de Hola.
>
>

- - -
* GUI de SAP (para fines de administración e instalación) pueden estar ya instalados en dicha plantilla.
* Cambiar el nombre de otro software necesario toorun hello las máquinas virtuales correctamente en escenarios entre locales puede instalarse como este software puede trabajar con hello de hello máquina virtual.

Si es lo suficientemente preparada Hola VM toobe genérica y finalmente independiente de cuentas/usuarios no está disponibles en hello como destino el escenario de implementación de Azure, se lleva a cabo el último paso de preparación Hola de generalización de esta imagen.

##### <a name="generalizing-a-vm"></a>Generalización de una máquina virtual
- - -
[comment]: <> (MShermannd TODO tiene toofind crear mejores artículos / documento sobre cómo generalizar Hola máquinas virtuales de ARM)
> ![Windows][Logo_Windows] Windows
>
> Hola último paso es toolog en tooa VM con una cuenta de administrador. Abra una ventana de comandos de Windows como administrador. Vaya too...\windows\system32\sysprep y ejecute sysprep.exe.
> Se mostrará una pequeña ventana. Es importante toocheck hello 'Generalizar' opción (no se controle de forma predeterminada de hello) y cambiar Hola opción de cierre debido a su valor predeterminado de 'Reiniciar' too'Shutdown'. Este procedimiento se supone que el proceso de sysprep de hello es ejecutada de forma local en hello SO invitado de una máquina virtual.
> Si desea procedimiento de hello tooperform con una máquina virtual que se esté ejecutando en Azure, siga los pasos de hello descritos en [este artículo][virtual-machines-windows-capture-image].
>
> ![Linux][Logo_Linux] Linux
>
> [¿Cómo toocapture un toouse de máquina virtual Linux como una plantilla de administrador de recursos][virtual-machines-linux-capture-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Transferir las máquinas virtuales y discos duros virtuales entre locales tooAzure
Dado que cargar tooAzure de imágenes y discos de máquina virtual no es posible a través de hello Portal de Azure, deberá toouse cmdlets de Azure PowerShell o CLI. Otra posibilidad es utilizar Hola Hola herramienta 'AzCopy'. herramienta de Hello puede copiar discos duros virtuales entre locales y Azure (en ambas direcciones). También puede copiar discos duros virtuales entre las regiones de Azure. Consulte [esta documentación][storage-use-azcopy] para conocer cómo descargar y usar AzCopy.

Una tercera alternativa sería toouse diversas herramientas de interfaz gráfica de usuario orientada a servicios de terceros. Sin embargo, asegúrese de que estas herramientas son compatibles con los blobs en páginas de Azure. Para nuestros propósitos necesitamos toouse Azure Blob en páginas store (Hola diferencias se describen aquí: <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>). También herramientas Hola proporcionadas por Azure son muy eficaces al comprimir hello las máquinas virtuales y discos duros virtuales que necesitan toobe cargado. Esto es importante porque esta eficacia en la compresión reduce el tiempo de carga de hello (que depende de todas formas Hola carga vínculo toohello internet desde las instalaciones locales de Hola y la región de implementación de Azure Hola de destino). Es una suposición razonable que cargar una VM o VHD de datos de Azure ubicación europea toohello sede en Estados Unidos centros tardará más tiempo que cargar Hola mismos centros de datos de máquinas virtuales/discos duros virtuales toohello Azure europeos.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Cargar un VHD local tooAzure
una máquina virtual existente o un VHD de hello local dicha VM de red o disco duro virtual tiene requisitos de hello toomeet como se muestra en el capítulo tooupload [antes de mover una máquina virtual de tooAzure local con un disco no generalizado] [ planning-guide-5.2.1] de este documento.

Dicha VM no es necesario toobe generalizado y se puede cargar en estado de Hola y la forma que ha apagado en hello lado local de una vez. Hello mismo puede decirse de discos duros virtuales adicionales que no contienen ningún sistema operativo.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Carga de un VHD y su conversión en un disco de Azure
En este caso se desea tooupload un disco duro virtual, con o sin un sistema operativo y monta tooa máquina virtual como un disco de datos o utilizarlo como disco del sistema operativo. Se trata de un proceso compuesto por varios pasos.

**PowerShell**

* Suscripción de inicio de sesión tooyour con *AzureRmAccount de inicio de sesión*
* Establecer suscripción Hola de su contexto con *conjunto AzureRmContext* y consulte el parámetro Id. de suscripción o SubscriptionName - <https://msdn.microsoft.com/library/mt619263.aspx>
* Cargar Hola VHD con *agregar AzureRmVhd* tooan cuenta de almacenamiento de Azure - vea <https://msdn.microsoft.com/library/mt603554.aspx>
* Disco de hello SO de conjunto de un nuevo toohello de configuración de máquina virtual VHD con *conjunto AzureRmVMOSDisk* -vea <https://msdn.microsoft.com/library/mt603746.aspx>
* Crear una nueva máquina virtual desde la configuración de máquina virtual de hello con *New-AzureRmVM* -vea <https://msdn.microsoft.com/library/mt603754.aspx>
* Agregar un tooa de disco de datos nueva máquina virtual con *agregar AzureRmVMDataDisk* -vea <https://msdn.microsoft.com/library/mt603673.aspx>

**CLI de Azure**

* Modo de administrador de recursos de conmutador tooAzure con *arm de modo de configuración de azure*
* Suscripción de inicio de sesión tooyour con *inicio de sesión de azure*
* Seleccione su suscripción con *azure account set`<subscription name or id`>*.
* Cargar Hola VHD con *carga de blobs de almacenamiento de azure* -vea [Using Hola CLI de Azure con el almacenamiento de Azure][storage-azure-cli]
* Crear una nueva máquina virtual especificando Hola carga VHD como disco del sistema operativo con *crear la máquina virtual de azure* y el parámetro -d
* Agregar un tooa de disco de datos nueva máquina virtual con *vm disco adjuntar-nuevo*

**Plantilla**

* Cargar Hola disco duro virtual con Powershell o CLI de Azure
* Implementar Hola VM con una plantilla JSON que hacen referencia a Hola VHD tal y como se muestra en [esta plantilla JSON de ejemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-from-specialized-vhd/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Implementación de una imagen de máquina virtual
una máquina virtual existente o un VHD de hello local red en orden toouse como una imagen de máquina virtual de Azure dicha VM o VHD necesita requisitos de hello toomeet enumerados en el capítulo tooupload [preparación para la implementación de una máquina virtual con una imagen específica del cliente para SAP] [ planning-guide-5.2.2] de este documento.

* Uso *sysprep* en Windows o *waagent-deprovision* en Linux toogeneralize el VM - vea [cómo toocapture una máquina virtual de Windows en la implementación del Administrador de recursos de hello modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] o [cómo toocapture una toouse de máquina virtual Linux como una plantilla de administrador de recursos][virtual-machines-linux-capture-image-capture]
* Suscripción de inicio de sesión tooyour con *AzureRmAccount de inicio de sesión*
* Establecer suscripción Hola de su contexto con *conjunto AzureRmContext* y consulte el parámetro Id. de suscripción o SubscriptionName - <https://msdn.microsoft.com/library/mt619263.aspx>
* Cargar Hola VHD con *agregar AzureRmVhd* tooan cuenta de almacenamiento de Azure - vea <https://msdn.microsoft.com/library/mt603554.aspx>
* Conjunto Hola SO disco de un nuevo toohello de configuración de máquina virtual VHD con *AzureRmVMOSDisk Set - SourceImageUri - CreateOption fromImage* -vea <https://msdn.microsoft.com/library/mt603746.aspx>
* Crear una nueva máquina virtual desde la configuración de máquina virtual de hello con *New-AzureRmVM* -vea <https://msdn.microsoft.com/library/mt603754.aspx>

**CLI de Azure**

* Uso *sysprep* en Windows o *waagent-deprovision* en Linux toogeneralize el VM - vea [cómo toocapture una máquina virtual de Windows en la implementación del Administrador de recursos de hello modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] o [cómo toocapture una toouse de máquina virtual Linux como una plantilla de administrador de recursos] [ virtual-machines-linux-capture-image-capture] para Linux
* Modo de administrador de recursos de conmutador tooAzure con *arm de modo de configuración de azure*
* Suscripción de inicio de sesión tooyour con *inicio de sesión de azure*
* Seleccione su suscripción con *azure account set`<subscription name or id`>*.
* Cargar Hola VHD con *carga de blobs de almacenamiento de azure* -vea [Using Hola CLI de Azure con el almacenamiento de Azure][storage-azure-cli]
* Crear una nueva máquina virtual especificando Hola carga VHD como disco del sistema operativo con *crear la máquina virtual de azure* y los parámetros -Q

**Plantilla**

* Uso *sysprep* en Windows o *waagent-deprovision* en Linux toogeneralize el VM - vea [cómo toocapture una máquina virtual de Windows en la implementación del Administrador de recursos de hello modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] o [cómo toocapture una toouse de máquina virtual Linux como una plantilla de administrador de recursos] [ virtual-machines-linux-capture-image-capture] para Linux
* Cargar Hola disco duro virtual con Powershell o CLI de Azure
* Implementar Hola VM con una plantilla JSON que hacen referencia a imagen Hola VHD tal y como se muestra en [esta plantilla JSON de ejemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-tooon-premises"></a>Descargar VHD tooon local
Infraestructura de Azure como un servicio no es una calle unidireccional de solo está tooupload capaz de discos duros virtuales y los sistemas SAP. Puede mover SAP sistemas de Azure nuevo en Hola a todos en local así.

Durante el tiempo de Hola de descarga de Hola Hola discos duros virtuales no puede estar activo. Incluso cuando se descargan los discos duros virtuales que están montados tooVMs, Hola VM debe toobe apagado. Si sólo desea buscar base de datos de Hola a toodownload contenido que, a continuación, debe ser tooset usa un sistema nuevo local y si es aceptable que durante el tiempo de Hola de hello descargar y Hola el programa de instalación del sistema nuevo Hola que Hola sistema en Azure todavía puede estar operativo , puede evitar un largo período de inactividad mediante la realización de una copia de seguridad de base de datos comprimida en un disco duro virtual y simplemente descargar que el disco duro virtual en lugar de descargar también Hola VM base del SO.

#### <a name="powershell"></a>PowerShell
Una vez que se ha detenido el sistema SAP de Hola y Hola VM está apagada, puede usar el cmdlet de PowerShell de hello AzureRmVhd guardar en hello local discos VHD de destino toodownload Hola hacer copia de mundo de toohello local. En orden toodo esto, necesita Hola URL de disco duro virtual que se puede encontrar en hello 'Almacenamiento Section' hello de hello Portal de Azure (necesidad toonavigate toohello hello y cuenta de almacenamiento contenedor de almacenamiento donde hello VHD creó) y necesita tooknow donde hello VHD debe ser copia en.

A continuación, puede aprovechar comando hello simplemente definiendo el parámetro hello SourceUri como dirección URL de Hola de toodownload de disco duro virtual de Hola y Hola LocalFilePath como ubicación física de Hola de hello VHD (incluido su nombre). comando Hello podría ser similar:

```powerhell
Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
```

Para obtener más detalles del cmdlet de hello AzureRmVhd guardar, revise lo siguiente <https://msdn.microsoft.com/library/mt622705.aspx>.

#### <a name="cli"></a>CLI
Una vez que se ha detenido el sistema SAP de Hola y Hola VM está apagada, puede usar descarga de blobs de almacenamiento de azure de comando de hello CLI de Azure en hello local discos VHD de destino toodownload Hola hacer copia de mundo de toohello local. En orden toodo esto, necesita nombre de Hola y el contenedor de Hola de disco duro virtual que se puede encontrar en hello 'Almacenamiento Section' hello de hello Portal de Azure (necesidad toonavigate toohello hello y cuenta de almacenamiento contenedor de almacenamiento donde hello VHD creó) y necesita tooknow donde Hola VHD debe copiarse al.

A continuación, puede aprovechar comando hello definiendo simplemente blobs de parámetros de Hola y el contenedor de toodownload de disco duro virtual de Hola y de destino de hello como ubicación de destino físico Hola de hello VHD (incluido su nombre). comando Hello podría ser similar:

```
azure storage blob download --blob <name of hello VHD toodownload> --container <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --destination <destination of hello VHD toodownload>
```

### <a name="transferring-vms-and-vhds-within-azure"></a>Transferencia de máquinas y discos duros virtuales dentro de Azure
#### <a name="copying-sap-systems-within-azure"></a>Copia de los sistemas SAP en Azure
Un sistema SAP o incluso un servidor DBMS dedicado que admita un nivel de aplicación de SAP probablemente se constan de varios discos duros virtuales que contengan cualquier Hola SO con archivos binarios de Hola u Hola datos y registrar los archivos de base de datos SAP de Hola. Hola Azure funcionalidad de copiar discos duros virtuales ni hello Azure funcionalidad de guardar toodisk de discos duros virtuales tiene un mecanismo de sincronización que tomaría instantánea varios discos duros virtuales de forma sincrónica. Por lo tanto, se copian o se guardan discos duros virtuales aunque se hayan montado estado Hola de hello contra Hola misma VM sería diferente. Esto significa que en caso concreto de Hola de tener datos diferentes y registro contenido en diferentes discos duros virtuales de Hola, Hola base de datos final de Hola sería incoherente.

**Conclusión: En orden toocopy o guardar discos duros virtuales que forman parte de una configuración de sistema SAP necesita toostop Hola SAP sistema y también debe tooshut hacia abajo Hola implementa máquina virtual. Solo puede copiar o descarga Hola conjunto de discos duros virtuales tooeither crear una copia del sistema SAP de hello en Azure o de forma local.**

Discos de datos se almacenan como archivos de disco duro virtual en una cuenta de almacenamiento de Azure y se pueden conectar máquina virtual de tooa directamente o puede usar como una imagen. En este caso, Hola VHD es la ubicación de tooanother copiado antes beeing adjunta la máquina virtual de toohello. nombre completo de Hello del archivo de disco duro virtual de hello en Azure debe ser único dentro de Azure. Como ya se ha mencionado anteriormente, nombre hello es tipo de un nombre de tres partes que el siguiente aspecto:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

##### <a name="powershell"></a>PowerShell
Puede usar cmdlets de PowerShell de Azure toocopy un disco duro virtual como se muestra en [este artículo][storage-powershell-guide-full-copy-vhd].

##### <a name="cli"></a>CLI
Puede usar Azure CLI toocopy un disco duro virtual como se muestra en [este artículo][storage-azure-cli-copy-blobs]

##### <a name="azure-storage-tools"></a>Herramientas de Almacenamiento de Azure
* <http://azurestorageexplorer.codeplex.com/releases/view/125870>

También hay ediciones profesionales del Explorador de almacenamiento de Azure, que podrá encontrar aquí:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

copia de Hola de un VHD dentro de una cuenta de almacenamiento es un proceso que tarda unos pocos segundos (tooSAN hardware similar a crear instantáneas con copia diferida y copia en escritura). Una vez haya una copia del archivo de disco duro virtual de hello puede adjuntar máquina virtual de tooa o el uso como una imagen tooattach copia de máquinas de toovirtual de disco duro virtual de Hola.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption fromImage
$vm | Update-AzureRmVM
```
##### <a name="cli"></a>CLI
```
azure config mode arm

# attach a vhd tooa vm
azure vm disk attach <resource group name> <vm name> <path toovhd>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Copia de discos entre cuentas de almacenamiento de Azure
No se puede realizar esta tarea en hello Portal de Azure. Puede usar cmdlets de Azure PowerShell, la CLI de Azure o un explorador de almacenamiento de terceros. cmdlets de PowerShell de Hola o comandos de CLI pueden crear y administrar blobs, que incluyen los blobs de copia de hello capacidad tooasynchronously a través de las cuentas de almacenamiento y las regiones dentro de hello suscripción de Azure.

##### <a name="powershell"></a>PowerShell
También es posible copiar discos duros virtuales entre suscripciones. Para más información, consulte [este artículo][storage-powershell-guide-full-copy-vhd].

flujo básico de Hola de hello lógica de cmdlet PS tiene el siguiente aspecto:

* Crear un contexto de la cuenta de almacenamiento para cuenta de almacenamiento de origen Hola con *New-AzureStorageContext* -vea <https://msdn.microsoft.com/library/dn806380.aspx>
* Crear un contexto de la cuenta de almacenamiento para cuenta de almacenamiento de destino de hello con *New-AzureStorageContext* -vea <https://msdn.microsoft.com/library/dn806380.aspx>
* Iniciar copia de hello con

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Comprobar el estado de Hola de copia de hello en un bucle con

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Asociar la máquina virtual de hello nuevo disco duro virtual tooa tal y como se ha descrito anteriormente.

Consulte [este artículo][storage-powershell-guide-full-copy-vhd] para obtener ejemplos.

##### <a name="cli"></a>CLI
* Iniciar copia de hello con

```
  azure storage blob copy start --source-blob <source blob name> --source-container <source container name> --account-name <source storage account name> --account-key <source storage account key> --dest-container <target container name> --dest-blob <target blob name> --dest-account-name <target storage account name> --dest-account-key <target storage account name>
```

* Comprobar estado de hello si hello copia en un bucle con

```
azure storage blob copy show --blob <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Asociar la máquina virtual de hello nuevo disco duro virtual tooa tal y como se ha descrito anteriormente.

Consulte [este artículo][storage-azure-cli-copy-blobs] para obtener ejemplos.

### <a name="disk-handling"></a>Administración de discos
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Estructura de VM/VHD para implementaciones de SAP
Lo ideal es que Hola control de la estructura de Hola de una máquina virtual y Hola asociado discos duros virtuales deben ser muy simples. En las instalaciones locales, los clientes han desarrollado muchas formas de estructurar una instalación de servidor.

* Un VHD base que contiene Hola sistema operativo y todos los archivos binarios de Hola de Hola DBMS o SAP. Desde marzo de 2015, este disco duro virtual puede estar too1TB de tamaño en lugar de las restricciones anteriores que lo limita too127GB.
* Uno o varios discos duros virtuales que contiene el archivo de registro DBMS Hola de base de datos SAP de Hola y el archivo de registro de hello de hello área de almacenamiento temporal de DBMS (si Hola DBMS admite esto). Si los requisitos de IOPS de registro de base de datos de hello son altos, necesita toostripe varios discos duros virtuales en el volumen de e/s por segundo orden tooreach Hola requerido.
* Un número de discos duros virtuales que contiene uno o dos archivos de base de datos de base de datos SAP de Hola y archivos de datos temporales de DBMS de Hola y (si Hola DBMS admite esto).

![Configuración de referencia de máquinas virtuales IaaS de Azure en SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd  TODO describe Linux structure  )

- - -
> ![Windows][Logo_Windows] Windows
>
> Con muchos clientes vimos configuraciones donde, por ejemplo, archivos binarios SAP y DBMS no estaban instalados en la unidad c:\ de Hola Hola SO se ha instalado. Existen varias razones para ello, pero cuando volvimos toohello raíz, generalmente ocurría que Hola discos eran pequeños y actualizaciones de sistema operativo necesitaban espacio adicional de 10 a 15 años. Ambas condiciones han dejado de aplicarse actualmente. Hoy en día se puede asignar la unidad c:\ de hello en máquinas virtuales o discos de gran volumen. En implementaciones de tookeep de orden simples en su estructura, resulta recomendable toofollow el siguiente patrón de implementación para sistemas de SAP NetWeaver en Azure
>
> debe ser el archivo de paginación del sistema operativo de Windows Hello en hello unidad D: (disco no persistente)
>
> ![Linux][Logo_Linux] Linux
>
> Coloque el archivo de intercambio de Linux de hello en/mnt/mnt/resource en Linux tal y como se describe en [este artículo][virtual-machines-linux-agent-user-guide]. archivo de intercambio de Hello puede configurarse en archivo de configuración de Hola de hello /etc/waagent.conf de agente de Linux. Agregar o cambiar Hola después de configuración:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

cambios de hello tooactivate, necesita toorestart Hola agente de Linux con

```
sudo service waagent restart
```

Lea la nota de SAP [1597355] para obtener más detalles sobre Hola recomienda el tamaño del archivo de intercambio

- - -
debe determinar el número de Hola de utilizados para los archivos de datos DBMS de Hola y el tipo de saludo de estos discos duros virtuales se hospedan en el almacenamiento de Azure por los requisitos de IOPS de Hola y latencia de hello necesaria. Las cuotas exactas se describen en [este artículo][virtual-machines-sizes].

Experiencia de las implementaciones de SAP a través de hello en los últimos años 2 nos enseñan algunas lecciones que se pueden resumir como:

* Archivos de datos de e/s por segundo tráfico toodifferent no es siempre hello mismo puesto que pueden que los sistemas existentes de cliente diferente tamaño datos archivos que representa sus bases de datos SAP. Como resultado resultó toobe mejor con una configuración de RAID en varios archivos de datos Hola de tooplace de discos duros virtuales, que los LUN se extraen de los. Hay situaciones, especialmente con donde una tasa de IOPS aciertos cuota Hola de un disco duro virtual solo en el registro de transacciones de DBMS Hola estándar de almacenamiento de Azure. Se recomienda en esa utilización de Hola de escenarios de almacenamiento Premium u o bien agregar varios VHD de almacenamiento estándar con un software RAID.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Procedimientos recomendados para SQL Server en Azure Virtual Machines][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Configuración del RAID de software en Linux][virtual-machines-linux-configure-raid]
> * [Configuración del LVM en una máquina virtual Linux en Azure][virtual-machines-linux-configure-lvm]
> * [Azure Storage secrets and Linux I/O optimizations (Secretos de Almacenamiento de Azure y optimizaciones de E/S de Linux)](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* El almacenamiento premium muestra un rendimiento bastante superior, especialmente en el caso de escrituras del registro de transacciones cruciales. En escenarios SAP están toodeliver esperado de producción como el rendimiento, se recomienda encarecidamente toouse Series de máquinas virtuales que pueden aprovechar el almacenamiento de Azure Premium.

Tenga en cuenta que Hola VHD que contiene Hola SO y tal y como se recomienda, hello archivos binarios de la base de datos SAP y hello (VM base), ya no está limitado too127GB. Ahora puede tener hasta too1TB de tamaño. Esto debe ser suficiente espacio tookeep todos Hola archivo necesario, por ejemplo, incluidos los registros de trabajos por lotes SAP.

Para conocer más sugerencias y obtener más detalles, específicamente para las VM de DBMS, con hello [Guía de implementación de DBMS][dbms-guide]

#### <a name="disk-handling"></a>Administración de discos
En la mayoría de los escenarios necesita toocreate discos adicionales en la base de datos SAP de orden toodeploy hello en hello máquina virtual. Hablamos sobre las consideraciones de hello en el número de discos duros virtuales en el capítulo [estructura VM/VHD para las implementaciones de SAP] [ planning-guide-5.5.1] de este documento. Hola Portal de Azure permite tooattach y desconectar discos una vez que se implementa una VM base. discos de Hello pueden conectar/desconectar cuando Hola VM está activo y en ejecución, así como cuando se detiene. Al conectar un disco, Hola Portal de Azure ofrece tooattach un disco vacío o un disco existente que en este momento no está conectado tooanother máquina virtual.

**Tenga en cuenta**: discos duros virtuales solo se pueden tooone adjunto VM en un momento dado.

![Conexión/desconexión de discos con el almacenamiento estándar de Azure][planning-guide-figure-1400]

Debe toodecide si desea toocreate un VHD nuevo y vacío (que se crea en Hola misma cuenta de almacenamiento como Hola VM base es en) o si desea que un disco duro virtual existente que se cargó anteriormente y debe ser tooselect adjunta toohello VM ahora.

**IMPORTANTE**: se **DO NOT** desea toouse almacenamiento en caché de Host con el almacenamiento de Azure estándar. Debería dejar preferencia de caché de Host de hello en hello valor predeterminado es NONE. Con el almacenamiento de Azure Premium debe habilitar el almacenamiento en caché de lectura si característica de E/S de hello es principalmente de lectura como tráfico de E/S típico en archivos de datos de la base de datos. En el caso del archivo de registro de transacciones, se recomienda no utilizar el almacenamiento en caché.

- - -
> ![Windows][Logo_Windows] Windows
>
> [¿Cómo tooattach datos de un disco en hello portal de Azure][virtual-machines-windows-attach-disk-portal]
>
> Si los discos están conectados, deberá toolog en hello tooopen VM Hola Administrador de discos de Windows. Si no está habilitado el montaje automático tal como se recomienda en el capítulo [configuración del montaje automático para los discos conectados][planning-guide-5.5.3], hello volumen recién conectado debe toobe realizada en línea y se inicializa.
>
> ![Linux][Logo_Linux] Linux
>
> Si los discos están conectados, necesita toolog en hello VM e inicializar discos Hola tal y como se describe en [este artículo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Si el nuevo disco de hello es un disco vacío, necesita disco así de tooformat Hola. Para dar formato, especialmente para DBMS archivos de registro y datos Hola mismas recomendaciones que las implementaciones de reconstrucción de hello DBMS se aplican.

Como ya se mencionó en el capítulo [Hola concepto de máquina Virtual de Microsoft Azure][planning-guide-3.2], una cuenta de almacenamiento de Azure no proporciona recursos infinitos en términos de volumen de E/S, IOPS y volumen de datos. Por lo general, las máquinas virtuales de DBMS son las que más afectadas se ven por esto. Puede que sea mejor toouse una cuenta de almacenamiento independiente para cada máquina virtual si tiene algunas toodeploy alta de máquinas virtuales de volumen de E/S en orden toostay en límite de Hola de hello volumen de la cuenta de almacenamiento de Azure. En caso contrario, debe toosee cómo pueden equilibrar estas máquinas virtuales entre las diferentes cuentas de almacenamiento sin llegar Hola límite de cada cuenta de almacenamiento único. Se analizan más detalles en hello [Guía de implementación de DBMS][dbms-guide]. También debe tener en cuenta estas limitaciones para máquinas virtuales de servidor de aplicaciones de SAP puras u otras VM que podrían terminar por necesitar VHD adicionales.

Otro tema que es relevante para las cuentas de almacenamiento es si Hola discos duros virtuales en una cuenta de almacenamiento se replican de manera geográfica. Replicación geográfica está habilitada o deshabilitada en hello cuenta de almacenamiento y no en hello nivel de máquina virtual. Si está habilitada la replicación geográfica, discos duros virtuales de hello dentro de la cuenta de almacenamiento podrían replicarse en otro centro de datos de Azure dentro de Hola Hola misma región. Antes de decidir esto, debería pensar en hello siguiente restricción:

Replicación geográfica de Azure funciona localmente en cada disco duro virtual en una máquina virtual y no replica Hola IOs en orden cronológico a través de varios discos duros virtuales en una máquina virtual. Por lo tanto, Hola VHD que representa Hola VM base, así como cualquier toohello adicional de discos duros virtuales conectados máquinas virtuales se replican independientes entre sí. Esto significa que no hay ninguna sincronización entre los cambios de Hola Hola diferentes discos duros virtuales. hecho de que Hola IOs Hello se replica una independientemente de orden de hello en lo que se escriben significa que la replicación geográfica no es de valor para los servidores de base de datos que tienen sus bases de datos que se distribuyen en varios discos duros virtuales. En suma toohello DBMS, también puede haber otras aplicaciones donde los procesos escriben o manipulan los datos en diferentes discos duros virtuales y donde es importante tookeep Hola orden de los cambios. Si esto último figura como requisito, no debe habilitarse la replicación geográfica en Azure. En función de si necesita o desea la habilitar la replicación geográfica para un conjunto de máquinas virtuales, pero no para otro conjunto, ya puede categorizar las VM y sus VHD relacionados en distintas cuentas de almacenamiento que tengan la replicación geográfica habilitada o deshabilitada.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Configuración de montaje automático para discos conectados
- - -
> ![Windows][Logo_Windows] Windows
>
> Para las máquinas virtuales que se crean a partir de imágenes propias o discos, es necesario toocheck y posiblemente establezca el parámetro del montaje automático de Hola. Establecer este parámetro permitirá Hola VM después de un reinicio o volver a implementar en Azure toomount Hola conectadas/montadas unidades nuevo de forma automática.
> Hola parámetro se establece para las imágenes de hello proporcionadas por Microsoft en hello Azure Marketplace.
>
> En orden tooset Hola automount, compruebe la documentación de Hola de hello línea de comandos ejecutable diskpart.exe aquí:
>
> * [Opciones de línea de comandos de DiskPart](https://technet.microsoft.com/library/cc766465.aspx)
> * [Automount (Montaje automático)](http://technet.microsoft.com/library/cc753703.aspx)
>
> ventana de línea de comandos de Windows Hello debe abrirse como administrador.
>
> Si los discos están conectados, deberá toolog en hello tooopen VM Hola Administrador de discos de Windows. Si no está habilitado el montaje automático tal como se recomienda en el capítulo [configuración del montaje automático para los discos conectados][planning-guide-5.5.3], Hola recién conectados volumen > necesita toobe realizada en línea y se inicializa.
>
> ![Linux][Logo_Linux] Linux
>
> Deberá tooinitialize un disco vacío recién adjunto tal y como se describe en [este artículo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> También debe tooadd nuevos discos toohello/etc/fstab.
>
>

- - -
### <a name="final-deployment"></a>Implementación final
Para hello implementación final y conocer los pasos exactos, especialmente con lo que respecta toohello implementación supervisión extendida de SAP, consulte toohello [Guía de implementación][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Acceso a sistemas SAP que se ejecutan en máquinas virtuales de Azure
Para los escenarios de solo en la nube, podría desear sistemas SAP de tooconnect toothose por hello internet pública mediante la GUI de SAP. Para estos casos, hello siguientes procedimientos deben toobe aplicado.

Más adelante en el documento de hello, veremos Hola otro escenario principal, conectar sistemas tooSAP en implementaciones entre entornos que tienen una conexión de sitio a sitio (túnel VPN) o conexión de ExpressRoute de Azure entre sistemas de hello local y Azure.

### <a name="remote-access-toosap-systems"></a>Sistemas de tooSAP de acceso remotos
Con el Administrador de recursos de Azure no hay ningún punto de conexión predeterminada ya como en el modelo clásico de hello anterior. Todos los puertos de una máquina virtual de Azure Resource Manager están abiertos siempre que se cumplan estos requisitos:

1. Ningún grupo de seguridad de red se define para la subred de Hola o interfaz de red de Hola. Tráfico de red tooAzure máquinas virtuales se puede proteger mediante denominadas "grupos de seguridad de red". Para más información, consulte [¿Qué es un grupo de seguridad de red?][virtual-networks-nsg]
2. Ningún equilibrador de carga de Azure se define para la interfaz de red de Hola   

Ver la diferencia de arquitectura de hello entre modelo clásico y ARM como se describe en [este artículo][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Configuración de hello conectividad sistema SAP y GUI de SAP para el escenario solo en la nube
Consulte este artículo que describe el tema de toothis detalles: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Cambio de la configuración del firewall en la máquina virtual
Puede que sea necesario tooconfigure firewall de hello en su tooallow de máquinas virtuales sistema SAP tooyour el tráfico de entrada.

- - -
> ![Windows][Logo_Windows] Windows
>
> De forma predeterminada, el Hola Firewall de Windows en una VM implementada Azure está activado. Ahora necesita tooallow Hola SAP puerto toobe abierto, en caso contrario Hola GUI de SAP no estará tooconnect pueda.
> toodo esto:
>
> * Abra el panel de Control y Seguridad\firewall too'Advanced configuración.
> * Ahora haga clic con el botón derecho en Reglas de entrada y seleccione "Nueva regla".
> * Hola Asistente siguiente eligió toocreate una nueva regla 'Puerto'.
> * En hello siguiente paso del Asistente de hello, dejar a configuración hello en TCP y el tipo en número de puerto de Hola que desee tooopen. Puesto que el identificador de instancia de SAP es 00, utilizamos 3200. Si la instancia tiene un número de instancia diferente, debe abrirse puerto Hola que se definió anteriormente basado en el número de instancia Hola.
> * En la parte siguiente de saludo del Asistente para hello, deberá elemento de hello tooleave comprobar ' Permitir conexión'.
> * En el siguiente paso del Asistente para Hola de hello debe toodefine si Hola regla se aplica para la red de dominio, privado y público. Realice ajustes si es necesario tooyour necesario. Conectar con la GUI de SAP de hello fuera a través de la red pública de hello, sin embargo, deberá toohave red pública de hello regla aplicada toohello.
> * En hello último paso del Asistente de hello, necesita hello toogive un nombre de regla y, a continuación, Guardar regla Hola presionando 'Finalizar'
>
> regla de Hello entrará en vigor inmediatamente.
>
> ![Definición de la regla de puertos][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> imágenes de Linux de Hello en hello Azure Marketplace no habilitan firewall de hello iptables de forma predeterminada y sistema SAP de hello conexión tooyour debería funcionar. Si habilitó iptables u otro firewall, consulte la documentación de toohello de iptables o hello usa firewall tooallow el tráfico tcp entrante demasiado puerto 32xx (donde xx es el número de sistema de Hola de su sistema SAP).
>
>

- - -
#### <a name="security-recommendations"></a>Recomendaciones de seguridad
Hola GUI de SAP no conecta inmediatamente tooany Hola de instancias de SAP (puerto 32xx) que se están ejecutando, pero primero se conecta mediante el proceso de servidor de hello puerto abierto toohello SAP mensaje (puerto 36xx). Hola más allá de hello mismo puerto usado por servidor de mensajes de Hola para instancias de la aplicación para la comunicación interna hello toohello. tooprevent local de servidores de aplicaciones sin darse cuenta se comunique con un servidor de mensajes en Azure Hola interno se pueden cambiar los puertos de comunicación. Se recomienda encarecidamente comunicación interna de hello toochange entre el servidor de mensaje de Hola SAP y su número de puerto diferente de tooa de instancias de aplicación en sistemas que se han clonado en sistemas locales, como un clon de desarrollo para probar el proyecto etcetera. Esto puede hacerse con el parámetro de perfil predeterminado de hello:

> rdisp/msserv_internal
>
>

como se documenta en: <https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm>.

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Conceptos de implementación solo en la nube de instancias de SAP
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Escenario de demostración/aprendizaje de máquina virtual única con SAP NetWeaver
![Ejecuta solo sistemas de demostración de SAP de VM con hello mismos nombres VM, aislada en los servicios de nube de Azure][planning-guide-figure-1700]

En este escenario (consulte el capítulo [solo en la nube] [ planning-guide-2.1] de este documento) estamos implementando un escenario de sistema típico de aprendizaje/demostración donde se encuentra el escenario de aprendizaje/demostración completa de hello dentro de una sola máquina virtual. Se supone que la implementación de Hola se realiza a través de plantillas de imagen de máquina virtual. También suponemos que varias de estas toobe de necesidad de máquinas virtuales de demostración/aprendizaje implementado con máquinas virtuales tener Hola Hola mismo nombre.

Hola supone que crea una imagen de VM como se describe en algunas secciones del capítulo [preparar las máquinas virtuales con SAP para Azure] [ planning-guide-5.2] en este documento.

secuencia de Hola de escenario de hello tooimplement de eventos tiene el siguiente aspecto:

[comment]: <> (MShermannd TODO tiene muestra ARM de tooprovide / descripción con plantilla json + clarificación con respecto a nombre de máquina virtual único dentro de la red virtual de ARM)   
##### <a name="powershell"></a>PowerShell
* Cree un nuevo grupo de recursos para cada entorno de aprendizaje o demostración.

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```

* Creación de una cuenta de almacenamiento nueva

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Crear una nueva red virtual para cada uso de aprendizaje/demostración horizontal tooenable Hola de hello mismo nombre de host y direcciones IP. red virtual de Hello está protegido por un grupo de seguridad de red que solo permite el acceso del tráfico tooport 3389 tooenable escritorio remoto y el puerto 22 de SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Crear una nueva dirección IP pública que puede ser utilizados tooaccess Hola virtual máquina de hello internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Crear una nueva interfaz de red de máquina virtual de Hola

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Cree una máquina virtual. Para el escenario de solo en la nube de hello cada VM tendrá Hola mismo nombre. Hola SID de SAP de hello instancias en esas máquinas virtuales de SAP NetWeaver Hola así mismo. Dentro de Hola el grupo de recursos de Azure, nombre de Hola de hello VM necesita toobe único, pero en diferentes grupos de recursos de Azure puede ejecutar máquinas virtuales con hello mismo nombre. Hola cuenta de 'Administrador' predeterminada de Windows o 'raíz' para Linux no es válido. Por lo tanto, un nuevo nombre de usuario de administrador debe toobe definido con una contraseña. tamaño de Hola de hello VM también debe toobe definido.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES" -Skus "12" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="os"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"
$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Opcionalmente, agregue discos adicionales y restaure el contenido necesario. Tenga en cuenta que todos los nombres de blob (blobs de toohello de direcciones URL) deben ser únicos dentro de Azure.

```powershell
# Optional: Attach additional data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Hola siguiendo el ejemplo de código se puede usar en Linux. Para Windows, por favor, use PowerShell como se describió anteriormente o adaptar Hola ejemplo toouse % rgName % en lugar de $rgName y establecer variable de entorno de hello mediante comandos de Windows hello *establecer*.

* Cree un nuevo grupo de recursos para cada entorno de aprendizaje o demostración.

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
azure group create $rgName "North Europe"
```

* Creación de una cuenta de almacenamiento nueva

```
azure storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku-name LRS $rgNameLower
```

* Crear una nueva red virtual para cada uso de aprendizaje/demostración horizontal tooenable Hola de hello mismo nombre de host y direcciones IP. red virtual de Hello está protegido por un grupo de seguridad de red que solo permite el acceso del tráfico tooport 3389 tooenable escritorio remoto y el puerto 22 de SSH.

```
azure network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

azure network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
azure network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group-name SAPERPDemoNSG
```

* Crear una nueva dirección IP pública que puede ser utilizados tooaccess Hola virtual máquina de hello internet

```
azure network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --domain-name-label $rgNameLower --allocation-method Dynamic
```

* Crear una nueva interfaz de red de máquina virtual de Hola

```
azure network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-name SAPERPDemoPIP --subnet-name Subnet1 --subnet-vnet-name SAPERPDemoVNet
```

* Cree una máquina virtual. Para el escenario de solo en la nube de hello cada VM tendrá Hola mismo nombre. Hola SID de SAP de hello instancias en esas máquinas virtuales de SAP NetWeaver Hola así mismo. Dentro de Hola el grupo de recursos de Azure, nombre de Hola de hello VM necesita toobe único, pero en diferentes grupos de recursos de Azure puede ejecutar máquinas virtuales con hello mismo nombre. Hola cuenta de 'Administrador' predeterminada de Windows o 'raíz' para Linux no es válido. Por lo tanto, un nuevo nombre de usuario de administrador debe toobe definido con una contraseña. tamaño de Hola de hello VM también debe toobe definido.

```
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn SUSE:SLES:12:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn RedHat:RHEL:7.2:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
#azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
```

* Opcionalmente, agregue discos adicionales y restaure el contenido necesario. Tenga en cuenta que todos los nombres de blob (blobs de toohello de direcciones URL) deben ser únicos dentro de Azure.

```
# Optional: Attach additional data disks
azure vm disk attach-new --resource-group $rgName --vm-name SAPERPDemo --size-in-gb 1023 --vhd-name datadisk
```

##### <a name="template"></a>Plantilla
Puede utilizar plantillas de ejemplo de Hola en el repositorio de plantillas de inicio rápido de azure de hello en github.

* [Máquina virtual de Linux simple](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Máquina virtual de Windows simple](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [Máquina virtual a partir de imagen](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implementar un conjunto de máquinas virtuales que necesitan toocommunicate dentro de Azure
Este escenario solo en la nube es un escenario típico para fines de aprendizaje y demostración donde hello software que representa Hola escenario de demostración/aprendizaje se extiende a varias máquinas virtuales. Hola diferentes componentes instalados en hello toocommunicate de necesidad de diferentes máquinas virtuales entre sí. Una vez más, en este escenario no se requiere ninguna comunicación de red local ni ningún escenario entre locales.

Este escenario es una extensión de instalación de Hola se describe en el capítulo [de VM simple con SAP NetWeaver escenario de demostración/aprendizaje] [ planning-guide-7.1] de este documento. En este caso más máquinas virtuales se agregará tooan grupo de recursos existente. Hola panorama de aprendizaje de Hola de ejemplo siguiente consta de una VM ASCS/SCS de SAP, una máquina virtual que ejecuta un DBMS y una instancia de servidor de aplicaciones SAP máquina virtual.

Antes de crear este escenario debe toothink acerca de la configuración básica como se hizo en el escenario de hello antes.

#### <a name="resource-group-and-virtual-machine-naming"></a>Nomenclatura de los grupos de recursos y las máquinas virtuales
Todos los nombres de los grupos de recursos deben ser únicos. Desarrolle su propio esquema de nomenclatura de los recursos como, por ejemplo, `<rg-name`>-sufijo.

nombre de la máquina virtual de Hello tiene toobe único en el grupo de recursos de Hola.

#### <a name="setup-network-for-communication-between-hello-different-vms"></a>Hola de configuración de red para la comunicación entre diferentes máquinas virtuales
![Conjunto de máquinas virtuales dentro de una red virtual de Azure][planning-guide-figure-1900]

tooprevent nomenclatura colisiones con clones de hello panoramas de aprendizaje/demostración mismo, deberá toocreate una red Virtual de Azure para cada entorno. Resolución de nombres DNS se proporcionarán con Azure o puede configurar su propio servidor DNS fuera de Azure (no toobe tratada con más detalle a continuación). En este escenario, no se debe configurar un DNS propio. La comunicación a través de los nombres de host se habilitará para todas las máquinas virtuales dentro de una red virtual de Azure.

Hola razones tooseparate panoramas de aprendizaje o demostración mediante redes virtuales y no solo recursos grupos podrían ser:

* Hola SAP horizontal como conjunto de necesidades de su propio AD/OpenLDAP y servidor de dominio necesidades toobe parte de cada uno de los panoramas de Hola.  
* Hola panorama de SAP como configurar tiene componentes que toowork necesidad con direcciones IP fijas.

Para obtener más información sobre redes virtuales de Azure y cómo toodefine ellos pueden encontrarse en [este artículo][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Implementación de máquinas virtuales de SAP con conectividad de red corporativa (entre locales)
Ejecutar un panorama de SAP y desea toodivide Hola implementación entre sin sistema operativo para servidores de DBMS de gama alta, entornos de virtualizadas locales para los niveles de la aplicación y más pequeños de 2 niveles configurado sistemas SAP e IaaS de Azure. la suposición base Hello es que los sistemas SAP en un panorama de SAP necesitan toocommunicate entre sí y con muchos otros componentes de software implementadas en la empresa de hello, independientemente de su forma de implementación. También debería haber diferencias presentadas mediante la forma de implementación de Hola para conectar con la GUI de SAP u otras interfaces Hola del usuario final. Estas condiciones solo pueden cumplirse cuando contamos con hello Active Directory/OpenLDAP local y servicios de DNS ampliados toohello sistemas de Azure a través de conectividad de sitio-a-sitio/varios sitios o conexiones privadas como ExpressRoute de Azure.

En orden tooget más en segundo plano en los detalles de implementación de Hola de SAP en Azure, le recomendamos capítulo tooread [implementación de conceptos de solo de las instancias de SAP] [ planning-guide-7] de este documento que explica algunos de los fundamentos de Hola de construcciones de Azure y cómo se debe usar con aplicaciones de SAP en Azure.

### <a name="scenario-of-a-sap-landscape"></a>Escenario de un entorno de SAP
escenario entre entornos de Hello puede describir como en gráficos de hello siguientes:

![Conectividad de sitio a sitio entre activos locales y de Azure][planning-guide-figure-2100]

Hello escenario mostrado anteriormente describe un escenario donde hello local AD/OpenLDAP y DNS se ha ampliado tooAzure. En el lado local de hello, un determinado intervalo de direcciones IP está reservado por suscripción de Azure. intervalo de direcciones IP de Hola se asignarán tooan red Virtual de Azure en hello parte de Azure.

#### <a name="security-considerations"></a>Consideraciones sobre la seguridad
Hello requisito mínimo es Hola uso de protocolos de comunicación segura, como SSL/TLS para acceso de explorador o conexiones basadas en VPN para sistema tener acceso a toohello Azure servicios. Hola, se supone que las empresas controlan conexión de VPN de hello entre su red corporativa y Azure de forma muy diferente. Algunas compañías podrían simplemente abrir todos los puertos de Hola. Algunas otras compañías podrían necesitar toobe muy preciso en los puertos que necesitan tooopen, etcetera.

En tabla de hello siguiente SAP típicos se enumeran los puertos de comunicación. Básicamente es suficiente tooopen Hola puerto de puerta de enlace SAP.

| Servicio | Nombre del puerto | Ejemplo `<nn`> = 01 | Intervalo predeterminado (mín.-máx.) | Comentario |
| --- | --- | --- | --- | --- |
| Distribuidor |sapdp`<nn>` consulte * |3201 |3200-3299 |Distribuidor de SAP, utilizado por la GUI de SAP para Windows y Java |
| Servidor de mensajes |sapms`<sid`> consulte ** |3600 |sapms libre`<anySID`> |sid = identificador del sistema SAP |
| Puerta de enlace |sapgw`<nn`> consulte * |3301 |libre |Puerta de enlace de SAP, utilizada para la comunicación de CPIC y RFC |
| Enrutador de SAP |sapdp99 |3299 |libre |Nombres de servicio CI (instancia central) solo se pueden reasignar en valores arbitrarios / etc/Services tooan después de la instalación. |

*) nn = número de instancia de SAP

**) sid = identificador del sistema SAP

Podrá encontrar información más detallada sobre los puertos necesarios para diferentes productos o servicios de productos de SAP aquí <http://scn.sap.com/docs/DOC-17124>.
Con este documento debe ser capaz de tooopen dedicado puertos en el dispositivo VPN de hello necesario para escenarios y productos SAP específicos.

Medidas de otro seguridad al implementar máquinas virtuales en este escenario podría ser toocreate una [grupo de seguridad de red] [ virtual-networks-nsg] toodefine reglas de acceso.

### <a name="dealing-with-different-virtual-machine-series"></a>Manejo de varias series de máquinas virtuales
En el curso de Hola de los últimos 12 meses Microsoft agregado muchos más tipos VM que se diferencian en el número de vCPU, memoria o más importante en un hardware que se ejecuta. No todas las máquinas virtuales son compatibles con SAP (consulte los tipos de VM admitidos en la nota de SAP [1928533]). Algunas de estas máquinas virtuales se ejecutan en generaciones de hardware de host distintas. Estas generaciones de hardware de host obtener se implementan en la granularidad de Hola de una unidad de escala de Azure. Pueden surgir significa casos donde diferentes tamaños VM Hola elegida no se puede ejecutar en Hola la misma unidad de escala. Un conjunto de disponibilidad está limitado en hello capacidad toospan que unidades de escala en función del hardware diferentes.  Por ejemplo, Si desea toorun Hola DBMS en máquinas virtuales de A5-A11 y Hola capa de aplicación de SAP en máquinas virtuales de serie G, sería toodeploy forzada un único sistema SAP o distintos sistemas SAP en diferentes conjuntos de disponibilidad.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Impresión en una impresora de red local desde la instancia de SAP en Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Impresión por TCP/IP en el escenario entre locales
Configuración de las impresoras de red local en función de TCP/IP en una máquina virtual de Azure es global Hola igual que en la red corporativa, suponiendo que tiene un túnel de VPN de sitio a sitio o conexión ExpressRoute establecida.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo esto:
>
> * Algunas impresoras de red incluyen un asistente de configuración que resulta fácil tooset la impresora en una máquina virtual de Azure. Si no dispone de ningún software de asistente distribuidas con la impresora Hola "manual" forma tooset una impresora de hello toocreate un nuevo puerto de impresora TCP/IP.
> * Abra Panel de control -> Dispositivos e impresoras -> Agregar una impresora.
> * Elija Agregar una impresora por medio de una dirección TCP/IP o un nombre de host.
> * Escriba Hola dirección IP de la impresora de Hola
> * Puerto de impresora estándar 9100.
> * Si es necesario instalar a controladores de impresora adecuados de hello manualmente.
>
> ![Linux][Logo_Linux] Linux
>
> * al igual que de Windows simplemente siga Hola procedimiento estándar tooinstall una impresora de red
> * sólo tiene que seguir guías de hello públicas Linux para [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) o [Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) acerca de cómo tooadd una impresora.
>
>

- - -
![Impresión en red][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Impresora basada en host por SMB (impresora compartida) en el escenario entre locales
Las impresoras basadas en host están diseñadas para no ser compatibles con la red. Pero una impresora basada en host puede compartirse entre equipos en una red siempre que sea de impresora Hola equipo encendido tooa conectado. Conecte la red corporativa sitio a sitio o por ExpressRoute y comparta la impresora local. Hola protocolo SMB usa NetBIOS en lugar de DNS como servicio de nombres. nombre de host de NetBIOS de Hello puede ser diferente del nombre de host DNS de Hola de. el caso típico de Hello es que el nombre de host de NetBIOS de Hola y el nombre de host DNS de hello son idénticos. dominio DNS de Hello no tiene sentido en el espacio de nombres de NetBIOS de Hola. En consecuencia, Hola nombre de host DNS completo que consta del nombre de host DNS de Hola y dominio DNS no debe usarse en el espacio de nombres de NetBIOS de Hola.

recurso compartido de impresora de Hola se identifica mediante un nombre único en la red de hello:

* Nombre de host SMB hello (siempre necesario).
* Nombre del recurso compartido de hello (siempre necesario).
* Nombre del dominio de hello si el recurso compartido de impresora no está en hello mismo dominio que el sistema SAP.
* Además, un nombre de usuario y una contraseña pueden ser necesario tooaccess Hola impresora compartida.

Control de

- - -
> ![Windows][Logo_Windows] Windows
>
> Comparta la impresora local.
> Hola Azure VM abra Hola el Explorador de Windows y escriba el nombre del recurso compartido de Hola de impresora Hola.
> Un Asistente para instalación de impresoras le guiará a través del proceso de instalación de Hola.
>
> ![Linux][Logo_Linux] Linux
>
> A continuación, se ofrecen algunos ejemplos de documentación sobre la configuración de impresoras de red en Linux e incluso un capítulo sobre la impresión en Linux. Funcionará Hola igual en una máquina virtual Linux de Azure mientras Hola VM forma parte de una VPN:
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-printing-smb-printer.html>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>Impresora USB (reenvío de impresora)
En cuanto a capacidad de hello Azure de hello servicios de escritorio remoto tooprovide usuarios Hola el acceso tootheir dispositivos de impresora local en una sesión remota no está disponible.

- - -
> ![Windows][Logo_Windows] Windows
>
> Se pueden encontrar más detalles sobre la impresión con Windows aquí: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Integración de sistemas SAP de Azure en el sistema de corrección y transporte (TMS) en el escenario entre locales
Hola tooexport toobe configurado de necesidades de cambio de SAP y sistema de transporte (TMS) e importar solicitudes de transporte en todos los sistemas en horizontal Hola. Se supone que las instancias de desarrollo de Hola de un sistema SAP (DEV) se encuentran en Azure, mientras que el control de calidad (QA) de Hola y (PRD) los sistemas productivos son locales. Además, se presupone que hay un directorio central de transporte.

##### <a name="configuring-hello-transport-domain"></a>Configurar el dominio de transporte de Hola
Configurar el dominio de transporte en sistema Hola designado como Hola controlador de dominio de transporte como se describe en [Hola Configurar controlador de dominio de transporte](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Requiere de un usuario del sistema que TMSADM se creará y Hola se generará el destino RFC. Puede comprobar estas conexiones RFC utilizando Hola transacción SM59. La resolución de nombre de host debe estar habilitada en todo el dominio de transporte.

Control de

* En nuestro escenario decidimos sistema QAS será el controlador de dominio de hello CTS a local de Hola. Llame al STMS de transacciones. aparece el cuadro de diálogo TMS Hola. Se mostrará un cuadro de diálogo Configure Transport Domain (Configurar dominio de transporte). (Este cuadro de diálogo aparecerá solo si todavía no ha configurado un dominio de transporte).
* Asegúrese de que ese usuario Hola crea automáticamente TMSADM está autorizado (SM59 -> conexión ABAP -> TMSADM@E61.DOMAIN_E61 -> detalles -> Utilidades (m) -> prueba de autorización). pantalla de bienvenida inicial de la transacción STMS debe mostrar que este sistema SAP ahora funciona como controlador de Hola de dominio de transporte Hola tal y como se muestra a continuación:

![Pantalla inicial de STMS de transacción en el controlador de dominio de Hola][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Incorporación de sistemas SAP en hello dominio de transporte
secuencia de Hola de inclusión de un sistema SAP en un dominio de transporte tiene el siguiente aspecto:

* En hello sistema DEV en Azure, vaya toohello sistema de transporte (cliente 000) y llame a la transacción STMS. Seleccione otra configuración de cuadro de diálogo de Hola y continúe con incluir sistema en el dominio. Especificar Hola controlador de dominio como host de destino ([incluidos los sistemas SAP en el dominio de transporte de hello](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). sistema de Hello ahora es toobe espera incluido en el dominio de transporte de Hola.
* Por motivos de seguridad, tiene tooconfirm del controlador de dominio de toogo toohello atrás la solicitud. Elija información general del sistema y aprobar del sistema de espera de Hola. A continuación, confirme que se distribuirá la configuración del símbolo del sistema y Hola Hola.

Este sistema SAP contiene ahora hello es necesario saber Hola todos los otros sistemas SAP en el dominio de transporte de Hola. En hello mismo tiempo, dirección de Hola se envían datos de sistema SAP nuevos hello tooall Hola otros sistemas SAP y Hola sistema SAP se escribe en el perfil de transporte de hello del programa de control de transporte de Hola. Comprueba si las solicitudes de cambio y el directorio de transporte de acceso toohello de dominio de hello funcionan.

Continuar con la configuración de Hola de su sistema de transporte como de costumbre tal como se describe en la documentación de hello [cambios y sistema de transporte](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Control de

* Asegúrese de que su STMS local está configurado correctamente.
* Asegúrese de que el nombre de host de hello del controlador de dominio de transporte de Hola puede resolverse mediante la máquina virtual en Azure y viceversa.
* Call transaction STMS (Llamar a STMS de transacciones) -> Other Configuration (Otra configuración) -> Include System in Domain (Incluir sistema en el dominio).
* Confirme la conexión de hello en hello en sistema TMS local.
* Configure las rutas, grupos y capas de transporte como de costumbre.

En escenarios conectados entre entornos de sitio a sitio, Hola latencia entre local y Azure aún puede ser considerable. Si se sigue hello secuencia de transportar objetos a través de tooproduction de sistemas de desarrollo y pruebas o pensar en aplicar los transportes o compatibilidad con paquetes toohello diferentes sistemas, se tenga en cuenta que, depende de la ubicación de Hola de transporte central Hola directorio, algunos de los sistemas de hello encontrará alta latencia leer o escribir datos en el directorio central de transporte de Hola. situación de Hello es configuraciones de panorama tooSAP similares donde se reparten los distintos sistemas de Hola a través de centros de datos diferentes con una distancia considerable entre centros de datos de Hola.

En Ordenar toowork alrededor tal latencia y tener sistemas de hello trabajen rápido en leer o escribir tooor desde el directorio de transporte de hello, puede configurar dos dominios de transporte STMS (uno para local. y otro con los sistemas de hello en dominios de transporte de hello Azure y vínculo Revise esta documentación que explica los principios de hello detrás de este concepto en hello TMS de SAP: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/FRAMESET.htm>.

Control de

* Configurar un dominio de transporte en cada ubicación (local y Azure) mediante STMS de transacciones <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Vincular dominios Hola con un vínculo de dominio y Hola vínculo entre dos dominios de Hola para confirmar.
  <http://help.SAP.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/Content.htm>
* Distribuir Hola configuración toohello vinculado sistema.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Tráfico de RFC entre las instancias de SAP ubicadas en Azure y las locales (entre locales)
El tráfico RFC entre sistemas que son locales y en Azure debe toowork. toosetup una conexión llame a la transacción SM59 en un sistema de origen donde debe toodefine una conexión RFC hacia el sistema de destino de Hola. configuración de Hello es similar toohello estándar el programa de instalación de una conexión RFC.

Se supone que en el escenario entre entornos de hello, hello las máquinas virtuales que ejecutan sistemas SAP que necesitan toocommunicate entre sí están en Hola mismo dominio. Por lo tanto, hello el programa de instalación de una conexión RFC entre sistemas SAP no son distintas de los pasos de configuración de Hola y entradas en escenarios locales.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Acceso a recursos compartidos de archivos "locales" desde instancias de SAP ubicadas en Azure o viceversa
Instancias de SAP situadas en Azure necesitan tooaccess recursos compartidos de archivos que están dentro de instalaciones corporativas Hola. Además, las instancias de SAP locales necesitan tooaccess recursos compartidos de archivos que se encuentran en Azure. tooenable Hola recursos compartidos de archivos, debe configurar permisos de Hola y opciones de uso compartido en el sistema local de Hola. Asegúrese de puertos de hello tooopen seguro en Hola VPN o conexión ExpressRoute entre Azure y el centro de datos.

## <a name="supportability"></a>Compatibilidad
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Solución de supervisión de Azure para SAP
En orden tooenable Hola supervisión de sistemas de misión críticos SAP en Azure Hola SAP herramientas de supervisión SAPOSCOL o agente de Host de SAP obtienen datos desde el host de servicio de máquinas virtuales de Azure de Hola a través de una extensión de supervisión de Azure para SAP. Puesto que las demandas de Hola de SAP eran muy específicas tooSAP aplicaciones, Microsoft decidió no toogenerically implementar Hola requerido la funcionalidad en Azure, pero deje para los clientes toodeploy Hola necesarios supervisión componentes y las configuraciones tootheir Máquinas virtuales que se ejecutan en Azure. Sin embargo, implementación y administración del ciclo de hello componentes de supervisión será mayormente automatizada por Azure.

#### <a name="solution-design"></a>Diseño de la solución
solución de Hello desarrollado tooenable que supervisión de SAP se basa en la arquitectura de Hola de agente de máquina virtual de Azure y el marco de la extensión. idea Hola de marco de trabajo de agente de máquina virtual de Azure y extensión de hello es tooallow instalación de aplicaciones de software disponibles en la Galería de extensión de máquina virtual de Azure de hello en una máquina virtual. Hola principio idea detrás de este concepto es tooallow (en casos como Hola extensión de supervisión de Azure para SAP), Hola de implementación de una funcionalidad especial en una configuración de máquina virtual y Hola de dicho software durante la implementación.

Desde febrero de 2014, hello 'Agente de máquina virtual de Azure' que permite controlar extensiones específicas de VM de Azure en hello que VM se inyecta en máquinas virtuales de Windows de forma predeterminada en la creación de VM en hello Portal de Azure. En el caso de hello SUSE o Red Hat Linux agente de máquina virtual ya forma parte de la imagen de Azure Marketplace. En caso de que uno podría cargar una VM Linux de agente de máquina virtual local tooAzure hello tiene toobe instalado manualmente.

Hola bloques de creación básicos de solución de supervisión de hello en Azure para SAP tiene el siguiente aspecto:

![Componentes de la extensión de Microsoft Azure][planning-guide-figure-2400]

Como se muestra en el diagrama de bloques de hello anterior, una parte del programa Hola a solución de supervisión para SAP está hospedada en hello imagen de máquina virtual de Azure y Galería de extensión de Azure que es un repositorio replicado a nivel mundial que administra las operaciones de Azure. Es responsabilidad de hello del equipo SAP/MS conjunta de Hola que trabajaba en hello Azure implementación de SAP toowork con las operaciones de Azure toopublish las nuevas versiones de hello extensión de supervisión de Azure para SAP. Esta extensión de supervisión de Azure para SAP utilizará Hola diagnósticos de Azure de Linux (LAD) o de extensiones de Microsoft Azure diagnósticos (WAD) tooget Hola información necesaria.

Cuando se implementa una nueva máquina virtual de Windows, se agrega automáticamente hello 'Agente de máquina virtual de Azure' en hello máquina virtual. función Hello de este agente es hello toocoordinate carga y la configuración de hello Azure extensiones para la supervisión de los sistemas SAP NetWeaver. Para máquinas virtuales Linux hello Azure VM Agent ya forma parte de imagen de SO de Azure Marketplace de Hola.

Sin embargo, hay un paso que todavía necesita toobe ejecutado por el cliente de Hola. Se trata de habilitación de Hola y la configuración de recopilación de rendimiento de Hola. relativos a los procesos de Hello toohello 'configuración' lo automatiza un script de PowerShell o un comando CLI. Hola script de PowerShell se puede descargar en hello Microsoft Azure Script Center como se describe en hello [Guía de implementación][deployment-guide].

Hello arquitectura global de hello Azure solución de supervisión para SAP es similar:

![Solución de supervisión de Azure para SAP NetWeaver][planning-guide-figure-2500]

**Para hello exactamente cómo-tooand para obtener pasos detallados del uso de estos cmdlets de PowerShell o el comando de CLI durante las implementaciones, siga las instrucciones de hello en hello [Guía de implementación][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Integración de una instancia de SAP ubicada en Azure en SAProuter
Instancias SAP que se ejecutan en Azure necesitan toobe accesibles desde SAProuter también.

![Conexión de red SAP-enrutador][planning-guide-figure-2600]

Un SAProuter permite la comunicación de TCP/IP de hello entre los sistemas participantes si no hay ninguna conexión IP directa. Esto proporciona la ventaja de Hola que ninguna conexión de extremo a extremo entre asociados de la comunicación de hello es necesaria en la red. Hola SAProuter está escuchando en el puerto 3299 de forma predeterminada.
tooconnect SAP instancias a través de un SAProuter necesita toogive Hola cadena SAProuter y nombre de host con cualquier tooconnect intento.

## <a name="sap-netweaver-as-java"></a>AS de SAP NetWeaver en Java
Hasta ahora Hola foco del documento de hello ha sido SAP NetWeaver en general o el Hola pila ABAP de SAP NetWeaver. En esta pequeña sección se enumeran consideraciones específicas para la pila de Java de SAP de Hola. Uno de los más importantes de las aplicaciones basadas en exclusivamente de Java de SAP NetWeaver hello es hello SAP Enterprise Portal. Otros SAP aplicaciones basadas en NetWeaver como SAP PI y el Administrador de solución de SAP utilizan Hola ABAP de SAP NetWeaver y pilas de Java. Por lo tanto, por supuesto, hay una necesidad tooconsider aspectos específicos relacionados toohello Java de SAP NetWeaver pila de así.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
configuración de Hola de un Portal de SAP en máquinas virtuales de Azure no se diferencia de una instalación local de si va a implementar en escenarios entre entornos. Desde Hola que DNS se realiza en local, es posible configuración de puertos de Hola de instancias individuales de hello como configuradas de forma local. recomendaciones de Hola y restricciones que se describen en este documento hasta ahora se aplican para una aplicación como SAP Enterprise Portal o la pila de Java de SAP NetWeaver hello en general.

![Exposición del portal de SAP][planning-guide-figure-2700]

Un escenario de implementación especial por algunos clientes es exposición directa de Hola de hello SAP Enterprise Portal toohello Internet mientras que los host de máquina virtual de hello es red de empresa de toohello conectado a través del túnel VPN o ExpressRoute de sitio a sitio. Para este escenario, deberá toomake seguro de que determinados puertos estén abiertos y no está bloqueado por grupo de seguridad de red o firewall. Hello misma mecánica deberá toobe aplica cuando desee que la instancia de SAP Java tooconnect tooan del entorno local en un escenario solo en la nube.

Hola URI inicial del portal es http (s):`<Portalserver`>: 5XX00/irj donde puerto Hola está formado por 50000 plus (Systemnumber × 100). Hola sistema de URI de SAP portal predeterminado 00 es `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Para más información, eche un vistazo a <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Configuración del punto de conexión][planning-guide-figure-2800]

Si desea toocustomize Hola URL o los puertos de SAP Enterprise Portal, revise esta documentación:

* [Change Portal URL (Cambio de la dirección URL del portal)](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Change Default port numbers, Portal port numbers (Cambio de los números de puerto predeterminados y los números de puerto del portal)](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

<a name="7cf991a1-badd-40a9-944e-7baae842a058"></a>
## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Alta disponibilidad (HA) y recuperación ante desastres (DR) para la ejecución de SAP NetWeaver en máquinas virtuales de Azure
### <a name="definition-of-terminologies"></a>Definición de terminología
Hola término **alta disponibilidad (HA)** es generalmente relacionado tooa un conjunto de tecnologías que minimiza las interrupciones de TI al proporcionar continuidad del negocio de servicios de TI mediante redundancia, tolerancia o componentes protegidos de conmutación por error dentro de hello **mismo** centro de datos. En nuestro caso, dentro de una sola región de Azure.

La **recuperación ante desastres (DR)** también tiene el objetivo de minimizar las interrupciones en los servicios de TI y recuperarlos pero en **distintos** centros de datos que suelen encontrarse a cientos de kilómetros de distancia. En nuestro caso normalmente entre diferentes regiones de Azure en hello misma región geopolítica o según lo establecido por el usuario como un cliente.

### <a name="overview-of-high-availability"></a>Información general sobre la alta disponibilidad
Se pueden podemos separar discusión Hola sobre SAP alta disponibilidad en Azure en dos partes:

* **Alta disponibilidad de la infraestructura de Azure**, por ejemplo, la alta disponibilidad del proceso (VM), la red, el almacenamiento, etc., y sus ventajas para aumentar la disponibilidad de las aplicaciones de SAP.
* **Alta disponibilidad de las aplicaciones de SAP**, por ejemplo, la alta disponibilidad de los componentes de software de SAP:
  * servidores de aplicaciones de SAP,
  * instancia de SAP ASCS/SCS,
  * servidor de base de datos,

y cómo se puede combinar con la alta disponibilidad de la infraestructura de Azure.

Alta disponibilidad SAP en Azure tiene algunos tooSAP diferencias en comparación con alta disponibilidad en un entorno físico o virtual de local. Hello siguiente documento de SAP describe las configuraciones de alta disponibilidad de SAP estándar en entornos virtualizados en Windows: <http://scn.sap.com/docs/DOC-44415>. No hay ninguna configuración de alta disponibilidad de SAP integrada en SAPInst para Linux como la que existe para Windows. Con respecto a la alta disponibilidad de SAP local para Linux, se puede encontrar más información aquí: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Alta disponibilidad de la infraestructura de Azure
Actualmente, no hay ningún acuerdo de nivel de servicio de VM única disponible para las máquinas virtuales de Azure. tooget una idea cómo disponibilidad Hola de una sola máquina virtual puede parecer que simplemente puede generar producto Hola de Hola distintos SLA de Azure disponibles: <https://azure.microsoft.com/support/legal/sla/>.

base de Hello para el cálculo de hello es 30 días por mes o 43200 minutos. Por lo tanto, el tiempo de inactividad de 0,05% corresponde too21.6 minutos. Como es habitual, disponibilidad de hello de servicios diferentes de Hola se multiplica Hola siguiente forma:

(Servicio de disponibilidad n.º 1/100) * (servicio de disponibilidad n.º 2/100) * (servicio de disponibilidad n.º 3/100) *…

Como, por ejemplo:

(99,95/100) * (99,9/100) * (99,9/100) = 0,9975 o una disponibilidad general del 99,75 %.

#### <a name="virtual-machine-vm-high-availability"></a>Alta disponibilidad de la máquina virtual (VM)
Hay dos tipos de eventos de la plataforma Windows Azure que pueden afectar a la disponibilidad de Hola de las máquinas virtuales: mantenimiento y trabajos de mantenimiento planificadas.

* Eventos de mantenimiento planeado son las actualizaciones periódicas realizadas por toohello Microsoft subyacente de la plataforma Windows Azure tooimprove confiabilidad general, el rendimiento y seguridad de infraestructura de plataforma de hello destinados a las máquinas virtuales.
* Cuando se ha producido un error hardware de Hola o infraestructura física subyacente de la máquina virtual de alguna manera, se producen eventos de mantenimiento no planeado. Entre estos podemos encontrar errores de la red local, errores de los discos locales u otras errores a nivel de bastidor. Cuando se detecta este error, Hola plataforma Windows Azure migrará automáticamente la máquina virtual de hello incorrecto físico servidor que hospeda el servidor físico correcto de tooa de máquina virtual. Estos eventos son poco frecuentes, pero también pueden provocar la tooreboot de máquina virtual.

Se pueden encontrar más detalles en esta documentación: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>.

#### <a name="azure-storage-redundancy"></a>Redundancia de almacenamiento de Azure
datos de Hello en la cuenta de almacenamiento de Microsoft Azure están siempre tooensure replicada durabilidad y alta disponibilidad, cumpliendo Hola SLA de almacenamiento de Azure incluso de cara de Hola de errores de hardware transitorios

Puesto que el almacenamiento de Azure se mantiene 3 imágenes de los datos de Hola de forma predeterminada, RAID 5 o RAID 1 en varios discos de Azure no son necesarios.

Se pueden encontrar más detalles en este artículo: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Utilización de VM se reinicia de Azure infraestructura tooAchieve "Mayor disponibilidad" de aplicaciones de SAP
Si decide no toouse funcionalidades como Windows Server conmutación por error de agrupación en clústeres (WSFC) o un equivalente de Linux (Hola último uno no se admite todavía en Azure en combinación con el software SAP), Azure VM se reinicia es tooprotect usan un sistema SAP contra planeada y tiempo de inactividad imprevisto de infraestructura de servidor físico Azure hello y plataforma de Azure subyacente general.

> [!NOTE]
> Es importante toomention que Azure VM se reinicia principalmente protege las máquinas virtuales y no las aplicaciones. El reinicio de VM no ofrece una alta disponibilidad en las aplicaciones de SAP, pero sí un cierto grado de disponibilidad de la infraestructura y, por tanto, ofrece indirectamente una "mayor disponibilidad" de los sistemas SAP. También no hay ningún SLA para hello tiempo que tardará toorestart una máquina virtual después de una interrupción planeada o no planeada de host. Por lo tanto, este método de "alta disponibilidad" no es adecuado para los componentes esenciales de un sistema SAP como (A)SCS o DBMS.
>
>

El almacenamiento es otro elemento infraestructural importante para la alta disponibilidad. Por ejemplo, el Acuerdo de Nivel de Servicio de almacenamiento de Azure presenta una disponibilidad del 99,9 %. Si se implementan todas las máquinas virtuales con sus discos en una sola cuenta de almacenamiento de Azure, la eventual indisponibilidad del almacenamiento de Azure ocasionará que no estén disponibles ninguna de las máquinas virtuales ubicadas en dicha cuenta de almacenamiento ni tampoco los componentes de SAP que se ejecutan dentro de esas máquinas virtuales.  

En lugar de colocar todas las máquinas virtuales en una sola cuenta de almacenamiento de Azure, también puede usar cuentas de almacenamiento dedicadas para cada máquina virtual y, de esta manera, aumentar la disponibilidad general de las aplicaciones de SAP al usar varias cuentas de almacenamiento de Azure independientes.

La arquitectura de un sistema SAP NetWeaver que utilice la alta disponibilidad de la infraestructura de Azure podría ser, por ejemplo, como la siguiente:

![Utilización de la infraestructura de Azure HA tooachieve SAP "superior" de disponibilidad de aplicaciones][planning-guide-figure-2900]

Para componentes críticos de SAP se consecución Hola después hasta ahora:

* Alta disponibilidad de los servidores de aplicaciones (AS) de SAP

Las instancias de los servidores de aplicaciones de SAP son componentes redundantes. Cada instancia del servidor de aplicaciones de SAP se implementa en su propia máquina virtual, que se ejecuta en otro dominio de error y de actualización de Azure (consulte los capítulos [Dominios de error][planning-guide-3.2.1] y [Dominios de actualización][planning-guide-3.2.2]). Esto se garantiza empleando conjuntos de disponibilidad de Azure (consulte el capítulo [Conjuntos de disponibilidad de Azure][planning-guide-3.2.3]). La eventual indisponibilidad planeada o no de un dominio de error o de actualización de Azure hará que un número limitado de máquinas virtuales y sus respectivas instancias de SAP no estén disponibles.
Cada instancia del servidor de aplicaciones de SAP se coloca en su propia cuenta de almacenamiento de Azure, por lo que la eventual indisponibilidad de una cuenta de almacenamiento de Azure hará que solo deje de estar disponible una máquina virtual y su respectiva instancia de SAP. Sin embargo, tenga en cuenta que las suscripciones de Azure admiten un número de cuentas de almacenamiento de Azure limitado. tooensure inicio automático de (A) instancia SCS después de reiniciar Hola VM, asegúrese de que tooset Autostart, parámetro en la instancia de (A) SCS iniciar perfil se describe en el capítulo [utilizando Autostart para las instancias de SAP][planning-guide-11.5].
Lea también el capítulo [Alta disponibilidad en los servidores de aplicaciones de SAP][planning-guide-11.4.1] para más información.

* *Mayor* disponibilidad de la instancia de SAP (A)SCS

Aquí usamos Azure VM se reinicia tooprotect Hola VM con la instancia de SAP (A) SCS instalada. En servidores de hello mayúsculas y minúsculas del tiempo de inactividad planeado o no de Azure, las máquinas virtuales se reiniciará en otro servidor disponible. Tal y como se mencionó anteriormente, principalmente VM se reinicia de Azure protege las máquinas virtuales y no las aplicaciones, en este caso Hola (A) instancia SCS. A través de hello reiniciar la máquina virtual se podrá alcanzar indirectamente "mayor disponibilidad" de la instancia de SAP (A) SCS. tooinsure inicio automático de (A) instancia SCS después de reiniciar Hola VM, asegúrese de que tooset Autostart, parámetro en la instancia de (A) SCS iniciar perfil se describe en el capítulo [utilizando Autostart para las instancias de SAP][planning-guide-11.5]. Esto significa hello (A) SCS ejecutándose como un único punto de error (SPOF) en una sola máquina virtual será un factor determinante Hola para disponibilidad Hola de panorama de SAP todo Hola.

* *Mayor* disponibilidad del servidor de DBMS

En este caso, caso de uso de la instancia de SAP (A) SCS toohello similar, usamos Azure VM se reinicia tooprotect Hola VM con software DBMS instalado y se lograr "mayor disponibilidad" de software DBMS a través de VM se reinicia.
DBMS que se ejecuta en una sola máquina virtual también es un SPOF y es un factor determinante Hola para disponibilidad Hola de panorama de SAP todo Hola.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Alta disponibilidad de las aplicaciones de SAP en IaaS de Azure
tooachieve completa SAP alta disponibilidad del sistema, necesitamos tooprotect todos los componentes de sistema SAP críticos, por ejemplo, redundancia servidores de aplicaciones de SAP, y componentes únicos (por ejemplo, punto de error único), como instancia de SAP (A) SCS y DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Alta disponibilidad en los servidores de aplicaciones de SAP
Para instancias de diálogo/servidores de aplicación de SAP de hello no es necesario toothink acerca de una solución de alta disponibilidad específico. La alta disponibilidad se consigue simplemente mediante la redundancia y, por tanto, disponiendo de la redundancia suficiente en las distintas máquinas virtuales. Deberían colocarse en hello tooavoid mismo conjunto de disponibilidad de Azure que Hola máquinas virtuales puedan actualizarse al Hola vez durante el tiempo de inactividad de mantenimiento planeado. funcionalidad básica de Hello, que se basa en diferentes dominios de error dentro de una unidad de escala de Azure y actualización ya se introdujo en el capítulo [actualizar dominios][planning-guide-3.2.2]. Los conjuntos de disponibilidad de Azure se presentaron en el capítulo [Conjuntos de disponibilidad de Azure][planning-guide-3.2.3] de este documento.

El número de dominios de error y de actualización que puede utilizar un conjunto de disponibilidad de Azure dentro de una unidad de escalado de Azure no es infinito. Esto significa que poner un número de máquinas virtuales en un conjunto de disponibilidad antes o después de hecho de Hola que más de una máquina virtual termina en hello mismo error o actualización del dominio

Implementación de servidor de aplicaciones de SAP algunas instancias en sus máquinas virtuales dedicadas y suponiendo que obtuvimos 5 dominios de actualización, emerge Hola después de la imagen final Hola. número real de max Hola de dominios de error y actualización dentro de un conjunto de disponibilidad podría cambiar en futuras hello:

![Alta disponibilidad de los servidores de aplicaciones de SAP en Azure][planning-guide-figure-3000]

Se pueden encontrar más detalles en esta documentación: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Alta disponibilidad para la instancia de SAP (A) SCS de hello en Windows
Clúster de conmutación por error de Windows Server (WSFC) es una instancia de SAP (A) SCS de soluciones usadas con frecuencia tooprotect Hola. Además, está integrada en SAPInst como una "instalación de alta disponibilidad". En este momento Hola infraestructura de Azure no es capaz de tooprovide Hola funcionalidad tooset seguridad Hola de clúster de conmutación por error de Windows Server Hola necesario misma forma en que se realiza en local.

A partir de enero de 2016 plataforma de nube de Azure Hola con sistema operativo de Windows de hello no proporciona la posibilidad de hello del uso de un volumen compartido de clúster en un disco compartido entre dos máquinas virtuales de Azure.

Una solución válida aunque es el uso de Hola de 3rd-fabricantes de software que proporciona un volumen compartido mediante la replicación sincrónica y transparente el disco que se puede integrar en WSFC. Este enfoque implica que ese nodo de clúster activo Hola sólo es capaz de tooaccess un disco de hello copia en un momento dado. A partir de enero de 2016 este HA configuración es instancia de SAP (A) SCS de hello tooprotect admitidos en Windows sistema operativo invitado en máquinas virtuales de Azure en combinación con el software de terceros 3rd SIOS DataKeeper.

Hola solución SIOS DataKeeper proporciona un tooWindows de recursos de clúster clústeres de conmutación por error de disco compartido al tener:

* Un VHD de Azure adicional conectado tooeach de hello máquinas virtuales () que se encuentran en una configuración de clúster de Windows
* SIOS DataKeeper Cluster Edition debe ejecutarse en ambos nodos de VM.
* Tener SIOS DataKeeper Cluster Edition configurado de forma que sincrónicamente refleja contenido Hola de hello adicional VHD conectado volumen del volumen de disco duro virtual conectado de origen máquinas virtuales tooadditional de máquina virtual de destino.
* SIOS DataKeeper está resumiendo volúmenes locales de origen y de destino de Hola y mostrándoles tooWindows clúster de conmutación por error como un único disco compartido.

Puede encontrar todos los detalles acerca de cómo tooinstall un clúster de conmutación por error de Windows con SIOS Datakeeper y SAP en hello [de agrupación en clústeres SAP ASCS instancia mediante el clúster de conmutación por error de Windows Server en Azure con SIOS DataKeeper] [ ha-guide-classic]notas del producto.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Alta disponibilidad para la instancia de SAP (A) SCS de hello en Linux
A partir de diciembre de 2015 también no hay ningún disco equivalente tooshared WSFC para máquinas virtuales de Linux en Azure. Las soluciones alternativas mediante software de terceros como SIOS para Windows aún no están validadas para que se en ejecuten en SAP en Linux con Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Alta disponibilidad para la instancia de base de datos SAP de Hola
Hello HA de SAP DBMS instalación típica se basa dos VM de DBMS, donde se utiliza la funcionalidad de alta disponibilidad DBMS tooreplicate datos de hello active DBMS instancia toohello segunda máquina virtual en una instancia pasiva de DBMS.

Funcionalidad de recuperación ante desastres y disponibilidad alta para DBMS en general, así como específicos de DBMS se describen en hello [Guía de implementación de DBMS][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>To-End de alta disponibilidad para Hola completas del sistema SAP
A continuación, se ofrecen dos ejemplos de una arquitectura completa de alta disponibilidad de SAP NetWeaver en Azure: una para Windows y otra para Linux.
conceptos de Hello tal y como se explica más adelante pueden necesitar toobe poner en peligro un poco implementar muchos sistemas SAP y número de Hola de máquinas virtuales implementadas es que excedan el límite máximo de Hola de cuentas de almacenamiento por suscripción. En esos casos, discos duros virtuales de máquinas virtuales necesita toobe combinado dentro de una cuenta de almacenamiento. Normalmente, este procedimiento se llevaría a cabo combinando los VHD de las máquinas virtuales de la capa de aplicación de SAP en diversos sistemas SAP.  También se combinan varios VHD de diversas máquinas virtuales del DBMS de sistemas SAP distintos en una sola cuenta de almacenamiento de Azure. Por tanto, teniendo presente límites de IOPS de Hola de cuentas de almacenamiento de Azure ( <https://azure.microsoft.com/documentation/articles/storage-scalability-targets> )

##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] Alta disponibilidad en Windows
![Arquitectura de alta disponibilidad de las aplicaciones de SAP NetWeaver con SQL Server en IaaS de Azure][planning-guide-figure-3200]

Hola siguientes construcciones de Azure se utiliza para el sistema de SAP NetWeaver hello, toominimize impacto por problemas de infraestructura y de host de aplicación de revisiones:

* sistema completo de Hola se implementa en Azure (requerido: capa de DBMS, (A) instancia SCS y toorun de necesidad de capa de aplicación completa en Hola la misma ubicación).
* sistema completo de Hola se ejecuta dentro de una suscripción de Azure (obligatorio).
* sistema completo de Hola se ejecuta en una red Virtual de Azure (obligatorio).
* separación de Hola de hello las máquinas virtuales de un sistema SAP en tres conjuntos de disponibilidad es posible incluso con todas las máquinas virtuales de Hola que pertenecen toohello misma red Virtual.
* Todas las máquinas virtuales que ejecutan instancias del DBMS de un sistema SAP se encuentran en un único conjunto de disponibilidad. Se presupone que hay más de una máquina virtual que ejecuta instancias del DBMS por sistema, ya que se utilizan características nativas de alta disponibilidad del DBMS como SQL Server AlwaysOn u Oracle Data Guard.
* Todas las máquinas virtuales que ejecutan instancias del DBMS utilizan su propia cuenta de almacenamiento. Archivos de registro y datos DBMS se replican desde una cuenta de almacenamiento tooanother de cuenta de almacenamiento, utilizando las funciones de alta disponibilidad DBMS que sincronización los datos de Hola. Falta de disponibilidad de una cuenta de almacenamiento hará falta de disponibilidad de un nodo de clúster de Windows de SQL, pero no Hola todo el servicio SQL Server.
* Todas las máquinas virtuales que ejecutan la instancia de (A)SCS de un sistema SAP se encuentran en un único conjunto de disponibilidad. Dentro de esas máquinas virtuales es configurar la instancia de clúster de conmutación por error de servidor de Windows (WSFC) tooprotect (A) SCS.
* Todas las máquinas virtuales que ejecutan instancias de (A)SCS utilizan su propia cuenta de almacenamiento. (A) Archivos de la instancia SCS y carpeta global de SAP se replican desde una cuenta de almacenamiento tooanother de cuenta de almacenamiento, utilizando la replicación SIOS DataKeeper. Falta de disponibilidad de una cuenta de almacenamiento hará que la falta de disponibilidad de uno (A) SCS Windows nodo del clúster, pero no todo Hola (A) servicio SCS.
* Todas las máquinas virtuales de Hola que representa el nivel de servidor de aplicación de SAP de hello están en un tercer conjunto de disponibilidad.
* Todas las máquinas virtuales de hello ejecuta servidores de aplicaciones SAP usan su propia cuenta de almacenamiento. Falta de disponibilidad de una cuenta de almacenamiento hará falta de disponibilidad de un servidor de aplicaciones de SAP, donde otros AS SAP continuar toorun.

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] Alta disponibilidad en Linux
arquitectura de Hola de HA de SAP en Linux en Azure es básicamente Hola mismas que para Windows como se ha descrito anteriormente. Sin embargo, desde enero de 2016 hay dos restricciones:

* Actualmente, solo SAP ASE 16 es compatible con Linux en Azure sin las características de replicación de ASE.
* Todavía no hay ninguna solución de alta disponibilidad de SAP (A)SCS compatible con Linux en Azure.

En consecuencia como de enero de 2016 no se puede lograr un sistema SAP-Linux-Azure Hola mismo disponibilidad como un sistema SAP-Windows-Azure debido a falta de alta disponibilidad para la instancia de hello (A) SCS y Hola base de datos de SAP ASE de instancia única.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Uso de Autostart en las instancias de SAP
SAP ofrece funcionalidad de hello toostart las instancias de SAP inmediatamente después del inicio de Hola de hello SO dentro de hello máquina virtual. los pasos exactos Hola documentados en el artículo de Knowledge Base SAP [1909114] : cómo toostart SAP instancias automáticamente con el parámetro Autostart. Sin embargo, SAP no recomienda toouse Hola ya configuración porque no hay ningún control en orden de Hola de reinicios de instancia, suponiendo que se obtuvo afectada más de una máquina virtual o varias instancias que se ejecutaron por máquina virtual. Suponiendo que un escenario típico de Azure de una instancia del servidor de aplicaciones SAP en caso de una sola máquina virtual obtener reinicia finalmente hello y VM, Hola Autostart no es realmente importante y puede habilitarse mediante la adición de este parámetro:

    Autostart = 1

En hello inicie el perfil de la instancia de SAP ABAP o Java Hola.

> [!NOTE]
> Autostart, parámetro Hello puede tener también algunos problemas. Con más detalle, los desencadenadores de parámetro de Hola Hola inicio de una instancia de SAP ABAP o Java cuando Hola relacionados se ha iniciado el servicio de Windows o Linux de la instancia de Hola. Por supuesto, que es el caso de hello, cuando se arranca Hola los sistemas operativos. Sin embargo, los reinicios de los servicios de SAP también son frecuentes en la funcionalidad de administración del ciclo de vida de software de SAP como SUM u otras actualizaciones o modificaciones. Estas funcionalidades no están esperando un toobe instancia reiniciado automáticamente en absoluto. Por lo tanto, Autostart, parámetro hello debe deshabilitarse antes de ejecutar estas tareas. Autostart, parámetro Hello también no se recomienda para las instancias de SAP que se agrupan en clústeres, como ASCS/SCS/elementos de configuración.
>
>

Se puede consultar más información sobre el inicio automático de las instancias de SAP aquí:

* [Start/Stop SAP along with your Unix Server Start/Stop (Inicio/detención de SAP al iniciar/detener el servidor de Unix)](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Starting and Stopping SAP NetWeaver Management Agents (Inicio y detención de los agentes de administración de SAP NetWeaver)](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [¿Cómo tooenable automáticamente el inicio de base de datos HANA](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Sistemas SAP de tres niveles más grandes
Los aspectos relativos a la alta disponibilidad de las configuraciones de SAP de tres niveles ya se comentaron en las secciones anteriores. Pero ¿qué ocurre con los sistemas que son demasiado grandes requisitos de servidor DBMS de hello toohave encuentran en Azure, pero el nivel de aplicación de SAP de hello podría implementarse en Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Ubicación de las configuraciones de SAP de tres niveles
No es capa de aplicación de hello toosplit compatibles propio o aplicación hello y capa de DBMS entre local y Azure. Los sistemas SAP se deben implementar completamente en el entorno local O en Azure. Tampoco es compatible toohave algunas Hola servidores de aplicaciones ejecutan en local y otros en Azure. Que es hello punto de inicio de discusión de Hola. Además, no son compatibles con los componentes DBMS toohave Hola de un sistema SAP y Hola capa de servidor de aplicaciones de SAP implementado en dos regiones diferentes de Azure. Por ejemplo, implementar el DBMS en el oeste de EE. UU. y la capa de aplicación de SAP en el centro de EE. UU. Razón para no son compatibles con estas configuraciones es sensibilidad de latencia de Hola de hello arquitectura de SAP NetWeaver.

Sin embargo, durante Hola de datos del último año asociados center desarrollan ubicaciones coadministradores tooAzure regiones. Estas ubicaciones coadministradores son a menudo en datos de Azure física muy cerca toohello centros dentro de una región de Azure. distancia corta Hello y conexión de activos en la ubicación compartida Hola a través de ExpressRoute en Azure pueden dar lugar a una latencia que sea inferior a 2ms. En tales casos, es posible toolocate Hola capa de DBMS (incluido el almacenamiento SAN/NAS) en como una ubicación compartida y capa de aplicación de SAP de hello en Azure. Desde diciembre de 2015, ya no se realizan implementaciones de ese tipo. No obstante, hay diversos clientes con implementaciones de aplicaciones distintas de SAP que siguen empleando tales métodos.

### <a name="offline-backup-of-sap-systems"></a>Copia de seguridad sin conexión de sistemas SAP
Dependiente de hello configuración de SAP seleccionada (2 o 3 niveles) se podría ser una necesidad toobackup. contenido de Hola de hello propia máquina virtual más toohave una copia de seguridad de base de datos de Hola. Hola DBMS relacionados con las copias de seguridad son toobe esperado realiza con métodos de la base de datos. Una descripción detallada de hello diferentes bases de datos, se puede encontrar en [guía DBMS][dbms-guide]. En Hola otra parte, Hola datos SAP puede se copia de seguridad en un modo sin conexión (incluido el contenido de base de datos de hello así) como se describe en esta sección o en línea como se describe en la sección siguiente de Hola.

copia de seguridad sin conexión Hola básicamente requeriría un apagado de hello VM a través de hello Portal de Azure y una copia del disco de máquina virtual base hello más todos los adjunta toohello VM de discos duros virtuales. Esto conserva un punto de la imagen en tiempo de hello VM y su disco asociado. Se recomienda toocopy hello 'copias de seguridad' en una cuenta de almacenamiento de Azure diferente. Por lo tanto, Hola procedimiento descrito en el capítulo [copiar discos entre cuentas de almacenamiento de Azure] [ planning-guide-5.4.2] aplicaría de este documento.
Además de hello usa apagado Hola Portal de Azure uno puede hacerlo a través de Powershell o CLI como se describe aquí: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Estaría formado por una restauración de ese estado de la eliminación de hello VM base, así como los discos originales de Hola de hello base VM y VHD montados, copiar Hola Atrás guarda discos duros virtuales toohello cuenta de almacenamiento original y, a continuación, volver a implementar Hola sistema.
Este artículo muestra un ejemplo de cómo tooscript este proceso de Powershell: <http://www.westerndevs.com/azure-snapshots/>

Asegúrese de tooinstall seguro de una nueva licencia SAP desde una copia de seguridad de máquina virtual como se describió anteriormente restoing crea una nueva clave de hardware.

### <a name="online-backup-of-an-sap-system"></a>Copia de seguridad en línea de un sistema SAP
Copia de seguridad de hello DBMS se realiza con métodos específicos de DBMS como se describe en hello [guía DBMS][dbms-guide].

Pueden que otras máquinas virtuales dentro de hello sistema SAP se copia mediante la funcionalidad de copia de seguridad de máquina Virtual de Azure. Copia de seguridad de máquina Virtual de Azure se introdujo al principio de 2015 y al mismo tiempo es un método estándar toobackup una máquina virtual completa en Azure. Copia de seguridad de Azure almacena las copias de seguridad de hello en Azure y permite una restauración de una máquina virtual de nuevo.

> [!NOTE]
> A partir de diciembre de 2015 mediante copia de seguridad de máquina virtual no se debe mantener único Hola Id. de máquina virtual que se utiliza para SAP licencias. Esto significa que una restauración desde una copia de seguridad de la máquina virtual requiere la instalación de una nueva clave de licencia SAP como Hola restaurada VM se considera toobe una nueva máquina virtual y no un reemplazo de la anterior que se guardó.
> Desde enero de 2016, la copia de seguridad de máquinas virtuales de Azure todavía no es compatible con las máquinas virtuales implementadas con Azure Resource Manager.
>
> ![Windows][Logo_Windows] Windows
>
> Teóricamente máquinas virtuales de las bases de datos de ejecución pueden ser copia de seguridad de forma coherente si admite de sistemas DBMS Hola Hola Windows VSS (Volume Shadow Copy Service <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx > ) como por ejemplo, SQL Server.
> Sin embargo, se debe tener en cuenta que no se pueden restaurar bases de datos en un momento dado a partir de las copias de seguridad de máquinas virtuales de Azure. Por lo tanto, la recomendación es tooperform copias de seguridad de bases de datos con la funcionalidad DBMS en lugar de depender de copia de seguridad de máquina virtual de Azure
>
> tooget familiarizado con copia de seguridad de máquina Virtual de Azure, empiece aquí: <https://azure.microsoft.com/documentation/articles/backup-azure-vms/>.
>
> Otras posibilidades son toouse una combinación de Microsoft Data Protection Manager instalado en una máquina virtual de Azure y copia de seguridad de Azure para las bases de datos de copia de seguridad/restauración. Se puede encontrar más información aquí: <https://azure.microsoft.com/documentation/articles/backup-azure-dpm-introduction/>.  
>
> ![Linux][Logo_Linux] Linux
>
> No hay ningún equivalente tooWindows VSS en Linux. Por lo tanto, solo se pueden realizar copias de seguridad coherentes con archivos, pero no copias de seguridad coherentes con la aplicación. Hello SAP DBMS copia de seguridad debe hacerse mediante la funcionalidad DBMS. Hello sistema de archivos que incluye Hola SAP relacionadas con datos pueden guardarse por ejemplo, con tar tal como se describe aquí: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure como sitio de recuperación ante desastres para entornos de producción de SAP
Desde mediados de 2014, componentes de las extensiones toovarious alrededor de Hyper-V, System Center y Azure permiten el uso de Hola de Azure como sitio de recuperación ante desastres para las máquinas virtuales que se ejecutan en función de Hyper-V en local.

Un blog que detalla cómo toodeploy esta solución está documentado aquí: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>

## <a name="summary"></a>Resumen
Hola los puntos clave de alta disponibilidad de los sistemas SAP en Azure son:

* En este momento, Hola único punto de error SAP no se pueden proteger exactamente Hola de igual manera que se puede realizar en las implementaciones locales. motivo de Hello es que clústeres de discos compartidos no todavía pueden construirse en Azure sin usar Hola 3rd fabricantes de software.
* Para la capa de DBMS Hola necesita funcionalidad DBMS toouse que no se basa en tecnología de clústeres de disco compartido. Los detalles están documentados en hello [guía DBMS][dbms-guide].
* impacto de hello toominimize de problemas dentro de dominios de error en hello Azure mantenimiento de infraestructura o un host, debe usar conjuntos de disponibilidad de Azure:
  * Se recomienda toohave una conjunto de disponibilidad para la capa de aplicación de SAP de Hola.
  * Se recomienda toohave establece una disponibilidad diferente de capa de DBMS de SAP de Hola.
  * NO se recomienda hello tooapply que conjunto de disponibilidad mismo para las máquinas virtuales de diferentes sistemas SAP.
* Para fines de copia de seguridad de capa de DBMS de SAP de hello, compruebe hello [guía DBMS][dbms-guide].
* Copia de seguridad de instancias de diálogo de SAP tiene poco sentido, ya que es instancias de diálogo simples tooredeploy suele ser más rápidos.
* Realizar copias de seguridad Hola VM que contiene el directorio global de Hola de hello sistema SAP y con él todos los perfiles de Hola de instancias diferentes de hello, tiene sentido y debe realizarse con copia de seguridad de Windows o tar p. ej. en Linux. Dado que existen diferencias entre Windows Server 2008 (R2) y Windows Server 2012 (R2), que harán más fácil toobackup con hello más reciente versiones de Windows Server, se recomienda toorun Windows Server 2012 (R2) como sistema operativo de Windows.
