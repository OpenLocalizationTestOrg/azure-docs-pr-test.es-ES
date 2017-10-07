---
title: aaaUsing escritorio remoto con los Roles de Azure | Documentos de Microsoft
description: Uso de Escritorio de remoto con los roles de Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Uso de Escritorio de remoto con los roles de Azure
Mediante el uso de hello Azure SDK y los servicios de escritorio remoto, puede tener acceso a las funciones de Azure y máquinas virtuales que se hospedan en Azure. En Visual Studio, puede configurar Servicios de Escritorio remoto desde un proyecto de servicio en la nube de Azure. tooenable de servicios de escritorio remoto, debe crear un proyecto totalmente funcional que contiene uno o más roles y, a continuación, publicarlo tooAzure.

> [!IMPORTANT]
> Debe tener acceso a un rol de Azure para solucionar problemas o desarrollo solamente. Hola propósito de cada máquina virtual es un rol concreto en la aplicación de Azure, no toorun toorun otras aplicaciones cliente. Si desea toouse toohost Azure una máquina virtual que puede utilizar para cualquier propósito, vea obtener acceso a máquinas virtuales de Azure del explorador de servidores.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable y usar Escritorio remoto para un rol de Azure
1. En el Explorador de soluciones, abra el menú contextual de hello para el proyecto de servicio de nube y, a continuación, elija **publicar**.
   
    Hola **publicar aplicación de Azure** aparece el Asistente para.
   
    ![Publicar el comando para un proyecto de servicio en la nube](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. En la parte inferior de Hola de **configuración de publicación de Microsoft Azure** página del Asistente de hello, seleccione hello **habilitar Escritorio remoto** para todos los roles de casilla. 
   
    Hola **configuración de escritorio remoto** aparece el cuadro de diálogo.
3. Final de Hola de hello **configuración de escritorio remoto** diálogo cuadro, elija hello **más opciones** botón. 
   
    Esto muestra un cuadro de lista desplegable que le permite crear o seleccionar un certificado para que puede cifrar la información de credenciales al conectarse a través de escritorio remoto.
4. En la lista desplegable de hello, elija  **&lt;crear >**, o elija uno ya existente de la lista de Hola. 
   
    Si selecciona un certificado existente, pase Hola pasos.
   
   > [!NOTE]
   > certificados de Hola que necesita para una conexión a escritorio remota son distintos de los certificados de Hola que se usan para otras operaciones de Azure. certificado de acceso remoto de Hello debe tener una clave privada.
   > 
   > 
   
    Hola **Create Certificate** aparece el cuadro de diálogo.
   
   1. Proporcione un nombre descriptivo para el nuevo certificado de Hola y, a continuación, elija Hola **Aceptar** botón. Hola nuevo certificado aparece en cuadro de lista desplegable de Hola.
   2. Hola **configuración de escritorio remoto** diálogo cuadro, proporcione un nombre de usuario y una contraseña.
      
       No se puede usar una cuenta existente. No especifique Administrador como nombre de usuario de hello para la nueva cuenta de hello.
      
      > [!NOTE]
      > Si la contraseña de hello no cumple los requisitos de complejidad de hello, aparecerá un icono rojo siguiente cuadro de texto de contraseña toohello. Hola contraseña debe contener letras mayúsculas, letras minúsculas y números o símbolos.
      > 
      > 
   3. Elija una fecha en que expirará la cuenta de hello y después se bloquearán las conexiones a Escritorio remoto.
   4. Cuando se haya proporcionado todos Hola información necesaria, elija hello **Aceptar** botón.
      
       Varias opciones de configuración que habilite los servicios de acceso remoto se agregan los archivos .cscfg y .csdef toohello.
5. Hola **configuración de publicación de Microsoft Azure** asistente, elija hello **Aceptar** botón cuando esté listo toopublish su servicio en la nube.
   
    Si no está listo toopublish, elija hello **cancelar** botón. Opciones de configuración de Hola se guardan y podrá publicar su servicio en la nube más adelante.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Conectar tooan rol de Azure mediante Escritorio remoto
Después de publicar el servicio de nube en Azure, puede usar toolog del explorador de servidores en máquinas virtuales de Hola que hospeda Azure. 

1. En el Explorador de servidores, expanda hello **Azure** nodo y a continuación, expanda el nodo de Hola para un servicio de nube y uno de su toodisplay una lista de instancias de roles.
2. Abra el acceso directo de Hola para un nodo de la instancia y, a continuación, elija **conectar usando Escritorio remoto**.
   
    ![Conexión a través del escritorio remoto](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Escriba el nombre de usuario de Hola y la contraseña que creó anteriormente. Ahora está registrado en la sesión remota.

