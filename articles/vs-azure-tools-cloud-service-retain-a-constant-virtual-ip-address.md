---
title: "aaaHow tooretain una dirección IP virtual constante para un servicio de nube de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo no cambia tooensure que Hola dirección IP virtual (VIP) del servicio en la nube de Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Conservación de una dirección IP virtual constante para un servicio en la nube de Azure
Al actualizar un servicio de nube que se hospeda en Azure, tendrá que tooensure que no cambia la dirección IP virtual de hello (VIP) del servicio de Hola. Muchos de los servicios de administración de dominio usan Hola sistema de nombres de dominio (DNS) para registrar nombres de dominio. DNS sólo funciona si Hola Hola VIP permanece igual. Puede usar hello **Asistente para publicación** en tooensure de Azure Tools que Hola VIP del servicio en la nube no cambia cuando se actualice. Para obtener más información acerca de cómo toouse administración de dominios DNS para servicios en la nube, consulte [configurar un nombre de dominio personalizado para un servicio de nube de Azure](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Publicación de un servicio en la nube sin cambiar su VIP
Hola VIP de un servicio de nube se asigna cuando primero lo implementa tooAzure en un entorno determinado, como el entorno de producción de hello. proceso de actualización de Hello VIP solo cambia si se elimina la implementación de hello explícitamente o implícitamente se elimina la implementación de Hola por la implementación de Hola. tooretain Hola VIP, no debe eliminar la implementación y asegúrese de que Visual Studio no elimine la implementación automáticamente. 

Puede especificar la configuración de implementación en hello **Asistente para publicación**, que admite varias opciones de implementación. Puede especificar una nueva implementación o una implementación de actualización, que puede ser incremental o simultánea. Ambos tipos de implementación de actualizaciones de conservan a Hola VIP. Para obtener definiciones de estos tipos diferentes de implementación, vea [Asistente Publicar aplicaciones de Azure](vs-azure-tools-publish-azure-application-wizard.md). Además, puede controlar si se elimina la implementación anterior de Hola de un servicio de nube si se produce un error. Si no establece esa opción correctamente, Hola VIP podría cambiar de forma inesperada.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Actualización de un servicio en la nube sin cambiar su VIP
1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio. 

2. En **el Explorador de soluciones**, proyecto de hello del menú contextual. En el menú contextual de hello, seleccione **publicar**.

    ![Publish menu](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. Hola **publicar aplicación de Azure** cuadro de diálogo, seleccione hello toowhich de suscripción de Azure que desee toodeploy. Inicie sesión en si es necesario y seleccione **Siguiente**.

    ![Página de inicio de sesión de Publicar aplicación de Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. En hello **configuración común** ficha, compruebe que ese nombre Hola de toowhich de servicio de nube Hola va a implementar, hello **entorno**, hello **configuración de compilación**, hello y **Configuración del servicio** son correctos.

    ![Pestaña Configuración común de Publicar aplicación de Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. En hello **configuración avanzada** , compruebe que hello **etiqueta de implementación** hello y **cuenta de almacenamiento** son correctos. Compruebe que hello **eliminar implementación en caso de error** casilla de verificación está desactivada y compruebe que hello **actualización de la implementación** casilla está activada. Al borrar hello **eliminar implementación en caso de error** casilla de verificación, se asegura de que la dirección VIP no se pierde si se produce un error durante la implementación. Si selecciona hello **actualización de la implementación** casilla de verificación, se garantiza que no se ha eliminado la implementación y la dirección VIP no se pierde cuando se vuelve a publicar la aplicación. 

    ![Pestaña Configuración avanzada de Publicar aplicación de Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther especificar cómo desea Hola roles toobe actualizado, seleccione **configuración** siguiente demasiado**actualización de la implementación**. Seleccione **Actualización incremental** o **Actualización simultánea** y seleccione **Aceptar**. Elija **actualización Incremental** tooupdate cada instancia de la aplicación, uno tras otro, por lo que Hola aplicación está siempre disponible. Elija **actualización simultánea** tooupdate todas las instancias de la aplicación hello en el mismo tiempo. La actualización simultánea es más rápida, pero el servicio podría no estar disponible durante el proceso de actualización de Hola. Cuando haya terminado, seleccione **Siguiente**.

    ![Página Configuración de implementación de Publicar aplicación de Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. Hola **publicar aplicación de Azure** cuadro de diálogo, seleccione **siguiente** hasta hello **resumen** se muestra la página. Compruebe la configuración y, luego, seleccione **Publicar**.
   
    ![Página de resumen de Publicar aplicación de Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Pasos siguientes
- [Uso de hello Visual Studio Azure Asistente para publicar aplicaciones](vs-azure-tools-publish-azure-application-wizard.md)

