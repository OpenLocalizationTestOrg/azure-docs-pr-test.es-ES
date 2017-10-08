---
title: aaaManage Azure Analysis Services | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage un Analysis Services server en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Administración de Analysis Services
Una vez que ha creado un servidor de Analysis Services en Azure, puede haber algunas tareas de administración y administración necesita tooperform inmediatamente o algún tiempo inactivo road Hola. Por ejemplo, ejecutar el procesamiento toohello de actualización de datos, controlar quién puede tener acceso a los modelos de hello en el servidor o supervisar el estado del servidor. Varias de estas tareas solo se pueden realizar en Azure Portal, otras en SQL Server Management Studio (SSMS) y otras se pueden realizar indistintamente en ambos.

## <a name="azure-portal"></a>Azure Portal
[Portal de Azure](http://portal.azure.com/) es donde puede crear y eliminar servidores, supervisar los recursos de servidor, cambiar el tamaño y administrar quién tiene acceso tooyour servidores.  Si tiene problemas, también puede enviar una solicitud de soporte técnico.

![Obtención del nombre del servidor en Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Conectar el servidor de tooyour en Azure es igual que conecta la instancia del servidor tooa en su propia organización. En SSMS, puede realizar muchas de hello mismo tareas como procesar los datos o crear una secuencia de comandos de procesamiento, administrar roles y usar PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Descarga e instalación de SSMS
tooget todos Hola características más recientes y experiencia más fluida de hello cuando se conecta el servidor de Analysis Services de Azure de tooyour, asegúrese de utiliza la versión más reciente de Hola de SSMS. 

[Descargue SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect con SSMS
 Cuando se usa SSMS, antes de conectar saludos del servidor tooyour primera vez, asegúrese de que el nombre de usuario se incluye en el grupo de administradores de servicios de análisis de Hola. más información, consulte toolearn [los administradores del servidor](#server-administrators) más adelante en este artículo.

1. Antes de conectar, necesita el nombre del servidor de tooget Hola. En **portal de Azure** > servidor > **Introducción** > **nombre del servidor**, el nombre del servidor de copia Hola.
   
    ![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. En SSMS > **Explorador de objetos**, haga clic en **Conectar** > **Analysis Services**.
3. Hola **conectar tooServer** cuadro de diálogo, pegar en nombre del servidor hello, a continuación, en **autenticación**, elija uno de los siguientes tipos de autenticación de hello:
   
    **Autenticación de Windows** toouse sus credenciales de dominio ombre de usuario y la contraseña de Windows.

    **Autenticación de contraseña de Active Directory** toouse una cuenta profesional. Por ejemplo, al establecer conexión desde un equipo unido que no es de dominio.

    **Autenticación Universal de Active Directory** toouse [la autenticación no interactiva o multifactor](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Conectar en SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Administradores del servidor y usuarios de la base de datos
En Azure Analysis Services hay dos tipos de usuarios: los administradores del servidor y los usuarios de la base de datos. Ambos tipos de usuarios deben estar en su instancia de Azure Active Directory y se deben especificar mediante la dirección de correo electrónico profesional o UPN. más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Solución de problemas de conexión
Cuando se conecta mediante SSMS, si experimenta problemas, puede que necesite caché de inicio de sesión de tooclear Hola. Nada es toodisc almacenado en caché. proceso de conexión de la caché de hello tooclear, cierre y reinicio Hola. 

## <a name="next-steps"></a>Pasos siguientes
Si ya no ha implementado un nuevo servidor de modelo tabular tooyour, ahora es un buen momento. más información, consulte toolearn [implementar tooAzure Analysis Services](analysis-services-deploy.md).

Si ha implementado un servidor de tooyour de modelo, le tooit tooconnect listo con un cliente o un explorador. más información, consulte toolearn [obtener datos del servidor de Analysis Services de Azure](analysis-services-connect.md).

