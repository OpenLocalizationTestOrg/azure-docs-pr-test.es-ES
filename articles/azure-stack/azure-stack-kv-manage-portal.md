---
title: "aaaManage el almacén de claves en la pila de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage el almacén de claves en la pila de Azure con PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a>Administrar el almacén de claves en la pila de Azure mediante el portal de Hola

Puede administrar el almacén de claves en la pila de Azure mediante el portal de Azure pila Hola. En este artículo le ayuda a obtener toocreate iniciada y administrar el almacén de claves en la pila de Azure. 

## <a name="prerequisites"></a>Requisitos previos  

* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Hola.  
* Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.  
 
## <a name="create-a-key-vault"></a>Creación de un Almacén de claves 

1. Inicie sesión en el portal de usuarios de toohello (https://portal.local.azurestack.external).  

2. En el panel de hello, haga clic en **nuevo > seguridad e identidad > almacén de claves**.  

    ![Pantalla de KV](media/azure-stack-kv-manage-portal/image1.png)  

3. En hello **crear el almacén de claves** hoja, asignar un **nombre** para el almacén. Nombre del almacén puede contener solo caracteres alfanuméricos, Hola carácter especial guiones (-), y no debe comenzar con un número.  

4. Elija un **suscripción** de lista de Hola de suscripciones disponibles. Todas las suscripciones que ofrecen servicio de almacén de claves de Hola se muestran en la lista desplegable de Hola.  

5. Seleccione un **Grupo de recursos** existente o cree uno.  

6. Seleccione hello **tarifa**.  
    >[!NOTE]
    > Los almacenes de claves de Azure Stack Development Kit admiten la SKU **Estándar** únicamente.

7. Elija **Directivas de acceso** existentes o cree una nueva. Directiva de acceso permite toogrant permisos para un usuario, aplicación o una seguridad agrupar las operaciones de tooperform con este almacén.  

8. Si lo desea, elija un **directiva de acceso avanzado** características de hello tooenable como el acceso a equipos de tooVirtual para la implementación, acceso tooResource Manager para la implementación de plantilla y acceso tooAzure cifrado del disco para el volumen cifrado. 
  
9.  Después de establecer la configuración de hello, haga clic en **Aceptar** y, a continuación, **crear**. Esto inicia la implementación de almacén de claves de Hola. 

## <a name="manage-keys-and-secrets"></a>Administración de claves y secretos

Después de crear un almacén, use Hola siguiendo los pasos toocreate y administración de claves y secretos en el almacén de Hola de.

## <a name="create-a-key"></a>Crear una clave

1. Inicie sesión en el portal de usuarios de toohello (https://portal.local.azurestack.external).  

2. En el panel de hello, haga clic en **todos los recursos** > almacén de claves de hello select que creó anteriormente > haga clic en hello **claves** icono.  

3. De hello **claves** hoja, haga clic en **agregar**. 

4. En hello **crear una clave** hoja, la lista de Hola de formulario de **opciones**, elija el método hello que desea toouse toocreate una clave. Puede **Generar** una nueva clave, **Cargar** una clave existente o **Restaurar copia de seguridad** de una clave.  

5. Escriba un **Nombre** para la clave. nombre de clave de Hola solo puede contener caracteres alfanuméricos y guiones de carácter especial de hello (-).  

6. Como alternativa, configure los valores de **Establecer la fecha de activación** y **Establecer fecha de expiración** para la clave.  

7. Haga clic en **crear** implementación de hello toostart.  

Después de que se crea correctamente la clave de hello, puede seleccionarlo de hello **claves** hoja y ver o modificar sus propiedades. sección de propiedades de Hello contiene Hola **identificador de clave de**, un URI que aplicaciones externas pueden tener acceso a esta clave. operaciones de toolimit en esta clave, configurar opciones en **las operaciones permitidas**.

![URI de clave](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a>Crear un secreto 

1. Inicie sesión en el portal de usuarios de toohello (https://portal.local.azurestack.external).  
2. En el panel de hello, haga clic en **todos los recursos** > almacén de claves de hello select que creó anteriormente > haga clic en hello **secretos** icono.  

3. De hello **secretos** hoja, haga clic en **agregar**.  

4. En hello **crear un secreto** hoja, en lista de Hola de **las opciones de carga**, elija una opción que se desea toocreate un secreto. Puede crear un secreto **manualmente** especificando un valor de secreto de Hola o cargue una **certificado** desde el equipo local.  

5. Escriba un **nombre** para secreto Hola. nombre de secreto Hola puede contener solo caracteres alfanuméricos y guiones de carácter especial de hello (-).  

6. Si lo desea, especifique hello **tipo de contenido**y configurar los valores de **establecer fecha de activación** y **establecer fecha de expiración** valores de secreto Hola.  

7. Haga clic en implementación de crear toostart Hola.  

Después de que el secreto de Hola se crea correctamente, puede seleccionarlo de hello **secretos** hoja y ver o modificar sus propiedades. sección de propiedades de Hello contiene **identificador de secreto**, un URI que aplicaciones externas pueden tener acceso a este secreto. 

![URI de secreto](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a>Pasos siguientes
* [Implementar una máquina virtual mediante la recuperación de contraseña de hello almacenada en un almacén de claves](azure-stack-kv-deploy-vm-with-secret.md)  
* [Implementar una VM con un certificado almacenado en un almacén de claves](azure-stack-kv-push-secret-into-vm.md)     


