---
title: "¿aaaWhat contiene imágenes de plantilla de hello Azure RemoteApp? | Microsoft Docs"
description: "Obtenga información acerca de las imágenes de plantilla de hello incluidas con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>¿Qué es imágenes de plantilla de hello Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

La suscripción de Azure RemoteApp incluye tres imágenes de plantilla:

* Windows Server 2012
* Microsoft Office 365 ProPlus (se requiere suscripción a Office 365)
* Microsoft Office Professional Plus 2013 (solo versión de prueba)

> [!IMPORTANT]
> Su suscripción de Azure RemoteApp concede que acceso toohello software en imágenes de hello, con excepción de Hola de Office 365 ProPlus, lo que requiere una suscripción independiente, y Office 2013, que no se puede usar en producción. Esto significa que puede compartir programas Hola o aplicaciones en imágenes de plantilla de hello con los usuarios. Por ejemplo, si crea una recopilación que use la imagen de Windows Server 2012 R2 de hello, puede publicar System Center Endpoint Protection para tooaccess a los usuarios a través de RemoteApp.
> 
> Extraer del repositorio hello [RemoteApp licencias detalles](remoteapp-licensing.md) para obtener más información. Y [usando Office con Azure RemoteApp](remoteapp-o365.md) para hello información de licencia de Office.
> 
> 

Siga leyendo para obtener más información sobre lo que contiene cada imagen.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("hello vainilla imagen")
Esta imagen se basa en el sistema operativo de Microsoft Windows Server 2012 R2 Datacenter y hello siguientes roles y características instaló toomeet requisitos de Hola para imágenes de plantilla de RemoteApp de Azure:

* .NET Framework 4.5, 3.5.1, 3.5
* Experiencia de escritorio
* Servicios de Escritura con lápiz y Escritura a mano
* Media Foundation
* Host de sesión de Escritorio remoto
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Compatibilidad con WoW64

Esta imagen también tiene Hola después de las aplicaciones instaladas:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (se requiere suscripción)
Office 365 es Hola más aplicación solicitada, por lo que se crea una imagen de "custom" toowork con.

Esta imagen es una extensión de imagen de vainilla hello y tiene hello siguientes componentes de Microsoft Office 365 ProPlus además toohello componentes instalados que se describe en la imagen de Windows Server 2012 R2 de hello:

* Access
* Excel
* Lync
* OneNote
* OneDrive para la empresa (tenga en cuenta ese agente de sincronización de hello no se admite para su uso con Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Herramientas de corrección de Microsoft Office

imagen de Hello también incluye Visio Pro y Project Pro.

Y Hola derivados de la solicitud, así:

* SQL Native Client
* Controlador ODBC
* Cliente de minería de datos para SQL Server
* Cliente MasterDataServices
* Microsoft Publisher
* PowerQuery
* PowerMap

La funcionalidad completa de las aplicaciones de Office 365 ProPlus está disponible solo para los usuarios que tienen un plan de Office 365 ProPlus. Para obtener más detalles sobre la suscripción de Office 365 Hola vea planes [planes de servicio de Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). ¿Todavía tiene preguntas? Extraer del repositorio hello [Office 365 + RemoteApp](remoteapp-o365.md) información. Desproteger nuevo artículo de hello, [cómo toouse la suscripción a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).

Tenga en cuenta que necesita toolicense Office 365 ProPlus, Visio Pro y proyecto Pro por separado, cada uno de ellos tiene su propia licencia.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office Professional Plus 2013 (solo versión de prueba)
Durante el período de evaluación gratuita de hello, puede probar servicio Hola con imagen Hola Office 2013.

Esta imagen es una extensión de imagen de vainilla hello y tiene hello siguientes componentes de Microsoft Office 2013 Professional Plus además toohello componentes instalados que se describe en la imagen de Windows Server 2012 R2 de hello:

* Access
* Excel
* Lync
* OneNote
* OneDrive para la empresa (tenga en cuenta ese agente de sincronización de hello no se admite para su uso con Azure RemoteApp)
* Outlook
* PowerPoint
* proyecto
* Visio
* Word
* Herramientas de corrección de Microsoft Office

> [!IMPORTANT]
> **Información legal** : esta imagen no incluye una licencia de Microsoft Office y *no se puede usar en producción*. imagen de Office 2013 Professional Plus Hola está pensado solo para fines de prueba. Si desea que las aplicaciones de Office toouse en Azure RemoteApp para la producción, debe imagen de Office 365 ProPlus toouse Hola. Para obtener más detalles sobre las licencias de Office, consulte [Uso de Office 365 con Azure RemoteApp](remoteapp-o365.md)
> 
> 

