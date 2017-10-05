---
title: "Instalación silenciosa de Azure Backup Server v2 | Microsoft Docs"
description: "Use un script de PowerShell para realizar una instalación silenciosa de Azure Backup Server v2. Este tipo de instalación también se denomina instalación desatendida."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="5ae8a-104">Ejecutar una instalación desatendida de Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="5ae8a-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="5ae8a-105">Obtenga información sobre cómo ejecutar una instalación desatendida de Azure Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="5ae8a-106">Estos pasos no se aplican si va a instalar Azure Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="5ae8a-107">Instalar Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="5ae8a-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="5ae8a-108">En el servidor que hospeda Azure Backup Server v2, cree un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="5ae8a-109">(Puede crear el archivo en el Bloc de notas o en otro editor de texto). Guarde el archivo como MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="5ae8a-110">Pegue el código siguiente en el archivo MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="5ae8a-111">Reemplace el texto entre corchetes (\< \>) por los valores de su entorno.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="5ae8a-112">A continuación se muestra un texto de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ae8a-112">The following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="5ae8a-113">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="5ae8a-113">Save the file.</span></span> <span data-ttu-id="5ae8a-114">Después, en un símbolo del sistema con privilegios elevados en el servidor de instalación, escriba este comando:</span><span class="sxs-lookup"><span data-stu-id="5ae8a-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="5ae8a-115">Puede usar estas marcas para la instalación:</span><span class="sxs-lookup"><span data-stu-id="5ae8a-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="5ae8a-116">
**/f**: ruta de acceso del archivo .ini</span><span class="sxs-lookup"><span data-stu-id="5ae8a-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="5ae8a-117">
**/l**: ruta de acceso del registro</span><span class="sxs-lookup"><span data-stu-id="5ae8a-117">
**/l**: Log path</span></span></br><span data-ttu-id="5ae8a-118">
**/i**: ruta de acceso de instalación</span><span class="sxs-lookup"><span data-stu-id="5ae8a-118">
**/i**: Installation path</span></span></br><span data-ttu-id="5ae8a-119">
**/x**: ruta de acceso de desinstalación</span><span class="sxs-lookup"><span data-stu-id="5ae8a-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="5ae8a-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ae8a-120">Next steps</span></span>
<span data-ttu-id="5ae8a-121">Después de instalar Backup Server, sepa cómo preparar el servidor o empezar a proteger la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5ae8a-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="5ae8a-122">Preparar cargas de trabajo de Backup Server</span><span class="sxs-lookup"><span data-stu-id="5ae8a-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="5ae8a-123">Usar Backup Server para hacer una copia de seguridad de un servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="5ae8a-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="5ae8a-124">Usar Backup Server para hacer una copia de seguridad de SQL Server</span><span class="sxs-lookup"><span data-stu-id="5ae8a-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="5ae8a-125">Agregar Modern Backup Storage a Backup Server</span><span class="sxs-lookup"><span data-stu-id="5ae8a-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
