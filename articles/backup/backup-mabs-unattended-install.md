---
title: "instalación de aaaSilent del servidor de copia de seguridad de Azure v2 | Documentos de Microsoft"
description: "Usar un toosilently de secuencia de comandos de PowerShell de instalación v2 del servidor de copia de seguridad de Azure. Este tipo de instalación también se denomina instalación desatendida."
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
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Ejecutar una instalación desatendida de Azure Backup Server v2

Obtenga información acerca de cómo toorun una instalación desatendida de v2 del servidor de copia de seguridad de Azure. 

Estos pasos no se aplican si va a instalar Azure Backup Server v1.

## <a name="install-backup-server-v2"></a>Instalar Backup Server v2

1. En el servidor de Hola que hospeda el servidor de copia de seguridad de Azure v2, cree un archivo de texto. (Puede crear archivo hello en el Bloc de notas o en otro texto editor.) Guarde el archivo hello como MABSSetup.ini. 

2. Pegue Hola después el código en un archivo MABSSetup.ini Hola. Reemplazar texto hello entre corchetes hello (\< \>) con valores de su entorno. Hola después de texto es un ejemplo:

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

3. Guarde el archivo hello. A continuación, en un símbolo con privilegios elevados en el servidor de instalación de hello, escriba este comando:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Puede usar estas marcas para la instalación de hello:</br>
**/f**: ruta de acceso del archivo .ini</br>
**/l**: ruta de acceso del registro</br>
**/i**: ruta de acceso de instalación</br>
**/x**: ruta de acceso de desinstalación</br>

## <a name="next-steps"></a>Pasos siguientes
Después de instalar el servidor de copia de seguridad, obtenga información acerca de cómo tooprepare el servidor, o empezar a proteger una carga de trabajo.

- [Preparar cargas de trabajo de Backup Server](backup-azure-microsoft-azure-backup.md)
- [Usar tooback del servidor de copia de seguridad de un servidor de VMware](backup-azure-backup-server-vmware.md)
- [Usar tooback del servidor de copia de seguridad de SQL Server](backup-azure-sql-mabs.md)
- [Agregar almacenamiento de copia de seguridad moderna tooBackup Server](backup-mabs-add-storage.md)
