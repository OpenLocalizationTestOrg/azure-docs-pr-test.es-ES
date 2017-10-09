---
title: registro Docker privada aaaCreate - portal de Azure | Documentos de Microsoft
description: Empezar a crear y administrar registros de contenedor de Docker privados con hello portal de Azure
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Crear un registro de contenedor de Docker privado mediante Hola portal de Azure
Usar hello toocreate portal Azure un registro de contenedor y administrar su configuración. También puede crear y administrar registros de contenedor con hello [comandos de CLI de Azure 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) o mediante programación con registro de contenedor de hello [API de REST](https://go.microsoft.com/fwlink/p/?linkid=834376).

En el fondo y conceptos, vea [Hola información general sobre](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Creación de un registro de contenedor
1. Hola [portal de Azure](https://portal.azure.com), haga clic en **+ nuevo**.
2. Busque en marketplace Hola para **registro de contenedor de Azure**.
3. Seleccione **Azure Container Registry**, con el publicador **Microsoft**.
    ![Servicio Container Registry en Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Haga clic en **Crear**. Hola **registro de contenedor de Azure** aparece hoja.

    ![Configuración de Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. Hola **registro de contenedor de Azure** hoja, escriba Hola siguiente información. Cuando haya terminado, haga clic en **Crear**.

    a. **Nombre del registro**: un nombre de dominio de nivel superior único global para el registro específico. En este ejemplo, es el nombre del registro de hello *myRegistry01*, pero sustituir un nombre único de su elección. Hola nombre puede contener sólo letras y números.

    b. **Grupo de recursos**: seleccione una existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo.

    c. **Ubicación**: seleccione la ubicación de centro de datos Azure donde es el servicio de hello [disponibles](https://azure.microsoft.com/regions/services/), como **Ee.uu. Central sur**.

    d. **El usuario administrador**: si lo desea, habilitar un registro de hello de tooaccess de usuario de administrador. Puede cambiar esta configuración después de crear el registro de hello.

      > [!IMPORTANT]
      > Además de acceso tooproviding a través de una cuenta de usuario de administrador, los registros de contenedor admiten la autenticación respaldada por entidades de servicio de Azure Active Directory. Para más información y otras consideraciones, consulte [Authenticate with the container registry](container-registry-authentication.md) (Autenticación con el registro de contenedor).
      >

    e. **Cuenta de almacenamiento**: usar Hola predeterminada configuración toocreate una [cuenta de almacenamiento](../storage/common/storage-introduction.md), o seleccione una cuenta de almacenamiento existente en hello misma ubicación. Premium Storage no se admite actualmente.

## <a name="manage-registry-settings"></a>Administración de la configuración del registro
Después de crear el registro de hello, buscar Hola configuración del registro a partir de hello **registros de contenedor** hoja en el portal de Hola. Por ejemplo, tendrá que toolog de configuración de hello en el registro de tooyour, o puede tener tooenable o deshabilitar al usuario de administrador de Hola.

1. En hello **registros de contenedor** hoja, haga clic en nombre de Hola de seguridad del registro.

    ![Hoja Registro de contenedor](./media/container-registry-get-started-portal/container-registry-blade.png)
2. Haga clic en configuración de acceso de toomanage, **clave de acceso**.

    ![Acceso al registro de contenedor](./media/container-registry-get-started-portal/container-registry-access.png)
3. Tenga en cuenta Hola después de configuración:

   * **Servidor de inicio de sesión** -nombre completo de hello usar toolog en el registro de toohello. En este ejemplo, es `myregistry01.azurecr.io`.
   * **El usuario administrador** : alternar tooenable o deshabilitar la cuenta de usuario de administrador del registro de hello.
   * **Nombre de usuario** y **contraseña** -Hola credenciales de cuenta de usuario de administrador de hello (si está habilitado) puede usar toolog en el registro de toohello. Si lo desea, puede volver a generar contraseñas de Hola. Se crean dos contraseñas para que pueda mantener registro toohello de conexiones mediante el uso de una contraseña mientras regenera Hola otra contraseña. tooauthenticate con una entidad de servicio en su lugar, vea [autenticar con un registro de contenedor de Docker privado](container-registry-authentication.md).

## <a name="next-steps"></a>Pasos siguientes
* [Insertar la primera imagen con hello CLI de Docker](container-registry-get-started-docker-cli.md)
