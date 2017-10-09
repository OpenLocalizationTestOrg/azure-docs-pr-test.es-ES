---
title: aaaMigrate de Azure RemoteApp tooCitrix XenApp Essentials | Documentos de Microsoft
description: "¿Cómo toomigrate de Azure RemoteApp tooCitrix XenApp Essentials"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Migrar de Azure RemoteApp tooCitrix XenApp Essentials

Si usas RemoteApp de Azure y desea toomigrate tooCitrix XenApp Essentials, hay algunos de los requisitos previos tookeep en cuenta. En primer lugar, lea la [guía de implementación técnica paso a paso de Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) y su [biblioteca técnica en línea](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Pasos de requisitos previos para la migración

1. Cree una red virtual nueva o determine en qué red virtual de Azure de Azure Resource Manager va a implementar Citrix XenApp Essentials. RemoteApp de Azure utiliza Hola portal de Azure clásico; Citrix XenApp Essentials sólo es compatible con el Administrador de recursos de Azure.  
2. Asegurarse de esa red virtual de Hola que seleccionó no tiene controlador de dominio tooyour acceso a redes porque Citrix sólo es compatible con las implementaciones híbridas. Si utilizas una implementación de nube de Azure RemoteApp, asegúrese de que la red virtual tiene el controlador de dominio de Active Directory de tooan de acceso a redes. También puede usar Azure Active Directory Domain Services (Azure AD DS). 
3. Asegúrese de que DNS está configurado correctamente para la red virtual de hello, por lo que esa unión a un dominio es correcta en el primer intento de Hola. Puede crear una máquina virtual (VM) en la red virtual de Hola que seleccionó y realizar un tooverify de combinación manual de los dominios que Hola DNS y unirse a un dominio funciona según lo previsto. Esto garantiza que es correcta Hola primera vez que implemente Citrix XenApp Essentials. 
4. En caso de que sea necesario, cree un emparejamiento de red virtual entre una red virtual del Portal de Azure clásico que usa con Azure RemoteApp y la red virtual de Azure Resource Manager. Si las redes Hola dos residen en hello igual que funciona este proceso emparejamiento región. Si no lo hace, use redes virtuales de sitio a sitio VPN tooconnect Hola para las redes. 
5. Si es necesario, lea [cómo toomigrate datos dentro y fuera de Azure RemoteApp](remoteapp-migrate.md). 
6. Actualizar su Hola de tooinclude de imagen existente de Azure RemoteApp componente Citrix VDA (para obtener instrucciones, consulte la documentación de Citrix de hello). 
7. Vaya toohello Azure Marketplace y comenzar la implementación de Citrix XenApp Essentials.

## <a name="other-considerations"></a>Otras consideraciones

Tenga en cuenta las siguientes consideraciones adicionales cuando se migra de hello:
- Citrix XenApp Essentials solo admite implementaciones híbridas. En otras palabras, requiere el controlador de dominio de tooa de acceso de red en la unión a un dominio tooperform orden. Si usa una implementación de nube de Azure RemoteApp, utilice Azure AD DS o asegúrese de que la red virtual tiene acceso tooActive directorio para unirse a un dominio. 
- toolearn tooCitrix de datos de usuario de toomove XenApp Essentials, vea [cómo toomigrate datos dentro y fuera de Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials solo admite cuentas de Active Directory. No se admiten cuentas de Microsoft (como outlook.com, msn.com o hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Facturación de Citrix XenApp Essentials

Para obtener detalles completos sobre los precios, vea hello [preguntas más frecuentes sobre](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) y [artículo de información general de Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Hay tres componentes de facturación tooCitrix XenApp Essentials:

- Hola Citrix cargo por servicio, que es 12 USD por usuario al mes. Al igual que todas las compras de Azure Marketplace, esto es el método de pago de facturación toohello asociado a su suscripción de Azure. Los clientes de Contrato Enterprise (EA) no pueden usar los créditos monetarios de Azure. 
- Licencias de acceso de cliente (CAL) de Servicios de datos remotos (RDS). Actualmente, puede adquirir Hola cuota de acceso remoto que está integrado con hello pago Citrix XenApp Essentials para $6,25. Si es un cliente EA, puede usar los créditos monetarios Azure toopay para este. Si desea toouse las CAL de RDS existentes, póngase en contacto con nosotros en [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), por lo que podemos aplicar este efecto tooyour. 
- Proceso y almacenamiento de Azure. Se trata de costo de almacenamiento de Azure de Hola y el consumo de proceso para las máquinas virtuales de hello utilizado. El precio es un factor que conviene tener en cuenta al seleccionar el tamaño de la máquina virtual y la densidad de usuarios. Si es un cliente EA, puede usar los créditos monetarios Azure toopay para este.

Si tiene más preguntas:
- Envíenos un correo electrónico a [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
- [Póngase en contacto con el equipo de soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Empiece por [abrir un caso de soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp con requisitos previos de los pasos 1 a 5. Para conocer los pasos 6 y 7, póngase en contacto con Citrix abriendo una incidencia de soporte técnico en el portal de administración de Citrix Hola. 
