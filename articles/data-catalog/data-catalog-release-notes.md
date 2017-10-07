---
title: "notas de la versión de aaaAzure el catálogo de datos | Documentos de Microsoft"
description: "Las notas de la versión del Catálogo de datos de Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Notas de la versión del Catálogo de datos de Azure
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Notas de versión de 20 de noviembre de 2015 Hola del catálogo de datos de Azure
### <a name="opening-data-sources-in-power-bi-desktop"></a>Apertura de orígenes de datos en Power BI Desktop
Cuando se usa la opción de "Abrir en Power BI Desktop" hello de hello **el catálogo de datos** portal, los usuarios pueden encontrarse alguno de estos dos problemas en hello aplicación de Power BI Desktop:

* Se muestra un cuadro de diálogo con el título de hello "No se puede tooOpen documento"
* se abre Hola aplicación de Power BI Desktop, pero archivo hello aparece toobe vacía

En cada situación, se puede resolver el problema de hello, descargue e instale la versión más reciente de Hola de Power BI Desktop desde [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Notas de versión de 13 de noviembre de 2015 Hola del catálogo de datos de Azure
### <a name="registering-and-connecting-tooteradata"></a>Registrar y conectar tooTeradata
Al conectarse a orígenes de datos de tooTeradata usuarios deben tener instalado el controlador ODBC Teradata correcto de Hola que coinciden con los bits de hello (32 bits o 64 bits) del software de Hola que se va a usar.

A partir de este ADC, fecha de lanzamiento, Hola más reciente [el controlador ODBC de Teradata para windows (versión 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) es compatible con Office 2013, pero no con Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Notas de versión de 13 de julio de 2015 Hola del catálogo de datos de Azure
### <a name="registering-and-connecting-toooracle-database"></a>Registrar y conectar tooOracle base de datos
Al conectar a los usuarios en orígenes de datos de base de datos en tooOracle debe haber instalado controladores Oracle correspondientes Hola que coinciden con los bits de hello (32 bits o 64 bits) del software de Hola que se va a usar.

* Al registrar los orígenes de datos de Oracle en un equipo que ejecuta Windows de 32 bits, se usará controladores de Oracle de 32 bits de Hola
* Al registrar los orígenes de datos de Oracle en un equipo que ejecuta Windows de 64 bits, se usará controladores de Oracle de 64 bits de Hola
* Al conectarse a orígenes de datos de tooOracle usa Excel en un equipo que ejecuta la versión de 32 bits de Hola de Microsoft Office, incluido en Windows de 64 bits, controladores de Oracle de 32 bits de Hola se utilizará
* Al conectarse a orígenes de datos de tooOracle usa Excel en un equipo que ejecuta la versión de 64 bits de Hola de Microsoft Office, se usará controladores de Oracle de 64 bits de Hola

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Registrar y conectar tooSQL Server Reporting Services
Compatibilidad con orígenes de datos de SQL Server Reporting Services (SSRS) está actualmente hay una limitación tooNative sólo los servidores de modo. La compatibilidad con SSRS en modo SharePoint se agregará en una versión posterior.

### <a name="opening-data-assets-in-excel"></a>Apertura de recursos de datos en Excel
Al abrir los activos de datos en Microsoft Excel de hello **el catálogo de datos** portal, los usuarios que se le pida con un **aviso de seguridad de Microsoft Excel** cuadro de diálogo. Se trata de estándar, pueden seleccionar el comportamiento esperado y los usuarios **habilitar** toocontinue.

Para obtener más información, vea [Habilitación o deshabilitación de alertas de seguridad sobre vínculos y archivos de sitios web sospechosos](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Configuración de proxy y directiva, y registro de orígenes de datos
Los usuarios pueden encontrarse en una situación donde poder iniciar sesión en el portal del catálogo de datos de Azure de toohello, pero cuando intenten toolog en la herramienta de registro del origen de datos de toohello que aparecen un mensaje de error que impide que iniciar sesión.

Hay dos causas posibles para este comportamiento del problema:

**Causa 1: Configuración de servicios de federación de Active Directory** herramienta de registro de origen de datos de hello usa inicios de sesión de autenticación de formularios toovalidate usuario en Active Directory. Para iniciar sesión correctamente, la autenticación de formularios debe habilitarse en hello directiva de autenticación Global por un administrador de Active Directory.

En algunas situaciones, este error puede ocurrir sólo cuando el usuario de hello en red de empresa de hello, o solo cuando Hola usuario se conecta desde la red de empresa de hello exterior. Hola directiva de autenticación Global permite toobe de métodos de autenticación habilitado por separado para la intranet y las conexiones de extranet. Si la autenticación de formularios no está habilitada para la red de Hola desde qué Hola usuario se conecta, pueden producirse errores de inicio de sesión.

Para obtener más información, vea [Configuración de directivas de autenticación](https://technet.microsoft.com/library/dn486781.aspx).

**Causa 2: Configuración de proxy de red** si red corporativa de hello usa un servidor proxy, la herramienta de registro de hello puede no ser capaz de tooconnect tooAzure Active Directory a través de proxy de Hola. Los usuarios pueden asegurarse de esa herramienta de registro de hello editando el archivo de configuración de la herramienta de hello, agregar este archivo de toohello de sección:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


archivo de RegistrationTool.exe.config de toolocate hello, inicie la herramienta de registro de hello y, a continuación, abra la utilidad de administrador de tareas de Windows hello. En la ficha de detalles de hello en el Administrador de tareas, haga doble clic en RegistrationTool.exe y elija Abrir ubicación del archivo desde el menú emergente de Hola.
