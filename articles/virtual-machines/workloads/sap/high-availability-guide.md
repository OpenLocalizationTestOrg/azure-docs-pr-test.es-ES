---
title: "Máquinas virtuales de alta disponibilidad para SAP NetWeaver aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="39a27-103">Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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


<span data-ttu-id="39a27-109">Máquinas virtuales de Azure es la solución de Hola para organizaciones que necesitan cálculo, almacenamiento y recursos de red, en un tiempo mínimo y sin ciclos de adquisición prolongados.</span><span class="sxs-lookup"><span data-stu-id="39a27-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="39a27-110">Puede usar máquinas virtuales de Azure toodeploy aplicaciones clásicas como ABAP basadas en SAP NetWeaver, Java y una pila ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="39a27-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="39a27-111">Amplíe la confiabilidad y disponibilidad sin recursos locales adicionales.</span><span class="sxs-lookup"><span data-stu-id="39a27-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="39a27-112">Azure Virtual Machines admite la conectividad entre locales, así que podrá integrar Azure Virtual Machines a los dominios locales, las nubes privadas y la infraestructura de sistema SAP de la organización.</span><span class="sxs-lookup"><span data-stu-id="39a27-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="39a27-113">En este artículo, se incluyen los pasos de Hola que debe seguir toodeploy sistemas SAP de alta disponibilidad en Azure utilizando el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39a27-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="39a27-114">Le guiaremos por estas tareas principales:</span><span class="sxs-lookup"><span data-stu-id="39a27-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="39a27-115">Buscar Hola derecho guías de instalación y las notas de SAP, aparecen en hello [recursos] [ sap-ha-guide-2] sección.</span><span class="sxs-lookup"><span data-stu-id="39a27-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="39a27-116">En este artículo complementa la documentación de la instalación de SAP y las notas de SAP, que son recursos principales de Hola que pueden ayudarle a instalar e implementar el software SAP en plataformas específicas.</span><span class="sxs-lookup"><span data-stu-id="39a27-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="39a27-117">Obtenga información acerca de las diferencias de hello entre modelo de implementación de Azure Resource Manager Hola y Hola implementación clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="39a27-118">Obtenga información acerca de los modos de quórum de clúster de conmutación por error de Windows Server, por lo que puede seleccionar el modelo de Hola que es adecuado para la implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="39a27-119">Obtener información sobre el almacenamiento compartido de Clústeres de conmutación por error de Windows Server en los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="39a27-120">Obtenga información acerca de cómo proteger los componentes de único punto de error como SAP Central servicios (ASCS) de Advanced Business aplicación Programming (ABAP) toohelp / Services Central (SCS) de SAP y sistemas de administración de bases de datos (DBMS) y componentes redundantes, como SAP Servidor de aplicaciones, en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="39a27-121">Seguir un ejemplo detallado de la instalación y configuración de un sistema SAP de alta disponibilidad en un clúster de Clústeres de conmutación por error de Windows Server mediante Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39a27-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="39a27-122">Obtenga información acerca de los clústeres de conmutación por error del servidor de Windows en Azure de toouse requiere pasos adicionales, pero que no son necesarios en una implementación local.</span><span class="sxs-lookup"><span data-stu-id="39a27-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="39a27-123">implementación de toosimplify y la configuración, en este artículo, usamos Hola plantillas del Administrador de recursos de alta disponibilidad de tres niveles SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="39a27-124">plantillas de Hello automatizan la implementación de hello toda la infraestructura que necesite para un sistema SAP de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="39a27-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="39a27-125">infraestructura Hola también admite el ajuste de tamaño de SAP aplicación rendimiento estándar (SAPS) del sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="39a27-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="39a27-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="39a27-127">Antes de empezar, asegúrese de que se cumplen los requisitos previos de Hola que se describen en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="39a27-128">Además, puede toocheck seguro de que todos los recursos enumerados en hello [recursos] [ sap-ha-guide-2] sección.</span><span class="sxs-lookup"><span data-stu-id="39a27-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="39a27-129">En este artículo usamos las plantillas de Azure Resource Manager para [SAP NetWeaver de tres niveles](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="39a27-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="39a27-130">Consulte [Plantillas de Azure Resource Manager para SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/) para ver información general útil sobre las plantillas.</span><span class="sxs-lookup"><span data-stu-id="39a27-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="39a27-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Recursos</span><span class="sxs-lookup"><span data-stu-id="39a27-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="39a27-132">Estos artículos también se refieren a las implementaciones de SAP en Azure:</span><span class="sxs-lookup"><span data-stu-id="39a27-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="39a27-133">[Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="39a27-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="39a27-134">[Implementación de Azure Virtual Machines para SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="39a27-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="39a27-135">[Implementación de DBMS de Azure Virtual Machines para SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="39a27-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="39a27-136">[Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver (esta guía)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="39a27-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-137">Siempre que sea posible, le ofrecemos un toohello de vínculo que hace referencia la Guía de instalación de SAP (consulte hello [guías de instalación de SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="39a27-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="39a27-138">Los requisitos previos y obtener información sobre el proceso de instalación de hello, que una instalación de SAP NetWeaver buena idea tooread Hola guía cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="39a27-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="39a27-139">En este artículo solo se abarcan tareas específicas para los sistemas basados en SAP NetWeaver que puede usar con Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="39a27-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="39a27-140">Estas notas de SAP están relacionadas toohello tema de SAP en Azure:</span><span class="sxs-lookup"><span data-stu-id="39a27-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="39a27-141">Número de nota</span><span class="sxs-lookup"><span data-stu-id="39a27-141">Note number</span></span> | <span data-ttu-id="39a27-142">Título</span><span class="sxs-lookup"><span data-stu-id="39a27-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="39a27-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="39a27-143">[1928533]</span></span> |<span data-ttu-id="39a27-144">SAP Applications on Azure: Supported Products and Sizing (Aplicaciones SAP en Azure: productos y tamaños compatibles)</span><span class="sxs-lookup"><span data-stu-id="39a27-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="39a27-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="39a27-145">[2015553]</span></span> |<span data-ttu-id="39a27-146">SAP on Microsoft Azure: Support Prerequisites (SAP en Microsoft Azure: requisitos previos de compatibilidad)</span><span class="sxs-lookup"><span data-stu-id="39a27-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="39a27-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="39a27-147">[1999351]</span></span> |<span data-ttu-id="39a27-148">Enhanced Azure Monitoring for SAP (Supervisión mejorada de Azure para SAP)</span><span class="sxs-lookup"><span data-stu-id="39a27-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="39a27-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="39a27-149">[2178632]</span></span> |<span data-ttu-id="39a27-150">Key Monitoring Metrics for SAP on Microsoft Azure (Métricas de supervisión clave para SAP en Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="39a27-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="39a27-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="39a27-151">[1999351]</span></span> |<span data-ttu-id="39a27-152">Virtualization on Windows: Enhanced Monitoring (Virtualización en Windows: supervisión mejorada)</span><span class="sxs-lookup"><span data-stu-id="39a27-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="39a27-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="39a27-153">[2243692]</span></span> |<span data-ttu-id="39a27-154">Uso de almacenamiento SSD premium de Azure para la instancia DBMS de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="39a27-155">Obtener más información sobre hello [limitaciones de las suscripciones de Azure][azure-subscription-service-limits-subscription], incluidas las limitaciones de general predeterminado y máximo.</span><span class="sxs-lookup"><span data-stu-id="39a27-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="39a27-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de alta disponibilidad con Azure Resource Manager frente a modelo de implementación clásica Azure Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="39a27-157">Hola, Administrador de recursos de Azure y modelos de implementación clásico de Azure son diferentes en hello siguientes áreas:</span><span class="sxs-lookup"><span data-stu-id="39a27-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="39a27-158">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="39a27-158">Resource groups</span></span>
- <span data-ttu-id="39a27-159">Azure interno cargar la dependencia de equilibrador de grupo de recursos de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="39a27-160">Soporte técnico para el escenario de varios SID de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="39a27-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="39a27-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="39a27-162">En el Administrador de recursos de Azure, puede usar toomanage de grupos de recursos todos los recursos de la aplicación hello en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="39a27-163">Un enfoque integrado en un grupo de recursos, todos los recursos se Hola mismo ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="39a27-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="39a27-164">Por ejemplo, todos los recursos se crean en hello mismo tiempo y se eliminan al Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="39a27-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="39a27-165">Más información sobre los [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="39a27-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="39a27-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno cargar la dependencia de equilibrador de grupo de recursos de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="39a27-167">En el modelo de implementación clásica Azure hello, hay una dependencia entre el grupo de servicio de nube de Hola y de equilibrador de carga interno de Azure de hello (servicio del equilibrador de carga de Azure).</span><span class="sxs-lookup"><span data-stu-id="39a27-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="39a27-168">Cada equilibrador de carga interno necesita un grupo de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="39a27-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="39a27-169">En el Administrador de recursos de Azure, no es necesario un toouse de grupo de recursos de Azure equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="39a27-170">entorno de Hello es más sencillo y flexible.</span><span class="sxs-lookup"><span data-stu-id="39a27-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="39a27-171">Soporte técnico para el escenario de varios SID de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="39a27-172">En Azure Resource Manager, puede instalar varias instancias de ASCS/SCS de identificador de sistema SAP (SID) en un clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="39a27-173">Esto es posible gracias a la compatibilidad con las distintas direcciones IP de cada equilibrador de carga interno de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="39a27-174">toouse Hola modelo de implementación clásico de Azure, siga los procedimientos de hello descritos en [SAP NetWeaver en Azure: instancias de clústeres de SAP ASCS/SCS mediante el uso de clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="39a27-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39a27-175">Se recomienda encarecidamente que utilice el modelo de implementación de hello Azure Resource Manager para las instalaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="39a27-176">Ofrece numerosas ventajas que no están disponibles en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="39a27-177">Obtenga más información sobre los [modelos de implementación de Azure][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="39a27-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="39a27-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Clústeres de conmutación por error de Windows Server</span><span class="sxs-lookup"><span data-stu-id="39a27-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="39a27-179">Clústeres de conmutación por error de Windows Server es el fundamento de Hola de una instalación de SAP ASCS/SCS de alta disponibilidad y DBMS en Windows.</span><span class="sxs-lookup"><span data-stu-id="39a27-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="39a27-180">Un clúster de conmutación por error es un grupo de 1 + n servidores independientes (nodos) que funcionan conjuntamente disponibilidad de hello tooincrease de aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="39a27-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="39a27-181">Si se produce un error en un nodo, clústeres de conmutación por error de Windows Server calcula el número de Hola de errores que pueden producirse al mantener un buen estado tooprovide aplicaciones y servicios de clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="39a27-182">Puede elegir entre diferentes quórum modos tooachieve conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="39a27-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="39a27-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modos de cuórum</span><span class="sxs-lookup"><span data-stu-id="39a27-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="39a27-184">Puede elegir entre cuatro modos de cuórum cuando use Clústeres de conmutación por error de Windows Server:</span><span class="sxs-lookup"><span data-stu-id="39a27-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="39a27-185">**Mayoría de nodo**.</span><span class="sxs-lookup"><span data-stu-id="39a27-185">**Node Majority**.</span></span> <span data-ttu-id="39a27-186">Cada nodo del clúster de Hola puede votar.</span><span class="sxs-lookup"><span data-stu-id="39a27-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="39a27-187">Hola clúster solo funciona con una mayoría de votos, es decir, con más de la mitad de los votos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="39a27-188">Se recomienda esta opción para los clústeres con un número impar de nodos.</span><span class="sxs-lookup"><span data-stu-id="39a27-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="39a27-189">Por ejemplo, pueden producir un error en tres nodos en un clúster de siete nodos e imágenes fijas de clúster de hello logra una mayoría y continúa toorun.</span><span class="sxs-lookup"><span data-stu-id="39a27-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="39a27-190">**Mayoría de disco y nodo**.</span><span class="sxs-lookup"><span data-stu-id="39a27-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="39a27-191">Todos los nodos y un disco designado (un testigo de disco) en el almacenamiento de clúster de hello pueden votar cuando estén disponibles y en la comunicación.</span><span class="sxs-lookup"><span data-stu-id="39a27-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="39a27-192">Hola clúster solo funciona con una mayoría de hello votos, es decir, con más de la mitad de los votos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="39a27-193">Este modo resulta útil en un entorno de clúster con un número par de nodos.</span><span class="sxs-lookup"><span data-stu-id="39a27-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="39a27-194">Si nodos mitad hello y disco Hola estén en línea, clúster de hello permanece en un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="39a27-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="39a27-195">**Mayoría de recurso compartido de archivos y nodo**.</span><span class="sxs-lookup"><span data-stu-id="39a27-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="39a27-196">Cada nodo más crea un recurso compartido de archivo designado (un testigo de recurso compartido de archivos) que Hola administrador puede votar, independientemente de si están disponibles para los nodos de Hola y recurso compartido de archivos y en la comunicación.</span><span class="sxs-lookup"><span data-stu-id="39a27-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="39a27-197">Hola clúster solo funciona con una mayoría de hello votos, es decir, con más de la mitad de los votos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="39a27-198">Este modo resulta útil en un entorno de clúster con un número par de nodos.</span><span class="sxs-lookup"><span data-stu-id="39a27-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="39a27-199">Es similar toohello nodo y el modo de mayoría de disco, pero usa un recurso compartido de archivos de testigo en lugar de un disco testigo.</span><span class="sxs-lookup"><span data-stu-id="39a27-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="39a27-200">Este modo es fácil tooimplement, pero si el recurso compartido de archivos de hello sí mismo no es de alta disponibilidad, es posible que un único punto de error.</span><span class="sxs-lookup"><span data-stu-id="39a27-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="39a27-201">**Sin mayoría: solo disco**.</span><span class="sxs-lookup"><span data-stu-id="39a27-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="39a27-202">clúster de Hello tiene un quórum si un nodo está disponible y en la comunicación con un disco concreto hello en almacenamiento de clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="39a27-203">Sólo los nodos Hola que también están en comunicación con ese disco pueden unirse a clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="39a27-204">No se recomienda usar este modo.</span><span class="sxs-lookup"><span data-stu-id="39a27-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="39a27-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Clústeres de conmutación por error de Windows Server local</span><span class="sxs-lookup"><span data-stu-id="39a27-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="39a27-206">En la figura 1 se muestra un clúster de dos nodos.</span><span class="sxs-lookup"><span data-stu-id="39a27-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="39a27-207">Si hello se produce un error en la conexión de red entre los nodos de Hola y ambos nodos se mantienen actualizados y en ejecución, un recurso compartido de archivo o el disco de quórum determina qué nodo continuará servicios y aplicaciones del clúster de tooprovide Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="39a27-208">nodo de Hola que tiene el disco de quórum de toohello de acceso o recurso compartido de archivo es Hola que garantiza que los servicios continúen.</span><span class="sxs-lookup"><span data-stu-id="39a27-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="39a27-209">Dado que este ejemplo utiliza un clúster de dos nodos, utilizamos Hola nodo y modo de quórum de mayoría de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="39a27-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="39a27-210">Hola nodo y mayoría de disco también es una opción válida.</span><span class="sxs-lookup"><span data-stu-id="39a27-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="39a27-211">En un entorno de producción, se recomienda usar un disco de cuórum.</span><span class="sxs-lookup"><span data-stu-id="39a27-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="39a27-212">Puede utilizar toomake de tecnología de sistema de almacenamiento y de red está altamente disponible.</span><span class="sxs-lookup"><span data-stu-id="39a27-212">You can use network and storage system technology toomake it highly available.</span></span>

![Figura 1: Ejemplo de una configuración de Clústeres de conmutación por error de Windows Server para ASCS/SCS de SAP en Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="39a27-214">_**Figura 1:** Ejemplo de una configuración de Clústeres de conmutación por error de Windows Server para ASCS/SCS de SAP en Azure_</span><span class="sxs-lookup"><span data-stu-id="39a27-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="39a27-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Almacenamiento compartido</span><span class="sxs-lookup"><span data-stu-id="39a27-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="39a27-216">En la figura 1 también se muestra un clúster de almacenamiento compartido de dos nodos.</span><span class="sxs-lookup"><span data-stu-id="39a27-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="39a27-217">En un clúster de almacenamiento compartido local, todos los nodos de clúster de hello detectan almacenamiento compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="39a27-218">Un mecanismo de bloqueo protege los datos de hello frente a daños.</span><span class="sxs-lookup"><span data-stu-id="39a27-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="39a27-219">Todos los nodos pueden detectar si se produce un error en otro nodo.</span><span class="sxs-lookup"><span data-stu-id="39a27-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="39a27-220">Si se produce un error en un nodo, los nodos restantes Hola toma posesión de recursos de almacenamiento de Hola y garantiza la disponibilidad de hello de servicios.</span><span class="sxs-lookup"><span data-stu-id="39a27-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-221">No necesita discos compartidos para obtener alta disponibilidad con algunas aplicaciones de DBMS, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39a27-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="39a27-222">SQL Server Always On replica los archivos de datos y de registro DBMS desde el disco local de hello un nodo toohello local del disco de clúster de otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="39a27-223">En ese caso, la configuración de clúster de Windows hello no necesita un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="39a27-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Redes y resolución de nombres</span><span class="sxs-lookup"><span data-stu-id="39a27-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="39a27-225">Los equipos cliente comunicarse con clúster Hola mediante una dirección IP virtual y un nombre de host virtual que Hola proporciona el servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="39a27-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="39a27-226">Hola nodos locales y de servidor DNS de hello puede administrar varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="39a27-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="39a27-227">En una configuración típica, puede usar dos o más conexiones de red:</span><span class="sxs-lookup"><span data-stu-id="39a27-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="39a27-228">Un almacenamiento de información de conexión dedicada toohello</span><span class="sxs-lookup"><span data-stu-id="39a27-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="39a27-229">Una conexión de red interna del clúster para el latido de Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="39a27-230">Una red pública que los clientes usan tooconnect toohello clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="39a27-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Clústeres de conmutación de Windows Server en Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="39a27-232">En comparación con las implementaciones de nube privada o metal toobare, máquinas virtuales de Azure requiere tooconfigure pasos adicionales clústeres de conmutación por error de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="39a27-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="39a27-233">Cuando se compila un disco de clúster compartido, debe tooset nombres de varias direcciones IP y el host virtual para la instancia de SAP ASCS/SCS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="39a27-234">En este artículo se tratan los conceptos clave y Hola pasos adicionales necesarios toobuild un clúster de alta disponibilidad de servicios centrales de SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="39a27-235">Le mostramos cómo tooset una herramienta de terceros de hello SIOS DataKeeper y cómo tooconfigure hello Azure interno equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="39a27-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="39a27-236">Puede usar estos toocreate herramientas un clúster de conmutación por error de Windows con un testigo de recurso compartido de archivos en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: Configuración de Clústeres de conmutación por error de Windows Server en Azure sin un disco compartido][sap-ha-guide-figure-1001]

<span data-ttu-id="39a27-238">_**Figura 2:** Configuración de Clústeres de conmutación por error de Windows Server en Azure sin un disco compartido_</span><span class="sxs-lookup"><span data-stu-id="39a27-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="39a27-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco compartido en Azure con SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="39a27-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="39a27-240">Se necesita almacenamiento compartido de clúster para una instancia de ASCS/SCS de SAP de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="39a27-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="39a27-241">Como de septiembre de 2016, Azure no ofrece almacenamiento compartido puede usar toocreate un clúster de almacenamiento compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="39a27-242">Puede utilizar software de terceros SIOS DataKeeper Cluster Edition toocreate un almacenamiento de reflejo que simula el almacenamiento compartido de clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="39a27-243">Hola solución SIOS proporciona replicación sincrónica de datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="39a27-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="39a27-244">Este es el procedimiento para crear un recurso de disco compartido para un clúster:</span><span class="sxs-lookup"><span data-stu-id="39a27-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="39a27-245">Adjuntar un tooeach adicionales Azure disco duro virtual (VHD) de hello las máquinas virtuales (VM) en una configuración de clúster de Windows.</span><span class="sxs-lookup"><span data-stu-id="39a27-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="39a27-246">Ejecute SIOS DataKeeper Cluster Edition en ambos nodos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="39a27-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="39a27-247">Configurar SIOS DataKeeper Cluster Edition de modo que refleje el contenido de Hola de volumen de disco duro virtual conectado adicional de Hola desde Hola máquina virtual toohello adicionales VHD adjuntada volumen de origen de máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="39a27-248">SIOS DataKeeper abstrae volúmenes locales de origen y de destino de Hola y a continuación, presenta tooWindows agrupación en clústeres de conmutación por error de servidor como un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="39a27-249">Obtenga más información sobre [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="39a27-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: Configuración de Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="39a27-251">_**Figura 3:** Configuración de Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-252">No necesita discos compartidos para obtener alta disponibilidad con algunos productos de DBMS, como SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39a27-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="39a27-253">SQL Server Always On replica los archivos de datos y de registro DBMS desde el disco local de hello un nodo toohello local del disco de clúster de otro nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="39a27-254">En este caso, la configuración de clúster de Windows hello no necesita un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="39a27-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Resolución de nombres en Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="39a27-256">plataforma de nube de Azure de Hello no ofrecen Hola opción tooconfigure direcciones IP virtuales, como las direcciones IP flotantes.</span><span class="sxs-lookup"><span data-stu-id="39a27-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="39a27-257">Es necesario un tooset de solución alternativa de un virtual tooreach Hola clúster recurso de dirección IP en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="39a27-258">Azure tiene un equilibrador de carga interno en hello servicio del equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="39a27-259">Con el equilibrador de carga interno de hello, los clientes tener acceso a clúster de Hola a través de la dirección IP virtual del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="39a27-260">Necesita el equilibrador de carga interno de toodeploy Hola Hola grupo de recursos que contiene los nodos del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="39a27-261">A continuación, configure todas las reglas de reenvío con el sondeo de Hola puertos del equilibrador de carga interno de Hola de puerto es necesario.</span><span class="sxs-lookup"><span data-stu-id="39a27-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="39a27-262">Hola clientes pueden conectarse a través del nombre de host virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="39a27-263">el servidor DNS de Hello resuelve la dirección IP del clúster hello y puerto de identificadores del equilibrador de carga interno de hello toohello nodo activo del clúster de Hola de reenvío.</span><span class="sxs-lookup"><span data-stu-id="39a27-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="39a27-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Alta disponibilidad de SAP NetWeaver en infraestructura como servicio (IaaS) de Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="39a27-265">tooachieve SAP de alta disponibilidad de aplicaciones, como para los componentes de software SAP, necesita hello tooprotect los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="39a27-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="39a27-266">Instancia de servidores de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-266">SAP Application Server instance</span></span>
* <span data-ttu-id="39a27-267">instancia de SAP ASCS/SCS,</span><span class="sxs-lookup"><span data-stu-id="39a27-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="39a27-268">servidor DBMS</span><span class="sxs-lookup"><span data-stu-id="39a27-268">DBMS server</span></span>

<span data-ttu-id="39a27-269">Para obtener más información sobre cómo proteger los componentes SAP en escenarios de alta disponibilidad, consulte [Planeamiento e implementación de Azure Virtual Machines para SAP NetWeaver](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="39a27-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="39a27-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Alta disponibilidad en los servidores de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="39a27-271">Normalmente, no necesita una solución de alta disponibilidad específica para las instancias de servidor de aplicaciones de SAP y cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="39a27-272">Obtiene alta disponibilidad mediante redundancia y configurará varias instancias de diálogo en distintas instancias de Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="39a27-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="39a27-273">Debe tener, como mínimo, 2 instancias de aplicaciones de SAP instaladas en 2 instancias de Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="39a27-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Alta disponibilidad en los servidores de aplicaciones de SAP][sap-ha-guide-figure-2000]

<span data-ttu-id="39a27-275">_**Figura 4**: Alta disponibilidad en los servidores de aplicaciones de SAP_</span><span class="sxs-lookup"><span data-stu-id="39a27-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="39a27-276">Debe colocar todas las máquinas virtuales que instancias de servidor de aplicaciones de SAP de host en Hola mismo conjunto de disponibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="39a27-277">Un conjunto de disponibilidad de Azure garantiza lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="39a27-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="39a27-278">Todas las máquinas virtuales forman parte del programa Hola mismo dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="39a27-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="39a27-279">Un dominio de actualización, por ejemplo, se asegura de que no se actualizan las máquinas virtuales hello en hello vez durante el tiempo de inactividad de mantenimiento planeado.</span><span class="sxs-lookup"><span data-stu-id="39a27-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="39a27-280">Todas las máquinas virtuales forman parte del programa Hola mismo dominio de error.</span><span class="sxs-lookup"><span data-stu-id="39a27-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="39a27-281">Un dominio de error, por ejemplo, se asegura que las máquinas virtuales se implementan para que ningún punto único de error afecta a la disponibilidad de Hola de todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="39a27-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="39a27-282">Más información acerca de cómo demasiado[administrar Hola disponibilidad de máquinas virtuales][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="39a27-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="39a27-283">Dado que hello cuenta de almacenamiento de Azure es un posible punto de error único, es importante toohave al menos dos cuentas de almacenamiento de Azure, en el que se distribuyen al menos dos máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="39a27-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="39a27-284">En una configuración ideal, discos de Hola de cada máquina virtual que está ejecutando una instancia del cuadro de diálogo SAP se implementaría en una cuenta de almacenamiento diferente.</span><span class="sxs-lookup"><span data-stu-id="39a27-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="39a27-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instancia de ASCS/SCS de SAP de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="39a27-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="39a27-286">La figura 5 es un ejemplo de una instancia de ASCS/SCS de SAP de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="39a27-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: Instancia de ASCS/SCS de SAP de alta disponibilidad][sap-ha-guide-figure-2001]

<span data-ttu-id="39a27-288">_**Figura 5:** Instancia de ASCS/SCS de SAP de alta disponibilidad_</span><span class="sxs-lookup"><span data-stu-id="39a27-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="39a27-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Alta disponibilidad de instancia de ASCS/SCS de SAP con Clústeres de conmutación por error de Windows Server en Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="39a27-290">En comparación con las implementaciones de nube privada o metal toobare, máquinas virtuales de Azure requiere tooconfigure pasos adicionales clústeres de conmutación por error de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="39a27-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="39a27-291">toobuild un clúster de conmutación por error de Windows, necesita un disco de clúster compartido, varias direcciones IP, varios nombres de host virtual y un equilibrador de carga interno de Azure para una instancia de SAP ASCS/SCS de agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="39a27-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="39a27-292">Esto se describe con más detalle más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-292">We discuss this in more detail later in hello article.</span></span>

![Figura 6: Clústeres de conmutación por error de Windows Server para una configuración de ASCS/SCS de SAP en Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="39a27-294">_**Figura 6:** Clústeres de conmutación por error de Windows Server para una configuración de ASCS/SCS de SAP en Azure con SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="39a27-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Alta disponibilidad para la instancia de DBMS</span><span class="sxs-lookup"><span data-stu-id="39a27-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="39a27-296">Hola DBMS es también un único punto de contacto en un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="39a27-297">Necesita tooprotect mediante una solución de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="39a27-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="39a27-298">La figura 7 muestra una solución de alta disponibilidad AlwaysOn de SQL Server en Azure, con clústeres de conmutación por error de Windows Server y hello Azure interno equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="39a27-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="39a27-299">SQL Server AlwaysOn replica los archivos de datos y de registro de DBMS con su propia replicación DBMS.</span><span class="sxs-lookup"><span data-stu-id="39a27-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="39a27-300">En este caso, no necesita agrupar discos compartidos, lo que simplifica el programa de instalación completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Figura 7: Ejemplo de DBMS de SAP de alta disponibilidad (SQL Server AlwaysOn)][sap-ha-guide-figure-2003]

<span data-ttu-id="39a27-302">_**Figura 7:** Ejemplo de DBMS de SAP de alta disponibilidad (SQL Server AlwaysOn)_</span><span class="sxs-lookup"><span data-stu-id="39a27-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="39a27-303">Para obtener más información acerca de la agrupación en clústeres de SQL Server en Azure mediante el modelo de implementación de hello Azure Resource Manager, vea estos artículos:</span><span class="sxs-lookup"><span data-stu-id="39a27-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="39a27-304">[Configuración de un grupo de disponibilidad AlwaysOn en Azure Virtual Machines mediante Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual].</span><span class="sxs-lookup"><span data-stu-id="39a27-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="39a27-305">[Configuración de un equilibrador de carga interno para un grupo de disponibilidad AlwaysOn de Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="39a27-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="39a27-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Escenarios de implementación completa de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="39a27-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="39a27-307">Escenario de implementación con la plantilla 1 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="39a27-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="39a27-308">En la figura 8 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **UN** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="39a27-309">Este escenario se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="39a27-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="39a27-310">Se utiliza un clúster dedicado para la instancia de SAP ASCS/SCS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="39a27-311">Se utiliza un clúster dedicado para la instancia DBMS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="39a27-312">Se implementan instancias de servidores de aplicaciones SAP en máquinas virtuales dedicadas propias.</span><span class="sxs-lookup"><span data-stu-id="39a27-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: Plantilla 1 de arquitectura de alta disponibilidad de SAP con un clúster dedicado para ASCS/SCS y DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="39a27-314">_**Figura 8**: Plantilla 1 de arquitectura de alta disponibilidad de SAP con un clúster dedicado para ASCS/SCS y DBMS_</span><span class="sxs-lookup"><span data-stu-id="39a27-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="39a27-315">Escenario de implementación con la plantilla 2 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="39a27-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="39a27-316">En la figura 9 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **UN** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="39a27-317">Este escenario se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="39a27-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="39a27-318">Se utiliza un clúster dedicado para **ambos** Hola SAP ASCS/SCS de la instancia y Hola DBMS.</span><span class="sxs-lookup"><span data-stu-id="39a27-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="39a27-319">Se implementan instancias de servidores de aplicaciones SAP en máquinas virtuales dedicadas propias.</span><span class="sxs-lookup"><span data-stu-id="39a27-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: Plantilla 2 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para ASCS/SCS y otro para la instancia de DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="39a27-321">_**Figura 9:** Plantilla 2 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para ASCS/SCS y otro para la instancia de DBMS_</span><span class="sxs-lookup"><span data-stu-id="39a27-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="39a27-322">Escenario de implementación con la plantilla 3 de arquitectura</span><span class="sxs-lookup"><span data-stu-id="39a27-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="39a27-323">En la figura 10 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **DOS** sistemas SAP, con &lt;SID1&gt; y &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="39a27-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="39a27-324">Este escenario se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="39a27-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="39a27-325">Se utiliza un clúster dedicado para **ambos** instancia Hola SAP ASCS/SCS SID1 *y* instancia Hola SAP ASCS/SCS SID2 (un clúster).</span><span class="sxs-lookup"><span data-stu-id="39a27-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="39a27-326">Se usa un clúster dedicado para SID 1 de DBMS y otro para SID2 de DBMS (dos clústeres).</span><span class="sxs-lookup"><span data-stu-id="39a27-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="39a27-327">Instancias de servidor de aplicaciones de SAP para hello sistema SAP SID1 tienen sus propias máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="39a27-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="39a27-328">Instancias de servidor de aplicaciones de SAP para hello sistema SAP SID2 tienen sus propias máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="39a27-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: Plantilla 3 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para las diferentes instancias de ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="39a27-330">_**Figura 10:** Plantilla 3 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para las diferentes instancias de ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="39a27-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="39a27-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparar la infraestructura de Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="39a27-332">Preparar la infraestructura de Hola para arquitectura de plantilla de 1</span><span class="sxs-lookup"><span data-stu-id="39a27-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="39a27-333">Las plantillas de Azure Resource Manager para SAP ayudan a simplificar la implementación de los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="39a27-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="39a27-334">plantillas de tres niveles de Hello en el Administrador de recursos de Azure también admiten escenarios de alta disponibilidad, como en la arquitectura 1 de plantilla, que tiene dos clústeres.</span><span class="sxs-lookup"><span data-stu-id="39a27-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="39a27-335">Cada clúster es un único punto de error de SAP para ASCS/SCS de SAP y DBMS.</span><span class="sxs-lookup"><span data-stu-id="39a27-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="39a27-336">Aquí es donde puede obtener plantillas del Administrador de recursos de Azure para el escenario de ejemplo de Hola que se describen en este artículo:</span><span class="sxs-lookup"><span data-stu-id="39a27-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="39a27-337">Imagen de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="39a27-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="39a27-338">Imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="39a27-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="39a27-339">infraestructura de hello tooprepare de arquitectura 1 de plantilla:</span><span class="sxs-lookup"><span data-stu-id="39a27-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="39a27-340">En el portal de Azure, en Hola Hola **parámetros** hoja en hello **SYSTEMAVAILABILITY** cuadro, seleccione **HA**.</span><span class="sxs-lookup"><span data-stu-id="39a27-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: Especificación de los parámetros de Azure Resource Manager para alta disponibilidad de SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="39a27-342">_**Figura 11:** Especificación de los parámetros de Azure Resource Manager para alta disponibilidad de SAP_</span><span class="sxs-lookup"><span data-stu-id="39a27-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="39a27-343">crean plantillas de Hello:</span><span class="sxs-lookup"><span data-stu-id="39a27-343">hello templates create:</span></span>

  * <span data-ttu-id="39a27-344">**Máquinas virtuales**:</span><span class="sxs-lookup"><span data-stu-id="39a27-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="39a27-345">Máquinas virtuales de Servidor de aplicaciones de SAP: <*SIDSistemaSAP*>-di-<*Número*></span><span class="sxs-lookup"><span data-stu-id="39a27-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="39a27-346">Máquinas virtuales de clúster de ASCS/SCS: <*SIDSistemaSAP*>-ascs-<*Número*></span><span class="sxs-lookup"><span data-stu-id="39a27-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="39a27-347">Un clúster de DBMS: <*SIDSistemaSAP*>-db-<*Número*></span><span class="sxs-lookup"><span data-stu-id="39a27-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="39a27-348">**Tarjetas de red para todas las máquinas virtuales con direcciones IP asociadas**:</span><span class="sxs-lookup"><span data-stu-id="39a27-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="39a27-349"><*SIDSistemaSAP*&gt;-nic-di-&lt;*Número*></span><span class="sxs-lookup"><span data-stu-id="39a27-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="39a27-350"><*SIDSistemaSAP*&gt;-nic-ascs-&lt;*Número*></span><span class="sxs-lookup"><span data-stu-id="39a27-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="39a27-351"><*SIDSistemaSAP*&gt;-nic-db-&lt;*Número*></span><span class="sxs-lookup"><span data-stu-id="39a27-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="39a27-352">**Cuentas de almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="39a27-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="39a27-353">**Grupos de disponibilidad** para:</span><span class="sxs-lookup"><span data-stu-id="39a27-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="39a27-354">Máquinas virtuales de Servidor de aplicaciones de SAP: <*SIDSistemaSAP*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="39a27-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="39a27-355">Máquinas virtuales de clúster de ASCS/SCS de SAP: <*SIDSistemaSAP*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="39a27-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="39a27-356">Máquinas virtuales de clúster de DBMS: <*SIDSistemaSAP*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="39a27-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="39a27-357">**Equilibrador de carga interno de Azure**:</span><span class="sxs-lookup"><span data-stu-id="39a27-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="39a27-358">Con todos los puertos para la instancia ASCS/SCS de Hola y la dirección IP <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="39a27-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="39a27-359">Con todos los puertos para hello DBMS de SQL Server y la dirección IP <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="39a27-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="39a27-360">**Grupo de seguridad de red**: &lt;*SIDSistemaSAP*&gt;-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="39a27-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="39a27-361">Con un toohello de puerto de protocolo de escritorio remoto (RDP) externo abierto <*SAPSystemSID*> 0 - ascs - virtual machine</span><span class="sxs-lookup"><span data-stu-id="39a27-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-362">Todas las direcciones IP de las tarjetas de red de Hola y equilibradores de carga interno de Azure son **dinámica** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="39a27-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="39a27-363">Cambiarlos demasiado**estático** direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="39a27-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="39a27-364">Se describe cómo toodo esto más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="39a27-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Implementar máquinas virtuales con la red corporativa conectividad (entre entornos) toouse en producción</span><span class="sxs-lookup"><span data-stu-id="39a27-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="39a27-366">Para los sistemas de producción de SAP, implemente máquinas virtuales de Azure con [conectividad de red corporativa (entre locales)][planning-guide-2.2] mediante el uso de VPN de sitio a sitio de Azure o Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="39a27-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-367">Puede usar la instancia de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="39a27-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="39a27-368">subred y red virtual de hello ya se crearon y preparados.</span><span class="sxs-lookup"><span data-stu-id="39a27-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="39a27-369">En el portal de Azure, en Hola Hola **parámetros** hoja en hello **NEWOREXISTINGSUBNET** cuadro, seleccione **existente**.</span><span class="sxs-lookup"><span data-stu-id="39a27-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="39a27-370">Hola **SUBNETID** , agregue la cadena completa de saludo de la red de Azure preparada SubnetID donde piensa toodeploy máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="39a27-371">tooget una lista de todas las subredes de red de Azure, ejecute este comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="39a27-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="39a27-372">Hola **identificador** campo muestra hello **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="39a27-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="39a27-373">tooget una lista de todos los **SUBNETID** valores, ejecute este comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="39a27-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="39a27-374">Hola **SUBNETID** tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="39a27-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="39a27-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Implementación solo en la nube de instancias de SAP para prueba o demostración</span><span class="sxs-lookup"><span data-stu-id="39a27-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="39a27-376">Puede implementar el sistema de SAP de alta disponibilidad en un modelo de implementación solo en la nube.</span><span class="sxs-lookup"><span data-stu-id="39a27-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="39a27-377">Este tipo de implementación se usa principalmente para demostrar o probar casos de uso.</span><span class="sxs-lookup"><span data-stu-id="39a27-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="39a27-378">No es idóneo para los casos de uso de producción.</span><span class="sxs-lookup"><span data-stu-id="39a27-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="39a27-379">En el portal de Azure, en Hola Hola **parámetros** hoja en hello **NEWOREXISTINGSUBNET** cuadro, seleccione **nueva**.</span><span class="sxs-lookup"><span data-stu-id="39a27-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="39a27-380">Deje hello **SUBNETID** campo vacío.</span><span class="sxs-lookup"><span data-stu-id="39a27-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="39a27-381">Hola SAP Azure Resource Manager plantilla crea automáticamente Hola subred y red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-382">También debe toodeploy al menos uno dedicado máquina virtual de Active Directory y DNS en Hola la misma instancia de la red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="39a27-383">plantilla de Hello no crea estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="39a27-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="39a27-384">Preparar la infraestructura de Hola para arquitectura de plantilla de 2</span><span class="sxs-lookup"><span data-stu-id="39a27-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="39a27-385">Puede usar esta plantilla de administrador de recursos de Azure para SAP toohelp simplificar la implementación de recursos de la infraestructura necesaria para SAP arquitectura plantilla 2.</span><span class="sxs-lookup"><span data-stu-id="39a27-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="39a27-386">Aquí puede obtener las plantillas de Azure Resource Manager para este escenario de implementación:</span><span class="sxs-lookup"><span data-stu-id="39a27-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="39a27-387">Imagen de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="39a27-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="39a27-388">Imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="39a27-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="39a27-389">Preparar la infraestructura de Hola para arquitectura de plantilla de 3</span><span class="sxs-lookup"><span data-stu-id="39a27-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="39a27-390">Puede preparar la infraestructura de Hola y configurar SAP para **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="39a27-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="39a27-391">Por ejemplo, puede agregar una instancia de ASCS/SCS de SAP adicional en una configuración de clúster *existente*.</span><span class="sxs-lookup"><span data-stu-id="39a27-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="39a27-392">Para obtener más información, consulte [configurar una instancia de SAP ASCS/SCS adicional en un toocreate de configuración de clúster una configuración de múltiples SID de SAP existente en el Administrador de recursos de Azure][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="39a27-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="39a27-393">Si desea toocreate un nuevo clúster de múltiples SID, puede usar Hola multi-SID [plantillas de inicio rápido en GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="39a27-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="39a27-394">toocreate un nuevo clúster de múltiples SID, necesita hello toodeploy después de tres plantillas:</span><span class="sxs-lookup"><span data-stu-id="39a27-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="39a27-395">Plantilla de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="39a27-396">Plantilla de base de datos</span><span class="sxs-lookup"><span data-stu-id="39a27-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="39a27-397">Plantilla de servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="39a27-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="39a27-398">Hello siguientes secciones contienen más detalles sobre las plantillas de Hola y parámetros de hello necesita tooprovide en las plantillas de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="39a27-399"><a name="ASCS-SCS-template"></a>Plantilla de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="39a27-400">plantilla de Hello ASCS/SCS implementa dos máquinas virtuales que se puede usar un clúster de conmutación por error de Windows Server que hospeda varias instancias ASCS/SCS toocreate.</span><span class="sxs-lookup"><span data-stu-id="39a27-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="39a27-401">tooset plantilla Hola ASCS/SCS multi-SID, Hola [plantilla de varias SID ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image], escriba los valores de hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="39a27-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="39a27-402">**Prefijo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="39a27-402">**Resource Prefix**.</span></span>  <span data-ttu-id="39a27-403">Establezca el prefijo del recurso de hello, que es usado tooprefix todos los recursos que se crean durante la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="39a27-404">Dado que no pertenecen a recursos de hello tooonly un sistema SAP, el prefijo de hello del recurso de hello no es Hola SID de un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="39a27-405">Hola prefijo debe estar entre **tres y seis caracteres**.</span><span class="sxs-lookup"><span data-stu-id="39a27-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="39a27-406">**Tipo de pila**.</span><span class="sxs-lookup"><span data-stu-id="39a27-406">**Stack Type**.</span></span> <span data-ttu-id="39a27-407">Seleccione el tipo de pila de Hola de hello sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="39a27-408">Según el tipo de la pila de hello, equilibrador de carga de Azure tiene uno (ABAP o Java solo) o dos (ABAP + Java) las direcciones IP privadas por el sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="39a27-409">**Tipo de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="39a27-409">**OS Type**.</span></span> <span data-ttu-id="39a27-410">Seleccione sistema de operativo Hola de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="39a27-411">**Recuento de sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="39a27-411">**SAP System Count**.</span></span> <span data-ttu-id="39a27-412">Seleccione el número de Hola de sistemas SAP que desee tooinstall en este clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="39a27-413">**Disponibilidad del sistema**.</span><span class="sxs-lookup"><span data-stu-id="39a27-413">**System Availability**.</span></span> <span data-ttu-id="39a27-414">Seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="39a27-414">Select **HA**.</span></span>
  -  <span data-ttu-id="39a27-415">**Nombre de usuario y contraseña del administrador**.</span><span class="sxs-lookup"><span data-stu-id="39a27-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="39a27-416">Cree un nuevo usuario que puede ser toosign usado en la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="39a27-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="39a27-417">**Subred nueva o existente**.</span><span class="sxs-lookup"><span data-stu-id="39a27-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="39a27-418">Establezca si es necesario crear una red virtual y subred nuevas o si se debe usar una subred existente.</span><span class="sxs-lookup"><span data-stu-id="39a27-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="39a27-419">Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione **existente**.</span><span class="sxs-lookup"><span data-stu-id="39a27-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="39a27-420">**Identificador de subred**. Id. de Hola de conjunto de máquinas virtuales de hello subred toowhich Hola debe estar conectado.</span><span class="sxs-lookup"><span data-stu-id="39a27-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="39a27-421">Seleccione subred Hola de su red privada virtual (VPN) o red de ExpressRoute red virtual tooconnect Hola máquina virtual tooyour local.</span><span class="sxs-lookup"><span data-stu-id="39a27-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="39a27-422">Id. de Hello normalmente este aspecto:</span><span class="sxs-lookup"><span data-stu-id="39a27-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="39a27-423">/subscriptions/<*identificador de suscripción*>/resourceGroups/<*nombre del grupo de recursos*>/providers/Microsoft.Network/virtualNetworks/<*nombre de la red virtual*>/subnets/<*nombre de la subred*></span><span class="sxs-lookup"><span data-stu-id="39a27-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="39a27-424">plantilla de Hello implementa una instancia de equilibrador de carga de Azure, lo que es compatible con varios sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="39a27-425">Hola ASCS se configuran para el número de instancia de 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="39a27-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="39a27-426">Hola SCS se configuran para el número de instancia 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="39a27-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="39a27-427">Hola ASCS Enqueue Replication Server (ERS) (solamente para Linux) se configuran para el número de instancia 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="39a27-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="39a27-428">Hola SCS ERS (solamente para Linux) se configuran para el número de instancia 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="39a27-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="39a27-429">Hello equilibrador de carga contiene 1 (2 para Linux) VIP(s), 1 x VIP para ASCS/SCS y 1 x VIP para ERS (solamente para Linux).</span><span class="sxs-lookup"><span data-stu-id="39a27-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="39a27-430">Hello siguiente lista contiene todas las reglas (donde x es el número de Hola de hello sistema SAP, por ejemplo, 1, 2, 3...) de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="39a27-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="39a27-431">Puertos específicos de Windows para cada sistema SAP 445, 5985</span><span class="sxs-lookup"><span data-stu-id="39a27-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="39a27-432">Puertos ASCS (número de instancia x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="39a27-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="39a27-433">Puertos SCS (número de instancia x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="39a27-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="39a27-434">Puertos ASCS ERS en Linux (número de instancia x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="39a27-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="39a27-435">Puertos SCS ERS en Linux (número de instancia x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="39a27-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="39a27-436">equilibrador de carga de Hello es hello toouse configurado siguiendo los puertos de sondeo (donde x es el número de Hola de hello sistema SAP, por ejemplo, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="39a27-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="39a27-437">Puerto de sondeo del equilibrador de carga interno de ASCS/SCS: 620x0</span><span class="sxs-lookup"><span data-stu-id="39a27-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="39a27-438">Puerto de sondeo del equilibrador de carga interno de ERS (solo para Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="39a27-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="39a27-439"><a name="database-template"></a> Plantilla de base de datos</span><span class="sxs-lookup"><span data-stu-id="39a27-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="39a27-440">plantilla de la base de datos de Hello implementa uno o dos máquinas virtuales que se puede usar tooinstall Hola sistema de administración de bases de datos relacionales (RDBMS) para un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="39a27-441">Por ejemplo, si implementa una plantilla de ASCS/SCS de cinco sistemas SAP, debe toodeploy esta plantilla cinco veces.</span><span class="sxs-lookup"><span data-stu-id="39a27-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="39a27-442">tooset plantilla de multi-SID de base de datos de Hola Hola [plantilla de SID de varias bases de datos][sap-templates-3-tier-multisid-db-marketplace-image], escriba los valores de hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="39a27-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="39a27-443">**Identificador de sistema SAP**. Escriba Hola identificador de hello sistema SAP que desee tooinstall el sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="39a27-444">Identificador de Hola se utilizará como prefijo para los recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="39a27-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="39a27-445">**Tipo de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="39a27-445">**Os Type**.</span></span> <span data-ttu-id="39a27-446">Seleccione sistema de operativo Hola de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="39a27-447">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="39a27-447">**Dbtype**.</span></span> <span data-ttu-id="39a27-448">Seleccione el tipo de saludo de la base de datos de hello desea tooinstall en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="39a27-449">Seleccione **SQL** si desea tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39a27-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="39a27-450">Seleccione **HANA** si tiene previsto tooinstall SAP HANA en máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="39a27-451">Asegúrese de que tooselect Hola tipo de sistema operativo correcto: seleccione **Windows** para SQL y seleccione una distribución de Linux para HANA.</span><span class="sxs-lookup"><span data-stu-id="39a27-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="39a27-452">Hello equilibrador de carga de Azure que está conectado toohello máquinas virtuales estarán configurar tipo de base de datos de toosupport Hola seleccionado:</span><span class="sxs-lookup"><span data-stu-id="39a27-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="39a27-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="39a27-453">**SQL**.</span></span> <span data-ttu-id="39a27-454">equilibrador de carga de Hello realizará el puerto 1433 de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="39a27-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="39a27-455">Asegúrese de que toouse este puerto para la instalación de SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="39a27-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="39a27-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="39a27-456">**HANA**.</span></span> <span data-ttu-id="39a27-457">equilibrador de carga de Hello va a equilibrar la carga de los puertos 35015 y 35017.</span><span class="sxs-lookup"><span data-stu-id="39a27-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="39a27-458">Asegúrese de que tooinstall SAP HANA con el número de instancia **50**.</span><span class="sxs-lookup"><span data-stu-id="39a27-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="39a27-459">equilibrador de carga de Hello usará el puerto de sondeo 62550.</span><span class="sxs-lookup"><span data-stu-id="39a27-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="39a27-460">**Tamaño del sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="39a27-460">**Sap System Size**.</span></span> <span data-ttu-id="39a27-461">Número de conjunto de Hola de nuevo sistema de SAPS Hola proporcionará.</span><span class="sxs-lookup"><span data-stu-id="39a27-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="39a27-462">Si no estás seguro de sistema de Hola de SAPS cuántos requerirá, pregunte al socio de tecnología de SAP o integrador de sistema.</span><span class="sxs-lookup"><span data-stu-id="39a27-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="39a27-463">**Disponibilidad del sistema**.</span><span class="sxs-lookup"><span data-stu-id="39a27-463">**System Availability**.</span></span> <span data-ttu-id="39a27-464">Seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="39a27-464">Select **HA**.</span></span>
  -  <span data-ttu-id="39a27-465">**Nombre de usuario y contraseña del administrador**.</span><span class="sxs-lookup"><span data-stu-id="39a27-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="39a27-466">Cree un nuevo usuario que puede ser toosign usado en la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="39a27-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="39a27-467">**Identificador de subred**. Escriba Hola Id. de subred de Hola que usó durante la implementación de Hola de plantilla ASCS/SCS de Hola o de Hola de subred de Hola que se creó como parte de la implementación de plantilla ASCS/SCS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="39a27-468"><a name="application-servers-template"></a>Plantilla de servidores de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="39a27-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="39a27-469">plantilla de servidores de aplicación Hola implementa dos o más máquinas virtuales que puede utilizarse como instancias del servidor de aplicaciones de SAP para un sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="39a27-470">Por ejemplo, si implementa una plantilla de ASCS/SCS de cinco sistemas SAP, debe toodeploy esta plantilla cinco veces.</span><span class="sxs-lookup"><span data-stu-id="39a27-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="39a27-471">tooset plantilla de multi-SID en servidores de aplicación de hello, Hola [plantilla de SID de varios servidores de aplicación][sap-templates-3-tier-multisid-apps-marketplace-image], escriba los valores de hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="39a27-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="39a27-472">**Identificador de sistema SAP**. Escriba Hola identificador de hello sistema SAP que desee tooinstall el sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="39a27-473">Identificador de Hola se utilizará como prefijo para los recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="39a27-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="39a27-474">**Tipo de sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="39a27-474">**Os Type**.</span></span> <span data-ttu-id="39a27-475">Seleccione sistema de operativo Hola de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="39a27-476">**Tamaño del sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="39a27-476">**Sap System Size**.</span></span> <span data-ttu-id="39a27-477">número de Hola de nuevo sistema de SAPS Hola proporcionará.</span><span class="sxs-lookup"><span data-stu-id="39a27-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="39a27-478">Si no estás seguro de sistema de Hola de SAPS cuántos requerirá, pregunte al socio de tecnología de SAP o integrador de sistema.</span><span class="sxs-lookup"><span data-stu-id="39a27-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="39a27-479">**Disponibilidad del sistema**.</span><span class="sxs-lookup"><span data-stu-id="39a27-479">**System Availability**.</span></span> <span data-ttu-id="39a27-480">Seleccione **Alta disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="39a27-480">Select **HA**.</span></span>
  -  <span data-ttu-id="39a27-481">**Nombre de usuario y contraseña del administrador**.</span><span class="sxs-lookup"><span data-stu-id="39a27-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="39a27-482">Cree un nuevo usuario que puede ser toosign usado en la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="39a27-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="39a27-483">**Identificador de subred**. Escriba Hola Id. de subred de Hola que usó durante la implementación de Hola de plantilla ASCS/SCS de Hola o de Hola de subred de Hola que se creó como parte de la implementación de plantilla ASCS/SCS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="39a27-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="39a27-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="39a27-485">En nuestro ejemplo, el espacio de direcciones de Hola de hello red virtual de Azure es 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="39a27-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="39a27-486">Hay una subred llamada **Subnet**, con un intervalo de direcciones de 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="39a27-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="39a27-487">Todas las máquinas virtuales y los equilibradores de carga internos están implementados en esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="39a27-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39a27-488">No realiza ningún cambio toohello configuración de red dentro de hello sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="39a27-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="39a27-489">Esto incluye direcciones IP, servidores DNS y subred.</span><span class="sxs-lookup"><span data-stu-id="39a27-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="39a27-490">Ajuste toda la configuración de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="39a27-491">Hola servicio de protocolo de configuración dinámica de Host (DHCP) propaga la configuración.</span><span class="sxs-lookup"><span data-stu-id="39a27-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="39a27-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Direcciones IP de DNS</span><span class="sxs-lookup"><span data-stu-id="39a27-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="39a27-493">Hola tooset requiere que direcciones IP de DNS, Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="39a27-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="39a27-494">En el portal de Azure, en Hola Hola **servidores DNS** hoja, asegúrese de que la red virtual **servidores DNS** opción se establece demasiado**DNS personalizada**.</span><span class="sxs-lookup"><span data-stu-id="39a27-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="39a27-495">Seleccione la configuración en función de tipo de Hola de red que tiene.</span><span class="sxs-lookup"><span data-stu-id="39a27-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="39a27-496">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="39a27-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="39a27-497">[Conectividad de red corporativa (entre entornos)][planning-guide-2.2]: agregar las direcciones IP de servidores DNS local Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="39a27-498">Puede extender local DNS servidores toohello máquinas virtuales que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="39a27-499">En ese caso, puede agregar direcciones IP de Hola de hello Azure máquinas virtuales en el que se ejecuta el servicio DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="39a27-500">[Implementación solo en la nube][planning-guide-2.1]: implementar una máquina virtual adicional en hello misma instancia de la red Virtual que actúa como un servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="39a27-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="39a27-501">Agregar direcciones IP de Hola de hello Azure máquinas virtuales que ha configurado el servicio DNS toorun.</span><span class="sxs-lookup"><span data-stu-id="39a27-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Figura 12: Configuración de servidores DNS para Azure Virtual Network][sap-ha-guide-figure-3001]

    <span data-ttu-id="39a27-503">_**Figura 12:** Configuración de servidores DNS para Azure Virtual Network_</span><span class="sxs-lookup"><span data-stu-id="39a27-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="39a27-504">Si cambia las direcciones IP de servidores DNS de Hola Hola, necesita toorestart Hola máquinas virtuales de Azure tooapply Hola cambio y propagar los nuevos servidores DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="39a27-505">En nuestro ejemplo, hello servicio DNS está instalado y configurado en estas máquinas virtuales de Windows:</span><span class="sxs-lookup"><span data-stu-id="39a27-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="39a27-506">Rol de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-506">Virtual machine role</span></span> | <span data-ttu-id="39a27-507">Nombre de host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-507">Virtual machine host name</span></span> | <span data-ttu-id="39a27-508">Nombre de tarjeta de red</span><span class="sxs-lookup"><span data-stu-id="39a27-508">Network card name</span></span> | <span data-ttu-id="39a27-509">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="39a27-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39a27-510">Primer servidor DNS</span><span class="sxs-lookup"><span data-stu-id="39a27-510">First DNS server</span></span> |<span data-ttu-id="39a27-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="39a27-511">domcontr-0</span></span> |<span data-ttu-id="39a27-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="39a27-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="39a27-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="39a27-513">10.0.0.10</span></span> |
| <span data-ttu-id="39a27-514">Segundo servidor DNS</span><span class="sxs-lookup"><span data-stu-id="39a27-514">Second DNS server</span></span> |<span data-ttu-id="39a27-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="39a27-515">domcontr-1</span></span> |<span data-ttu-id="39a27-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="39a27-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="39a27-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="39a27-517">10.0.0.11</span></span> |

### <span data-ttu-id="39a27-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Los nombres de host y direcciones IP estáticas para la instancia en clúster de SAP ASCS/SCS de Hola y de instancia en clúster de DBMS</span><span class="sxs-lookup"><span data-stu-id="39a27-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="39a27-519">Para la implementación local, necesita estas direcciones IP y nombres de host reservados:</span><span class="sxs-lookup"><span data-stu-id="39a27-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="39a27-520">Rol de nombre de host virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-520">Virtual host name role</span></span> | <span data-ttu-id="39a27-521">Nombre de host virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-521">Virtual host name</span></span> | <span data-ttu-id="39a27-522">Dirección IP estática virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39a27-523">Primer nombre de host virtual de clúster de ASCS/SCS de SAP (para la administración del clúster)</span><span class="sxs-lookup"><span data-stu-id="39a27-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="39a27-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="39a27-524">pr1-ascs-vir</span></span> |<span data-ttu-id="39a27-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="39a27-525">10.0.0.42</span></span> |
| <span data-ttu-id="39a27-526">Nombre de host virtual de la instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="39a27-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="39a27-527">pr1-ascs-sap</span></span> |<span data-ttu-id="39a27-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="39a27-528">10.0.0.43</span></span> |
| <span data-ttu-id="39a27-529">Segundo nombre de host virtual de clúster de DBMS de SAP (administración del clúster)</span><span class="sxs-lookup"><span data-stu-id="39a27-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="39a27-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="39a27-530">pr1-dbms-vir</span></span> |<span data-ttu-id="39a27-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="39a27-531">10.0.0.32</span></span> |

<span data-ttu-id="39a27-532">Al crear el clúster de hello, crear Hola nombres de host virtual **pr1-ascs-EE.** y **pr1-dbms-EE.** y Hola asociadas direcciones IP que administración el propio clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="39a27-533">Para obtener información acerca de cómo toodo, vea [recopilar los nodos del clúster en una configuración de clúster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="39a27-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="39a27-534">Puede crear manualmente Hola otros dos nombres de host virtual **pr1-ascs-sap** y **pr1-dbms-sap**, y Hola asociadas direcciones IP, en el servidor DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="39a27-535">Hello instancia SAP ASCS/SCS en clúster y la instancia DBMS de hello en clúster usan estos recursos.</span><span class="sxs-lookup"><span data-stu-id="39a27-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="39a27-536">Para obtener información acerca de cómo toodo, vea [crear un nombre de host virtual para una instancia agrupada de SAP ASCS/SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="39a27-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="39a27-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Conjunto de direcciones IP estáticas para máquinas virtuales SAP de Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="39a27-538">Después de implementar hello toouse de máquinas virtuales en el clúster, debe tooset las direcciones IP estáticas para todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="39a27-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="39a27-539">Haga esto en la configuración de red Virtual de Azure de hello y no en el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="39a27-540">Hola portal de Azure, seleccione **grupo de recursos** > **tarjeta de red** > **configuración** > **dirección IP** .</span><span class="sxs-lookup"><span data-stu-id="39a27-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="39a27-541">En hello **direcciones IP** hoja, en **asignación**, seleccione **estático**.</span><span class="sxs-lookup"><span data-stu-id="39a27-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="39a27-542">Hola **dirección IP** cuadro, escriba la dirección IP de Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="39a27-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="39a27-543">Si cambia la dirección IP de Hola Hola de tarjeta de red, necesita toorestart Hola máquinas virtuales de Azure tooapply Hola cambio.</span><span class="sxs-lookup"><span data-stu-id="39a27-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Figura 13: Conjunto de direcciones IP estáticas para la tarjeta de red de Hola de cada máquina virtual][sap-ha-guide-figure-3002]

  <span data-ttu-id="39a27-545">_**Figura 13:** establecer direcciones IP estáticas para la tarjeta de red de Hola de cada máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="39a27-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="39a27-546">Repita este paso para todas las interfaces de red, es decir, para todas las máquinas virtuales, incluidas las máquinas virtuales que necesite toouse para el servicio de Active Directory/DNS.</span><span class="sxs-lookup"><span data-stu-id="39a27-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="39a27-547">En este ejemplo, aparecen estas máquinas virtuales y direcciones IP estáticas:</span><span class="sxs-lookup"><span data-stu-id="39a27-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="39a27-548">Rol de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-548">Virtual machine role</span></span> | <span data-ttu-id="39a27-549">Nombre de host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39a27-549">Virtual machine host name</span></span> | <span data-ttu-id="39a27-550">Nombre de tarjeta de red</span><span class="sxs-lookup"><span data-stu-id="39a27-550">Network card name</span></span> | <span data-ttu-id="39a27-551">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="39a27-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39a27-552">Primer servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-552">First SAP Application Server instance</span></span> |<span data-ttu-id="39a27-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="39a27-553">pr1-di-0</span></span> |<span data-ttu-id="39a27-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="39a27-554">pr1-nic-di-0</span></span> |<span data-ttu-id="39a27-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="39a27-555">10.0.0.50</span></span> |
| <span data-ttu-id="39a27-556">Segundo servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="39a27-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="39a27-557">pr1-di-1</span></span> |<span data-ttu-id="39a27-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="39a27-558">pr1-nic-di-1</span></span> |<span data-ttu-id="39a27-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="39a27-559">10.0.0.51</span></span> |
| <span data-ttu-id="39a27-560">...</span><span class="sxs-lookup"><span data-stu-id="39a27-560">...</span></span> |<span data-ttu-id="39a27-561">...</span><span class="sxs-lookup"><span data-stu-id="39a27-561">...</span></span> |<span data-ttu-id="39a27-562">...</span><span class="sxs-lookup"><span data-stu-id="39a27-562">...</span></span> |<span data-ttu-id="39a27-563">...</span><span class="sxs-lookup"><span data-stu-id="39a27-563">...</span></span> |
| <span data-ttu-id="39a27-564">Último servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="39a27-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="39a27-565">pr1-di-5</span></span> |<span data-ttu-id="39a27-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="39a27-566">pr1-nic-di-5</span></span> |<span data-ttu-id="39a27-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="39a27-567">10.0.0.55</span></span> |
| <span data-ttu-id="39a27-568">Primer nodo de clúster para la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="39a27-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="39a27-569">pr1-ascs-0</span></span> |<span data-ttu-id="39a27-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="39a27-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="39a27-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="39a27-571">10.0.0.40</span></span> |
| <span data-ttu-id="39a27-572">Segundo nodo de clúster para la instancia de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="39a27-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="39a27-573">pr1-ascs-1</span></span> |<span data-ttu-id="39a27-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="39a27-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="39a27-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="39a27-575">10.0.0.41</span></span> |
| <span data-ttu-id="39a27-576">Primer nodo de clúster para la instancia de DBMS</span><span class="sxs-lookup"><span data-stu-id="39a27-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="39a27-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="39a27-577">pr1-db-0</span></span> |<span data-ttu-id="39a27-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="39a27-578">pr1-nic-db-0</span></span> |<span data-ttu-id="39a27-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="39a27-579">10.0.0.30</span></span> |
| <span data-ttu-id="39a27-580">Segundo nodo de clúster para la instancia de DBMS</span><span class="sxs-lookup"><span data-stu-id="39a27-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="39a27-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="39a27-581">pr1-db-1</span></span> |<span data-ttu-id="39a27-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="39a27-582">pr1-nic-db-1</span></span> |<span data-ttu-id="39a27-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="39a27-583">10.0.0.31</span></span> |

### <span data-ttu-id="39a27-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Establecer una dirección IP estática para el equilibrador de carga interno de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="39a27-585">plantilla de SAP Azure Resource Manager Hola crea un equilibrador de carga interno de Azure que se utiliza para el clúster de instancia de SAP ASCS/SCS de Hola y Hola DBMS.</span><span class="sxs-lookup"><span data-stu-id="39a27-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39a27-586">Hello dirección IP del nombre de host virtual Hola de hello SAP ASCS/SCS es Hola igual como dirección IP de Hola de hello equilibrador de carga interno de SAP ASCS/SCS: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="39a27-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="39a27-587">Hello dirección IP del nombre virtual de Hola de hello DBMS es Hola igual como dirección IP de Hola de hello equilibrador de carga interno de DBMS: **pr1 lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="39a27-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="39a27-588">equilibrador de carga de tooset una dirección IP estática para hello Azure interna:</span><span class="sxs-lookup"><span data-stu-id="39a27-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="39a27-589">Hello implementación inicial establece dirección IP del equilibrador de carga interno de hello demasiado**dinámica**.</span><span class="sxs-lookup"><span data-stu-id="39a27-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="39a27-590">En el portal de Azure, en Hola Hola **direcciones IP** hoja, en **asignación**, seleccione **estático**.</span><span class="sxs-lookup"><span data-stu-id="39a27-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="39a27-591">Configurar dirección IP de hello del equilibrador de carga interno de hello **pr1-lb-ascs** toohello dirección IP del nombre de host virtual Hola de instancia de SAP ASCS/SCS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="39a27-592">Configurar dirección IP de hello del equilibrador de carga interno de hello **pr1 lb-dbms** toohello dirección IP del nombre de host virtual Hola de instancia DBMS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Figura 14: Establecer las direcciones IP estáticas para el equilibrador de carga interno de hello para la instancia de SAP ASCS/SCS de Hola][sap-ha-guide-figure-3003]

  <span data-ttu-id="39a27-594">_**Figura 14:** configurar direcciones IP estáticas para el equilibrador de carga interno de hello para la instancia de SAP ASCS/SCS Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="39a27-595">En este ejemplo, aparecen 2 equilibradores de carga internos de Azure que tienen estas direcciones IP estáticas:</span><span class="sxs-lookup"><span data-stu-id="39a27-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="39a27-596">Rol del equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-596">Azure internal load balancer role</span></span> | <span data-ttu-id="39a27-597">Nombre del equilibrador de carga interno de Azure</span><span class="sxs-lookup"><span data-stu-id="39a27-597">Azure internal load balancer name</span></span> | <span data-ttu-id="39a27-598">Dirección IP estática</span><span class="sxs-lookup"><span data-stu-id="39a27-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39a27-599">Equilibrador de carga interno de instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="39a27-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="39a27-600">pr1-lb-ascs</span></span> |<span data-ttu-id="39a27-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="39a27-601">10.0.0.43</span></span> |
| <span data-ttu-id="39a27-602">Equilibrador de carga interno de DBMS de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="39a27-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="39a27-603">pr1-lb-dbms</span></span> |<span data-ttu-id="39a27-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="39a27-604">10.0.0.33</span></span> |


### <span data-ttu-id="39a27-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Reglas para el equilibrador de carga interno de Azure de Hola de equilibrio de carga ASCS/SCS de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="39a27-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="39a27-606">plantilla de SAP Azure Resource Manager Hola crea puertos de Hola que tiene:</span><span class="sxs-lookup"><span data-stu-id="39a27-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="39a27-607">Una instancia de ABAP ASCS, con el número de instancia predeterminado de hello **00**</span><span class="sxs-lookup"><span data-stu-id="39a27-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="39a27-608">Una instancia de Java SCS, con el número de instancia predeterminado de hello **01**</span><span class="sxs-lookup"><span data-stu-id="39a27-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="39a27-609">Cuando se instala la instancia de SAP ASCS/SCS, debe utilizar el número de instancia predeterminado de hello **00** para el número de instancia ABAP ASCS hello y la instancia predeterminada **01** para la instancia de Java SCS.</span><span class="sxs-lookup"><span data-stu-id="39a27-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="39a27-610">A continuación, crear puntos de conexión para puertos de SAP NetWeaver Hola de equilibrio de carga interno necesario.</span><span class="sxs-lookup"><span data-stu-id="39a27-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="39a27-611">toocreate requieren extremos de equilibrio de carga interno, en primer lugar, cree estos extremos para los puertos de SAP NetWeaver ABAP ASCS Hola de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="39a27-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="39a27-612">Nombre de regla de equilibrio de carga/servicio</span><span class="sxs-lookup"><span data-stu-id="39a27-612">Service/load balancing rule name</span></span> | <span data-ttu-id="39a27-613">Números de puerto predeterminados</span><span class="sxs-lookup"><span data-stu-id="39a27-613">Default port numbers</span></span> | <span data-ttu-id="39a27-614">Puertos concretos para (instancia de ASCS con el número de instancia 00) (ERS con 10)</span><span class="sxs-lookup"><span data-stu-id="39a27-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39a27-615">Enqueue Server/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="39a27-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="39a27-616">32<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-617">3200</span><span class="sxs-lookup"><span data-stu-id="39a27-617">3200</span></span> |
| <span data-ttu-id="39a27-618">ABAP Message Server/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="39a27-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="39a27-619">36<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-620">3600</span><span class="sxs-lookup"><span data-stu-id="39a27-620">3600</span></span> |
| <span data-ttu-id="39a27-621">Internal ABAP Message/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="39a27-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="39a27-622">39<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-623">3900</span><span class="sxs-lookup"><span data-stu-id="39a27-623">3900</span></span> |
| <span data-ttu-id="39a27-624">Message Server HTTP/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="39a27-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="39a27-625">81<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-626">8100</span><span class="sxs-lookup"><span data-stu-id="39a27-626">8100</span></span> |
| <span data-ttu-id="39a27-627">SAP Start Service ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="39a27-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="39a27-628">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="39a27-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="39a27-629">50013</span><span class="sxs-lookup"><span data-stu-id="39a27-629">50013</span></span> |
| <span data-ttu-id="39a27-630">SAP Start Service ASCS HTTPS/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="39a27-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="39a27-631">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="39a27-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="39a27-632">50014</span><span class="sxs-lookup"><span data-stu-id="39a27-632">50014</span></span> |
| <span data-ttu-id="39a27-633">Enqueue Replication/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="39a27-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="39a27-634">5<*NúmeroInstancia*>16</span><span class="sxs-lookup"><span data-stu-id="39a27-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="39a27-635">50016</span><span class="sxs-lookup"><span data-stu-id="39a27-635">50016</span></span> |
| <span data-ttu-id="39a27-636">SAP Start Service ERS HTTP/ *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="39a27-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="39a27-637">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="39a27-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="39a27-638">51013</span><span class="sxs-lookup"><span data-stu-id="39a27-638">51013</span></span> |
| <span data-ttu-id="39a27-639">SAP Start Service ERS HTTP/ *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="39a27-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="39a27-640">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="39a27-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="39a27-641">51014</span><span class="sxs-lookup"><span data-stu-id="39a27-641">51014</span></span> |
| <span data-ttu-id="39a27-642">Win RM/ *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="39a27-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="39a27-643">5985</span><span class="sxs-lookup"><span data-stu-id="39a27-643">5985</span></span> |
| <span data-ttu-id="39a27-644">File Share/ *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="39a27-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="39a27-645">445</span><span class="sxs-lookup"><span data-stu-id="39a27-645">445</span></span> |

<span data-ttu-id="39a27-646">_**Tabla 1:** números de instancias de SAP NetWeaver ABAP ASCS Hola de puerto_</span><span class="sxs-lookup"><span data-stu-id="39a27-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="39a27-647">A continuación, cree estos extremos para los puertos de SAP NetWeaver Java SCS Hola de equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="39a27-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="39a27-648">Nombre de regla de equilibrio de carga/servicio</span><span class="sxs-lookup"><span data-stu-id="39a27-648">Service/load balancing rule name</span></span> | <span data-ttu-id="39a27-649">Números de puerto predeterminados</span><span class="sxs-lookup"><span data-stu-id="39a27-649">Default port numbers</span></span> | <span data-ttu-id="39a27-650">Puertos concretos para (instancia de SCS con el número de instancia 01) (ERS con 11)</span><span class="sxs-lookup"><span data-stu-id="39a27-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39a27-651">Enqueue Server/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="39a27-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="39a27-652">32<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-653">3201</span><span class="sxs-lookup"><span data-stu-id="39a27-653">3201</span></span> |
| <span data-ttu-id="39a27-654">Gateway Server/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="39a27-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="39a27-655">33<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-656">3301</span><span class="sxs-lookup"><span data-stu-id="39a27-656">3301</span></span> |
| <span data-ttu-id="39a27-657">Java Message Server/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="39a27-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="39a27-658">39<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-659">3901</span><span class="sxs-lookup"><span data-stu-id="39a27-659">3901</span></span> |
| <span data-ttu-id="39a27-660">Message Server HTTP/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="39a27-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="39a27-661">81<*NúmeroInstancia*></span><span class="sxs-lookup"><span data-stu-id="39a27-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="39a27-662">8101</span><span class="sxs-lookup"><span data-stu-id="39a27-662">8101</span></span> |
| <span data-ttu-id="39a27-663">SAP Start Service SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="39a27-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="39a27-664">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="39a27-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="39a27-665">50113</span><span class="sxs-lookup"><span data-stu-id="39a27-665">50113</span></span> |
| <span data-ttu-id="39a27-666">SAP Start Service SCS HTTPS/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="39a27-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="39a27-667">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="39a27-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="39a27-668">50114</span><span class="sxs-lookup"><span data-stu-id="39a27-668">50114</span></span> |
| <span data-ttu-id="39a27-669">Enqueue Replication/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="39a27-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="39a27-670">5<*NúmeroInstancia*>16</span><span class="sxs-lookup"><span data-stu-id="39a27-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="39a27-671">50116</span><span class="sxs-lookup"><span data-stu-id="39a27-671">50116</span></span> |
| <span data-ttu-id="39a27-672">SAP Start Service ERS HTTP/ *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="39a27-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="39a27-673">5<*NúmeroInstancia*>13</span><span class="sxs-lookup"><span data-stu-id="39a27-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="39a27-674">51113</span><span class="sxs-lookup"><span data-stu-id="39a27-674">51113</span></span> |
| <span data-ttu-id="39a27-675">SAP Start Service ERS HTTPS/ *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="39a27-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="39a27-676">5<*NúmeroInstancia*>14</span><span class="sxs-lookup"><span data-stu-id="39a27-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="39a27-677">51114</span><span class="sxs-lookup"><span data-stu-id="39a27-677">51114</span></span> |
| <span data-ttu-id="39a27-678">Win RM/ *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="39a27-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="39a27-679">5985</span><span class="sxs-lookup"><span data-stu-id="39a27-679">5985</span></span> |
| <span data-ttu-id="39a27-680">File Share/ *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="39a27-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="39a27-681">445</span><span class="sxs-lookup"><span data-stu-id="39a27-681">445</span></span> |

<span data-ttu-id="39a27-682">_**Tabla 2:** números de instancias de SAP NetWeaver Java SCS Hola de puerto_</span><span class="sxs-lookup"><span data-stu-id="39a27-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: Reglas para el equilibrador de carga interno de Azure Hola de equilibrio de carga de predeterminado ASCS/SCS][sap-ha-guide-figure-3004]

<span data-ttu-id="39a27-684">_**Figura 15:** carga predeterminada ASCS/SCS reglas para el equilibrador de carga interno de Azure Hola de equilibrio_</span><span class="sxs-lookup"><span data-stu-id="39a27-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="39a27-685">Establecer dirección IP de Hola Hola de equilibrador de carga **pr1 lb-dbms** toohello dirección IP del nombre de host virtual Hola de instancia DBMS Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="39a27-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Cambiar las reglas para el equilibrador de carga interno de Azure Hola de equilibrio de carga de predeterminado de hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="39a27-687">Si desea toouse un número diferente de Hola SAP ASCS o instancias SCS, debe cambiar Hola nombres y valores de sus puertos de valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="39a27-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="39a27-688">Hola portal de Azure, seleccione  **<* SID*> cargar - lb - ascs equilibrador ** > **reglas de equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="39a27-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="39a27-689">Para todas las reglas que pertenezcan toohello SAP ASCS o instancia SCS de equilibrio de la carga, cambiar estos valores:</span><span class="sxs-lookup"><span data-stu-id="39a27-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="39a27-690">Nombre</span><span class="sxs-lookup"><span data-stu-id="39a27-690">Name</span></span>
  * <span data-ttu-id="39a27-691">Port</span><span class="sxs-lookup"><span data-stu-id="39a27-691">Port</span></span>
  * <span data-ttu-id="39a27-692">Puerto de back-end</span><span class="sxs-lookup"><span data-stu-id="39a27-692">Back-end port</span></span>

  <span data-ttu-id="39a27-693">Por ejemplo, si desea que el número de instancia de toochange Hola predeterminado ASCS de too31 00, necesita cambios de hello toomake para todos los puertos enumerados en la tabla 1.</span><span class="sxs-lookup"><span data-stu-id="39a27-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="39a27-694">A continuación, se muestra un ejemplo de una actualización para el puerto *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="39a27-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Cambiar las reglas para el equilibrador de carga interno de Azure Hola de equilibrio de carga de predeterminado de hello ASCS/SCS][sap-ha-guide-figure-3005]

  <span data-ttu-id="39a27-696">_**Figura 16:** cambio Hola ASCS/SCS predeterminado equilibrar las reglas para el equilibrador de carga interno de Azure Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="39a27-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Agregar dominio de toohello de máquinas virtuales de Windows</span><span class="sxs-lookup"><span data-stu-id="39a27-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="39a27-698">Después de asignar un máquinas de virtuales de toohello de dirección IP estática, agregar dominio toohello de hello máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="39a27-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Figura 17: Agregar un dominio de tooa de máquina virtual][sap-ha-guide-figure-3006]

<span data-ttu-id="39a27-700">_**Figura 17:** agregar un dominio de tooa de máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="39a27-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="39a27-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Agregar entradas del registro en ambos nodos del clúster de instancia de SAP ASCS/SCS Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="39a27-702">Equilibrador de carga de Azure tiene un equilibrador de carga interno que se cierra conexiones cuando las conexiones de hello están inactivas durante un determinado intervalo de tiempo (un tiempo de inactividad).</span><span class="sxs-lookup"><span data-stu-id="39a27-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="39a27-703">Procesos de trabajo SAP en el cuadro de diálogo instancias conexiones abiertas toohello SAP enqueue procesan tan pronto como Hola primera enqueue y dequeue solicitar toobe necesidades enviado.</span><span class="sxs-lookup"><span data-stu-id="39a27-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="39a27-704">Estas conexiones normalmente permanecen establecidas hasta que el proceso de trabajo de Hola o reinicios del proceso de poner en cola Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="39a27-705">Sin embargo, si conexión Hola está inactivo durante un período de tiempo establecido, Hola conexiones Hola de carga interno de Azure equilibrador se cierra.</span><span class="sxs-lookup"><span data-stu-id="39a27-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="39a27-706">Esto no es un problema porque Hola proceso de trabajo SAP restablece el proceso de poner en cola de hello conexión toohello si ya no existe.</span><span class="sxs-lookup"><span data-stu-id="39a27-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="39a27-707">Estas actividades se documentan en los seguimientos de desarrollador de Hola de procesos SAP, pero crean una gran cantidad de contenido adicional en los seguimientos.</span><span class="sxs-lookup"><span data-stu-id="39a27-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="39a27-708">Es un Hola de toochange buena idea TCP/IP `KeepAliveTime` y `KeepAliveInterval` en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="39a27-709">Combinar estos cambios en los parámetros de TCP/IP Hola con parámetros de perfil SAP, que se describe más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="39a27-710">las entradas del registro de tooadd en ambos nodos del clúster de instancia de SAP ASCS/SCS de hello, en primer lugar, agregan estas entradas del registro de Windows en ambos nodos de clúster de Windows para SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="39a27-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="39a27-711">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="39a27-711">Path</span></span> | <span data-ttu-id="39a27-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="39a27-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="39a27-713">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="39a27-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="39a27-714">Tipo de variable</span><span class="sxs-lookup"><span data-stu-id="39a27-714">Variable type</span></span> |<span data-ttu-id="39a27-715">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="39a27-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="39a27-716">Valor</span><span class="sxs-lookup"><span data-stu-id="39a27-716">Value</span></span> |<span data-ttu-id="39a27-717">120000</span><span class="sxs-lookup"><span data-stu-id="39a27-717">120000</span></span> |
| <span data-ttu-id="39a27-718">Vínculo toodocumentation</span><span class="sxs-lookup"><span data-stu-id="39a27-718">Link toodocumentation</span></span> |[<span data-ttu-id="39a27-719">https://technet.microsoft.com/es-es/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="39a27-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="39a27-720">_**Tabla 3:** cambio Hola TCP/IP primero_</span><span class="sxs-lookup"><span data-stu-id="39a27-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="39a27-721">Luego, agregue estas entradas del Registro de Windows en los nodos de clúster de Windows para ASCS/SCS de SAP:</span><span class="sxs-lookup"><span data-stu-id="39a27-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="39a27-722">path</span><span class="sxs-lookup"><span data-stu-id="39a27-722">Path</span></span> | <span data-ttu-id="39a27-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="39a27-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="39a27-724">Nombre de la variable</span><span class="sxs-lookup"><span data-stu-id="39a27-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="39a27-725">Tipo de variable</span><span class="sxs-lookup"><span data-stu-id="39a27-725">Variable type</span></span> |<span data-ttu-id="39a27-726">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="39a27-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="39a27-727">Valor</span><span class="sxs-lookup"><span data-stu-id="39a27-727">Value</span></span> |<span data-ttu-id="39a27-728">120000</span><span class="sxs-lookup"><span data-stu-id="39a27-728">120000</span></span> |
| <span data-ttu-id="39a27-729">Vínculo toodocumentation</span><span class="sxs-lookup"><span data-stu-id="39a27-729">Link toodocumentation</span></span> |[<span data-ttu-id="39a27-730">https://technet.microsoft.com/es-es/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="39a27-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="39a27-731">_**Tabla 4:** parámetro cambio Hola de segundo TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="39a27-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="39a27-732">**los cambios de hello tooapply, reinicie ambos nodos de clúster**.</span><span class="sxs-lookup"><span data-stu-id="39a27-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="39a27-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configuración del clúster de Clústeres de conmutación por error de Windows para la instancia de ASCS/SCS de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="39a27-734">Para configurar el clúster de Clústeres de conmutación por error de Windows para la instancia de ASCS/SCS de SAP, hay que realizar estas tareas:</span><span class="sxs-lookup"><span data-stu-id="39a27-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="39a27-735">Recopilación de nodos de clúster de hello en una configuración de clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="39a27-736">Configuración de un testigo de recurso compartido de archivos de clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="39a27-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Recopilar los nodos de clúster de hello en una configuración de clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="39a27-738">Hola Add Role y Asistente para características, agregar tooboth nodos del clúster de agrupación en clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="39a27-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="39a27-739">Configurar el clúster de conmutación por error de hello mediante el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="39a27-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="39a27-740">En el Administrador de clústeres de conmutación por error, seleccione **crear clúster**y, a continuación, agregue solo Hola nombre del primer clúster hello, nodo A. No agregue el segundo nodo de hello aún; podrá agregar Hola segundo nodo en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="39a27-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Figura 18: Agregar servidor de Hola o un nombre de máquina virtual del primer nodo del clúster Hola][sap-ha-guide-figure-3007]

  <span data-ttu-id="39a27-742">_**Figura 18:** los nombre de servidor o una máquina virtual de hello agregar del primer nodo del clúster Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="39a27-743">Escriba el nombre de red de hello (nombre de host virtual) de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Figura 19: Escriba el nombre del clúster de Hola][sap-ha-guide-figure-3008]

  <span data-ttu-id="39a27-745">_**Figura 19:** escriba el nombre de clúster de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="39a27-746">Después de crear el clúster de hello, ejecute una prueba de validación de clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Figura 20: Ejecutar la comprobación de validación de clúster de Hola][sap-ha-guide-figure-3009]

  <span data-ttu-id="39a27-748">_**Figura 20:** Ejecutar comprobación de validación de clúster de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="39a27-749">Puede pasar por alto las advertencias acerca de los discos en este momento en el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="39a27-750">Podrá agregar que un recurso compartido de archivos y Hola SIOS discos comparten más adelante.</span><span class="sxs-lookup"><span data-stu-id="39a27-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="39a27-751">En esta fase, no es necesario tooworry relacionado con un quórum.</span><span class="sxs-lookup"><span data-stu-id="39a27-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Figura 21: No se encuentra disco de cuórum][sap-ha-guide-figure-3010]

  <span data-ttu-id="39a27-753">_**Figura 21:** No se encuentra disco de cuórum_</span><span class="sxs-lookup"><span data-stu-id="39a27-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: El recurso de clúster principal necesita una dirección IP nueva][sap-ha-guide-figure-3011]

  <span data-ttu-id="39a27-755">_**Figura 22:** El recurso de clúster principal necesita una dirección IP nueva_</span><span class="sxs-lookup"><span data-stu-id="39a27-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="39a27-756">Cambiar la dirección IP de hello del servicio de cluster Server core Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="39a27-757">clúster de Hello no se iniciará hasta que cambie la dirección IP de hello del servicio de Cluster Server core de hello, como dirección IP de saludo del servidor de hello apunta tooone de nodos de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="39a27-758">Hacer esto en hello **propiedades** página del recurso IP del servicio de Cluster Server de hello core.</span><span class="sxs-lookup"><span data-stu-id="39a27-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="39a27-759">Por ejemplo, necesitamos tooassign una dirección IP (en nuestro ejemplo, **10.0.0.42**) para el nombre de host virtual del clúster de hello **pr1-ascs-EE.**.</span><span class="sxs-lookup"><span data-stu-id="39a27-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figura 23: En el cuadro de diálogo de propiedades de hello, cambiar la dirección IP de Hola][sap-ha-guide-figure-3012]

  <span data-ttu-id="39a27-761">_**Figura 23:** en hello **propiedades** cuadro de diálogo, cambiar dirección IP de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Figura 24: Asignar dirección IP de Hola que está reservado para el clúster de Hola][sap-ha-guide-figure-3013]

  <span data-ttu-id="39a27-763">_**Figura 24:** asignar dirección IP de Hola que está reservado para el clúster de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="39a27-764">Ponga el nombre de host virtual de clúster de hello en línea.</span><span class="sxs-lookup"><span data-stu-id="39a27-764">Bring hello cluster virtual host name online.</span></span>

  ![Figura 25: Servicio de Cluster Server core está activo y ejecutándose y con hello corrija la dirección IP][sap-ha-guide-figure-3014]

  <span data-ttu-id="39a27-766">_**Figura 25:** servicio de clúster principal está activo y en ejecución y con hello corrija la dirección IP_</span><span class="sxs-lookup"><span data-stu-id="39a27-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="39a27-767">Agregue el segundo nodo de clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="39a27-768">Ahora que el servicio de Cluster Server core de hello está en funcionamiento, puede agregar el segundo nodo de clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Ilustración 26: Agregar Hola segundo nodo de clúster][sap-ha-guide-figure-3015]

  <span data-ttu-id="39a27-770">_**Ilustración 26:** segundo nodo de clúster de agregar Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="39a27-771">Escriba un nombre de host del nodo de clúster segundo Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-771">Enter a name for hello second cluster node host.</span></span>

  ![Figura 27: Escriba el nombre de host de nodo de segundo clúster de Hola][sap-ha-guide-figure-3016]

  <span data-ttu-id="39a27-773">_**Figura 27:** ENTRAR Hola segundo clúster host nombre de nodo_</span><span class="sxs-lookup"><span data-stu-id="39a27-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="39a27-774">Asegúrese de que hello **agregar todo el almacenamiento apto toohello clúster** casilla de verificación está **no** seleccionado.</span><span class="sxs-lookup"><span data-stu-id="39a27-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: No seleccione la casilla de verificación de Hola][sap-ha-guide-figure-3017]

  <span data-ttu-id="39a27-776">_**Figura 28:** hacer **no** seleccione Hola casilla de verificación_</span><span class="sxs-lookup"><span data-stu-id="39a27-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="39a27-777">Puede pasar por alto las advertencias sobre el cuórum y los discos.</span><span class="sxs-lookup"><span data-stu-id="39a27-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="39a27-778">Se configuran Hola quórum y recurso compartido de hello el disco de una versión posterior, como se describe en [instalar SIOS DataKeeper Cluster Edition para el disco del recurso compartido de clúster de SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="39a27-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Ignorar las advertencias sobre el quórum de disco Hola][sap-ha-guide-figure-3018]

  <span data-ttu-id="39a27-780">_**Figura 29:** ignorar las advertencias sobre el quórum de disco Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="39a27-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configuración de un testigo de recurso compartido de archivos de clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="39a27-782">Para configurar un testigo de recurso compartido de archivos de clúster, hay que realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="39a27-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="39a27-783">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="39a27-783">Creating a file share</span></span>
- <span data-ttu-id="39a27-784">Configuración de quórum de testigo de recurso compartido de archivos de hello en el Administrador de clústeres de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="39a27-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="39a27-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="39a27-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="39a27-786">Seleccione un testigo de recurso de archivos en lugar de un disco de cuórum.</span><span class="sxs-lookup"><span data-stu-id="39a27-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="39a27-787">SIOS DataKeeper admite esta opción.</span><span class="sxs-lookup"><span data-stu-id="39a27-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="39a27-788">En los ejemplos de hello en este artículo, Hola testigo de recurso compartido de archivos está en hello Active Directory o servidor DNS que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="39a27-789">Hello testigo de recurso compartido de archivo se denomina **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="39a27-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="39a27-790">Dado que habría configuró un tooAzure de conexión VPN (a través de VPN de sitio a sitio o ExpressRoute de Azure), su Active Directory/DNS service es local y no es adecuado toorun un archivo de testigo de recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="39a27-791">Si el servicio de Active Directory/DNS ejecuta solo en local, no configure el testigo de recurso compartido de archivo hello Active Directory y DNS en sistemas operativos en que se ejecuta en local.</span><span class="sxs-lookup"><span data-stu-id="39a27-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="39a27-792">La latencia de red entre los nodos de clúster que se ejecutan en Azure y Active Directory/DNS local puede ser demasiado grande y provocar problemas de conectividad.</span><span class="sxs-lookup"><span data-stu-id="39a27-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="39a27-793">Ser seguro tooconfigure Hola archivo testigo de recurso compartido en una máquina virtual de Azure que está ejecutando el nodo del clúster toohello cerrar.</span><span class="sxs-lookup"><span data-stu-id="39a27-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="39a27-794">unidad de quórum de Hello necesita al menos 1024 MB de espacio libre.</span><span class="sxs-lookup"><span data-stu-id="39a27-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="39a27-795">Se recomienda 2.048 MB de espacio libre para la unidad de quórum de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="39a27-796">Agregue el objeto de nombre de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-796">Add hello cluster name object.</span></span>

  ![Figura 30: Asignar permisos de hello en recurso compartido de hello para el objeto de nombre de clúster de Hola][sap-ha-guide-figure-3019]

  <span data-ttu-id="39a27-798">_**Figura 30:** asignar permisos de hello en el recurso compartido de hello para el objeto de nombre de clúster de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="39a27-799">Asegúrese de que los permisos de hello incluyen datos de la CA toochange hello en recurso compartido de hello para el objeto de nombre de clúster de hello (en nuestro ejemplo, **pr1-ascs-EE. $**).</span><span class="sxs-lookup"><span data-stu-id="39a27-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="39a27-800">tooadd Hola clúster nombre toohello lista de objetos, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="39a27-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="39a27-801">Cambiar hello toocheck de filtro para los objetos de equipo, en toothose de suma que se muestra en la figura 31.</span><span class="sxs-lookup"><span data-stu-id="39a27-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Figura 31: Cambia los equipos de tooinclude de tipos de objeto de Hola][sap-ha-guide-figure-3020]

  <span data-ttu-id="39a27-803">_**Figura 31:** cambia los equipos de tooinclude de tipos de objeto de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Figura 32: Active la casilla de verificación de los equipos de Hola][sap-ha-guide-figure-3021]

  <span data-ttu-id="39a27-805">_**Figura 32:** Hola seleccione **equipos** casilla de verificación_</span><span class="sxs-lookup"><span data-stu-id="39a27-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="39a27-806">Especifique el objeto de nombre de clúster de hello tal y como se muestra en la figura 31.</span><span class="sxs-lookup"><span data-stu-id="39a27-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="39a27-807">Porque ya se ha creado el registro de hello, puede cambiar los permisos de hello, tal como se muestra en la figura 30.</span><span class="sxs-lookup"><span data-stu-id="39a27-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="39a27-808">Seleccione hello **seguridad** ficha del recurso compartido de hello y, después, establezca más detallados permisos de objeto de nombre de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Figura 33: Establecer atributos de seguridad de hello para el objeto de nombre de clúster de hello en el quórum de recurso compartido de archivos de Hola][sap-ha-guide-figure-3022]

  <span data-ttu-id="39a27-810">_**Figura 33:** establecer atributos de seguridad de hello para el objeto de nombre de clúster de hello en el quórum de recurso compartido de archivos de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="39a27-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Establecer en el Administrador de clústeres de conmutación por error de quórum de testigo de recurso compartido de archivos de Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="39a27-812">Abra Hola Asistente de configuración de quórum de configuración.</span><span class="sxs-lookup"><span data-stu-id="39a27-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Figura 34: Hola Asistente de configuración de quórum de clúster de configuración de inicio][sap-ha-guide-figure-3023]

  <span data-ttu-id="39a27-814">_**Figura 34:** inicio Hola configurar Asistente de configuración de quórum de clúster_</span><span class="sxs-lookup"><span data-stu-id="39a27-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="39a27-815">En hello **Seleccionar configuración de quórum** , seleccione **seleccionar testigo de quórum de hello**.</span><span class="sxs-lookup"><span data-stu-id="39a27-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Figura 35: Configuraciones de cuórum que puede elegir][sap-ha-guide-figure-3024]

  <span data-ttu-id="39a27-817">_**Figura 35:** Configuraciones de cuórum que puede elegir_</span><span class="sxs-lookup"><span data-stu-id="39a27-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="39a27-818">En hello **seleccionar testigo de quórum** , seleccione **configurar un testigo de recurso compartido de archivos**.</span><span class="sxs-lookup"><span data-stu-id="39a27-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figura 36: Testigo de recurso compartido de archivo Hola Select][sap-ha-guide-figure-3025]

  <span data-ttu-id="39a27-820">_**Figura 36:** seleccionar testigo de recurso compartido de archivos de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="39a27-821">Escriba Hola ruta de acceso toohello recurso compartido UNC (en nuestro ejemplo, \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="39a27-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="39a27-822">una lista de cambios de Hola que puede realizar, seleccione toosee **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="39a27-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Figura 37: Definir la ubicación del recurso compartido de archivo hello para el recurso compartido de testigo de Hola][sap-ha-guide-figure-3026]

  <span data-ttu-id="39a27-824">_**Figura 37:** definir la ubicación del recurso compartido de archivo hello para el recurso compartido de testigo de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="39a27-825">Seleccione Hola cambios que desee y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="39a27-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="39a27-826">Necesita toosuccessfully volver a configurar la configuración de clúster de hello tal como se muestra en la figura 38.</span><span class="sxs-lookup"><span data-stu-id="39a27-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Figura 38: Confirmación que ha configurado de nuevo clúster Hola][sap-ha-guide-figure-3027]

  <span data-ttu-id="39a27-828">_**Figura 38:** confirmación de que ha configurado de nuevo clúster Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="39a27-829">Después de instalar correctamente el clúster de conmutación por error de Windows hello, cambios necesitan toobe realizado tooconditions de detección de conmutación por error de toosome umbrales tooadapt en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="39a27-830">Hello toobe parámetros cambiado documentados en este blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="39a27-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="39a27-831">Si damos por hecho que los dos máquinas virtuales que generar Hola configuración de clúster de Windows para ASCS/SCS están en Hola misma subred, los parámetros siguientes hello necesitan toobe cambiado toothese valores:</span><span class="sxs-lookup"><span data-stu-id="39a27-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="39a27-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="39a27-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="39a27-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="39a27-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="39a27-834">Esta configuración se han probado con los clientes y proporciona un toobe buen compromiso suficientemente resistente en el lado "uno" Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="39a27-835">En hello otra parte dicha configuración proporciona rápido suficiente conmutación por error en las condiciones de error real en caso de error de software o nodo/VM de SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="39a27-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Instalar SIOS DataKeeper Cluster Edition para el disco del recurso compartido de clúster de hello SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="39a27-837">Ahora tiene una configuración de Clústeres de conmutación por error de Windows Server activa en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="39a27-838">Pero, tooinstall una instancia de SAP ASCS/SCS, necesita un recurso de disco compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="39a27-839">No se puede crear recursos de disco de Hola compartido que necesita en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="39a27-840">SIOS DataKeeper Cluster Edition es una solución de terceros pueden usar recursos de disco de toocreate compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="39a27-841">Instalar SIOS DataKeeper Cluster Edition para hello SAP ASCS/SCS disco del recurso compartido de clúster implica estas tareas:</span><span class="sxs-lookup"><span data-stu-id="39a27-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="39a27-842">Agregar Hola .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="39a27-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="39a27-843">Instalación de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="39a27-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="39a27-844">Configuración de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="39a27-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="39a27-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Agregar Hola .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="39a27-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="39a27-846">Hola Microsoft .NET Framework 3.5 automáticamente no está activado o instalado en Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="39a27-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="39a27-847">Dado que SIOS DataKeeper requiere toobe de .NET Framework de hello en todos los nodos que se instala DataKeeper en, debe instalar Hola .NET Framework 3.5 en hello sistema operativo de todas las máquinas virtuales en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="39a27-848">Hay dos Hola de tooadd maneras .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="39a27-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="39a27-849">Utilice Hola agregar Roles y características de Asistente de Windows como se muestra en la Figura 39.</span><span class="sxs-lookup"><span data-stu-id="39a27-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Instalar Hola .NET Framework 3.5 mediante Hola agregar Roles y características de Asistente][sap-ha-guide-figure-3028]

  <span data-ttu-id="39a27-851">_**Figura 39:** Hola de instalar .NET Framework 3.5 mediante el uso de hello agregar Roles y características de Asistente_</span><span class="sxs-lookup"><span data-stu-id="39a27-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![La figura 40: Progreso de la instalación barra cuando instala Hola .NET Framework 3.5 mediante el uso de hello agregar Roles y características de Asistente][sap-ha-guide-figure-3029]

  <span data-ttu-id="39a27-853">_**Figura 40:** barra cuando instala Hola .NET Framework 3.5 mediante el uso de hello agregar Roles y características de Asistente de progreso de instalación_</span><span class="sxs-lookup"><span data-stu-id="39a27-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="39a27-854">Usar dism.exe de la herramienta de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="39a27-855">Para este tipo de instalación, deberá directorio tooaccess Hola SxS Hola medios de instalación de Windows.</span><span class="sxs-lookup"><span data-stu-id="39a27-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="39a27-856">En un símbolo del sistema con privilegios elevados, escriba:</span><span class="sxs-lookup"><span data-stu-id="39a27-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="39a27-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Instalación de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="39a27-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="39a27-858">Instale SIOS DataKeeper Cluster Edition en cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="39a27-859">almacenamiento compartido virtual de toocreate con SIOS DataKeeper, crear un espejo sincronizado y, a continuación, simular almacenamiento compartido de clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="39a27-860">Antes de instalar software SIOS hello, cree el usuario del dominio de hello **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="39a27-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-861">Agregar hello **DataKeeperSvc** usuario toohello **administrador Local** grupo en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="39a27-862">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="39a27-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="39a27-863">Instalar software SIOS hello en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![Instalador de SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: La primera página de hello instalación SIOS DataKeeper][sap-ha-guide-figure-3031]

  <span data-ttu-id="39a27-866">_**Figura 41:** primera página de hello instalación SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="39a27-867">En el cuadro de diálogo de Hola se muestra en la Figura 42, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="39a27-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: DataKeeper le informa que se deshabilitará un servicio][sap-ha-guide-figure-3032]

  <span data-ttu-id="39a27-869">_**Figura 42:** DataKeeper le informa que se deshabilitará un servicio_</span><span class="sxs-lookup"><span data-stu-id="39a27-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="39a27-870">En el cuadro de diálogo de Hola se muestra en figura 43, le recomendamos que seleccione **cuenta de dominio o servidor**.</span><span class="sxs-lookup"><span data-stu-id="39a27-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Selección del usuario para SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="39a27-872">_**Figura 43:** Selección del usuario para SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="39a27-873">Escriba el nombre de usuario de cuenta de dominio de Hola y las contraseñas que ha creado para SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="39a27-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Escriba nombre de usuario de dominio de hello y una contraseña para hello instalación SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="39a27-875">_**Figura 44:** escriba nombre de usuario de dominio de hello y una contraseña para hello instalación SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="39a27-876">Instale la clave de licencia de hello para la instancia de SIOS DataKeeper tal y como se muestra en figura 45.</span><span class="sxs-lookup"><span data-stu-id="39a27-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: Ingreso de la licencia de SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="39a27-878">_**Figura 45:** Especificación de la licencia de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="39a27-879">Cuando se le solicite, reinicie la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="39a27-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configuración de SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="39a27-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="39a27-881">Después de instalar SIOS DataKeeper en ambos nodos, necesita una configuración toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="39a27-882">objetivo de Hola de configuración de hello es toohave la replicación de datos sincrónica entre hello tooeach de discos duros virtuales conectados adicional de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="39a27-883">Inicie hello DataKeeper administración y herramienta de configuración y, a continuación, seleccione **conectar servidor**.</span><span class="sxs-lookup"><span data-stu-id="39a27-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="39a27-884">(En la figura 46, esta opción aparece rodeada de un círculo de color rojo).</span><span class="sxs-lookup"><span data-stu-id="39a27-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Herramienta de configuración y administración de SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="39a27-886">_**Figura 46:** Herramienta de configuración y administración de SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="39a27-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="39a27-887">Escriba el nombre de Hola o dirección TCP/IP de hello primer nodo Hola administración herramienta de configuración y debe conectarse a y, en una segunda fase, el segundo nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Figura 47: Nombre de Hola de inserción o la dirección de TCP/IP de hello primer nodo Hola administración herramienta de configuración y debe conectarse a y en un segundo paso, el segundo nodo de Hola][sap-ha-guide-figure-3037]

  <span data-ttu-id="39a27-889">_**Figura 47:** nombre de Hola de inserción o la dirección de TCP/IP de hello primer nodo Hola administración herramienta de configuración y debe conectarse a y en un segundo paso, el segundo nodo de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="39a27-890">Crear trabajo de replicación de hello entre dos nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-890">Create hello replication job between hello two nodes.</span></span>

  ![Figura 48: Creación de un trabajo de replicación][sap-ha-guide-figure-3038]

  <span data-ttu-id="39a27-892">_**Figura 48:** Creación de un trabajo de replicación_</span><span class="sxs-lookup"><span data-stu-id="39a27-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="39a27-893">Un asistente le guía a través del proceso de Hola de creación de un trabajo de replicación.</span><span class="sxs-lookup"><span data-stu-id="39a27-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="39a27-894">Definir nombre de hello, la dirección TCP/IP y el volumen de disco Hola del nodo de origen.</span><span class="sxs-lookup"><span data-stu-id="39a27-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Figura 49: Definir nombre de Hola de trabajo de replicación de Hola][sap-ha-guide-figure-3039]

  <span data-ttu-id="39a27-896">_**Figura 49:** Definir nombre de Hola de trabajo de replicación de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Figura 50: Definir datos de base de Hola de nodo de hello, que debe ser el nodo de origen actual de Hola][sap-ha-guide-figure-3040]

  <span data-ttu-id="39a27-898">_**Figura 50:** definir datos de base de Hola de nodo de hello, que debe ser el nodo de origen actual de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="39a27-899">Definir nombre hello, dirección TCP/IP y el volumen de disco de nodo de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Figura 51: Definir datos de base de Hola de nodo de hello, que debe ser el nodo de destino actual de Hola][sap-ha-guide-figure-3041]

  <span data-ttu-id="39a27-901">_**Figura 51:** definir datos de base de Hola de nodo de hello, que debe ser el nodo de destino actual de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="39a27-902">Definir los algoritmos de compresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-902">Define hello compression algorithms.</span></span> <span data-ttu-id="39a27-903">En nuestro ejemplo, le recomendamos que comprima el flujo de replicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="39a27-904">Especialmente en situaciones de resincronización, compresión de Hola de flujo de replicación de hello reduce considerablemente el tiempo de resincronización.</span><span class="sxs-lookup"><span data-stu-id="39a27-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="39a27-905">Tenga en cuenta que la compresión utiliza recursos de CPU y RAM Hola de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="39a27-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="39a27-906">A medida que aumenta la velocidad de compresión de hello, por lo que Hola volumen de recursos de CPU que se usa.</span><span class="sxs-lookup"><span data-stu-id="39a27-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="39a27-907">También puede ajustar esta configuración más adelante.</span><span class="sxs-lookup"><span data-stu-id="39a27-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="39a27-908">Otra configuración necesita toocheck es si se produce la replicación Hola sincrónica o asincrónica.</span><span class="sxs-lookup"><span data-stu-id="39a27-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="39a27-909">*Cuando proteja las configuraciones de ASCS/SCS de SAP, debe usar la replicación sincrónica*.</span><span class="sxs-lookup"><span data-stu-id="39a27-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definición de los detalles de la replicación][sap-ha-guide-figure-3042]

  <span data-ttu-id="39a27-911">_**Figura 52:** Definición de los detalles de la replicación_</span><span class="sxs-lookup"><span data-stu-id="39a27-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="39a27-912">Definir si volumen Hola que se replica mediante replicación Hola debe ser la configuración de clúster de clústeres de conmutación por error de Windows Server de tooa representado como un disco compartido.</span><span class="sxs-lookup"><span data-stu-id="39a27-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="39a27-913">Para la configuración de SAP ASCS/SCS de hello, seleccione **Sí** para que Windows hello clúster ve Hola replicada volumen como un disco compartido que puede usar como un volumen de clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: Seleccione la opción Sí tooset Hola replica volumen como un volumen de clúster][sap-ha-guide-figure-3043]

  <span data-ttu-id="39a27-915">_**Figura 53:** seleccione **Sí** tooset Hola replica volumen como volumen de clúster_</span><span class="sxs-lookup"><span data-stu-id="39a27-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="39a27-916">Después de crea el volumen de hello, herramienta de configuración y administración de DataKeeper de hello muestra que ese trabajo de replicación Hola está activo.</span><span class="sxs-lookup"><span data-stu-id="39a27-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Figura 54: DataKeeper sincrónica creación de reflejo de disco del recurso compartido de SAP ASCS/SCS Hola está activo][sap-ha-guide-figure-3044]

  <span data-ttu-id="39a27-918">_**Figura 54:** DataKeeper creación de reflejos sincrónica para SAP ASCS/SCS hello compartir disco está activo_</span><span class="sxs-lookup"><span data-stu-id="39a27-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="39a27-919">El Administrador de clústeres de conmutación por error muestra ahora disco Hola como un disco DataKeeper, tal como se muestra en la figura 55.</span><span class="sxs-lookup"><span data-stu-id="39a27-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: Muestra el Administrador de clústeres de conmutación por error de disco Hola que replican DataKeeper][sap-ha-guide-figure-3045]

  <span data-ttu-id="39a27-921">_**Figura 55:** Administrador de clústeres de conmutación por error muestra disco Hola ese DataKeeper replicado_</span><span class="sxs-lookup"><span data-stu-id="39a27-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="39a27-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalar el sistema de SAP NetWeaver Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="39a27-923">No describimos el programa de instalación DBMS de hello porque configuraciones varían en función hello sistema DBMS que use.</span><span class="sxs-lookup"><span data-stu-id="39a27-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="39a27-924">Sin embargo, se supone que se solucionan los problemas de alta disponibilidad con hello DBMS con funcionalidades de hello admiten distintos proveedores DBMS Hola de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="39a27-925">Por ejemplo, AlwaysOn o creación de reflejo de la base de datos para SQL Server y Oracle Data Guard para Oracle.</span><span class="sxs-lookup"><span data-stu-id="39a27-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="39a27-926">En el escenario de Hola que se usa en este artículo, no agregamos más protección toohello DBMS.</span><span class="sxs-lookup"><span data-stu-id="39a27-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="39a27-927">No hay ninguna consideración especial cuando distintos servicios de DBMS interactúan con esta variante de configuración de ASCS/SCS de SAP en clúster en Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-928">procedimientos de instalación de Hola de sistemas de ABAP de SAP NetWeaver, sistemas de Java y sistemas ABAP + Java son casi idénticos.</span><span class="sxs-lookup"><span data-stu-id="39a27-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="39a27-929">diferencia más importante de Hello es que un sistema SAP ABAP tiene una instancia ASCS.</span><span class="sxs-lookup"><span data-stu-id="39a27-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="39a27-930">Hola sistema SAP Java tiene una instancia SCS.</span><span class="sxs-lookup"><span data-stu-id="39a27-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="39a27-931">Hola sistema SAP ABAP + Java tiene una instancia ASCS y ejecuta en una instancia SCS Hola mismo grupo de clústeres de conmutación por error de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="39a27-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="39a27-932">Cualquier diferencia de instalación de cada pila de instalación de SAP NetWeaver se menciona explícitamente.</span><span class="sxs-lookup"><span data-stu-id="39a27-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="39a27-933">Se puede suponer que se Hola a todos los demás elementos iguales.</span><span class="sxs-lookup"><span data-stu-id="39a27-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="39a27-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Instalación de SAP con una instancia de ASCS/SCS de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="39a27-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39a27-935">Asegúrese de no tooplace la página de archivos en DataKeeper volúmenes reflejados.</span><span class="sxs-lookup"><span data-stu-id="39a27-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="39a27-936">DataKeeper no admite los volúmenes reflejados.</span><span class="sxs-lookup"><span data-stu-id="39a27-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="39a27-937">Puede dejar el archivo de paginación en la unidad temporal de hello D de una máquina virtual de Azure, que es el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="39a27-938">Si aún no está allí, mueva Hola Windows página archivo toodrive D de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="39a27-939">Para instalar SAP con una instancia de ASCS/SCS de alta disponibilidad, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="39a27-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="39a27-940">Crear un nombre de host virtual para la instancia de SAP ASCS/SCS de hello en clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="39a27-941">Instalar el primer nodo de clúster de hello SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="39a27-942">Modificar perfil de SAP de Hola de instancia de hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="39a27-943">Incorporación de un puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="39a27-943">Adding a probe port</span></span>
- <span data-ttu-id="39a27-944">Abrir el puerto de sondeo de firewall de Windows hello</span><span class="sxs-lookup"><span data-stu-id="39a27-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="39a27-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Crear un nombre de host virtual para la instancia de SAP ASCS/SCS de hello en clúster</span><span class="sxs-lookup"><span data-stu-id="39a27-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="39a27-946">En el Administrador de DNS de Windows hello, cree una entrada DNS para el nombre de host virtual Hola de instancia de hello ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="39a27-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="39a27-947">Hello dirección IP que asigna el nombre de host virtual toohello de hello ASCS/SCS instancia debe ser Hola igual como dirección IP de Hola que asigna tooAzure equilibrador de carga (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="39a27-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="39a27-948">Hola dirección IP del nombre de host de SAP ASCS/SCS virtual hello (**pr1-ascs-sap**) Hola igual como dirección IP de hello del equilibrador de carga de Azure (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="39a27-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definir la entrada DNS de hello para el nombre virtual del clúster de SAP ASCS/SCS hello y dirección TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="39a27-950">_**Figura 56:** definir Hola entrada DNS para el nombre virtual del clúster de SAP ASCS/SCS hello y una dirección TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="39a27-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="39a27-951">toodefine Hola IP dirección asignada toohello nombre de host virtual, seleccione **el Administrador de DNS** > **dominio**.</span><span class="sxs-lookup"><span data-stu-id="39a27-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Nuevo nombre virtual y dirección TCP/IP para la configuración del clúster de ASCS/SCS de SAP][sap-ha-guide-figure-3047]

  <span data-ttu-id="39a27-953">_**Figura 57:** Nuevo nombre virtual y dirección TCP/IP para la configuración del clúster de ASCS/SCS de SAP_</span><span class="sxs-lookup"><span data-stu-id="39a27-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="39a27-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Instalar el primer nodo de clúster de hello SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="39a27-955">Ejecutar Hola primera opción de nodo de clúster en el nodo de clúster a Por ejemplo, en hello **pr1-ascs-0** host.</span><span class="sxs-lookup"><span data-stu-id="39a27-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="39a27-956">puertos predeterminados que hello tookeep para hello Azure interno equilibrador de carga, seleccione:</span><span class="sxs-lookup"><span data-stu-id="39a27-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="39a27-957">**Sistema ABAP**: número de instancia de **ASCS****00**</span><span class="sxs-lookup"><span data-stu-id="39a27-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="39a27-958">**Sistema Java**: número de instancia de **SCS****01**</span><span class="sxs-lookup"><span data-stu-id="39a27-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="39a27-959">**Sistema ABAP+Java**: número de instancia de **ASCS****00** y número de instancia de **SCS****01**</span><span class="sxs-lookup"><span data-stu-id="39a27-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="39a27-960">instancia de toouse números distinto de 00 para hello ABAP ASCS 01 para la instancia de Java SCS de Hola e instancia, en primer lugar debe toochange Hola carga interno de Azure equilibrador predeterminado equilibrio de carga, se describe en [carga predeterminada de cambio Hola ASCS/SCS reglas para el equilibrador de carga interno de Azure Hola de equilibrio][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="39a27-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="39a27-961">Hello siguientes algunas tareas no se describen en la documentación de instalación de SAP estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-962">Hola documentación de la instalación de SAP describe cómo tooinstall Hola primer nodo del clúster ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="39a27-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="39a27-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificar perfil SAP de Hola de instancia de hello ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="39a27-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="39a27-964">Deberá tooadd un nuevo parámetro de perfil.</span><span class="sxs-lookup"><span data-stu-id="39a27-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="39a27-965">parámetro del perfil Hola evita que las conexiones entre los procesos de trabajo SAP y el servidor de poner en cola Hola cierre cuando están inactivos durante demasiado tiempo.</span><span class="sxs-lookup"><span data-stu-id="39a27-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="39a27-966">Hemos mencionado escenario de problema de hello en [agregar entradas del registro en ambos nodos del clúster de instancia de SAP ASCS/SCS de hello][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="39a27-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="39a27-967">En esa sección, también presentamos dos cambios toosome básica TCP/IP parámetros de conexión.</span><span class="sxs-lookup"><span data-stu-id="39a27-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="39a27-968">En un segundo paso, necesita tooset Hola enqueue server toosend un `keep_alive` de señal para que las conexiones de hello no supere el umbral de inactividad del equilibrador de carga interno de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="39a27-969">Hola toomodify perfil SAP de instancia ASCS/SCS de hello:</span><span class="sxs-lookup"><span data-stu-id="39a27-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="39a27-970">Agregue este toohello de parámetro perfil de la instancia de SAP ASCS/SCS de perfil:</span><span class="sxs-lookup"><span data-stu-id="39a27-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="39a27-971">En nuestro ejemplo, ruta de acceso de hello es:</span><span class="sxs-lookup"><span data-stu-id="39a27-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="39a27-972">Por ejemplo, perfil de instancia de toohello SCS de SAP y ruta de acceso correspondiente:</span><span class="sxs-lookup"><span data-stu-id="39a27-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="39a27-973">cambios de hello tooapply, reinicie la instancia de SAP ASCS /SCS de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="39a27-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Incorporación de un puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="39a27-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="39a27-975">Use el trabajo de la configuración del equilibrador de carga interno de hello sondeo funcionalidad toomake Hola todo el clúster con el equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="39a27-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="39a27-976">equilibrador de carga interno de Azure Hola normalmente distribuye la carga de trabajo entrante de Hola por igual entre las máquinas virtuales participantes.</span><span class="sxs-lookup"><span data-stu-id="39a27-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="39a27-977">Sin embargo, esto no funcionará en algunas configuraciones de clúster porque solo hay una instancia activa.</span><span class="sxs-lookup"><span data-stu-id="39a27-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="39a27-978">Hola otra instancia es pasivo y no puede aceptar cualquier carga de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="39a27-979">Le ayuda una funcionalidad de sondeo cuando asigna de equilibrador de carga interno de Azure de hello trabajan tooan solo de instancias activas.</span><span class="sxs-lookup"><span data-stu-id="39a27-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="39a27-980">Con la funcionalidad de sondeo de hello, equilibrador de carga interno de hello puede detectar las instancias que están activas y, a continuación, solo el Hola instancia con cargas de trabajo de Hola de destino.</span><span class="sxs-lookup"><span data-stu-id="39a27-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="39a27-981">tooadd un puerto de sondeo:</span><span class="sxs-lookup"><span data-stu-id="39a27-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="39a27-982">Comprobar Hola actual **ProbePort** configuración ejecutando el siguiente comando de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="39a27-983">Ejecutarlo desde dentro de una de las máquinas virtuales de hello en configuración de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="39a27-984">Defina un puerto de sondeo.</span><span class="sxs-lookup"><span data-stu-id="39a27-984">Define a probe port.</span></span> <span data-ttu-id="39a27-985">número de puerto de sondeo de Hello predeterminada es **0**.</span><span class="sxs-lookup"><span data-stu-id="39a27-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="39a27-986">En el ejemplo, se usa el puerto de sondeo **62000**.</span><span class="sxs-lookup"><span data-stu-id="39a27-986">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: puerto de sondeo de configuración de clúster de hello es 0 de forma predeterminada][sap-ha-guide-figure-3048]

  <span data-ttu-id="39a27-988">_**Figura 58:** puerto de sondeo de configuración de clúster de hello predeterminado es 0_</span><span class="sxs-lookup"><span data-stu-id="39a27-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="39a27-989">número de puerto de Hola se define en plantillas de SAP Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39a27-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="39a27-990">Puede asignar el número de puerto de hello en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39a27-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="39a27-991">un nuevo valor de ProbePort para hello tooset  **SAP <*SID*> IP ** recurso de clúster, ejecute el siguiente script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="39a27-992">Actualice las variables de PowerShell de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="39a27-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="39a27-993">Después de ejecutar el script de Hola, podrá toorestart solicitadas Hola SAP clúster grupo tooactivate Hola cambios.</span><span class="sxs-lookup"><span data-stu-id="39a27-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

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
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

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

  <span data-ttu-id="39a27-994">Después de conectar hello  **SAP <*SID*> ** clúster en línea, compruebe que **ProbePort** se establece toohello nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="39a27-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Sondeo de puerto de clúster de hello después de establecer el nuevo valor de Hola][sap-ha-guide-figure-3049]

  <span data-ttu-id="39a27-996">_**Figura 59:** sondeo de puerto de clúster de hello después de establecer el nuevo valor de Hola_</span><span class="sxs-lookup"><span data-stu-id="39a27-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="39a27-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Abra el puerto de sondeo de firewall de Windows hello</span><span class="sxs-lookup"><span data-stu-id="39a27-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="39a27-998">Deberá tooopen un puerto de sondeo de firewall de Windows en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="39a27-999">Usar hello sigue la secuencia de comandos tooopen un puerto de sondeo de firewall de Windows.</span><span class="sxs-lookup"><span data-stu-id="39a27-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="39a27-1000">Actualice las variables de PowerShell de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="39a27-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="39a27-1001">Hola **ProbePort** se establece demasiado**62000**.</span><span class="sxs-lookup"><span data-stu-id="39a27-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="39a27-1002">Ahora puede tener acceso a recurso compartido de archivos de hello  **\\\ascsha-clsap\sapmnt** de otros hosts, tales como from **ascsha DBA**.</span><span class="sxs-lookup"><span data-stu-id="39a27-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="39a27-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Instalar la instancia de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="39a27-1004">base de datos de tooinstall Hola instancia, siga el proceso de hello descrito en hello documentación de la instalación de SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="39a27-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar el segundo nodo de clúster Hola</span><span class="sxs-lookup"><span data-stu-id="39a27-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="39a27-1006">tooinstall Hola segundo clúster, siga los pasos de Hola Hola Guía de instalación de SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="39a27-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Cambiar tipo de inicio de Hola de instancia de servicio de SAP ERS Windows hello</span><span class="sxs-lookup"><span data-stu-id="39a27-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="39a27-1008">Cambiar el tipo de inicio de Hola de hello servicio SAP ERS Windows demasiado**automático (Inicio retrasado)** en ambos nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="39a27-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Cambiar el tipo de servicio de Hola para hello SAP ERS instancia toodelayed automática][sap-ha-guide-figure-3050]

<span data-ttu-id="39a27-1010">_**Figura 60:** cambiar tipo de servicio de Hola de hello SAP ERS instancia toodelayed automática_</span><span class="sxs-lookup"><span data-stu-id="39a27-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="39a27-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Instalar Hola servidor principal de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="39a27-1012">Instalar la instancia de servidor de aplicación principal (PAS) Hola <*SID*> - di - 0 en la máquina virtual de Hola que ha designado toohost Hola PA.</span><span class="sxs-lookup"><span data-stu-id="39a27-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="39a27-1013">No hay ninguna dependencia de Azure ni aspectos específicos de DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="39a27-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="39a27-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalar Hola adicional servidor de aplicaciones SAP</span><span class="sxs-lookup"><span data-stu-id="39a27-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="39a27-1015">Instalar un servidor de aplicación adicionales (AAS) de SAP en todas las máquinas virtuales de Hola que ha designado toohost una instancia de servidor de aplicaciones SAP.</span><span class="sxs-lookup"><span data-stu-id="39a27-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="39a27-1016">Por ejemplo, en <*SID*> - di - 1 demasiado <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="39a27-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="39a27-1017">Esto finaliza la instalación de Hola de un sistema SAP NetWeaver de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="39a27-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="39a27-1018">Después, continúe con las pruebas de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="39a27-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="39a27-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Probar la replicación de SIOS y conmutación por error de hello SAP ASCS/SCS instancia</span><span class="sxs-lookup"><span data-stu-id="39a27-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="39a27-1020">Es fácil tootest y supervisar una instancia de SAP ASCS/SCS conmutación por error y replicación de disco SIOS mediante el Administrador de clústeres de conmutación por error y la herramienta de configuración y administración de SIOS DataKeeper de Hola.</span><span class="sxs-lookup"><span data-stu-id="39a27-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="39a27-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> La instancia de ASCS/SCS de SAP se ejecuta en el nodo de clúster A</span><span class="sxs-lookup"><span data-stu-id="39a27-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="39a27-1022">Hola **PR1 de SAP** grupo de clúster se ejecuta en el nodo de clúster A. Por ejemplo, en **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="39a27-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="39a27-1023">Asignar la unidad de disco de hello compartido S, que forma parte del programa Hola a **PR1 de SAP** grupo de clúster, y qué instancia ASCS/SCS hello usa, toocluster nodo A.</span><span class="sxs-lookup"><span data-stu-id="39a27-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Figura 61: El Administrador de clústeres de conmutación por error: grupo de clústeres SAP < SID > Hola se ejecuta en el nodo de clúster A][sap-ha-guide-figure-5000]

<span data-ttu-id="39a27-1025">_**Figura 61:** Administrador de clústeres de conmutación por error: Hola SAP <*SID*> grupo de clúster se ejecuta en el nodo de clúster A_</span><span class="sxs-lookup"><span data-stu-id="39a27-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="39a27-1026">En hello SIOS DataKeeper administración y herramienta de configuración, puede ver ese disco compartido Hola datos se replican de forma sincrónica de la unidad de volumen de origen Hola S en el nodo de clúster de una unidad de volumen de destino toohello S en el nodo de clúster B. Por ejemplo, se replique desde **pr1-ascs-0 [10.0.0.40]** demasiado**pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="39a27-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: En SIOS DataKeeper, replicar volumen local Hola desde el nodo de clúster un nodo toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="39a27-1028">_**Figura 62:** en DataKeeper de SIOS, replicar volumen local Hola desde el nodo de clúster un nodo toocluster B_</span><span class="sxs-lookup"><span data-stu-id="39a27-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="39a27-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Conmutación por error de nodo A toonode B</span><span class="sxs-lookup"><span data-stu-id="39a27-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="39a27-1030">Elija una de estas opciones tooinitiate una conmutación por error de hello SAP <*SID*> grupo de clúster de nodo de clúster nodo A toocluster B:</span><span class="sxs-lookup"><span data-stu-id="39a27-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="39a27-1031">Uso del Administrador de clústeres de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="39a27-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="39a27-1032">Uso de PowerShell del clúster de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="39a27-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="39a27-1033">Reinicie el nodo de clúster A sistema de operativo de invitado de Windows hello (este comando inicia una conmutación por error automática del programa Hola a SAP <*SID*> grupo de clúster de nodo A toonode B).</span><span class="sxs-lookup"><span data-stu-id="39a27-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="39a27-1034">Reinicie el nodo de clúster A de hello portal de Azure (este comando inicia una conmutación por error automática del programa Hola a SAP <*SID*> grupo de clúster de nodo A toonode B).</span><span class="sxs-lookup"><span data-stu-id="39a27-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="39a27-1035">Reinicie un nodo de clúster mediante el uso de PowerShell de Azure (este comando inicia una conmutación por error automática del programa Hola a SAP <*SID*> grupo de clúster de nodo A toonode B).</span><span class="sxs-lookup"><span data-stu-id="39a27-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="39a27-1036">Después de la conmutación por error, Hola SAP <*SID*> grupo de clúster se ejecuta en el nodo de clúster B. Por ejemplo, se está ejecutando en **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="39a27-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: En el Administrador de clústeres de conmutación por error, grupo de clústeres SAP < SID > Hola se ejecuta en el nodo de clúster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="39a27-1038">_**Figura 63**: conmutación por error de administrador de clústeres de hello SAP <*SID*> grupo de clúster se ejecuta en el nodo de clúster B_</span><span class="sxs-lookup"><span data-stu-id="39a27-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="39a27-1039">Hello disco compartido está ahora montado en clúster de nodo B. SIOS DataKeeper es replicar datos de la unidad de volumen de origen S en el nodo B tootarget volumen unidad agrupada S en el nodo de clúster A. Por ejemplo, está replicando de **pr1-ascs-1 [10.0.0.41]** demasiado**pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="39a27-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: SIOS DataKeeper replica volumen local Hola del clúster B toocluster nodo A][sap-ha-guide-figure-5003]

  <span data-ttu-id="39a27-1041">_**Figura 64:** SIOS DataKeeper replica volumen local Hola del nodo de clúster nodo B toocluster A_</span><span class="sxs-lookup"><span data-stu-id="39a27-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
