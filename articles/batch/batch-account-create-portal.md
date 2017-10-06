---
title: aaaCreate una cuenta de lote en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un lote de Azure cuenta hello Azure toorun portal las cargas de trabajo paralelas a gran escala en la nube de Hola"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Crear una cuenta de lote con hello portal de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](batch-account-create-portal.md)
> * [NET de Administración de Lote](batch-management-dotnet.md)
>
>

Obtenga información acerca de cómo toocreate un lote de Azure cuenta Hola [portal de Azure][azure_portal]y elija Propiedades de la cuenta de hello que se ajusten a su escenario de proceso. Obtenga información acerca de dónde propiedades de cuenta importante de toofind como teclas de acceso y las direcciones URL de cuenta.

Para obtener información acerca de los escenarios y las cuentas por lotes, vea hello [Introducción a las funciones](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Crear una cuenta de lote

Usar Hola portal toocreate una cuenta de lote en uno de dos hello *modos de asignación del grupo*: **por lotes servicio** modo o versiones más recientes de hello **suscripción de usuario** modo, que requiere más configuración. Para obtener información acerca de estos dos modos, vea hello [Introducción a las funciones](batch-api-basics.md#account). Para las características del modo de suscripción de usuario de hello, vea también hello [entrada de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Modo de servicio de Batch



1. Inicie sesión en toohello [portal de Azure][azure_portal].
2. Haga clic en **Nuevo** > **Proceso** > **Servicio de Batch**.

    ![Lote de hello Marketplace][marketplace_portal]
3. Hola **nueva cuenta de lote** hoja se muestra. Ver una descripción de hello debajo de cada elemento de la hoja.

    ![Crear una cuenta de lote][account_portal]

    a. **Nombre de la cuenta**: nombre de cuenta de lote Hola que elija debe ser único dentro de la región de Azure donde se crea la cuenta de Hola Hola (vea **ubicación** a continuación). nombre de la cuenta de Hello puede contener solo caracteres en minúsculas o números y debe ser 3 y 24 caracteres de longitud.

    b. **Suscripción**: Hola suscripción en qué hello toocreate cuenta de lote. Si tiene una sola suscripción, se selecciona de forma predeterminada.

    c. **Modo de asignación de grupo**: seleccione **Servicio Batch**.

    c. **Grupo de recursos**: seleccione un grupo de recursos existente para la nueva cuenta de Batch, o bien cree uno nuevo.

    d. **Ubicación**: Hola región de Azure en qué hello toocreate cuenta de lote. Solo las regiones de hello compatibles con su suscripción y el grupo de recursos se muestran como opciones.

    e. **Cuenta de almacenamiento** (opcional): cuenta de Azure Storage de uso general que se asocia a la cuenta de Batch. Se recomienda su uso para la mayoría de las cuentas de Batch. Consulte [Cuenta de Azure Storage vinculada](#linked-azure-storage-account) más adelante en este artículo para más información.

4. Haga clic en **crear** cuenta de hello toocreate.

   portal de Hello indica la implementación está en curso. Una vez completada, se mostrará la notificación **Implementaciones correctas** en **Notificaciones**.

## <a name="user-subscription-mode"></a>Modo de suscripción de usuario

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Permitir Azure Batch tooaccess suscripción hello (operación única)
Al crear la primera cuenta de lote en modo de suscripción de usuario, realizar Hola siguiendo los pasos tooregister su suscripción con el lote. (Si lo hizo anteriormente, omita la sección siguiente toohello.)

1. Inicie sesión en toohello [portal de Azure][azure_portal].

2. Haga clic en **más servicios** > **suscripciones**y haga clic en la suscripción de Hola que desee toouse para hello cuenta de lote.

3. Hola **suscripción** hoja, haga clic en **(de índices IAM) de control de acceso** > **agregar**.

    ![Control de acceso a la suscripción][subscription_access]

4. En hello **agregar permisos** hoja, seleccione hello **colaborador** rol, busque Hola API de lote. Buscar cada una de estas cadenas hasta que encuentre Hola API:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Los inquilinos más recientes de Azure AD pueden utilizar este nombre.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** es Id. de Hola para hello API de lote. 

5. Una vez que encuentre Hola API de lote, selecciónelo y haga clic en **guardar**.

    ![Adición de permisos de Batch][add_permission]

### <a name="create-a-key-vault"></a>Creación de un Almacén de claves
En el modo de suscripción de usuario, se requiere un almacén de claves de Azure que pertenece toothe mismo grupo de recursos como toobe de cuenta de lote Hola creado. Asegúrese de que el grupo de recursos de hello está en una región donde es el proceso por lotes [disponibles](https://azure.microsoft.com/regions/services/) y que es compatible con su suscripción.

1. Hola [portal de Azure][azure_portal], haga clic en **New** > **seguridad e identidad** > **el almacén de claves** .

2. Hola **crear el almacén de claves** hoja, escriba un nombre para el almacén de claves de Hola y crear un grupo de recursos en la región de Hola que desee para su cuenta de lote. Deje Hola restantes parámetros utilizando valores predeterminados, a continuación, haga clic en **crear**.

### <a name="create-a-batch-account"></a>Crear una cuenta de lote

1. Hola [portal de Azure][azure_portal], haga clic en **New** > **proceso** > **elservicioporlotes**.

    ![Lote de hello Marketplace][marketplace_portal]
3. Hola **nueva cuenta de lote** hoja se muestra. Ver una descripción de hello debajo de cada elemento de la hoja.

    ![Crear una cuenta de lote][account_portal_byos]

    a. **Nombre de la cuenta**: nombre de cuenta de lote Hola que elija debe ser único dentro de la región de Azure donde se crea la cuenta de Hola Hola (vea **ubicación** a continuación). nombre de la cuenta de Hello puede contener solo caracteres en minúsculas o números y debe ser 3 y 24 caracteres de longitud.

    b. **Suscripción**: si tiene más de una suscripción, seleccione la suscripción de Hola que ha registrado con hello servicio por lotes.

    c. **Modo de asignación de grupo**: seleccione **Suscripción del usuario**.

    d. **Almacén de claves**: almacén de claves de hello Select que creó para la cuenta de lote en la sección anterior de Hola. También puede crear un nuevo almacén de claves. Después de seleccionar el almacén de hello, seleccione Hola casilla toogrant Azure Batch acceso toohello el almacén de claves.

    c. **Grupo de recursos**: grupo de recursos de hello Select en la que creó el almacén de claves Hola.

    d. **Ubicación**: Hola región de Azure en la que creó el almacén de claves de Hola Hola cuenta de lote.

    e. **Cuenta de almacenamiento** (opcional): cuenta de Azure Storage de uso general que se asocia a la cuenta de Batch. Se recomienda su uso para la mayoría de las cuentas de Batch. Consulte [Cuenta de Almacenamiento de Azure vinculada](#linked-azure-storage-account) a continuación para más información.

4. Haga clic en **crear** cuenta de hello toocreate.

   portal de Hello indica la implementación está en curso. Una vez completada, se mostrará la notificación **Implementaciones correctas** en **Notificaciones**.



## <a name="view-batch-account-properties"></a>Visualización de propiedades de la cuenta de Lote
Una vez que se ha creado la cuenta de hello, puede abrir hello **hoja de la cuenta de lote** tooaccess su configuración y las propiedades. Puede tener acceso a todas las propiedades y configuración de la cuenta mediante el uso de menú de la izquierda Hola de hoja de cuenta de lote de Hola.

![Hoja Cuenta de Batch en el Portal de Azure][account_blade]

* **URL de la cuenta de lote**: al desarrollar una aplicación con hello [API de lote](batch-apis-tools.md#azure-accounts-for-batch-development), necesitará un tooaccess de dirección URL de la cuenta los recursos de proceso por lotes. Una URL de la cuenta de lote tiene Hola siguiendo el formato:

    `https://<account_name>.<region>.batch.azure.com`

![Dirección URL de la cuenta de Batch en el portal][account_url]

* **Las claves de acceso** (modo de servicio por lotes): tooauthenticate acceso tooyour cuenta de lote de la aplicación, necesitará una clave de acceso de cuenta. (Esta configuración no está disponible en el modo de suscripción de usuario, en el que se usa la autenticación de Azure Active Directory).

    tooview o regenerar claves de acceso de su cuenta de lote, escriba `keys` en el menú de la izquierda hello **búsqueda** cuadro hoja de cuenta de lote de hello, a continuación, seleccione **claves**.

    ![Claves de la cuenta de Lote en el Portal de Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Cuenta de Almacenamiento de Azure vinculada

Opcionalmente, puede vincular un uso general tooyour de cuenta cuenta de lote de almacenamiento de Azure. Hola [paquetes de aplicación](batch-application-packages.md) característica del lote utiliza el almacenamiento de blobs de Azure, igual hello [.NET de convenciones de archivo por lotes](batch-task-output.md) biblioteca. Estas características opcionales le ayudará a implementar aplicaciones de Hola que se ejecutan las tareas por lotes y conservar los datos de Hola que generan.

Se recomienda crear una cuenta de Storage nueva para que la use exclusivamente su cuenta de Batch.

![Creación de una cuenta de almacenamiento de uso general][storage_account]

> [!NOTE]
> Lote de Azure admite actualmente solo Hola almacenamiento cuenta tipos de uso general. Este tipo de cuenta se describe en el paso 5, [Crear una cuenta de almacenamiento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), de [Acerca de las cuentas de Azure Storage](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Tenga cuidado al volver a generar las claves de acceso de Hola de una cuenta de almacenamiento vinculada. Volver a generar solo una clave de cuenta de almacenamiento y haga clic en **claves sincronización** en hello vinculado hoja de la cuenta de almacenamiento. Espere cinco minutos tooallow Hola claves toopropagate toohello nodos de cálculo en los grupos, a continuación, volver a generar y sincronizar Hola otra clave si es necesario. Si vuelve a generarlas claves en hello mismo tiempo, los nodos de proceso no será capaz de toosynchronize la clave y perderá la cuenta de almacenamiento de toohello de acceso.
>
>

![Regeneración de claves de cuenta de almacenamiento][4]

## <a name="batch-service-quotas-and-limits"></a>Límites y cuotas del servicio Lote
Ten en cuenta que como con la suscripción de Azure y otro Azure servicios, ciertos [cuotas y límites](batch-quota-limit.md) tooBatch cuentas se aplican. Las cuotas de actuales de una cuenta de lote aparecen en portal de hello en la cuenta de hello **propiedades**.

![Cuotas de la cuenta de Lote en el Portal de Azure][quotas]



Además, muchas de estas cuotas pueden aumentarse simplemente con una solicitud de soporte técnico de producto gratuito enviada en hello portal de Azure. Vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener más información sobre cómo aumentar la cuota se solicita.

## <a name="other-batch-account-management-options"></a>Otras opciones de administración de la cuenta de Lote
Además toousing Hola portal de Azure, también puede crear y administrar cuentas de lote con siguiente hello:

* [Cmdlets de PowerShell de Batch](batch-powershell-cmdlets-get-started.md)
* [CLI de Azure](batch-cli-get-started.md)
* [NET de Administración de Lote](batch-management-dotnet.md)

## <a name="next-steps"></a>Pasos siguientes
* Vea hello [Introducción a la característica por lotes](batch-api-basics.md) toolearn más información sobre características y conceptos del servicio por lotes. artículo de Hola describe los recursos de proceso por lotes principales hello como grupos, los nodos de proceso, trabajos y tareas y proporciona una visión general de hello características del servicio que permiten la ejecución de la carga de trabajo de proceso a gran escala.
* Información sobre conceptos básicos de Hola de desarrollar una aplicación habilitada por lotes con hello [biblioteca de cliente .NET de lote](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md). Estos artículos de Introducción le guiará a través de una aplicación que usa Hola lote servicio tooexecute una carga de trabajo en varios nodos de ejecución e incluye el uso de almacenamiento de Azure para recuperación y almacenamiento provisional del archivo de carga de trabajo.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Regeneración de claves de cuenta de almacenamiento"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
