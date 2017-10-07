---
title: "aaaAzure cifrado del servicio de almacenamiento mediante el cliente administrado claves en el almacén de claves de Azure | Documentos de Microsoft"
description: "Use Hola cifrado del servicio de almacenamiento de Azure característica tooencrypt el almacenamiento de blobs de Azure en el lado del servicio de hello al almacenar los datos de Hola y descifrarlo al recuperar datos de hello mediante cliente claves administradas."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Storage Service Encryption mediante claves administradas por el cliente en Azure Key Vault

Microsoft Azure es toohelping firme compromiso de proteger y proteger su toomeet de datos de la seguridad de la organización y los compromisos de cumplimiento de normas.  Una manera puede proteger los datos en reposo es toouse cifrado de servicio de almacenamiento (SSE), que cifra los datos al escribir toostorage automáticamente y descifra los datos al recuperarlos. Hola cifrado y descifrado es completamente transparente y automática y usa 256 bits [el cifrado AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), uno de bloque más fuerte Hola cifrados disponibles.

Puede usar claves de cifrado administradas por Microsoft con SSE o puede utilizar sus propias claves de cifrado. En este artículo trataremos más Hola este último. Para más información sobre el uso de claves administradas por Microsoft, o sobre SSE en general, vea [Storage Service Encryption para datos en reposo](storage-service-encryption.md).

tooprovide Hola capacidad toouse en sus propias claves de cifrado de SSE para el almacenamiento de blobs se integra con el almacén de claves de Azure (claves). Puede crear sus propias claves de cifrado y almacenarlos en claves, o puede usar claves de cifrado de claves API toogenerate. No sólo claves permiten toomanage y controlar las claves, también permite tooaudit el uso de claves. 

¿Por qué desearía toocreate sus propias claves? Le ofrece más flexibilidad, incluyendo toocreate de capacidad de hello, girar, deshabilitar y definir controles de acceso y tooprotect de tooaudit Hola cifrado claves que se utilizan los datos.

## <a name="sse-with-customer-managed-keys-preview"></a>SSE con la versión preliminar de las claves administradas de por el cliente

Esta funcionalidad actualmente está en su versión preliminar. toouse esta característica, deberá toocreate una nueva cuenta de almacenamiento. Puede crear un almacén de claves y una clave nuevos, o bien puede usar un almacén de claves y una clave existentes. cuenta de almacenamiento de Hola y el almacén de claves de hello deben estar en hello puede ser la misma región, pero en distintas suscripciones.

tooparticipate en la vista previa de hello póngase en contacto con [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Se proporcionará un vínculo especial tooparticipate en la vista previa de Hola.

toolearn más información, consulte toohello [preguntas más frecuentes sobre](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Debe registrarse para pasos de Hola Hola preview toofollowing anterior de este artículo. Sin acceso de vista previa, no podrá ser capaz de tooenable esta característica en el portal de Hola.

## <a name="getting-started"></a>Introducción
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Paso 1: [Crear una cuenta de almacenamiento nueva](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Paso 2: Habilitar el cifrado
Puede habilitar SSE Hola cuenta de almacenamiento con hello [portal de Azure](https://portal.azure.com). En la hoja de configuración de Hola Hola cuenta de almacenamiento, busque Hola sección del servicio Blob como se muestra en la figura a continuación y haga clic en el cifrado.

![Captura de pantalla del portal que muestra la opción de cifrado](./media/storage-service-encryption/image1.png)
<br/>*Habilitar SSE para Blob service*

Si desea que tooprogrammatically habilitar o deshabilitar Hola cifrado del servicio de almacenamiento en una cuenta de almacenamiento, puede usar hello [API de REST de proveedor de recursos de almacenamiento de Azure](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [biblioteca de cliente del proveedor de recursos de almacenamiento para .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), o hello [CLI de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

En esta pantalla, si no ve la casilla "usar su propia clave" Hola, no ha se ha aprobado para la vista previa de Hola. Envíe un correo electrónico[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) y solicitar la aprobación.

![Captura de pantalla del portal que muestra la versión preliminar del cifrado](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

De forma predeterminada, SSE utilizará claves administradas de Microsoft. toouse sus propias claves, active la casilla de Hola. A continuación, puede especificar su clave de URI o seleccionar una clave y un almacén de claves de selector de Hola.

## <a name="step-3-select-your-key"></a>Paso 3: Seleccionar su clave

![Captura de pantalla del portal que muestra el cifrado con la opción de uso de su propia clave](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Captura de pantalla del portal que muestra el cifrado con la opción de especificación del UIR de la clave](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Si cuenta de almacenamiento de hello no tiene acceso toohello el almacén de claves, puede ejecutar Hola siguiente comando mediante cuentas de almacenamiento de toohello en acceso de Azure Powershell toogrant toohello requiere el almacén de claves.

![Captura de pantalla de portal que muestra el acceso denegado para el almacén de claves](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

También puede conceder acceso a través del portal de Azure hello toohello el almacén de claves de Azure en hello portal de Azure y conceder acceso a cuenta de almacenamiento de toohello.

## <a name="step-4-copy-data-toostorage-account"></a>Paso 4: Copia de cuentas de toostorage de datos
Si desea que tootransfer datos en la nueva cuenta de almacenamiento, por lo que se cifra, consulte demasiado[paso 3 de introducción en el cifrado de servicio de almacenamiento de datos en reposo](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Paso 5: Consultar el estado del programa Hola Hola de datos cifrados
estado de hello tooquery de datos de hello cifrado Consulte demasiado[paso 4 de introducción en el cifrado de servicio de almacenamiento de datos en reposo](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Preguntas más frecuentes acerca de Cifrado del servicio de Almacenamiento para datos en reposo
**P: Uso Premium Storage. ¿Puedo usar SSE con claves administradas por el cliente?**

R: Sí, SSE con claves administradas por Microsoft y claves administradas el cliente es compatible tanto con almacenamiento estándar como con almacenamiento premium. 

**P: ¿Puedo crear cuentas de almacenamiento con SSE con claves administradas por el cliente habilitado a través de Azure PowerShell y la CLI de Azure?**

R: Sí.

**P: ¿Cuánto aumenta el costo de Azure Storage si se habilita SSE con claves administradas por el cliente?**

R: Hay un costo asociado para usar Azure Key Vault. Para más información, visite [Key Vault Precios](https://azure.microsoft.com/en-us/pricing/details/key-vault/). No hay ningún coste adicional por usar SSE.

**P: ¿puedo revocar el acceso a claves de cifrado de toohello?**

R: Sí, puede revocar el acceso en cualquier momento. Hay varias maneras toorevoke acceso tooyour claves. Consulte demasiado[almacén de claves de Azure PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) y [CLI de almacén de claves de Azure](https://docs.microsoft.com/en-us/cli/azure/keyvault) para obtener más detalles. Revocar el acceso eficazmente bloqueará el acceso tooall blobs en la cuenta de almacenamiento de hello como Hola clave de cifrado de la cuenta no es accesible por el almacenamiento de Azure.

**P: ¿puedo crear una cuenta de almacenamiento y un clave en una región diferente?**

R: no, la cuenta de almacenamiento de Hola y almacén clave necesidad toobe en Hola misma región. 

**P: ¿puedo habilitar SSE con claves administradas por el cliente durante la creación de cuenta de almacenamiento de hello?**

R.: No. Cuando se habilita SSE al crear la cuenta de almacenamiento de hello, solo se pueden usar claves de administrada por Microsoft. Si desea que las claves de toouse administradas por el cliente deberá propiedades de la cuenta de almacenamiento de tooupdate Hola. Puede usar REST o uno de tooprogrammatically de bibliotecas de cliente de almacenamiento de hello actualizar su cuenta de almacenamiento, o actualizar propiedades de la cuenta de almacenamiento hello mediante Hola Portal de Azure después de crear la cuenta de hello.

**P: ¿Puedo deshabilitar el cifrado mientras utilizo SSE con claves administradas por el cliente?**

R: No, no puede deshabilitar el cifrado mientras utiliza SSE con claves administradas por el cliente. cifrado de toodisable, necesitará las claves de tooswitch toousing administrada por Microsoft. Puede hacerlo mediante el portal de Azure de Hola o PowerShell.

**P: ¿SSE está habilitado de manera predeterminada cuando creo una cuenta de almacenamiento?**

R: SSE no está habilitado de forma predeterminada; Puede usar hello tooenable de portal de Azure. Mediante programación, puede habilitar esta característica con hello API de REST de proveedor de recursos de almacenamiento. 

**P: No puedo habilitar el cifrado en mi cuenta de almacenamiento.**

R: ¿Es una cuenta de almacenamiento de Resource Manager? Las cuentas de almacenamiento clásico no son compatibles. SSE con claves administradas por el cliente también se puede habilitar únicamente en las cuentas de almacenamiento de Resource Manager recién creadas.

**P: ¿Solo se permite en determinadas regiones a SSE con claves administradas por el cliente?**

R: SSE está disponible solamente en determinadas regiones para Blob Storage para esta versión preliminar. Envíe un correo electrónico [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck para obtener más información sobre la vista previa y disponibilidad. 

**P: ¿cómo póngase en contacto con alguien si tiene algún problema o desea tooprovide comentarios?**

R: póngase en contacto con [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) para ver los problemas relacionados con tooStorage cifrado del servicio. 

## <a name="next-steps"></a>Pasos siguientes

*   Para obtener más información sobre el conjunto completo de Hola de seguridad funcionalidades que ayudan a los desarrolladores crear aplicaciones seguras, vea hello [Guía de seguridad de almacenamiento](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Para información general sobre Azure Key Vault, consulte [¿Qué es Azure Key Vault?](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)
*   Para una introducción sobre Azure Key Vault, consulte [Introducción al Almacén de claves de Azure](../key-vault/key-vault-get-started.md).
