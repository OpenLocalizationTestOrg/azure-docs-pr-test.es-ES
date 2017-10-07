---
title: "Credenciales de implementación del servicio de aplicación aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola credenciales de implementación de servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Configuración de credenciales de implementación para Azure App Service
[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) admite dos tipos de credenciales para la [implementación de GIT local](app-service-deploy-local-git.md) y la [implementación FTP/S](app-service-deploy-ftp.md). Estos son no Hola igual que sus credenciales de Azure Active Directory.

* **Las credenciales de nivel de usuario**: un conjunto de credenciales de cuenta de Azure completo Hola. Puede ser usado toodeploy tooApp servicio para cualquier aplicación en una suscripción que Hola cuenta de Azure tiene permiso tooaccess. Se trata de conjunto de credenciales de hello predeterminado que se configura en **servicios de aplicaciones** > **&lt;app_name >** > **decredencialesdeimplementación**. Esto también es Hola conjunto predeterminado que aparece en el portal de hello interfaz gráfica de usuario (como hello **Introducción** y **propiedades** de la aplicación [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Al delegar el acceso a los recursos a través de Control de acceso basado en roles (RBAC) o los permisos de Coadministrador tooAzure, cada usuario de Azure que recibe acceso tooan aplicación puede usar sus credenciales de nivel de usuario personales hasta que se revoca el acceso. Estas credenciales de implementación no deben compartirse con otros usuarios de Azure.
    >
    >

* **Credenciales de nivel de aplicación**: un conjunto de credenciales para cada aplicación. Puede ser usado toodeploy toothat solo aplicación. las credenciales de Hola para cada aplicación se genera automáticamente al crear la aplicación y se encuentra en la aplicación hello perfil de publicación. No se puede configurar manualmente las credenciales de hello, pero puede restablecerlas para una aplicación en cualquier momento.

    > [!NOTE]
    > En orden toogive a alguien acceso credenciales toothese a través de Control de acceso de en función de roles (RBAC), deberá toomake ellos colaborador o superior en hello Web App. Los lectores no se permiten toopublish y, por tanto, no pueden tener acceso a esas credenciales.
    >
    >

## <a name="userscope"></a>Establecimiento y restablecimiento de credenciales de nivel de usuario

Puede configurar las credenciales de nivel de usuario en cualquier [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de la aplicación. Independientemente de qué aplicación configurar estas credenciales, aplica tooall aplicaciones y para todas las suscripciones de Azure de la cuenta. 

tooconfigure sus credenciales de nivel de usuario:

1. Hola [portal de Azure](https://portal.azure.com), haga clic en el servicio de aplicaciones >  **&lt;any_app >** > **las credenciales de implementación**.

    > [!NOTE]
    > En el portal de hello, debe tener al menos una aplicación antes de que se puede tener acceso a la hoja de credenciales de implementación de Hola. Sin embargo, con hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), puede configurar las credenciales de nivel de usuario sin una aplicación existente.

2. Configurar el nombre de usuario de Hola y la contraseña y, a continuación, haga clic en **guardar**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Una vez haya configurado las credenciales de implementación, puede encontrar Hola *Git* nombre de usuario de implementación de la aplicación **Introducción**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

y el nombre de usuario de implementación de *FTP* en las **Propiedades** de la aplicación.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure no muestra la contraseña de la implementación de nivel de usuario. Si olvida la contraseña de hello, no podrá recuperarlo. Sin embargo, puede restablecer las credenciales siguiendo los pasos de hello en esta sección.
>
>  

## <a name="appscope"></a>Obtención y restablecimiento de las credenciales de nivel de aplicación
Para cada aplicación de servicio de aplicaciones, sus credenciales de nivel de aplicación se almacenan en hello perfil de publicación de XML.

credenciales de nivel de aplicación de Hola tooget:

1. Hola [portal de Azure](https://portal.azure.com), haga clic en el servicio de aplicaciones >  **&lt;any_app >** > **Introducción**.

2. Haga clic en **... Más** > **Obtener perfil de publicación** para que comience la descarga de un archivo .PublishSettings.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Hola abierto. Archivo de configuración de publicación y encontrar Hola `<publishProfile>` etiqueta con hello atributo `publishMethod="FTP"`. A continuación, obtenga sus atributos `userName` y `password`.
Estas son las credenciales de nivel de aplicación Hola.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Credenciales de nivel de usuario toohello similar, nombre de usuario de implementación de hello FTP está en formato de Hola de `<app_name>\<username>`, y es el nombre de usuario de hello Git implementación `<username>` sin Hola anterior `<app_name>\`.

credenciales de nivel de aplicación de Hola tooreset:

1. Hola [portal de Azure](https://portal.azure.com), haga clic en el servicio de aplicaciones >  **&lt;any_app >** > **Introducción**.

2. Haga clic en **... Más** > **Restablecer perfil de publicación**. Haga clic en **Sí** tooconfirm Hola restablece.

    acción de restablecimiento de Hello invalida cualquier descargados anteriormente. Archivos de configuración de publicación.

## <a name="next-steps"></a>Pasos siguientes

Obtener información sobre cómo toouse estas credenciales toodeploy la aplicación de [Git local](app-service-deploy-local-git.md) o con [FTP/S](app-service-deploy-ftp.md).
