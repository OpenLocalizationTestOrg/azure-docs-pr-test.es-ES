---
title: Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver | Microsoft Docs
description: "Guía de alta disponibilidad para SAP NetWeaver en Azure Virtual Machines"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 65236f527b62b4990b062fb6a54ce13b3c182e93
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="5b1cb-103">Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
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
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="5b1cb-109">Azure Virtual Machines es la solución para organizaciones que necesitan recursos de red, almacenamiento y proceso, en un tiempo mínimo y sin ciclos de adquisición prolongados.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="5b1cb-110">Puede usar Azure Virtual Machines para implementar aplicaciones clásicas como ABAP basado en SAP NetWeaver, Java y la pila de ABAP+Java.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="5b1cb-111">Amplíe la confiabilidad y disponibilidad sin recursos locales adicionales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="5b1cb-112">Azure Virtual Machines admite la conectividad entre locales, así que podrá integrar Azure Virtual Machines a los dominios locales, las nubes privadas y la infraestructura de sistema SAP de la organización.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="5b1cb-113">En este artículo analizaremos los pasos que puede llevar a cabo para implementar sistemas SAP de alta disponibilidad en Azure con el uso del modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="5b1cb-114">Le guiaremos por estas tareas principales:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="5b1cb-115">Encontrar las notas y guías de instalación de SAP adecuadas, que aparecen en la sección [Recursos][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="5b1cb-116">Este documento complementa la documentación sobre la instalación de SAP y las notas de SAP, que son los recursos principales que lo ayudan a instalar e implementar software de SAP en plataformas específicas.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="5b1cb-117">Conocer las diferencias entre el modelo de implementación clásica de Azure y el modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="5b1cb-118">Obtener información sobre los modos de cuórum de Clústeres de conmutación por error de Windows Server, a fin de poder seleccionar el modelo adecuado para la implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="5b1cb-119">Obtener información sobre el almacenamiento compartido de Clústeres de conmutación por error de Windows Server en los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="5b1cb-120">Obtener información sobre cómo proteger en Azure los componentes con un único punto de error, como Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) y sistemas de administración de bases de datos (DBMS), además de componentes redundantes como los servidores de aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="5b1cb-121">Seguir un ejemplo detallado de la instalación y configuración de un sistema SAP de alta disponibilidad en un clúster de Clústeres de conmutación por error de Windows Server mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="5b1cb-122">Obtener información sobre los pasos adicionales que se necesitan para usar Clústeres de conmutación por error de Windows Server en Azure, pero que no son necesarios en una implementación local.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="5b1cb-123">Para simplificar la implementación y configuración, en este artículo usamos las nuevas plantillas de Resource Manager de alta disponibilidad y de tres niveles de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="5b1cb-124">Las plantillas automatizan la implementación de toda la infraestructura que necesita en un sistema SAP de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="5b1cb-125">La infraestructura también admite el ajuste de tamaño de SAP Application Performance Standard (SAPS) del sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="5b1cb-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="5b1cb-127">Antes de comenzar, asegúrese de cumplir los requisitos previos que se describen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="5b1cb-128">Además, asegúrese de revisar todos los recursos que aparecen en la sección [Recursos][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="5b1cb-129">En este artículo usamos las plantillas de Azure Resource Manager para [SAP NetWeaver de tres niveles](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="5b1cb-130">Consulte [Plantillas de Azure Resource Manager para SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/) para ver información general útil sobre las plantillas.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="5b1cb-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Recursos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="5b1cb-132">Estos artículos también se refieren a las implementaciones de SAP en Azure:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="5b1cb-133">[Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="5b1cb-134">[Implementación de Azure Virtual Machines para SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="5b1cb-135">[Implementación de DBMS de Azure Virtual Machines para SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="5b1cb-136">[Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver (esta guía)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-137">Siempre que sea posible, aparece un vínculo a la guía de instalación de SAP a la que se hace referencia (consulte las [guías de instalación de SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="5b1cb-138">Para consultar los requisitos previos e información sobre el proceso de instalación, se recomienda leer cuidadosamente las guías de instalación de SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="5b1cb-139">En este artículo solo se abarcan tareas específicas para los sistemas basados en SAP NetWeaver que puede usar con Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="5b1cb-140">Estas notas de SAP están relacionadas con el tema de SAP en Azure:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="5b1cb-141">Número de nota</span><span class="sxs-lookup"><span data-stu-id="5b1cb-141">Note number</span></span> | <span data-ttu-id="5b1cb-142">Título</span><span class="sxs-lookup"><span data-stu-id="5b1cb-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="5b1cb-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-143">[1928533]</span></span> |<span data-ttu-id="5b1cb-144">SAP Applications on Azure: Supported Products and Sizing (Aplicaciones SAP en Azure: productos y tamaños compatibles)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="5b1cb-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-145">[2015553]</span></span> |<span data-ttu-id="5b1cb-146">SAP on Microsoft Azure: Support Prerequisites (SAP en Microsoft Azure: requisitos previos de compatibilidad)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="5b1cb-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-147">[1999351]</span></span> |<span data-ttu-id="5b1cb-148">Enhanced Azure Monitoring for SAP (Supervisión mejorada de Azure para SAP)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="5b1cb-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-149">[2178632]</span></span> |<span data-ttu-id="5b1cb-150">Key Monitoring Metrics for SAP on Microsoft Azure (Métricas de supervisión clave para SAP en Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="5b1cb-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-151">[1999351]</span></span> |<span data-ttu-id="5b1cb-152">Virtualization on Windows: Enhanced Monitoring (Virtualización en Windows: supervisión mejorada)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="5b1cb-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-153">[2243692]</span></span> |<span data-ttu-id="5b1cb-154">Uso de almacenamiento SSD premium de Azure para la instancia DBMS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="5b1cb-155">Obtenga más información sobre las [limitaciones de las suscripciones de Azure][azure-subscription-service-limits-subscription], incluidas las limitaciones máximas y predeterminadas generales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="5b1cb-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de alta disponibilidad con el modelo de implementación de Azure Resource Manager en comparación con el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="5b1cb-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="5b1cb-157">El modelo de implementación de Azure Resource Manager y el modelo de implementación clásica se diferencian de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="5b1cb-158">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-158">Resource groups</span></span>
- <span data-ttu-id="5b1cb-159">Dependencia del equilibrador de carga interno de Azure en el grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="5b1cb-160">Soporte técnico para el escenario de varios SID de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="5b1cb-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="5b1cb-162">En Azure Resource Manager, puede usar los grupos de recursos para administrar todos los recursos de aplicación de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="5b1cb-163">En un enfoque integrado, todos los recursos de un grupo de recursos tienen el mismo ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="5b1cb-164">Por ejemplo, todos los recursos se crean en el mismo momento y se eliminan de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="5b1cb-165">Más información sobre los [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="5b1cb-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Dependencia del equilibrador de carga interno de Azure en el grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="5b1cb-167">En el modelo de implementación clásica de Azure, hay una dependencia entre el equilibrador de carga interno de Azure (servicio Azure Load Balancer) y el grupo de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service group.</span></span> <span data-ttu-id="5b1cb-168">Cada equilibrador de carga interno necesita un grupo de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="5b1cb-169">En el modelo de Azure Resource Manager, no necesita un grupo de recursos de Azure para usar Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-169">In Azure Resource Manager, you don't need an Azure resource group to use Azure Load Balancer.</span></span> <span data-ttu-id="5b1cb-170">El entorno es más sencillo y flexible.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-170">The environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="5b1cb-171">Soporte técnico para el escenario de varios SID de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="5b1cb-172">En Azure Resource Manager, puede instalar varias instancias de ASCS/SCS de identificador de sistema SAP (SID) en un clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="5b1cb-173">Esto es posible gracias a la compatibilidad con las distintas direcciones IP de cada equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="5b1cb-174">Si desea usar el modelo de implementación clásica de Azure, siga los procedimientos que se describen en [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056) (SAP NetWeaver en Azure: agrupación de clústeres de instancias de ASCS/SCS de SAP mediante Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-174">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b1cb-175">Recomendamos encarecidamente usar el modelo de implementación de Azure Resource Manager para las instalaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-175">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="5b1cb-176">Ofrece muchas ventajas que no están disponibles en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-176">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="5b1cb-177">Obtenga más información sobre los [modelos de implementación de Azure][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="5b1cb-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Clústeres de conmutación por error de Windows Server</span><span class="sxs-lookup"><span data-stu-id="5b1cb-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="5b1cb-179">Clústeres de conmutación por error de Windows Server es la base de una instalación de ASCS/SCS de SAP de alta disponibilidad y DBMS en Windows.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-179">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="5b1cb-180">Un clúster de conmutación por error es un grupo de 1+n servidores independientes (nodos) que colaboran para aumentar la disponibilidad de aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-180">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="5b1cb-181">Si se produce un error de nodo, Clústeres de conmutación por error de Windows Server calcula el número de errores que se pueden producir y mantiene un clúster en buen estado para proporcionar aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-181">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="5b1cb-182">Para conseguir clústeres de conmutación por error, puede elegir entre distintos modos de cuórum.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-182">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="5b1cb-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modos de cuórum</span><span class="sxs-lookup"><span data-stu-id="5b1cb-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="5b1cb-184">Puede elegir entre cuatro modos de cuórum cuando use Clústeres de conmutación por error de Windows Server:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="5b1cb-185">**Mayoría de nodo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-185">**Node Majority**.</span></span> <span data-ttu-id="5b1cb-186">Cada nodo del clúster puede votar.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-186">Each node of the cluster can vote.</span></span> <span data-ttu-id="5b1cb-187">El clúster funciona solamente con la mayoría de los votos, es decir, con más de la mitad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-187">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5b1cb-188">Se recomienda esta opción para los clústeres con un número impar de nodos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="5b1cb-189">Por ejemplo, 3 nodos de un clúster de 7 nodos pueden presentar un error y el clúster todavía obtendrá la mayoría y se seguirá ejecutando.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-189">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="5b1cb-190">**Mayoría de disco y nodo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="5b1cb-191">Cada nodo y disco designado (un testigo de disco) en el almacenamiento del clúster puede votar siempre que esté disponible y comunicándose.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-191">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="5b1cb-192">El clúster funciona solamente con la mayoría de los votos, es decir, con más de la mitad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-192">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5b1cb-193">Este modo resulta útil en un entorno de clúster con un número par de nodos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="5b1cb-194">Si la mitad de los nodos y el disco están en línea, el clúster permanece en buen estado.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-194">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="5b1cb-195">**Mayoría de recurso compartido de archivos y nodo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="5b1cb-196">Cada nodo más un recurso compartido de archivos designado (un testigo de recurso de archivos) que el administrador crea puede votar, independientemente de si los nodos y el recurso compartido de archivos están disponibles y comunicándose.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-196">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="5b1cb-197">El clúster funciona solamente con la mayoría de los votos, es decir, con más de la mitad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-197">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5b1cb-198">Este modo resulta útil en un entorno de clúster con un número par de nodos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="5b1cb-199">Es similar al modo Mayoría de disco y nodo, pero usa un recurso compartido de archivos testigo en lugar de un disco testigo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-199">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="5b1cb-200">Este modo es fácil de implementar pero, si el recurso compartido de archivos en sí no es de alta disponibilidad, es posible que se convierta en un único punto de error.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-200">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="5b1cb-201">**Sin mayoría: solo disco**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="5b1cb-202">El clúster tiene cuórum si hay un nodo disponible y comunicándose con un disco específico en el almacenamiento del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-202">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="5b1cb-203">Los únicos nodos que pueden unirse al clúster son aquellos que estén comunicándose con ese disco.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-203">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="5b1cb-204">No se recomienda usar este modo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="5b1cb-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Clústeres de conmutación por error de Windows Server local</span><span class="sxs-lookup"><span data-stu-id="5b1cb-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="5b1cb-206">En la figura 1 se muestra un clúster de dos nodos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="5b1cb-207">Si se produce un error en la conexión de red entre los nodos pero ambos nodos se mantienen activos y en ejecución, un recurso compartido de archivos o un disco de cuórum determinará el nodo que seguirá proporcionando las aplicaciones y servicios del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-207">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="5b1cb-208">El nodo que tiene acceso al recurso compartido de archivos o disco de cuórum es el nodo que garantiza la continuación de los servicios.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-208">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="5b1cb-209">Debido a que este ejemplo usa un clúster de dos nodos, usamos el modo de cuórum Mayoría de recurso compartido de archivos y nodo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-209">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="5b1cb-210">Otra opción válida es el modo Mayoría de disco y nodo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-210">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="5b1cb-211">En un entorno de producción, se recomienda usar un disco de cuórum.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="5b1cb-212">Puede usar tecnología de sistema de almacenamiento y red para hacerlo de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-212">You can use network and storage system technology to make it highly available.</span></span>

![Figura 1: Ejemplo de una configuración de Clústeres de conmutación por error de Windows Server para ASCS/SCS de SAP en Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="5b1cb-214">_**Figura 1:** Ejemplo de una configuración de Clústeres de conmutación por error de Windows Server para ASCS/SCS de SAP en Azure_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="5b1cb-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Almacenamiento compartido</span><span class="sxs-lookup"><span data-stu-id="5b1cb-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="5b1cb-216">En la figura 1 también se muestra un clúster de almacenamiento compartido de dos nodos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="5b1cb-217">En un clúster de almacenamiento compartido local, todos los nodos del clúster detectan el almacenamiento compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-217">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="5b1cb-218">Un mecanismo de bloqueo protege los datos contra daños.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-218">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="5b1cb-219">Todos los nodos pueden detectar si se produce un error en otro nodo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="5b1cb-220">Si se produce un error en un nodo, el nodo restante asume la propiedad de los recursos de almacenamiento y garantiza la disponibilidad de los servicios.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-220">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-221">No necesita discos compartidos para obtener alta disponibilidad con algunas aplicaciones de DBMS, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="5b1cb-222">SQL Server Always On replica archivos de registro y datos de DBMS desde el disco local de un nodo del clúster hasta el disco local del otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-222">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="5b1cb-223">En ese caso, la configuración de clúster de Windows no necesita un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-223">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="5b1cb-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Redes y resolución de nombres</span><span class="sxs-lookup"><span data-stu-id="5b1cb-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="5b1cb-225">Los equipos cliente se comunican con el clúster a través de una dirección IP virtual y un nombre de host virtual que el servidor DNS proporciona.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-225">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="5b1cb-226">Los nodos locales y el servidor DNS pueden administrar varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-226">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="5b1cb-227">En una configuración típica, puede usar dos o más conexiones de red:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="5b1cb-228">Una conexión dedicada al almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-228">A dedicated connection to the storage</span></span>
* <span data-ttu-id="5b1cb-229">Una conexión de red interna del clúster para el latido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-229">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="5b1cb-230">Una red pública que los clientes usan para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-230">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="5b1cb-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Clústeres de conmutación de Windows Server en Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="5b1cb-232">En comparación con las implementaciones de nube privada o sin sistema operativo, Azure Virtual Machines requiere pasos adicionales para configurar Clústeres de conmutación por error de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-232">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="5b1cb-233">Cuando compila un disco de clúster compartido, deberá establecer varias direcciones IP y nombres de host virtual para la instancia de ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-233">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="5b1cb-234">En este artículo se analizan los conceptos clave y los pasos adicionales que se requieren para compilar un clúster de servicios centrales de alta disponibilidad de SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-234">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="5b1cb-235">Mostramos cómo configurar la herramienta de terceros SIOS DataKeeper y configurar el equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-235">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="5b1cb-236">Puede usar estas herramientas para crear un clúster de conmutación por error de Windows con un testigo de recurso compartido de archivos en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-236">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: Configuración de Clústeres de conmutación por error de Windows Server en Azure sin un disco compartido][sap-ha-guide-figure-1001]

<span data-ttu-id="5b1cb-238">_**Figura 2:** Configuración de Clústeres de conmutación por error de Windows Server en Azure sin un disco compartido_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="5b1cb-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco compartido en Azure con SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5b1cb-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="5b1cb-240">Se necesita almacenamiento compartido de clúster para una instancia de ASCS/SCS de SAP de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5b1cb-241">A partir de septiembre de 2016, Azure no ofrece almacenamiento compartido que puede usar para crear un clúster de almacenamiento compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-241">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="5b1cb-242">Puede usar el software de terceros SIOS DataKeeper Cluster Edition para crear un almacenamiento reflejado que simula el almacenamiento compartido de clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-242">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="5b1cb-243">La solución SIOS proporciona replicación sincrónica de datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-243">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="5b1cb-244">Este es el procedimiento para crear un recurso de disco compartido para un clúster:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="5b1cb-245">Conecte un disco duro virtual (VHD) de Azure adicional a cada una de las máquinas virtuales de una configuración de clúster de Windows.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-245">Attach an additional Azure virtual hard disk (VHD) to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="5b1cb-246">Ejecute SIOS DataKeeper Cluster Edition en ambos nodos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="5b1cb-247">Configure SIOS DataKeeper Cluster Edition de forma que refleje el contenido del volumen del VHD adicional conectado desde la máquina virtual de origen al volumen conectado del VHD adicional de la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional VHD attached volume from the source virtual machine to the additional VHD attached volume of the target virtual machine.</span></span> <span data-ttu-id="5b1cb-248">SIOS DataKeeper abstrae los volúmenes locales de origen y de destino, y los presenta a Clústeres de conmutación por error de Windows Server como un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-248">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="5b1cb-249">Obtenga más información sobre [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: Configuración de Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="5b1cb-251">_**Figura 3:** Configuración de Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-252">No necesita discos compartidos para obtener alta disponibilidad con algunos productos de DBMS, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="5b1cb-253">SQL Server Always On replica archivos de registro y datos de DBMS desde el disco local de un nodo del clúster hasta el disco local del otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-253">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="5b1cb-254">En este caso, la configuración de clúster de Windows no necesita un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-254">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="5b1cb-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Resolución de nombres en Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="5b1cb-256">La plataforma en la nube de Azure no ofrece la opción de configurar direcciones IP virtuales, como direcciones IP flotantes.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-256">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="5b1cb-257">Necesita una solución alternativa para configurar una dirección IP virtual que se comunique con el recurso de clúster en la nube.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-257">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="5b1cb-258">Azure tiene un equilibrador de carga interno en el servicio Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-258">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="5b1cb-259">Con el equilibrador de carga interno, los clientes se comunican con el clúster a través de la dirección IP virtual del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-259">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="5b1cb-260">Necesita implementar el equilibrador de carga interno en el grupo de recursos que contiene los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-260">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="5b1cb-261">Luego, configure todas las reglas de enrutamiento de puerto necesarias con los puertos de sondeo del equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-261">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="5b1cb-262">Los clientes se pueden conectar por medio del nombre de host virtual.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-262">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="5b1cb-263">El servidor DNS resuelve la dirección IP del clúster y el equilibrador de carga interno controla el enrutamiento de puerto al nodo activo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-263">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="5b1cb-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Alta disponibilidad de SAP NetWeaver en infraestructura como servicio (IaaS) de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="5b1cb-265">Para obtener alta disponibilidad en las aplicaciones de SAP, como para los componentes de software de SAP, necesita proteger los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-265">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="5b1cb-266">Instancia de servidores de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-266">SAP Application Server instance</span></span>
* <span data-ttu-id="5b1cb-267">instancia de SAP ASCS/SCS,</span><span class="sxs-lookup"><span data-stu-id="5b1cb-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="5b1cb-268">servidor DBMS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-268">DBMS server</span></span>

<span data-ttu-id="5b1cb-269">Para obtener más información sobre cómo proteger los componentes SAP en escenarios de alta disponibilidad, consulte [Planeamiento e implementación de Azure Virtual Machines para SAP NetWeaver](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="5b1cb-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Alta disponibilidad en los servidores de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="5b1cb-271">Por lo general, no se necesita una solución de alta disponibilidad específica para las instancias de diálogo y servidores de aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-271">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="5b1cb-272">Obtiene alta disponibilidad mediante redundancia y configurará varias instancias de diálogo en distintas instancias de Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="5b1cb-273">Debe tener, como mínimo, 2 instancias de aplicaciones de SAP instaladas en 2 instancias de Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Alta disponibilidad en los servidores de aplicaciones de SAP][sap-ha-guide-figure-2000]

<span data-ttu-id="5b1cb-275">_**Figura 4**: Alta disponibilidad en los servidores de aplicaciones de SAP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="5b1cb-276">Debe colocar todas las máquinas virtuales que hospedan instancias de servidores de aplicaciones de SAP en el mismo conjunto de disponibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-276">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="5b1cb-277">Un conjunto de disponibilidad de Azure garantiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="5b1cb-278">Todas las máquinas virtuales forman parte del mismo dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-278">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="5b1cb-279">Por ejemplo, un dominio de actualización garantiza que las máquinas virtuales no se actualicen al mismo tiempo durante un tiempo de inactividad de mantenimiento planeado.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-279">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="5b1cb-280">Todas las máquinas virtuales forman parte del mismo dominio de error.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-280">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="5b1cb-281">Por ejemplo, un dominio de error garantiza que las máquinas virtuales estén implementadas de tal manera que ningún único punto de error afecte la disponibilidad de todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="5b1cb-282">Aprenda cómo [administrar la disponibilidad de las máquinas virtuales][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-282">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="5b1cb-283">Como la cuenta de almacenamiento de Azure es un punto único de error potencial, es importante tener, como mínimo, 2 cuentas de almacenamiento de Azure, en los cuales hay distribuidas, al menos, 2 máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-283">Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="5b1cb-284">En una configuración ideal, los discos de cada máquina virtual que ejecuta una instancia de diálogo de SAP estarían implementados en una cuenta de almacenamiento distinta.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-284">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="5b1cb-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instancia de ASCS/SCS de SAP de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="5b1cb-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="5b1cb-286">La figura 5 es un ejemplo de una instancia de ASCS/SCS de SAP de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: Instancia de ASCS/SCS de SAP de alta disponibilidad][sap-ha-guide-figure-2001]

<span data-ttu-id="5b1cb-288">_**Figura 5:** Instancia de ASCS/SCS de SAP de alta disponibilidad_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="5b1cb-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Alta disponibilidad de instancia de ASCS/SCS de SAP con Clústeres de conmutación por error de Windows Server en Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="5b1cb-290">En comparación con las implementaciones de nube privada o sin sistema operativo, Azure Virtual Machines requiere pasos adicionales para configurar Clústeres de conmutación por error de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-290">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="5b1cb-291">A fin de compilar un clúster de conmutación por error de Windows, necesita un disco de clúster compartido, varias direcciones IP, varios nombres de host virtual y un equilibrador de carga interno de Azure para la agrupación en clústeres de una instancia de ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-291">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5b1cb-292">Analizaremos esto con más detalle más adelante en el artículo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-292">We discuss this in more detail later in the article.</span></span>

![Figura 6: Clústeres de conmutación por error de Windows Server para una configuración de ASCS/SCS de SAP en Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="5b1cb-294">_**Figura 6:** Clústeres de conmutación por error de Windows Server para una configuración de ASCS/SCS de SAP en Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="5b1cb-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Alta disponibilidad para la instancia de DBMS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="5b1cb-296">DBMS también es un único punto de contacto de un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-296">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="5b1cb-297">Debe protegerlo con una solución de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-297">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="5b1cb-298">La figura 7 muestra una solución de alta disponibilidad de SQL Server AlwaysOn en Azure mediante el uso de Clústeres de conmutación por error de Windows Server y el equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="5b1cb-299">SQL Server AlwaysOn replica los archivos de datos y de registro de DBMS con su propia replicación DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="5b1cb-300">En este caso, no se necesitan discos compartidos de clúster, lo que simplifica toda la configuración.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-300">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Figura 7: Ejemplo de DBMS de SAP de alta disponibilidad (SQL Server AlwaysOn)][sap-ha-guide-figure-2003]

<span data-ttu-id="5b1cb-302">_**Figura 7:** Ejemplo de DBMS de SAP de alta disponibilidad (SQL Server AlwaysOn)_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="5b1cb-303">Para más información sobre cómo agrupar el clústeres SQL Server en Azure con el modelo de implementación de Azure Resource Manager, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-303">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="5b1cb-304">[Configuración de un grupo de disponibilidad AlwaysOn en Azure Virtual Machines mediante Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="5b1cb-305">[Configuración de un equilibrador de carga interno para un grupo de disponibilidad AlwaysOn de Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="5b1cb-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="5b1cb-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Escenarios de implementación completa de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="5b1cb-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="5b1cb-307">Escenario de implementación con la plantilla 1 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="5b1cb-308">En la figura 8 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **UN** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="5b1cb-309">Este escenario se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5b1cb-310">Se usa un clúster dedicado para la instancia de ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-310">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="5b1cb-311">Se usa un clúster dedicado para la instancia de DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-311">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="5b1cb-312">Se implementan instancias de servidores de aplicaciones SAP en máquinas virtuales dedicadas propias.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: Plantilla 1 de arquitectura de alta disponibilidad de SAP con un clúster dedicado para ASCS/SCS y DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="5b1cb-314">_**Figura 8**: Plantilla 1 de arquitectura de alta disponibilidad de SAP con un clúster dedicado para ASCS/SCS y DBMS_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="5b1cb-315">Escenario de implementación con la plantilla 2 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="5b1cb-316">En la figura 9 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **UN** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="5b1cb-317">Este escenario se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5b1cb-318">Se usa un clúster dedicado **TANTO** para la instancia de ASCS/SCS de SAP como para la de DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-318">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="5b1cb-319">Se implementan instancias de servidores de aplicaciones SAP en máquinas virtuales dedicadas propias.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: Plantilla 2 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para ASCS/SCS y otro para la instancia de DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="5b1cb-321">_**Figura 9:** Plantilla 2 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para ASCS/SCS y otro para la instancia de DBMS_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="5b1cb-322">Escenario de implementación con la plantilla 3 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="5b1cb-323">En la figura 10 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **DOS** sistemas SAP, con &lt;SID1&gt; y &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="5b1cb-324">Este escenario se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5b1cb-325">Un clúster dedicado se usa **TANTO** para la instancia SID1 de ASCS/SCS *como* para la instancia SID2 de ASCS/SCS de SAP (un clúster).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-325">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="5b1cb-326">Se usa un clúster dedicado para SID 1 de DBMS y otro para SID2 de DBMS (dos clústeres).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="5b1cb-327">Las instancias de servidores de aplicaciones SAP del SID1 del sistema SAP tienen su propia máquina virtual dedicada.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-327">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="5b1cb-328">Las instancias de servidores de aplicaciones SAP del SID2 del sistema SAP tienen su propia máquina virtual dedicada.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-328">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: Plantilla 3 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para las diferentes instancias de ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="5b1cb-330">_**Figura 10:** Plantilla 3 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para las diferentes instancias de ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="5b1cb-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Preparación de la infraestructura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="5b1cb-332">Preparación de la infraestructura de la plantilla 1 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-332">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="5b1cb-333">Las plantillas de Azure Resource Manager para SAP ayudan a simplificar la implementación de los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="5b1cb-334">Las plantillas de 3 niveles de Azure Resource Manager también admiten escenarios de alta disponibilidad, como la plantilla 1 de arquitectura, que tiene 2 clústeres.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-334">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="5b1cb-335">Cada clúster es un único punto de error de SAP para ASCS/SCS de SAP y DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="5b1cb-336">Aquí puede obtener las plantillas de Azure Resource Manager para el escenario de ejemplo que se describe en este artículo:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-336">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="5b1cb-337">Imagen de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5b1cb-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="5b1cb-338">Imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="5b1cb-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="5b1cb-339">Para preparar la plantilla 1 de arquitectura, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-339">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="5b1cb-340">En Azure Portal, en la hoja **Parámetros** del cuadro **SYSTEMAVAILABILITY**, seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-340">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: Especificación de los parámetros de Azure Resource Manager para alta disponibilidad de SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="5b1cb-342">_**Figura 11:** Especificación de los parámetros de Azure Resource Manager para alta disponibilidad de SAP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="5b1cb-343">Las plantillas crean:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-343">The templates create:</span></span>

  * <span data-ttu-id="5b1cb-344">**Máquinas virtuales**:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="5b1cb-345">Máquinas virtuales de Servidor de aplicaciones de SAP: <*SIDSistemaSAP*>-di-<*Número*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="5b1cb-346">Máquinas virtuales de clúster de ASCS/SCS: <*SIDSistemaSAP*>-ascs-<*Número*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="5b1cb-347">Un clúster de DBMS: <*SIDSistemaSAP*>-db-<*Número*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="5b1cb-348">**Tarjetas de red para todas las máquinas virtuales con direcciones IP asociadas**:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="5b1cb-349"><*SIDSistemaSAP*>-nic-di-<*Número*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="5b1cb-350"><*SIDSistemaSAP*>-nic-ascs-<*Número*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="5b1cb-351"><*SIDSistemaSAP*>-nic-db-<*Número*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="5b1cb-352">**Cuentas de almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="5b1cb-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="5b1cb-353">**Grupos de disponibilidad** para:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="5b1cb-354">Máquinas virtuales de Servidor de aplicaciones de SAP: <*SIDSistemaSAP*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="5b1cb-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="5b1cb-355">Máquinas virtuales de clúster de ASCS/SCS de SAP: <*SIDSistemaSAP*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="5b1cb-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="5b1cb-356">Máquinas virtuales de clúster de DBMS: <*SIDSistemaSAP*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="5b1cb-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="5b1cb-357">**Equilibrador de carga interno de Azure**:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="5b1cb-358">Con todos los puertos para la dirección IP y la instancia de ASCS/SCS <*SIDSistemaSAP*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5b1cb-358">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="5b1cb-359">Con todos los puertos para la dirección IP y DBMS de SQL Server <*SIDSistemaSAP*>-lb-db</span><span class="sxs-lookup"><span data-stu-id="5b1cb-359">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="5b1cb-360">**Grupo de seguridad de red**: <*SIDSistemaSAP*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="5b1cb-361">Con un puerto de Protocolo de escritorio remoto (RDP) externo abierto para la máquina virtual <*SIDSistemaSAP*>-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-361">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-362">De manera predeterminada, todas las direcciones IP de las tarjetas de red y los equilibradores de carga internos de Azure son **dinámicos**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-362">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="5b1cb-363">Cámbielas a direcciones IP **estáticas**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-363">Change them to **static** IP addresses.</span></span> <span data-ttu-id="5b1cb-364">Esto se describe más adelante en el artículo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-364">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="5b1cb-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Implementación de máquinas virtuales con conectividad de red corporativa (entre locales) para uso en producción</span><span class="sxs-lookup"><span data-stu-id="5b1cb-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="5b1cb-366">Para los sistemas de producción de SAP, implemente máquinas virtuales de Azure con [conectividad de red corporativa (entre locales)][planning-guide-2.2] mediante el uso de VPN de sitio a sitio de Azure o Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-367">Puede usar la instancia de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="5b1cb-368">La red virtual y la subred ya se crearon y están preparadas.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-368">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="5b1cb-369">En Azure Portal, en la hoja **Parámetros** del cuadro **NEWOREXISTINGSUBNET**, seleccione **Existente**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-369">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="5b1cb-370">En el cuadro **SUBNETID**, agregue la cadena completa de SubnetID de la red de Azure, donde planea implementar las máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-370">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="5b1cb-371">Ejecute este comando de PowerShell para obtener una lista de todas las subredes de red de Azure:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-371">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="5b1cb-372">El campo **ID** muestra el valor de **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-372">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="5b1cb-373">Ejecute este comando de PowerShell para obtener una lista de todos los valores de **SUBNETID**:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-373">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="5b1cb-374">El aspecto del identificador **SUBNETID** es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-374">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="5b1cb-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Implementación solo en la nube de instancias de SAP para prueba o demostración</span><span class="sxs-lookup"><span data-stu-id="5b1cb-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="5b1cb-376">Puede implementar el sistema de SAP de alta disponibilidad en un modelo de implementación solo en la nube.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="5b1cb-377">Este tipo de implementación se usa principalmente para demostrar o probar casos de uso.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="5b1cb-378">No es idóneo para los casos de uso de producción.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="5b1cb-379">En Azure Portal, en la hoja **Parámetros** del cuadro **NEWOREXISTINGSUBNET**, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-379">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="5b1cb-380">Deje vacío el campo **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-380">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="5b1cb-381">La plantilla de Azure Resource Manager para SAP crea automáticamente la subred y red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-381">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-382">También debe implementar, como mínimo, una máquina virtual dedicada para Active Directory y DNS en la misma instancia de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-382">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="5b1cb-383">La plantilla no crea estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-383">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="5b1cb-384">Preparación de la infraestructura de la plantilla 2 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-384">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="5b1cb-385">Puede usar estas plantillas de Azure Resource Manager para simplificar la implementación de los recursos de la infraestructura necesarios para la plantilla 2 de arquitectura de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-385">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="5b1cb-386">Aquí puede obtener las plantillas de Azure Resource Manager para este escenario de implementación:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="5b1cb-387">Imagen de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5b1cb-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="5b1cb-388">Imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="5b1cb-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="5b1cb-389">Preparación de la infraestructura de la plantilla 3 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="5b1cb-389">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="5b1cb-390">Puede preparar la infraestructura y configurar SAP para **varios SID**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-390">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="5b1cb-391">Por ejemplo, puede agregar una instancia de ASCS/SCS de SAP adicional en una configuración de clúster *existente*.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="5b1cb-392">Para obtener más información, consulte [Configuración de una instancia adicional de ASCS/SCS de SAP en una configuración de clúster existente para crear una configuración de varios SID de SAP: Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="5b1cb-393">Si desea crear un nuevo clúster de varios SID, puede usar las [plantillas de inicio rápido en GitHub](https://github.com/Azure/azure-quickstart-templates) para varios SID.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-393">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="5b1cb-394">Para crear un nuevo clúster de varios SID, debe implementar las tres plantillas siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-394">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="5b1cb-395">Plantilla de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="5b1cb-396">Plantilla de base de datos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="5b1cb-397">Plantilla de servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="5b1cb-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="5b1cb-398">Las siguientes secciones contienen más detalles sobre las plantillas y los parámetros que debe proporcionar en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-398">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="5b1cb-399"><a name="ASCS-SCS-template"></a>Plantilla de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="5b1cb-400">La plantilla de ASCS/SCS permite implementar dos máquinas virtuales que se pueden usar para crear un clúster de conmutación por error de Windows Server que hospeda varias instancias de ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-400">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="5b1cb-401">Para configurar la plantilla de varios SID de ASCS/SCS, en la [plantilla de varios SID de ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image], especifique valores para los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-401">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for the following parameters:</span></span>

  - <span data-ttu-id="5b1cb-402">**Prefijo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-402">**Resource Prefix**.</span></span>  <span data-ttu-id="5b1cb-403">Establezca el prefijo de recurso, que se utiliza para prefijar todos los recursos que se hayan creado durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-403">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="5b1cb-404">Dado que los recursos no pertenecen a un único sistema SAP, el prefijo del recurso no es el SID de un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-404">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="5b1cb-405">El prefijo debe tener entre **tres y seis caracteres**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-405">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="5b1cb-406">**Tipo de pila**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-406">**Stack Type**.</span></span> <span data-ttu-id="5b1cb-407">Seleccione el tipo de la pila del sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-407">Select the stack type of the SAP system.</span></span> <span data-ttu-id="5b1cb-408">Dependiendo del tipo de la pila, Azure Load Balancer tendrá una (solo ABAP o JAVA) o dos (ABAP + JAVA) direcciones IP privadas por cada sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-408">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="5b1cb-409">**Tipo de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-409">**OS Type**.</span></span> <span data-ttu-id="5b1cb-410">Seleccione el sistema operativo de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-410">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5b1cb-411">**Recuento de sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-411">**SAP System Count**.</span></span> <span data-ttu-id="5b1cb-412">Seleccione número de sistemas SAP que desea instalar en este clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-412">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="5b1cb-413">**Disponibilidad del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-413">**System Availability**.</span></span> <span data-ttu-id="5b1cb-414">Seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-414">Select **HA**.</span></span>
  -  <span data-ttu-id="5b1cb-415">**Nombre de usuario y contraseña del administrador**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5b1cb-416">Cree un nuevo usuario que pueda usarse para iniciar sesión en la máquina.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-416">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5b1cb-417">**Subred nueva o existente**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="5b1cb-418">Establezca si es necesario crear una red virtual y subred nuevas o si se debe usar una subred existente.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="5b1cb-419">Si ya tiene una red virtual conectada a la red local, seleccione la **existente**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-419">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="5b1cb-420">**Identificador de subred**. Establezca el identificador de la subred a la que deben conectarse las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-420">**Subnet Id**. Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="5b1cb-421">Seleccione la subred de la red privada virtual (VPN) o la red virtual de ExpressRoute para conectar la máquina virtual a la red local.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-421">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="5b1cb-422">Normalmente, el identificador tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-422">The ID usually looks like this:</span></span>

   <span data-ttu-id="5b1cb-423">/subscriptions/<*identificador de suscripción*>/resourceGroups/<*nombre del grupo de recursos*>/providers/Microsoft.Network/virtualNetworks/<*nombre de la red virtual*>/subnets/<*nombre de la subred*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="5b1cb-424">La plantilla implementa una instancia de Azure Load Balancer que admite varios sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-424">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="5b1cb-425">Las instancias de ASCS se configuran según el número de instancia 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-425">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="5b1cb-426">Las instancias de SCS se configuran según el número de instancia 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-426">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="5b1cb-427">Las instancias de ASCS Enqueue Replication Server (ERS) (solo Linux) se configuran según el número de instancia 02, 12, 22, etc.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-427">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="5b1cb-428">Las instancias de SCS ERS (solo Linux) se configuran según el número de instancia 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-428">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="5b1cb-429">El equilibrador de carga contiene 1 (2 para Linux) VIP, 1 VIP para ASCS/SCS y 1 VIP para ERS (solo Linux).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-429">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="5b1cb-430">En la lista siguiente se incluyen todas las reglas de equilibrio de carga (donde x es el número del sistema SAP, por ejemplo, 1, 2, 3, etc.):</span><span class="sxs-lookup"><span data-stu-id="5b1cb-430">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="5b1cb-431">Puertos específicos de Windows para cada sistema SAP 445, 5985</span><span class="sxs-lookup"><span data-stu-id="5b1cb-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="5b1cb-432">Puertos ASCS (número de instancia x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="5b1cb-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="5b1cb-433">Puertos SCS (número de instancia x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="5b1cb-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="5b1cb-434">Puertos ASCS ERS en Linux (número de instancia x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="5b1cb-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="5b1cb-435">Puertos SCS ERS en Linux (número de instancia x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="5b1cb-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="5b1cb-436">El equilibrador de carga se configurará para usar los siguientes puertos de sondeo (donde x es el número del sistema SAP, por ejemplo, 1, 2, 3,...):</span><span class="sxs-lookup"><span data-stu-id="5b1cb-436">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="5b1cb-437">Puerto de sondeo del equilibrador de carga interno de ASCS/SCS: 620x0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="5b1cb-438">Puerto de sondeo del equilibrador de carga interno de ERS (solo para Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="5b1cb-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="5b1cb-439"><a name="database-template"></a> Plantilla de base de datos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="5b1cb-440">La plantilla de la base de datos implementa uno o dos máquinas virtuales que puede usar para instalar el sistema de administración de bases de datos relacionales (RDBMS) de un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-440">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="5b1cb-441">Por ejemplo, si ha implementado una plantilla de ASCS/SCS para 5 sistemas SAP, debe implementar esta plantilla cinco veces.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="5b1cb-442">Para configurar la plantilla de varios SID de las bases de datos, especifique [en ella][sap-templates-3-tier-multisid-db-marketplace-image] los valores para los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-442">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="5b1cb-443">**Identificador de sistema SAP**. Escriba el identificador del sistema SAP que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-443">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="5b1cb-444">El identificador se utilizará como prefijo para los recursos que se implementen.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-444">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="5b1cb-445">**Tipo de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-445">**Os Type**.</span></span> <span data-ttu-id="5b1cb-446">Seleccione el sistema operativo de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-446">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5b1cb-447">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-447">**Dbtype**.</span></span> <span data-ttu-id="5b1cb-448">Seleccione el tipo de base de datos que desea instalar en el clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-448">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="5b1cb-449">Seleccione **SQL** si desea instalar Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-449">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="5b1cb-450">Seleccione **HANA** si tiene previsto instalar SAP HANA en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-450">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="5b1cb-451">Asegúrese de seleccionar el tipo de sistema operativo correcto: **Windows** para SQL y una distribución de Linux para HANA.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-451">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="5b1cb-452">La instancia de Azure Load Balancer que está conectada a las máquinas virtuales se configurará para admitir el tipo de base de datos seleccionado:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-452">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="5b1cb-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-453">**SQL**.</span></span> <span data-ttu-id="5b1cb-454">El equilibrador de carga equilibrará la carga del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-454">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="5b1cb-455">Asegúrese de que utiliza este puerto para la configuración de SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-455">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="5b1cb-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-456">**HANA**.</span></span> <span data-ttu-id="5b1cb-457">El equilibrador de carga equilibrará la carga de los puertos 35015 y 35017.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-457">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="5b1cb-458">Asegúrese de instalar SAP HANA con el número de instancia **50**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-458">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="5b1cb-459">El equilibrador de carga usará el puerto de sondeo 62550.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-459">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="5b1cb-460">**Tamaño del sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-460">**Sap System Size**.</span></span> <span data-ttu-id="5b1cb-461">La cantidad de sistemas SAP que proporcionará el sistema nuevo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-461">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="5b1cb-462">Si no está seguro de cuántos SAPS necesitará el sistema, consulte con el integrador de sistemas o el asociado tecnológico de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-462">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="5b1cb-463">**Disponibilidad del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-463">**System Availability**.</span></span> <span data-ttu-id="5b1cb-464">Seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-464">Select **HA**.</span></span>
  -  <span data-ttu-id="5b1cb-465">**Nombre de usuario y contraseña del administrador**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5b1cb-466">Cree un nuevo usuario que pueda usarse para iniciar sesión en la máquina.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-466">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5b1cb-467">**Identificador de subred**. Escriba el identificador de la subred que usó durante la implementación de la plantilla de ASCS/SCS o el identificador de la subred que se creó como parte de la implementación de esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-467">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="5b1cb-468"><a name="application-servers-template"></a>Plantilla de servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="5b1cb-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="5b1cb-469">La plantilla de servidores de aplicaciones permite implementar dos o más máquinas virtuales que se pueden usar como instancias de servidores de aplicaciones SAP en un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-469">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="5b1cb-470">Por ejemplo, si ha implementado una plantilla de ASCS/SCS para 5 sistemas SAP, debe implementar esta plantilla cinco veces.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="5b1cb-471">Para configurar la plantilla de varios SID de servidores de aplicaciones, especifique [en ella][sap-templates-3-tier-multisid-apps-marketplace-image] valores para los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-471">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="5b1cb-472">**Identificador de sistema SAP**. Escriba el identificador del sistema SAP que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-472">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="5b1cb-473">El identificador se utilizará como prefijo para los recursos que se implementen.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-473">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="5b1cb-474">**Tipo de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-474">**Os Type**.</span></span> <span data-ttu-id="5b1cb-475">Seleccione el sistema operativo de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-475">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5b1cb-476">**Tamaño del sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-476">**Sap System Size**.</span></span> <span data-ttu-id="5b1cb-477">La cantidad de SAPS que proporcionará el sistema nuevo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-477">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="5b1cb-478">Si no está seguro de cuántos SAPS necesitará el sistema, consulte con el integrador de sistemas o el asociado tecnológico de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-478">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="5b1cb-479">**Disponibilidad del sistema**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-479">**System Availability**.</span></span> <span data-ttu-id="5b1cb-480">Seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-480">Select **HA**.</span></span>
  -  <span data-ttu-id="5b1cb-481">**Nombre de usuario y contraseña del administrador**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5b1cb-482">Cree un nuevo usuario que pueda usarse para iniciar sesión en la máquina.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-482">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5b1cb-483">**Identificador de subred**. Escriba el identificador de la subred que usó durante la implementación de la plantilla de ASCS/SCS o el identificador de la subred que se creó como parte de la implementación de esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-483">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="5b1cb-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="5b1cb-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="5b1cb-485">En nuestro ejemplo, el espacio de direcciones de la máquina virtual de Azure es 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-485">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="5b1cb-486">Hay una subred llamada **Subnet**, con un intervalo de direcciones de 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="5b1cb-487">Todas las máquinas virtuales y los equilibradores de carga internos están implementados en esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b1cb-488">No haga ningún cambio en la configuración de red dentro del sistema operativo invitado.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-488">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="5b1cb-489">Esto incluye direcciones IP, servidores DNS y subred.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="5b1cb-490">Ajuste toda la configuración de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="5b1cb-491">El servicio Protocolo de configuración dinámica de host (DHCP) propaga la configuración.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-491">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="5b1cb-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Direcciones IP de DNS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="5b1cb-493">Para configurar las direcciones IP de DNS que se requieren, realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-493">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="5b1cb-494">En Azure Portal, en la hoja **Servidores DNS**, asegúrese de que la opción **Servidores DNS** de la red virtual está establecida en **DNS personalizado**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-494">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="5b1cb-495">Seleccione la configuración según el tipo de red que tiene.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-495">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="5b1cb-496">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-496">For more information, see the following resources:</span></span>
    * <span data-ttu-id="5b1cb-497">[Conectividad de red corporativa (entre locales)][planning-guide-2.2]: agregue las direcciones IP de los servidores DNS locales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="5b1cb-498">Puede extender los servidores DNS locales a las máquinas virtuales que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-498">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="5b1cb-499">En ese escenario, puede agregar las direcciones IP de las máquinas virtuales de Azure en las que ejecuta el servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-499">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="5b1cb-500">[Implementación solo en la nube][planning-guide-2.1]: implemente una máquina virtual adicional en la misma instancia de Virtual Network que actúa como servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="5b1cb-501">Agregue las direcciones IP de las máquinas virtuales de Azure que configuró para ejecutar el servicio DNS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-501">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![Figura 12: Configuración de servidores DNS para Azure Virtual Network][sap-ha-guide-figure-3001]

    <span data-ttu-id="5b1cb-503">_**Figura 12:** Configuración de servidores DNS para Azure Virtual Network_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="5b1cb-504">Si cambia las direcciones IP de los servidores DNS, debe reiniciar las máquinas virtuales de Azure para aplicar el cambio y propagar los nuevos servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-504">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="5b1cb-505">En este ejemplo, el servicio DNS está instalado y configurado en estas máquinas virtuales de Windows:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-505">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="5b1cb-506">Rol de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-506">Virtual machine role</span></span> | <span data-ttu-id="5b1cb-507">Nombre de host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-507">Virtual machine host name</span></span> | <span data-ttu-id="5b1cb-508">Nombre de tarjeta de red</span><span class="sxs-lookup"><span data-stu-id="5b1cb-508">Network card name</span></span> | <span data-ttu-id="5b1cb-509">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="5b1cb-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b1cb-510">Primer servidor DNS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-510">First DNS server</span></span> |<span data-ttu-id="5b1cb-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-511">domcontr-0</span></span> |<span data-ttu-id="5b1cb-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="5b1cb-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="5b1cb-513">10.0.0.10</span></span> |
| <span data-ttu-id="5b1cb-514">Segundo servidor DNS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-514">Second DNS server</span></span> |<span data-ttu-id="5b1cb-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-515">domcontr-1</span></span> |<span data-ttu-id="5b1cb-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="5b1cb-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="5b1cb-517">10.0.0.11</span></span> |

### <span data-ttu-id="5b1cb-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Nombres de host y direcciones IP estáticas para la instancia en clúster de ASCS/SCS de SAP y la instancia de clúster de DBMS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="5b1cb-519">Para la implementación local, necesita estas direcciones IP y nombres de host reservados:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="5b1cb-520">Rol de nombre de host virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-520">Virtual host name role</span></span> | <span data-ttu-id="5b1cb-521">Nombre de host virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-521">Virtual host name</span></span> | <span data-ttu-id="5b1cb-522">Dirección IP estática virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b1cb-523">Primer nombre de host virtual de clúster de ASCS/SCS de SAP (para la administración del clúster)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="5b1cb-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="5b1cb-524">pr1-ascs-vir</span></span> |<span data-ttu-id="5b1cb-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="5b1cb-525">10.0.0.42</span></span> |
| <span data-ttu-id="5b1cb-526">Nombre de host virtual de la instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="5b1cb-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="5b1cb-527">pr1-ascs-sap</span></span> |<span data-ttu-id="5b1cb-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="5b1cb-528">10.0.0.43</span></span> |
| <span data-ttu-id="5b1cb-529">Segundo nombre de host virtual de clúster de DBMS de SAP (administración del clúster)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="5b1cb-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="5b1cb-530">pr1-dbms-vir</span></span> |<span data-ttu-id="5b1cb-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="5b1cb-531">10.0.0.32</span></span> |

<span data-ttu-id="5b1cb-532">Cuando crea el clúster, crea los nombres de host virtual **pr1-ascs-vir** y **pr1-dbms-vir**, además de las direcciones IP asociadas que administrar el clúster mismo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-532">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="5b1cb-533">Para obtener información sobre cómo hacerlo, consulte [Recopilación de nodos del clúster en la configuración de clúster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-533">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="5b1cb-534">Puede crear manualmente los otros 2 nombres de host virtual, **pr1-ascs-sap** y **pr1-dbms-sap**, y las direcciones IP asociadas en el servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-534">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="5b1cb-535">La instancia de ASCS/SCS de SAP en clúster y la instancia de DBMS en clúster usan estos recursos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-535">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="5b1cb-536">Para obtener información sobre cómo hacerlo, consulte [Creación de un nombre de host virtual para la instancia de ASCS/SCS de SAP en clúster][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-536">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="5b1cb-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Configuración de direcciones IP estáticas para las máquinas virtuales SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="5b1cb-538">Después de implementar las máquinas virtuales que usará en el clúster, deberá establecer direcciones IP estáticas para todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-538">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="5b1cb-539">Debe hacerlo en la configuración de Azure Virtual Network y no en el sistema operativo invitado.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-539">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="5b1cb-540">En Azure Portal, seleccione **Grupo de recursos** > **Tarjeta de red** > **Configuración** > **Dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-540">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="5b1cb-541">En la hoja **Direcciones IP**, en **Asignación**, seleccione **Estática**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-541">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="5b1cb-542">En el cuadro **Dirección IP**, escriba la dirección IP que desea usar.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-542">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5b1cb-543">Si cambia la dirección IP de la tarjeta de red, deberá reiniciar las máquinas virtuales de Azure para aplicar el cambio.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-543">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![Figura 13: Establecimiento de direcciones IP estáticas para la tarjeta de red de cada máquina virtual][sap-ha-guide-figure-3002]

  <span data-ttu-id="5b1cb-545">_**Figura 13:** Establecimiento de direcciones IP estáticas para la tarjeta de red de cada máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-545">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="5b1cb-546">Repita este paso para todas las interfaces de red, es decir, para todas las máquinas virtuales, incluidas las que desea usar para Active Directory/servicio DNS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="5b1cb-547">En este ejemplo, aparecen estas máquinas virtuales y direcciones IP estáticas:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="5b1cb-548">Rol de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-548">Virtual machine role</span></span> | <span data-ttu-id="5b1cb-549">Nombre de host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5b1cb-549">Virtual machine host name</span></span> | <span data-ttu-id="5b1cb-550">Nombre de tarjeta de red</span><span class="sxs-lookup"><span data-stu-id="5b1cb-550">Network card name</span></span> | <span data-ttu-id="5b1cb-551">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="5b1cb-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5b1cb-552">Primer servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-552">First SAP Application Server instance</span></span> |<span data-ttu-id="5b1cb-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-553">pr1-di-0</span></span> |<span data-ttu-id="5b1cb-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-554">pr1-nic-di-0</span></span> |<span data-ttu-id="5b1cb-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="5b1cb-555">10.0.0.50</span></span> |
| <span data-ttu-id="5b1cb-556">Segundo servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="5b1cb-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-557">pr1-di-1</span></span> |<span data-ttu-id="5b1cb-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-558">pr1-nic-di-1</span></span> |<span data-ttu-id="5b1cb-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="5b1cb-559">10.0.0.51</span></span> |
| <span data-ttu-id="5b1cb-560">...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-560">...</span></span> |<span data-ttu-id="5b1cb-561">...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-561">...</span></span> |<span data-ttu-id="5b1cb-562">...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-562">...</span></span> |<span data-ttu-id="5b1cb-563">...</span><span class="sxs-lookup"><span data-stu-id="5b1cb-563">...</span></span> |
| <span data-ttu-id="5b1cb-564">Último servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="5b1cb-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="5b1cb-565">pr1-di-5</span></span> |<span data-ttu-id="5b1cb-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="5b1cb-566">pr1-nic-di-5</span></span> |<span data-ttu-id="5b1cb-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="5b1cb-567">10.0.0.55</span></span> |
| <span data-ttu-id="5b1cb-568">Primer nodo de clúster para la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5b1cb-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-569">pr1-ascs-0</span></span> |<span data-ttu-id="5b1cb-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="5b1cb-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="5b1cb-571">10.0.0.40</span></span> |
| <span data-ttu-id="5b1cb-572">Segundo nodo de clúster para la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5b1cb-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-573">pr1-ascs-1</span></span> |<span data-ttu-id="5b1cb-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="5b1cb-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="5b1cb-575">10.0.0.41</span></span> |
| <span data-ttu-id="5b1cb-576">Primer nodo de clúster para la instancia de DBMS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="5b1cb-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-577">pr1-db-0</span></span> |<span data-ttu-id="5b1cb-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="5b1cb-578">pr1-nic-db-0</span></span> |<span data-ttu-id="5b1cb-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="5b1cb-579">10.0.0.30</span></span> |
| <span data-ttu-id="5b1cb-580">Segundo nodo de clúster para la instancia de DBMS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="5b1cb-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-581">pr1-db-1</span></span> |<span data-ttu-id="5b1cb-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="5b1cb-582">pr1-nic-db-1</span></span> |<span data-ttu-id="5b1cb-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="5b1cb-583">10.0.0.31</span></span> |

### <span data-ttu-id="5b1cb-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Configuración de una dirección IP estática para el equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="5b1cb-585">La plantilla de Azure Resource Manager para SAP crea un equilibrador de carga interno de Azure que se usa para el clúster de instancia de ASCS/SCS de SAP y el clúster de DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-585">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b1cb-586">La dirección IP del nombre de host virtual de la instancia de ASCS/SCS de SAP es la misma dirección IP del equilibrador de carga interno de ASCS/SCS de SAP, **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-586">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="5b1cb-587">La dirección IP del nombre virtual de la instancia de DBMS es la misma dirección IP del equilibrador de carga interno de DBMS, **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-587">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="5b1cb-588">Para configurar una dirección IP estática para el equilibrador de carga interno de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-588">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="5b1cb-589">En la implementación inicial se establece la dirección IP del equilibrador de carga interno como **Dinámica**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-589">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="5b1cb-590">En la hoja **Direcciones IP** de Azure Portal, en **Asignación**, seleccione **Estática**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-590">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="5b1cb-591">Establezca la dirección IP del equilibrador de carga interno **pr1-lb-ascs** en la dirección IP del nombre de host virtual de la instancia de ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-591">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="5b1cb-592">Establezca la dirección IP del equilibrador de carga interno **pr1-lb-dbms** en la dirección IP del nombre de host virtual de la instancia de DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-592">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![Figura 14: Establecimiento de direcciones IP estáticas para el equilibrador de carga interno de la instancia de ASCS/SCS de SAP][sap-ha-guide-figure-3003]

  <span data-ttu-id="5b1cb-594">_**Figura 14:** Establecimiento de direcciones IP estáticas para el equilibrador de carga interno de la instancia de ASCS/SCS de SAP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-594">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="5b1cb-595">En este ejemplo, aparecen 2 equilibradores de carga internos de Azure que tienen estas direcciones IP estáticas:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="5b1cb-596">Rol del equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-596">Azure internal load balancer role</span></span> | <span data-ttu-id="5b1cb-597">Nombre del equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-597">Azure internal load balancer name</span></span> | <span data-ttu-id="5b1cb-598">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="5b1cb-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b1cb-599">Equilibrador de carga interno de instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="5b1cb-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5b1cb-600">pr1-lb-ascs</span></span> |<span data-ttu-id="5b1cb-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="5b1cb-601">10.0.0.43</span></span> |
| <span data-ttu-id="5b1cb-602">Equilibrador de carga interno de DBMS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="5b1cb-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="5b1cb-603">pr1-lb-dbms</span></span> |<span data-ttu-id="5b1cb-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="5b1cb-604">10.0.0.33</span></span> |


### <span data-ttu-id="5b1cb-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="5b1cb-606">La plantilla de Azure Resource Manager para SAP crea los puertos que necesita:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-606">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="5b1cb-607">Una instancia de ASCS ABAP con el número de instancia predeterminado **00**</span><span class="sxs-lookup"><span data-stu-id="5b1cb-607">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="5b1cb-608">Una instancia de SCS de Java con el número de instancia predeterminado **01**</span><span class="sxs-lookup"><span data-stu-id="5b1cb-608">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="5b1cb-609">Cuando instala la instancia de ASCS/SCS de SAP, debe usar el número de instancia predeterminado **00** para la instancia de ASCS ABAP y el número de instancia predeterminado **01** para la instancia de SCS de Java.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-609">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="5b1cb-610">Después, cree estos puntos de conexión de equilibrio de carga interno necesarios para los puertos de SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-610">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="5b1cb-611">Para crear estos puntos de conexión de equilibrio de carga interno necesarios, créelos para los puertos de ASCS ABAP de SAP NetWeaver:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-611">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="5b1cb-612">Nombre de regla de equilibrio de carga/servicio</span><span class="sxs-lookup"><span data-stu-id="5b1cb-612">Service/load balancing rule name</span></span> | <span data-ttu-id="5b1cb-613">Números de puerto predeterminados</span><span class="sxs-lookup"><span data-stu-id="5b1cb-613">Default port numbers</span></span> | <span data-ttu-id="5b1cb-614">Puertos concretos para (instancia de ASCS con el número de instancia 00) (ERS con 10)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b1cb-615">Enqueue Server/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="5b1cb-616">32<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-617">3200</span><span class="sxs-lookup"><span data-stu-id="5b1cb-617">3200</span></span> |
| <span data-ttu-id="5b1cb-618">ABAP Message Server/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="5b1cb-619">36<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-620">3600</span><span class="sxs-lookup"><span data-stu-id="5b1cb-620">3600</span></span> |
| <span data-ttu-id="5b1cb-621">Internal ABAP Message/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="5b1cb-622">39<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-623">3900</span><span class="sxs-lookup"><span data-stu-id="5b1cb-623">3900</span></span> |
| <span data-ttu-id="5b1cb-624">Message Server HTTP/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="5b1cb-625">81<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-626">8100</span><span class="sxs-lookup"><span data-stu-id="5b1cb-626">8100</span></span> |
| <span data-ttu-id="5b1cb-627">SAP Start Service ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="5b1cb-628">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="5b1cb-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5b1cb-629">50013</span><span class="sxs-lookup"><span data-stu-id="5b1cb-629">50013</span></span> |
| <span data-ttu-id="5b1cb-630">SAP Start Service ASCS HTTPS/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="5b1cb-631">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="5b1cb-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5b1cb-632">50014</span><span class="sxs-lookup"><span data-stu-id="5b1cb-632">50014</span></span> |
| <span data-ttu-id="5b1cb-633">Enqueue Replication/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="5b1cb-634">5<*NúmeroInstancia*>16</span><span class="sxs-lookup"><span data-stu-id="5b1cb-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="5b1cb-635">50016</span><span class="sxs-lookup"><span data-stu-id="5b1cb-635">50016</span></span> |
| <span data-ttu-id="5b1cb-636">SAP Start Service ERS HTTP/ *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="5b1cb-637">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="5b1cb-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5b1cb-638">51013</span><span class="sxs-lookup"><span data-stu-id="5b1cb-638">51013</span></span> |
| <span data-ttu-id="5b1cb-639">SAP Start Service ERS HTTP/ *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="5b1cb-640">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="5b1cb-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5b1cb-641">51014</span><span class="sxs-lookup"><span data-stu-id="5b1cb-641">51014</span></span> |
| <span data-ttu-id="5b1cb-642">Win RM/ *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="5b1cb-643">5985</span><span class="sxs-lookup"><span data-stu-id="5b1cb-643">5985</span></span> |
| <span data-ttu-id="5b1cb-644">File Share/ *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="5b1cb-645">445</span><span class="sxs-lookup"><span data-stu-id="5b1cb-645">445</span></span> |

<span data-ttu-id="5b1cb-646">_**Tabla 1:** Números de puerto de las instancias de ASCS ABAP de SAP NetWeaver_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-646">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="5b1cb-647">Luego, cree estos puntos de conexión de equilibrio de carga interno para los puertos de SCS de Java de SAP NetWeaver:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-647">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="5b1cb-648">Nombre de regla de equilibrio de carga/servicio</span><span class="sxs-lookup"><span data-stu-id="5b1cb-648">Service/load balancing rule name</span></span> | <span data-ttu-id="5b1cb-649">Números de puerto predeterminados</span><span class="sxs-lookup"><span data-stu-id="5b1cb-649">Default port numbers</span></span> | <span data-ttu-id="5b1cb-650">Puertos concretos para (instancia de SCS con el número de instancia 01) (ERS con 11)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b1cb-651">Enqueue Server/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="5b1cb-652">32<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-653">3201</span><span class="sxs-lookup"><span data-stu-id="5b1cb-653">3201</span></span> |
| <span data-ttu-id="5b1cb-654">Gateway Server/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="5b1cb-655">33<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-656">3301</span><span class="sxs-lookup"><span data-stu-id="5b1cb-656">3301</span></span> |
| <span data-ttu-id="5b1cb-657">Java Message Server/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="5b1cb-658">39<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-659">3901</span><span class="sxs-lookup"><span data-stu-id="5b1cb-659">3901</span></span> |
| <span data-ttu-id="5b1cb-660">Message Server HTTP/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="5b1cb-661">81<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="5b1cb-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="5b1cb-662">8101</span><span class="sxs-lookup"><span data-stu-id="5b1cb-662">8101</span></span> |
| <span data-ttu-id="5b1cb-663">SAP Start Service SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="5b1cb-664">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="5b1cb-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5b1cb-665">50113</span><span class="sxs-lookup"><span data-stu-id="5b1cb-665">50113</span></span> |
| <span data-ttu-id="5b1cb-666">SAP Start Service SCS HTTPS/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="5b1cb-667">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="5b1cb-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5b1cb-668">50114</span><span class="sxs-lookup"><span data-stu-id="5b1cb-668">50114</span></span> |
| <span data-ttu-id="5b1cb-669">Enqueue Replication/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="5b1cb-670">5<*NúmeroInstancia*>16</span><span class="sxs-lookup"><span data-stu-id="5b1cb-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="5b1cb-671">50116</span><span class="sxs-lookup"><span data-stu-id="5b1cb-671">50116</span></span> |
| <span data-ttu-id="5b1cb-672">SAP Start Service ERS HTTP/ *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="5b1cb-673">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="5b1cb-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5b1cb-674">51113</span><span class="sxs-lookup"><span data-stu-id="5b1cb-674">51113</span></span> |
| <span data-ttu-id="5b1cb-675">SAP Start Service ERS HTTPS/ *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="5b1cb-676">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="5b1cb-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5b1cb-677">51114</span><span class="sxs-lookup"><span data-stu-id="5b1cb-677">51114</span></span> |
| <span data-ttu-id="5b1cb-678">Win RM/ *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="5b1cb-679">5985</span><span class="sxs-lookup"><span data-stu-id="5b1cb-679">5985</span></span> |
| <span data-ttu-id="5b1cb-680">File Share/ *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="5b1cb-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="5b1cb-681">445</span><span class="sxs-lookup"><span data-stu-id="5b1cb-681">445</span></span> |

<span data-ttu-id="5b1cb-682">_**Tabla 2:** Números de puerto de las instancias de SCS de Java de SAP NetWeaver_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-682">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: Reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure][sap-ha-guide-figure-3004]

<span data-ttu-id="5b1cb-684">_**Figura 15:** Reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-684">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="5b1cb-685">Establezca la dirección IP del equilibrador de carga **pr1-lb-dbms** en la dirección IP del nombre de host virtual de la instancia de DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-685">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="5b1cb-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Cambio de las reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="5b1cb-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="5b1cb-687">Si desea usar otros números para las instancias de ASCS o SCS de SAP, debe actualizar los nombres y valores de sus puertos a partir de los predeterminados.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-687">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="5b1cb-688">En Azure Portal, seleccione **<*SID*>-lb-ascs load balancer** > **Reglas de equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-688">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="5b1cb-689">Cambie estos valores para todas las reglas de equilibrio de carga que pertenezcan a la instancia de ASCS o SCS de SAP:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-689">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="5b1cb-690">Nombre</span><span class="sxs-lookup"><span data-stu-id="5b1cb-690">Name</span></span>
  * <span data-ttu-id="5b1cb-691">Port</span><span class="sxs-lookup"><span data-stu-id="5b1cb-691">Port</span></span>
  * <span data-ttu-id="5b1cb-692">Puerto de back-end</span><span class="sxs-lookup"><span data-stu-id="5b1cb-692">Back-end port</span></span>

  <span data-ttu-id="5b1cb-693">Por ejemplo, si desea cambiar el número de instancia de ASCS predeterminado de 00 a 31, debe hacer cambios en todos los puertos que aparecen en la tabla 1.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-693">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="5b1cb-694">A continuación, se muestra un ejemplo de una actualización para el puerto *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Cambio de las reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure][sap-ha-guide-figure-3005]

  <span data-ttu-id="5b1cb-696">_**Figura 16:** Cambio de las reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-696">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="5b1cb-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Incorporación de máquinas virtuales de Windows al dominio</span><span class="sxs-lookup"><span data-stu-id="5b1cb-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="5b1cb-698">Después de asignar una dirección IP estática a las máquinas virtuales, agregue las máquinas virtuales al dominio.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-698">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Figura 17: Incorporación de una máquina virtual a un dominio][sap-ha-guide-figure-3006]

<span data-ttu-id="5b1cb-700">_**Figura 17:** Incorporación de una máquina virtual a un dominio_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-700">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="5b1cb-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Incorporación de entradas del Registro en ambos nodos del clúster usados para la instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="5b1cb-702">Azure Load Balancer tiene un equilibrador de carga interno que cierra las conexiones cuando están inactivas durante un período establecido (tiempo de espera de inactividad).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-702">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="5b1cb-703">Los proceso de trabajo de SAP en instancias de diálogo abren conexiones con el proceso de puesta en cola de SAP tan pronto como se deba enviar la primera solicitud para poner en cola y para quitar de la cola.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-703">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="5b1cb-704">Estas conexiones suelen mantenerse hasta que el proceso de trabajo o el de puesta en cola se reinicia.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-704">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="5b1cb-705">Sin embargo, si la conexión está inactiva durante un periodo, el equilibrador de carga interno de Azure cierra la conexión.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-705">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="5b1cb-706">Esto no supone un problema, porque el proceso de trabajo de SAP restablece la conexión con el proceso de puesta en cola si ya no existe.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-706">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="5b1cb-707">Estas actividades se documentan en los seguimientos de desarrollador de los procesos de SAP, pero crean una gran cantidad de contenido adicional en esos seguimientos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-707">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="5b1cb-708">Se recomienda cambiar los parámetros de TCP/IP `KeepAliveTime` y `KeepAliveInterval` en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-708">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="5b1cb-709">Combine estos cambios en los parámetros de TCP/IP con los parámetros de perfil de SAP, lo que se describe más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-709">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="5b1cb-710">Para agregar entradas de registro en los dos nodos de clúster de la instancia de ASCS/SCS de SAP, en primer lugar, agregue estas entradas del registro de Windows en ambos nodos de clúster de Windows para ASCS/SCS de SAP:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-710">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="5b1cb-711">path</span><span class="sxs-lookup"><span data-stu-id="5b1cb-711">Path</span></span> | <span data-ttu-id="5b1cb-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="5b1cb-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="5b1cb-713">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="5b1cb-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="5b1cb-714">Tipo de variable</span><span class="sxs-lookup"><span data-stu-id="5b1cb-714">Variable type</span></span> |<span data-ttu-id="5b1cb-715">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="5b1cb-716">Valor</span><span class="sxs-lookup"><span data-stu-id="5b1cb-716">Value</span></span> |<span data-ttu-id="5b1cb-717">120000</span><span class="sxs-lookup"><span data-stu-id="5b1cb-717">120000</span></span> |
| <span data-ttu-id="5b1cb-718">Vínculo a la documentación</span><span class="sxs-lookup"><span data-stu-id="5b1cb-718">Link to documentation</span></span> |[<span data-ttu-id="5b1cb-719">https://technet.microsoft.com/es-es/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="5b1cb-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="5b1cb-720">_**Tabla 3:** Cambio del primer parámetro de TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-720">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="5b1cb-721">Luego, agregue estas entradas del Registro de Windows en los nodos de clúster de Windows para ASCS/SCS de SAP:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="5b1cb-722">path</span><span class="sxs-lookup"><span data-stu-id="5b1cb-722">Path</span></span> | <span data-ttu-id="5b1cb-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="5b1cb-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="5b1cb-724">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="5b1cb-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="5b1cb-725">Tipo de variable</span><span class="sxs-lookup"><span data-stu-id="5b1cb-725">Variable type</span></span> |<span data-ttu-id="5b1cb-726">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="5b1cb-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="5b1cb-727">Valor</span><span class="sxs-lookup"><span data-stu-id="5b1cb-727">Value</span></span> |<span data-ttu-id="5b1cb-728">120000</span><span class="sxs-lookup"><span data-stu-id="5b1cb-728">120000</span></span> |
| <span data-ttu-id="5b1cb-729">Vínculo a la documentación</span><span class="sxs-lookup"><span data-stu-id="5b1cb-729">Link to documentation</span></span> |[<span data-ttu-id="5b1cb-730">https://technet.microsoft.com/es-es/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="5b1cb-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="5b1cb-731">_**Tabla 4:** Cambio del segundo parámetro de TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-731">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="5b1cb-732">**Para aplicar los cambios, reinicie ambos nodos del clúster**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-732">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="5b1cb-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configuración del clúster de Clústeres de conmutación por error de Windows para la instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="5b1cb-734">Para configurar el clúster de Clústeres de conmutación por error de Windows para la instancia de ASCS/SCS de SAP, hay que realizar estas tareas:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="5b1cb-735">Recopilación de nodos del clúster en la configuración de clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-735">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="5b1cb-736">Configuración de un testigo de recurso compartido de archivos de clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="5b1cb-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Recopilación de nodos del clúster en la configuración de clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="5b1cb-738">En el Asistente para Agregar roles y características, agregue a ambos nodos del clúster agrupaciones en clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-738">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="5b1cb-739">Configure el clúster de conmutación por error mediante el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-739">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="5b1cb-740">En el Administrador de clústeres de conmutación por error, seleccione **Crear clúster** y, luego, agregue solo el nombre del primer clúster, el nodo A. No agregue el segundo nodo aún, ya que lo agregará en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-740">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![Figura 18: Incorporación del nombre de servidor o máquina virtual del primer nodo del clúster][sap-ha-guide-figure-3007]

  <span data-ttu-id="5b1cb-742">_**Figura 18:** Incorporación del nombre de servidor o máquina virtual del primer nodo del clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-742">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="5b1cb-743">Escriba el nombre de red (nombre de host virtual) del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-743">Enter the network name (virtual host name) of the cluster.</span></span>

  ![Figura 19: Escriba el nombre del clúster][sap-ha-guide-figure-3008]

  <span data-ttu-id="5b1cb-745">_**Figura 19:** Escriba el nombre del clúster._</span><span class="sxs-lookup"><span data-stu-id="5b1cb-745">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="5b1cb-746">Una vez creado el clúster, ejecute una prueba de validación del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-746">After you've created the cluster, run a cluster validation test.</span></span>

  ![Figura 20: Ejecución de la comprobación de validación del clúster][sap-ha-guide-figure-3009]

  <span data-ttu-id="5b1cb-748">_**Figura 20:** Ejecución de la comprobación de validación del clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-748">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="5b1cb-749">En este punto del proceso, puede omitir cualquier advertencia sobre los discos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-749">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="5b1cb-750">Agregará un testigo de recurso de archivos y los discos compartidos de SIOS más tarde.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-750">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="5b1cb-751">En esta fase, no es necesario preocuparse por el cuórum.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-751">At this stage, you don't need to worry about having a quorum.</span></span>

  ![Figura 21: No se encuentra disco de cuórum][sap-ha-guide-figure-3010]

  <span data-ttu-id="5b1cb-753">_**Figura 21:** No se encuentra disco de cuórum_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: El recurso de clúster principal necesita una dirección IP nueva][sap-ha-guide-figure-3011]

  <span data-ttu-id="5b1cb-755">_**Figura 22:** El recurso de clúster principal necesita una dirección IP nueva_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="5b1cb-756">Cambie la dirección IP del servicio de clúster principal.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-756">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="5b1cb-757">El clúster no se puede iniciar hasta que no cambie la dirección IP del servicio de clúster principal, porque la dirección IP del servidor apunta a uno de los nodos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-757">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="5b1cb-758">Para ello, vaya a la página **Propiedad** del recurso de dirección IP del servicio de clúster principal.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-758">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="5b1cb-759">Por ejemplo, necesitamos asignar una dirección IP (**10.0.0.42** en el ejemplo) para el nombre de host virtual del clúster **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-759">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figura 23: En el cuadro de diálogo Propiedades, cambie la dirección IP.][sap-ha-guide-figure-3012]

  <span data-ttu-id="5b1cb-761">_**Figura 23:** En el cuadro de diálogo **Propiedades**, cambie la dirección IP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-761">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![Figura 24: Asignación de la dirección IP reservada para el clúster][sap-ha-guide-figure-3013]

  <span data-ttu-id="5b1cb-763">_**Figura 24:** Asignación de la dirección IP reservada para el clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-763">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="5b1cb-764">Escriba el nombre del host virtual del clúster en línea.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-764">Bring the cluster virtual host name online.</span></span>

  ![Figura 25: El servicio principal del clúster está activo, en ejecución y tiene la dirección IP correcta][sap-ha-guide-figure-3014]

  <span data-ttu-id="5b1cb-766">_**Figura 25:** El servicio principal del clúster está activo, en ejecución y tiene la dirección IP correcta_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-766">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="5b1cb-767">Agregue el segundo nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-767">Add the second cluster node.</span></span>

  <span data-ttu-id="5b1cb-768">Ahora que el servicio de clúster principal está en funcionamiento, puede agregar el segundo nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-768">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![Figura 26: Incorporación del segundo nodo del clúster][sap-ha-guide-figure-3015]

  <span data-ttu-id="5b1cb-770">_**Figura 26:** Incorporación del segundo nodo del clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-770">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="5b1cb-771">Escriba un nombre para el segundo host del nodo de clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-771">Enter a name for the second cluster node host.</span></span>

  ![Figura 27: Escriba el segundo nombre de host del nodo de clúster.][sap-ha-guide-figure-3016]

  <span data-ttu-id="5b1cb-773">_**Figura 27:** Escriba el segundo nombre de host del nodo de clúster._</span><span class="sxs-lookup"><span data-stu-id="5b1cb-773">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5b1cb-774">Asegúrese de que la casilla **Agregar todo el almacenamiento apto al clúster** **NO** esté activada.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-774">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: No active la casilla][sap-ha-guide-figure-3017]

  <span data-ttu-id="5b1cb-776">_**Figura 28:** **NO** active la casilla_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-776">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="5b1cb-777">Puede pasar por alto las advertencias sobre el cuórum y los discos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="5b1cb-778">Establecerá el cuórum y compartirá el disco más adelante, tal como se describe en [Instalación de SIOS DataKeeper Cluster Edition para un disco compartido de clúster de ASCS/SCS de SAP][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-778">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Omisión de las advertencias sobre el cuórum de disco][sap-ha-guide-figure-3018]

  <span data-ttu-id="5b1cb-780">_**Figura 29:** Omisión de las advertencias sobre el cuórum de disco_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-780">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="5b1cb-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configuración de un testigo de recurso compartido de archivos de clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="5b1cb-782">Para configurar un testigo de recurso compartido de archivos de clúster, hay que realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="5b1cb-783">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-783">Creating a file share</span></span>
- <span data-ttu-id="5b1cb-784">Configuración del cuórum de testigo del recurso compartido de archivos en el Administrador de clústeres de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="5b1cb-784">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="5b1cb-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="5b1cb-786">Seleccione un testigo de recurso de archivos en lugar de un disco de cuórum.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="5b1cb-787">SIOS DataKeeper admite esta opción.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="5b1cb-788">En los ejemplos de este artículo, el testigo de recurso compartido de archivos se encuentra en la instancia de Active Directory/el servidor DNS que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-788">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="5b1cb-789">El testigo de recurso compartido de archivos se llama **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-789">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="5b1cb-790">Dado que habría configurado una conexión de VPN con Azure (a través de VPN de sitio a sitio o Azure ExpressRoute), su instancia de Active Directory/servidor DNS es local y no es apta para ejecutar un testigo de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-790">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5b1cb-791">Si la instancia de Active Directory/el servidor DNS solo se ejecuta localmente, no configure el testigo de recurso compartido de archivos en la instancia de Active Directory/sistema operativo Windows de DNS que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="5b1cb-792">La latencia de red entre los nodos de clúster que se ejecutan en Azure y Active Directory/DNS local puede ser demasiado grande y provocar problemas de conectividad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="5b1cb-793">Asegúrese de configurar el testigo de recurso compartido de archivos en una máquina virtual de Azure que se ejecuta cerca del nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-793">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="5b1cb-794">La unidad de cuórum necesita, como mínimo, 1024 MB de espacio disponible.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-794">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="5b1cb-795">Se recomienda 2048 MB de espacio disponible en la unidad de cuórum.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-795">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="5b1cb-796">Agregue el objeto de nombre de clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-796">Add the cluster name object.</span></span>

  ![Figura 30: Asignación de los permisos en el recurso compartido para el objeto de nombre de clúster][sap-ha-guide-figure-3019]

  <span data-ttu-id="5b1cb-798">_**Figura 30:** Asignación de los permisos en el recurso compartido para el objeto de nombre de clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-798">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="5b1cb-799">Asegúrese de que los permisos incluyan la autoridad para cambiar datos en el recurso compartido para el objeto de nombre de clúster (**pr1-ascs-vir$** en el ejemplo).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-799">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="5b1cb-800">Para agregar el objeto de nombre de clúster a la lista, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-800">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="5b1cb-801">Cambie el filtro para buscar objetos de equipo, además de los que aparecen en la figura 31.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-801">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![Figura 31: Cambio del tipo de objeto para incluir los objetos de equipo][sap-ha-guide-figure-3020]

  <span data-ttu-id="5b1cb-803">_**Figura 31:** Cambio del tipo de objeto para incluir los equipos_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-803">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![Figura 32: Activación de la casilla Equipos][sap-ha-guide-figure-3021]

  <span data-ttu-id="5b1cb-805">_**Figura 32:** Active la casilla **Equipos**_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-805">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="5b1cb-806">Escriba el objeto de nombre de clúster, como aparece en la figura 31.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-806">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="5b1cb-807">Como ya se creó el registro, puede cambiar los permisos, tal como aparece en la figura 30.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-807">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="5b1cb-808">Seleccione la pestaña **Seguridad** del recurso compartido y, luego, establezca permisos más detallados para el objeto de nombre de clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-808">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![Figura 33: Establecimiento de los atributos de seguridad para el objeto de nombre de clúster en el cuórum de recurso compartido de archivos][sap-ha-guide-figure-3022]

  <span data-ttu-id="5b1cb-810">_**Figura 33:** Establecimiento de los atributos de seguridad para el objeto de nombre de clúster en el cuórum de recurso compartido de archivos_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-810">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="5b1cb-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Configuración del cuórum de testigo del recurso compartido de archivos en el Administrador de clústeres de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="5b1cb-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="5b1cb-812">Abra el Asistente para la configuración de cuórum.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-812">Open the Configure Quorum Setting Wizard.</span></span>

  ![Figura 34: Inicio del Asistente para configurar cuórum de clúster][sap-ha-guide-figure-3023]

  <span data-ttu-id="5b1cb-814">_**Figura 34:** Inicio del Asistente para configurar cuórum de clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-814">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="5b1cb-815">En la página **Seleccionar opción de configuración de cuórum**, seleccione **Seleccionar el testigo de cuórum**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-815">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![Figura 35: Configuraciones de cuórum que puede elegir][sap-ha-guide-figure-3024]

  <span data-ttu-id="5b1cb-817">_**Figura 35:** Configuraciones de cuórum que puede elegir_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="5b1cb-818">En la página **Seleccionar testigo de cuórum**, elija **Configurar un testigo de recurso compartido de archivos**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-818">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figura 36: Selección del testigo de recurso compartido de archivos][sap-ha-guide-figure-3025]

  <span data-ttu-id="5b1cb-820">_**Figura 36:** Selección del testigo de recurso compartido de archivos_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-820">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="5b1cb-821">Escriba la ruta de acceso UNC al recurso compartido de archivos (\\domcontr-0\FSW en el ejemplo).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-821">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="5b1cb-822">Seleccione **Siguiente** para ver una lista de los cambios que puede hacer.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-822">To see a list of the changes you can make, select **Next**.</span></span>

  ![Figura 37: Definición de la ubicación del recurso compartido de archivos para el recurso compartido testigo][sap-ha-guide-figure-3026]

  <span data-ttu-id="5b1cb-824">_**Figura 37:** Definición de la ubicación del recurso compartido de archivos para el recurso compartido testigo_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-824">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="5b1cb-825">Seleccione los cambios que desee y, luego, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-825">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="5b1cb-826">En este último paso, necesita volver a configurar correctamente el clúster, tal como aparece en la figura 38.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-826">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![Figura 38: Confirmación de que volvió a configurar el clúster][sap-ha-guide-figure-3027]

  <span data-ttu-id="5b1cb-828">_**Figura 38:** Confirmación de que volvió a configurar el clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-828">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="5b1cb-829">Después de instalar correctamente el clúster de conmutación por error de Windows, se deben realizar cambios en algunos umbrales para adaptar la detección de conmutación por error a las condiciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-829">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="5b1cb-830">Los parámetros que se van a cambiar se documentan en este blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-830">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="5b1cb-831">Suponiendo que las dos máquinas virtuales que compilación la configuración de clúster de Windows para ASCS/SCS están en la misma subred, los parámetros siguientes deben cambiarse a estos valores:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-831">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="5b1cb-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="5b1cb-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="5b1cb-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="5b1cb-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="5b1cb-834">Esta configuración se ha probado con los clientes y proporciona un buen compromiso para que, por un lado, sea lo suficientemente resistente.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-834">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="5b1cb-835">Por otro lado, dicha configuración proporciona una conmutación por error lo suficientemente rápida en condiciones de error real en caso de error de máquinas virtuales o nodos, o de software SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-835">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="5b1cb-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Instalación de SIOS DataKeeper Cluster Edition para un disco compartido de clúster de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="5b1cb-837">Ahora tiene una configuración de Clústeres de conmutación por error de Windows Server activa en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="5b1cb-838">Pero, para instalar una instancia de ASCS/SCS de SAP, necesita un recurso de disco compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-838">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="5b1cb-839">No puede crear los recursos de disco compartido que necesita en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-839">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="5b1cb-840">SIOS DataKeeper Cluster Edition es una solución de terceros que puede usar para crear recursos de disco compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="5b1cb-841">Para instalar SIOS DataKeeper Cluster Edition en un disco compartido de clúster de ASCS/SCS de SAP, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-841">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="5b1cb-842">Incorporación de .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="5b1cb-842">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="5b1cb-843">Instalación de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5b1cb-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="5b1cb-844">Configuración de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5b1cb-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="5b1cb-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Incorporación de la característica .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="5b1cb-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="5b1cb-846">Microsoft .NET Framework 3.5 no está activo ni instalado automáticamente en Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-846">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="5b1cb-847">Dado que SIOS DataKeeper requiere .NET Framework como en todos los nodos donde se instala DataKeeper, debe instalar .NET Framework 3.5 en el sistema operativo invitado de todas las máquinas virtuales del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-847">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="5b1cb-848">Hay dos maneras de agregar .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-848">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="5b1cb-849">Use el Asistente para agregar roles y características en Windows, que se muestra en la figura 39.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-849">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Instalación de .NET Framework 3.5 por medio del Asistente para agregar roles y características][sap-ha-guide-figure-3028]

  <span data-ttu-id="5b1cb-851">_**Figura 39:** Instalación de .NET Framework 3.5 por medio del Asistente para agregar roles y características_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-851">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![Figura 40: Barra de progreso de instalación cuando instala .NET Framework 3.5 por medio del Asistente para agregar roles y características][sap-ha-guide-figure-3029]

  <span data-ttu-id="5b1cb-853">_**Figura 40**: Barra de progreso de instalación cuando instala .NET Framework 3.5 por medio del Asistente para agregar roles y características_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-853">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="5b1cb-854">Utilice la herramienta de línea de comandos dism.exe.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-854">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="5b1cb-855">Para este tipo de instalación, necesita tener acceso al directorio SxS en los medios de instalación de Windows.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-855">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="5b1cb-856">En un símbolo del sistema con privilegios elevados, escriba:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="5b1cb-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Instalación de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5b1cb-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="5b1cb-858">Instale SIOS DataKeeper Cluster Edition en cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-858">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="5b1cb-859">Con SIOS DataKeeper, para crear el almacenamiento compartido virtual, cree un reflejo sincronizado y, luego, simule el almacenamiento compartido de clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-859">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="5b1cb-860">Antes de instalar el software SIOS, cree el usuario de dominio **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-860">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-861">Agregue el usuario **DataKeeperSvc** al grupo de **administradores locales** en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-861">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="5b1cb-862">Para instalar SIOS DataKeeper, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-862">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="5b1cb-863">Instale el software SIOS en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-863">Install the SIOS software on both cluster nodes.</span></span>

  ![Instalador de SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Primera página de la instalación de SIOS DataKeeper][sap-ha-guide-figure-3031]

  <span data-ttu-id="5b1cb-866">_**Figura 41:** Primera página de la instalación de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-866">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="5b1cb-867">En el cuadro de diálogo que aparece en la figura 42, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-867">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: DataKeeper le informa que se deshabilitará un servicio][sap-ha-guide-figure-3032]

  <span data-ttu-id="5b1cb-869">_**Figura 42:** DataKeeper le informa que se deshabilitará un servicio_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="5b1cb-870">En el cuadro de diálogo que aparece en la figura 43, se recomienda seleccionar **Cuenta de dominio o de servidor**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-870">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Selección del usuario para SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="5b1cb-872">_**Figura 43:** Selección del usuario para SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="5b1cb-873">Escriba el nombre de usuario y contraseñas de cuenta de dominio que creó para SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-873">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Ingreso del nombre de usuario y contraseña de dominio para la instalación de SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="5b1cb-875">_**Figura 44:** Ingreso del nombre de usuario y contraseña de dominio para la instalación de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-875">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="5b1cb-876">Instale la clave de licencia para la instancia de SIOS DataKeeper, tal como aparece en la figura 45.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-876">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: Ingreso de la licencia de SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="5b1cb-878">_**Figura 45:** Especificación de la licencia de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="5b1cb-879">Cuando se le solicite, reinicie la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-879">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="5b1cb-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configuración de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5b1cb-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="5b1cb-881">Después de instalar SIOS DataKeeper en ambos nodos, debe iniciar la configuración.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-881">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="5b1cb-882">El objetivo de la configuración es conseguir la replicación sincrónica de datos entre los VHD adicionales conectados a cada una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-882">The goal of the configuration is to have synchronous data replication between the additional VHDs attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="5b1cb-883">Inicie la herramienta de configuración y administración de DataKeeper y, luego, seleccione **Servidor de conexión**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-883">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="5b1cb-884">(En la figura 46, esta opción aparece rodeada de un círculo de color rojo).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Herramienta de configuración y administración de SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="5b1cb-886">_**Figura 46:** Herramienta de configuración y administración de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="5b1cb-887">Escriba el nombre o la dirección TCP/IP del primer nodo al que se debe conectar la herramienta de configuración y administración y, en un segundo paso, el segundo nodo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-887">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![Figura 47: Inserción del nombre o la dirección TCP/IP del primer nodo al que se debe conectar la herramienta de configuración y administración y, en un segundo paso, el segundo nodo][sap-ha-guide-figure-3037]

  <span data-ttu-id="5b1cb-889">_**Figura 47:** Inserción del nombre o la dirección TCP/IP del primer nodo al que se debe conectar la herramienta de configuración y administración y, en un segundo paso, el segundo nodo_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-889">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="5b1cb-890">Cree el trabajo de replicación entre los dos nodos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-890">Create the replication job between the two nodes.</span></span>

  ![Figura 48: Creación de un trabajo de replicación][sap-ha-guide-figure-3038]

  <span data-ttu-id="5b1cb-892">_**Figura 48:** Creación de un trabajo de replicación_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="5b1cb-893">Un asistente le guía por el proceso de crear un trabajo de replicación.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-893">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="5b1cb-894">Defina el nombre, la dirección TCP/IP y el volumen de disco del nodo de origen.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-894">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![Figura 49: Definición del nombre del trabajo de replicación][sap-ha-guide-figure-3039]

  <span data-ttu-id="5b1cb-896">_**Figura 49:** Definición del nombre del trabajo de replicación_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-896">_**Figure 49:** Define the name of the replication job_</span></span>

  ![Figura 50: Definición de los datos básicos para el nodo que debe ser el nodo de origen actual][sap-ha-guide-figure-3040]

  <span data-ttu-id="5b1cb-898">_**Figura 50:** Definición de los datos básicos para el nodo que debe ser el nodo de origen actual_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-898">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="5b1cb-899">Defina el nombre, la dirección TCP/IP y el volumen de disco del nodo de destino.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-899">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![Figura 51: Definición de los datos básicos para el nodo que debe ser el nodo de destino actual][sap-ha-guide-figure-3041]

  <span data-ttu-id="5b1cb-901">_**Figura 51:** Definición de los datos básicos para el nodo que debe ser el nodo de destino actual_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-901">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="5b1cb-902">Defina los algoritmos de compresión.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-902">Define the compression algorithms.</span></span> <span data-ttu-id="5b1cb-903">En el ejemplo, se recomienda comprimir el flujo de replicación.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-903">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="5b1cb-904">Especialmente en situaciones de resincronización, la compresión del flujo de replicación reduce considerablemente el tiempo que se tarda en resincronizar.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-904">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="5b1cb-905">Tenga en cuenta que la compresión usa los recursos de CPU y RAM de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-905">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="5b1cb-906">A medida que aumenta la tasa de compresión, también aumenta el volumen de los recursos de CPU usados.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-906">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="5b1cb-907">También puede ajustar esta configuración más adelante.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="5b1cb-908">Otra configuración que debe comprobar es si la replicación se ejecuta de forma sincrónica o asincrónica.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-908">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="5b1cb-909">*Cuando proteja las configuraciones de ASCS/SCS de SAP, debe usar la replicación sincrónica*.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definición de los detalles de la replicación][sap-ha-guide-figure-3042]

  <span data-ttu-id="5b1cb-911">_**Figura 52:** Definición de los detalles de la replicación_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="5b1cb-912">Defina si el volumen que el trabajo de replicación replica se debe representar en una configuración de clúster de Clústeres de conmutación por error de Windows Server como disco compartido.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-912">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="5b1cb-913">Para la configuración de ASCS/SCS de SAP, seleccione **Sí** de manera que el clúster de Windows vea el volumen replicado como un disco compartido que puede usar como volumen de clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-913">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: Selección de Sí para establecer el volumen replicado como volumen de clúster][sap-ha-guide-figure-3043]

  <span data-ttu-id="5b1cb-915">_**Figura 53:** Selección de **Sí** para establecer el volumen replicado como volumen de clúster_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-915">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="5b1cb-916">Una vez creado el volumen, la herramienta de configuración y administración de DataKeeper muestra que el trabajo de replicación está activo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-916">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![Figura 54: El reflejo sincrónico de DataKeeper para el disco compartido de ASCS/SCS de SAP está activo][sap-ha-guide-figure-3044]

  <span data-ttu-id="5b1cb-918">_**Figura 54:** El reflejo sincrónico de DataKeeper para el disco compartido de ASCS/SCS de SAP está activo_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-918">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="5b1cb-919">Ahora, el Administrador de clústeres de conmutación por error muestra el disco como un disco de DataKeeper, tal como aparece en la figura 55.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-919">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: El Administrador de clústeres de conmutación por error muestra el disco que DataKeeper replicó][sap-ha-guide-figure-3045]

  <span data-ttu-id="5b1cb-921">_**Figura 55:** El Administrador de clústeres de conmutación por error muestra el disco que DataKeeper replicó_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-921">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="5b1cb-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Instalación del sistema SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="5b1cb-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="5b1cb-923">No se describirá la configuración de DBMS, porque las configuraciones varían en función del sistema de DBMS que usa.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-923">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="5b1cb-924">Sin embargo, se da por supuesto que las inquietudes respecto de la alta disponibilidad con DBMS se abordan con las funcionalidades que admiten los diversos proveedores de DBMS para Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-924">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="5b1cb-925">Por ejemplo, AlwaysOn o creación de reflejo de la base de datos para SQL Server y Oracle Data Guard para Oracle.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="5b1cb-926">En el escenario de este artículo, no se agregó más protección a DBMS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-926">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="5b1cb-927">No hay ninguna consideración especial cuando distintos servicios de DBMS interactúan con esta variante de configuración de ASCS/SCS de SAP en clúster en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-928">Los procedimientos de instalación de sistemas ABAP de SAP NetWeaver, sistemas Java y sistemas ABAP+Java son casi idénticos.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-928">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="5b1cb-929">La diferencia más significativa es que un sistema ABAP de SAP tiene una instancia de ASCS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-929">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="5b1cb-930">El sistema Java de SAP tiene una instancia de SCS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-930">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="5b1cb-931">El sistema ABAP+Java de SAP tiene una instancia de ASCS y una instancia de SCS en ejecución en el mismo grupo de clústeres de conmutación por error de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-931">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="5b1cb-932">Cualquier diferencia de instalación de cada pila de instalación de SAP NetWeaver se menciona explícitamente.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="5b1cb-933">Puede asumir que todos los demás componentes son iguales.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-933">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="5b1cb-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Instalación de SAP con una instancia de ASCS/SCS de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="5b1cb-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b1cb-935">Asegúrese de no colocar el archivo de paginación en los volúmenes reflejados de DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-935">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="5b1cb-936">DataKeeper no admite los volúmenes reflejados.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="5b1cb-937">Puede dejar el archivo de paginación en la unidad temporal D de una máquina virtual de Azure, que es la opción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-937">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="5b1cb-938">Si todavía no se encuentra ahí, mueva el archivo de paginación de Windows a la unidad D de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-938">If it's not already there, move the Windows page file to drive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="5b1cb-939">Para instalar SAP con una instancia de ASCS/SCS de alta disponibilidad, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="5b1cb-940">Creación de un nombre de host virtual para la instancia de ASCS/SCS de SAP en clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-940">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="5b1cb-941">Instalación del primer nodo de clúster de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-941">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="5b1cb-942">Modificación del perfil SAP de la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-942">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="5b1cb-943">Incorporación de un puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="5b1cb-943">Adding a probe port</span></span>
- <span data-ttu-id="5b1cb-944">Apertura del puerto de sondeo de Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="5b1cb-944">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="5b1cb-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Creación de un nombre de host virtual para la instancia de ASCS/SCS de SAP en clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="5b1cb-946">En el Administrador de DNS de Windows, cree una entrada de DNS para el nombre de host virtual de la instancia de ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-946">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5b1cb-947">La dirección IP que asigna al nombre de host virtual de la instancia de ASCS/SCS debe ser la misma dirección IP que asignó a Azure Load Balancer (**<*SID*>-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-947">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="5b1cb-948">La dirección IP del nombre de host de ASCS/SCS de SAP virtual (**pr1-ascs-sap**) es la misma dirección IP de Azure Load Balancer (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-948">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definición de la entrada DNS del nombre virtual del clúster de ASCS/SCS de SAP y la dirección TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="5b1cb-950">_**Figura 56:** Definición de la entrada DNS del nombre virtual del clúster de ASCS/SCS de SAP y la dirección TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-950">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="5b1cb-951">Para definir la dirección IP asignada al nombre de host virtual, seleccione **Administrador de DNS** > **Dominio**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-951">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Nuevo nombre virtual y dirección TCP/IP para la configuración del clúster de ASCS/SCS de SAP][sap-ha-guide-figure-3047]

  <span data-ttu-id="5b1cb-953">_**Figura 57:** Nuevo nombre virtual y dirección TCP/IP para la configuración del clúster de ASCS/SCS de SAP_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="5b1cb-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Instalación del primer nodo de clúster de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="5b1cb-955">Ejecute la opción de primer nodo del clúster en el nodo de clúster A, por ejemplo, en el host **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-955">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="5b1cb-956">Para mantener los puertos predeterminados para el equilibrador de carga interno de Azure, seleccione:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-956">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="5b1cb-957">**Sistema ABAP**: número de instancia de **ASCS** **00**</span><span class="sxs-lookup"><span data-stu-id="5b1cb-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="5b1cb-958">**Sistema Java**: número de instancia de **SCS** **01**</span><span class="sxs-lookup"><span data-stu-id="5b1cb-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="5b1cb-959">**Sistema ABAP+Java**: número de instancia de **ASCS** **00** y número de instancia de **SCS** **01**</span><span class="sxs-lookup"><span data-stu-id="5b1cb-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="5b1cb-960">Para usar números de instancia diferentes de 00 para la instancia de ASCS de ABAP y 01 para la instancia de SCS de Java, primero debe cambiar las reglas predeterminadas de equilibrio de carga del equilibrador de carga interno de Azure, tal como se describe en [Cambio de las reglas predeterminadas de equilibrio de carga de ASCS/SCS para el equilibrador de carga interno de Azure][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-960">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="5b1cb-961">Luego, realice unos pasos que no se describen en la documentación de instalación usual de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-961">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-962">La documentación de instalación de SAP describe cómo instalar el primer nodo de clúster de ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-962">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="5b1cb-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modificación del perfil SAP de la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="5b1cb-964">Debe agregar un nuevo parámetro de perfil.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-964">You need to add a new profile parameter.</span></span> <span data-ttu-id="5b1cb-965">El parámetro de perfil evita el cierre de las conexiones entre los procesos de trabajo de SAP y el servidor de puesta en cola cuando lleven inactivas demasiado tiempo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-965">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="5b1cb-966">Mencionamos el escenario del problema en [Incorporación de entradas del Registro en ambos nodos del clúster usados para la instancia de ASCS/SCS de SAP][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="5b1cb-966">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="5b1cb-967">En esa sección, también se presentan 2 cambios para algunos parámetros básicos de la conexión TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-967">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="5b1cb-968">En el segundo paso, es necesario configurar el servidor de puesta en cola para enviar una señal `keep_alive` de forma que las conexiones no alcancen el umbral de inactividad del equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-968">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="5b1cb-969">Para modificar el perfil SAP de la instancia de ASCS/SCS, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-969">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="5b1cb-970">Agregue este parámetro de perfil al perfil de la instancia de ASCS/SCS de SAP:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-970">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="5b1cb-971">En este ejemplo, la ruta de acceso es:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-971">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="5b1cb-972">Por ejemplo, al perfil de la instancia de SCS de SAP y la ruta de acceso correspondiente:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-972">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="5b1cb-973">Para aplicar los cambios, reinicie la instancia de ASCS/SCS de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-973">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="5b1cb-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Incorporación de un puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="5b1cb-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="5b1cb-975">Use la funcionalidad de sondeo del equilibrador de carga interno para que toda la configuración del clúster funcione con Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-975">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="5b1cb-976">Habitualmente, el equilibrador de carga interno de Azure distribuye la carga de trabajo entrante de manera equitativa entre las máquinas virtuales que participan.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-976">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="5b1cb-977">Sin embargo, esto no funcionará en algunas configuraciones de clúster porque solo hay una instancia activa.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="5b1cb-978">La otra instancia es pasiva y no puede aceptar nada de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-978">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="5b1cb-979">Una funcionalidad de sondeo resulta útil cuando el equilibrador de carga interno de Azure asigna trabajo solo a una instancia activa.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-979">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="5b1cb-980">Con la funcionalidad de sondeo, el equilibrador de carga interno puede detectar cuáles son las instancias activas y, luego, orientarse solo a la instancia con la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-980">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="5b1cb-981">Para agregar un puerto de sondeo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-981">To add a probe port:</span></span>

1.  <span data-ttu-id="5b1cb-982">Primero, compruebe la configuración de **ProbePort** actual con este comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-982">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="5b1cb-983">Ejecútelo dentro de una de las máquinas virtuales de la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-983">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="5b1cb-984">Defina un puerto de sondeo.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-984">Define a probe port.</span></span> <span data-ttu-id="5b1cb-985">El número de puerto de sondeo predeterminado es **0**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-985">The default probe port number is **0**.</span></span> <span data-ttu-id="5b1cb-986">En el ejemplo, se usa el puerto de sondeo **62000**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-986">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: De manera predeterminada, el puerto de sondeo de configuración de clúster es 0][sap-ha-guide-figure-3048]

  <span data-ttu-id="5b1cb-988">_**Figura 58:** El puerto de sondeo de configuración de clúster es 0_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-988">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="5b1cb-989">El número de puerto está definido en las plantillas de Azure Resource Manager para SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-989">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="5b1cb-990">Puede asignar el número de puerto en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-990">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="5b1cb-991">Para establecer un nuevo valor de ProbePort del recurso de clúster **SAP <*SID*> IP**, ejecute el siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-991">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="5b1cb-992">Actualice las variables de PowerShell de su entorno.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-992">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="5b1cb-993">Después de ejecutar el script, se le pedirá que reinicie el grupo de clústeres de SAP para activar los cambios.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-993">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="5b1cb-994">Después de conectar el rol de clúster **SAP <*SID*>**, compruebe que **ProbePort** esté establecido en el nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-994">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Sondeo del puerto de clúster después de establecer el valor nuevo][sap-ha-guide-figure-3049]

  <span data-ttu-id="5b1cb-996">_**Figura 59:** Sondeo del puerto de clúster después de establecer el valor nuevo_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-996">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="5b1cb-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Apertura del puerto de sondeo de Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="5b1cb-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="5b1cb-998">Debe abrir el puerto de sondeo de firewall de Windows en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-998">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="5b1cb-999">El siguiente script permite abrir un puerto de sondeo de firewall de Windows.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-999">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="5b1cb-1000">Actualice las variables de PowerShell de su entorno.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1000">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="5b1cb-1001">El valor **ProbePort** está establecido en **62000**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1001">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="5b1cb-1002">Ahora puede tener acceso al recurso compartido de archivos **\\\ascsha-clsap\sapmnt** desde otros hosts, como **ascsha-dbas**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1002">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="5b1cb-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Instalación de la instancia de base de datos</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="5b1cb-1004">Para instalar la instancia de base de datos, siga el proceso que se describe en la documentación de instalación de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1004">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="5b1cb-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Instalación del segundo nodo del clúster</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="5b1cb-1006">Para instalar el segundo clúster, siga los pasos que aparecen en la guía de instalación de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1006">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="5b1cb-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Cambio del tipo de inicio del servicio de Windows para la instancia de ERS de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="5b1cb-1008">Cambie el tipo de inicio del servicio o servicios de Windows de ERS de SAP a **Automático (inicio retrasado)** en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1008">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Cambio del tipo de servicio de la instancia de ERS de SAP a automático retrasado][sap-ha-guide-figure-3050]

<span data-ttu-id="5b1cb-1010">_**Figura 60:** Cambio del tipo de servicio de la instancia de ERS de SAP a automático retrasado_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1010">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="5b1cb-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Instalación del servidor de aplicaciones principal de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="5b1cb-1012">Instale la instancia del servidor de aplicaciones principal (PAS) <*SID*>-di-0 en la máquina virtual que designó para hospedar el PAS.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1012">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="5b1cb-1013">No hay ninguna dependencia de Azure ni aspectos específicos de DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="5b1cb-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Instalación del servidor de aplicaciones adicional de SAP</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="5b1cb-1015">Instale un servidor de aplicaciones adicional (AAS) de SAP en todas las máquinas virtuales que designó para hospedar una instancia de servidores de aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1015">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="5b1cb-1016">Por ejemplo, en <*SID*>-di-1 a <*SID*>-di-&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1016">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1cb-1017">Esta acción finaliza la instalación de un sistema SAP NetWeaver de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1017">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="5b1cb-1018">Después, continúe con las pruebas de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="5b1cb-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Prueba de la conmutación por error de la instancia de ASCS/SCS de SAP y de la replicación de SIOS</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="5b1cb-1020">Es fácil probar y supervisar la conmutación por error de la instancia de ASCS/SCS de SAP y la replicación de disco de SIOS mediante el uso del Administrador de clústeres de conmutación por error, la interfaz de usuario de SIOS DataKeeper y la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1020">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="5b1cb-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> La instancia de ASCS/SCS de SAP se ejecuta en el nodo de clúster A</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="5b1cb-1022">El grupo de clústeres **SAP PR1** se ejecuta en el nodo de clúster A. Por ejemplo, en **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1022">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="5b1cb-1023">Asigne la unidad de disco compartido S, que forma parte del grupo de clústeres **SAP PR1** y que la instancia de ASCS/SCS usa, al nodo de clúster A.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1023">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![Figura 61: Administrador de clústeres de conmutación por error (el grupo de clústeres <SID> de SAP se ejecuta en el nodo del clúster A)][sap-ha-guide-figure-5000]

<span data-ttu-id="5b1cb-1025">_**Figura 61:** Administrador de clústeres de conmutación por error: el grupo de clústeres <*SID*> de SAP se ejecuta en el nodo del clúster A_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1025">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="5b1cb-1026">En la interfaz de usuario de SIOS DataKeeper y la herramienta de configuración, puede ver que los datos del disco compartido se replican sincrónicamente desde la unidad de volumen de origen S en el nodo de clúster A. Por ejemplo, de **pr1-ascs-0 [10.0.0.40]** a **pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1026">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: En SIOS DataKeeper, replique el volumen local desde el nodo de clústeres A al nodo de clústeres B][sap-ha-guide-figure-5001]

<span data-ttu-id="5b1cb-1028">_**Figura 62:** En SIOS DataKeeper, replique el volumen local desde el nodo de clústeres A al nodo de clústeres B_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1028">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="5b1cb-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Conmutación por error del nodo A al nodo B</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="5b1cb-1030">Elija una de estas opciones para iniciar una conmutación por error del grupo de clústeres <*SID*> de SAP desde el nodo del clúster A al nodo del clúster B:</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1030">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="5b1cb-1031">Uso del Administrador de clústeres de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="5b1cb-1032">Uso de PowerShell del clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="5b1cb-1033">Reinicie el nodo del clúster A dentro del sistema operativo invitado Windows (inicia una conmutación por error automática del grupo de clústeres <*SID*> de SAP desde el nodo A al nodo B).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1033">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="5b1cb-1034">Reinicie el nodo del clúster A desde Azure Portal (inicia una conmutación por error automática del grupo de clústeres <*SID*> de SAP desde el nodo A al nodo B).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1034">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="5b1cb-1035">Reinicie el nodo del clúster A con Azure PowerShell (inicia una conmutación por error automática del grupo de clústeres de SAP <*SID*> desde el nodo A al nodo B).</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="5b1cb-1036">Después de la conmutación por error, el grupo de clústeres <*SID*> de SAP se ejecuta en el nodo del clúster B. Por ejemplo, en **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1036">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: En el Administrador de clústeres de conmutación por error, el grupo de clústeres <SID> de SAP se ejecuta en el nodo del clúster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="5b1cb-1038">_**Figura 63:** En el Administrador de clústeres de conmutación por error, el grupo de clústeres <*SID*> de SAP se ejecuta en el nodo del clúster B_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1038">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="5b1cb-1039">Ahora, el disco compartido ahora está montado en el nodo del clúster B. SIOS DataKeeper replica datos desde la unidad de volumen de origen S en el nodo del clúster B a la unidad de volumen de destino S en el nodo del clúster A. Por ejemplo, de **pr1-ascs-1 [10.0.0.41]** a **pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1039">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: SIOS DataKeeper replica el volumen local desde el nodo del clúster B al nodo del clúster A][sap-ha-guide-figure-5003]

  <span data-ttu-id="5b1cb-1041">_**Figura 64:** SIOS DataKeeper replica el volumen local desde el nodo del clúster B al nodo del clúster A_</span><span class="sxs-lookup"><span data-stu-id="5b1cb-1041">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
