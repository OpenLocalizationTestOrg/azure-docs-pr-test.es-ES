---
title: aaaEnable cifrado para la cuenta de almacenamiento en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendaciones de Azure Security Center ** habilitar el cifrado para Azure almacenamiento cuenta **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Habilitación del cifrado para la cuenta de Azure Storage en Azure Security Center
Azure Security Center puede recomendar que habilite el cifrado del servicio de Azure Storage para datos en reposo.

Cifrado de servicio de almacenamiento (SSE) funciona al cifrar los datos de hello cuando se escribe tooAzure almacenamiento y descifrar datos Hola antes de la recuperación.  SSE actualmente solo está disponible para hello servicio Blob de Azure y puede usarse para blobs en bloques, blobs de página y blobs en anexos.  más información, consulte toolearn [cifrado del servicio de almacenamiento de datos en reposo](../storage/common/storage-service-encryption.md).


> [!Note]
> Después de habilitar el cifrado, se cifran únicamente los datos nuevos. Los blobs existentes en la cuenta de almacenamiento permanecen sin cifrar. tooencrypt blobs existentes, vea hello [preguntas más frecuentes sobre el cifrado del servicio de almacenamiento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

El Cifrado del servicio de almacenamiento solo se admite en las cuentas de almacenamiento de Resource Manager. Las cuentas de almacenamiento clásico no se admiten en este momento. Hola toounderstand clásico y modelos de implementación del Administrador de recursos, consulte [modelos de implementación de Azure](../azure-classic-rm.md).

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  Este documento no es una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **habilitar el cifrado para la cuenta de almacenamiento de Azure**.
   ![Habilitar el cifrado para la cuenta de almacenamiento][1]
2. Hola **Habilitar cifrado de almacenamiento** abre la hoja. Esta hoja enumera las cuentas de almacenamiento de Azure Hola donde se deshabilita el cifrado de almacenamiento. En este ejemplo, vamos a seleccionar **storageacct1**.
   ![Habilitar el cifrado de almacenamiento][2]
3. Hola **cifrado** hoja para **storageacct1** se abre. Seleccione **Habilitado**.
   ![Hoja de cifrado][3]
4. Seleccione **Guardar**.

Ahora ha habilitado el cifrado de almacenamiento para **storageacct1**.


## <a name="see-also"></a>Otras referencias
Este documento se ha explicado cómo tooimplement Hola centro de seguridad recomendación "Habilitar el cifrado para la cuenta de almacenamiento de Azure." toolearn más información acerca del cifrado del servicio de almacenamiento de Azure, vea Hola recursos siguientes:

* [Cifrado del servicio Azure Storage para datos en reposo (versión preliminar)](../storage/common/storage-service-encryption.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) -Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) -Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) -Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) -buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
