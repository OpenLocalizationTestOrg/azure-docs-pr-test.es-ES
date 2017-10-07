---
title: aaaAzure lista de cuentas de almacenamiento
description: "Administrar la configuración de la cuenta de almacenamiento mediante Hola Kit de herramientas de Azure para Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Lista de cuentas de almacenamiento de Azure
Almacenamiento de Azure cuentas permiten descargar toobe de ubicaciones que se usa para el JDK, servidor de aplicaciones y componentes arbitrarios, así como para almacenar el estado cuando se usa el almacenamiento en caché. Eclipse mantiene una lista de cuentas de almacenamiento conocidas que son proyectos tooyour disponible en el área de trabajo de Eclipse. Hola tooopen **cuentas de almacenamiento** cuadro de diálogo, que es usado toomanage que enumeran, en Eclipse, haga clic en **ventana**, haga clic en **preferencias**, expanda **Azure** y, a continuación, haga clic en **cuentas de almacenamiento**.

siguiente Hello muestra hello **cuentas de almacenamiento** cuadro de diálogo.

![][ic719496]

También se puede abrir este cuadro de diálogo desde un **cuentas** vínculo en los cuadros de diálogo que utilizan cuentas de almacenamiento, como siguiente hello:

* Hola **JDK** ficha de hello **configuración del servidor** cuadro de diálogo.
* Hola **Server** ficha de hello **configuración del servidor** cuadro de diálogo.
* Hola **Agregar componente** cuadro de diálogo.
* Hola **Caching** cuadro de diálogo Propiedades.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>tooimport el almacenamiento de cuentas con un archivo de configuración de publicación
1. Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en **importar desde el archivo de configuración de publicación**.

2. (Omita este paso si ya ha guardado un equipo local tooyour del archivo de publicación configuración). Hola **Import Subscription Information** cuadro de diálogo, haga clic en **Download PUBLISH-SETTINGS File**. Si no ha iniciado ya sesión en su cuenta de Azure, es posible que toolog solicitada en. A continuación, se le pedirá una Azure toosave archivo de configuración de publicación. (Puede omitir instrucciones de hello resultante que se muestra en las páginas de inicio de sesión de hello - se proporcionan por hello portal de Azure y están pensadas para usuarios de Visual Studio.) Guárdelo tooyour de equipo local.

3. Aún en hello **Import Subscription Information** cuadro de diálogo, haga clic en hello **examinar** button, seleccione Hola publicar el archivo de configuración que ha guardado localmente anteriormente y, a continuación, haga clic en **abrir**.

4. Haga clic en **Aceptar** tooclose hello **Import Subscription Information** cuadro de diálogo.

## <a name="toocreate-a-new-storage-account"></a>toocreate una cuenta de almacenamiento
1. Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en **agregar**.

2. Dentro de hello **agregar una cuenta de almacenamiento** cuadro de diálogo, haga clic en **nuevo**.

3. Dentro de hello **nueva cuenta de almacenamiento** cuadro de diálogo, especifique los valores siguientes de hello:

   * Nombre de la cuenta de almacenamiento.

   * Ubicación de la cuenta de almacenamiento de Hola.

   * Descripción de la cuenta de almacenamiento de Hola.

   * cuenta de almacenamiento de Hello suscripción toowhich Hola pertenece.

4. Haga clic en **Aceptar** tooclose hello **nueva cuenta de almacenamiento** cuadro de diálogo.

Puede tardar varios minutos para su toobe de cuenta de almacenamiento creado. Después de crearla, haga clic en **Aceptar** tooclose hello **agregar una cuenta de almacenamiento** cuadro de diálogo y la nueva cuenta de almacenamiento se agregarán toohello lista de cuentas de almacenamiento disponible.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd una lista de toohello de cuenta de almacenamiento existente
1. Si ya tiene un almacenamiento de Azure de la cuenta, cree una forma Hola pasos enumeran en hello **toocreate una nueva sección de la cuenta de almacenamiento** anteriormente. (O bien, puede crear una nueva cuenta de almacenamiento en hello [Portal de administración de Azure][Azure Management Portal].)

2. Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en **agregar**.

3. Dentro de hello **agregar una cuenta de almacenamiento** cuadro de diálogo, especifique los valores de **nombre** y **clave de acceso**. clave de acceso y nombre de la cuenta de Hello debe ser para una cuenta de almacenamiento de Azure existente. Hola de uso **almacenamiento** sección de hello [Portal de administración de Azure] [ Azure Management Portal] tooview nombres y claves de la cuenta de almacenamiento. Su **agregar una cuenta de almacenamiento** cuadro de diálogo tendrá un aspecto similar a continuación toohello.
   
   ![][ic719497]

4. Haga clic en **Aceptar** tooclose hello **agregar una cuenta de almacenamiento** cuadro de diálogo.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify un toouse de cuenta de almacenamiento una nueva clave de acceso
1. Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en la cuenta de almacenamiento de Hola que desee tooedit y, a continuación, haga clic en **editar**.

2. Dentro de hello **editar la clave de acceso de la cuenta de almacenamiento** cuadro de diálogo Modificar hello **clave de acceso** valor.

3. Haga clic en **Aceptar** tooclose hello **editar la clave de acceso de la cuenta de almacenamiento** cuadro de diálogo.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove mantiene de una cuenta de almacenamiento de la lista de hello en Eclipse
1. Dentro de hello **cuentas de almacenamiento** cuadro de diálogo, haga clic en la cuenta de almacenamiento de Hola que desee tooedit y, a continuación, haga clic en **quitar**.

2. Haga clic en **Aceptar** cuando tooremove solicitada Hola cuenta de almacenamiento.

> [!NOTE]
> Quitar la cuenta de almacenamiento de Hola a través de hello **cuentas de almacenamiento** cuadro de diálogo solo quita de la lista de Hola de cuentas de almacenamiento pueden visualizar en Eclipse. No quita la cuenta de almacenamiento de Hola desde su suscripción de Azure. Además, cuenta de almacenamiento de hello podría aparecer de nuevo en la lista después de que Eclipse vuelva a cargar los detalles de Hola de su suscripción.
> 
> 

## <a name="see-also"></a>Otras referencias
[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]

[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
