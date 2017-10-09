---
title: "aaaSetting seguridad denominado las credenciales de autenticación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo el servicio de nube credenciales tootooprovide que Visual Studio pueda utilizar tooauthenticate solicitudes tooAzure toopublish una tooAzure de aplicación desde Visual Studio o toomonitor existente... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Configuración de credenciales de autenticación con nombre
toopublish una tooAzure de aplicación desde Visual Studio o toomonitor un servicio de nube existente, debe proporcionar las credenciales que Visual Studio pueda utilizar tooauthenticate solicita tooAzure. Hay varios lugares en Visual Studio donde puede iniciar sesión en tooprovide estas credenciales. Por ejemplo, en Explorador de servidores de hello, puede abrir menú contextual Hola Hola **Azure** nodo y elija **conectar tooMicrosoft suscripción de Azure...** . Al iniciar sesión, información de suscripción de hello asociada con su cuenta de Azure está disponible en Visual Studio y no hay nada más que tiene toodo.

Herramientas de Azure también admite una forma más antigua de proporcionar credenciales, mediante el archivo de suscripción de hello (archivo .publishsettings). En este tema se describe este método, que todavía se admite en el SDK 2.2 de Azure.

Hola siguientes elementos es necesario para la autenticación tooAzure:

* Su Id. de suscripción
* Un certificado X.509 v3 válido

> [!NOTE]
> longitud de Hola de clave del certificado X.509 v3 Hola debe ser al menos 2048 bits. Azure rechazará cualquier certificado que no cumpla este requisito o que no sea válido.
>
>

Visual Studio usa el identificador de suscripción junto con los datos del certificado hello como credenciales. las credenciales adecuadas de Hola se hace referencia en hello suscripción (archivo .publishsettings), que contiene una clave pública para el certificado de Hola. archivo de suscripción de Hello puede contener credenciales de más de una suscripción.

Puede editar información de suscripción de Hola de hello **nueva/Editar suscripción** cuadro de diálogo, como se explica más adelante en este tema.

Si desea toocreate un certificado usted mismo, puede hacer referencia a instrucciones toohello [crear y cargar un certificado de administración para Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) y, a continuación, cargar manualmente Hola certificado toohello [portal de Azure clásico ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Estas credenciales que Visual Studio requiere toomanage que no son servicios en la nube Hola mismas credenciales que están tooauthenticate requiere una solicitud en servicios de almacenamiento de Azure de Hola.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importación, configuración o edición de las credenciales de autenticación en Visual Studio
Puede importar, configurar o modificar las credenciales de autenticación en hello **nueva suscripción** cuadro de diálogo que aparece si lleva a cabo Hola después de acción:

* En **Explorador de servidores**, abra menú contextual Hola Hola **Azure** nodo, elija **administrar y filtrar suscripciones...** , elija hello **certificados** ficha y siga uno de los procedimientos de hello:

    * Elija **importar** diálogo de tooopen Hola Importar suscripciones de Microsoft Azure donde podrá descargar archivo de las suscripciones de hello para hello actualmente cargado o suscripción, tooits de examinar la ubicación de descarga y, a continuación, importarlo para su uso en autenticación.
    * Elija **New** diálogo de nueva suscripción de hello tooopen donde puede configurar una nueva suscripción para su uso en la autenticación.
    * Elija **editar** (después de elegir su suscripción activa) diálogo de Editar suscripción hello tooopen donde puede editar una suscripción existente para su uso en la autenticación. 

Hello siguiente procedimiento se da por supuesto que hello **nueva suscripción** cuadro de diálogo está abierto.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset credenciales de autenticación en Visual Studio
1. Hola **seleccionar un certificado existente** para lista de autenticación, seleccione un certificado.
2. Elija hello **ruta de acceso completa de copia hello** vínculo. ruta de acceso de Hello para el certificado de hello (archivo .cer) es copiada toohello Portapapeles.

   > [!IMPORTANT]
   > toopublish su aplicación de Azure desde Visual Studio, debe cargar este certificado toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload Hola certificado toohello portal de Azure:

   1. Abra hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. Si se le solicita, inicie sesión en el portal de toohello y, a continuación, navegue demasiado**configuración**, **certificados de administración**.
   3. En el panel de certificados de administración de hello, elija **cargar**.
   4. Seleccione la suscripción de Azure, pegue Hola ruta de acceso completa del archivo .cer de Hola que acaba de crear y elija **cargar**.
