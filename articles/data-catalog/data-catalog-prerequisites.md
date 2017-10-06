---
title: "requisitos previos del catálogo de datos de aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre los requisitos previos de hello que necesita tooget iniciado con el catálogo de datos de Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Requisitos previos de Catálogo de datos de Azure

Debe tootake cuidado algunas cosas para poder configurar el catálogo de datos de Azure. No se preocupe, este proceso lleva poco tiempo.

## <a name="azure-subscription"></a>Suscripción de Azure
tooset el catálogo de datos, debe ser propietario de Hola o copropietario de una suscripción de Azure.

Suscripciones de Azure le ayudarán a organizar los recursos de toocloud-servicio de acceso como el catálogo de datos. También le ayudan a controlar cómo se informa, factura y paga el uso de recursos. Cada suscripción puede tener una configuración de facturación y pago independiente, por lo que puede tener suscripciones y planes que varían según el departamento, proyecto, oficina regional, etc. Cada servicio en la nube pertenece tooa suscripción, y deberá toohave una suscripción antes de configurar el catálogo de datos. más información, consulte toolearn [administrar cuentas, suscripciones y roles administrativos](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset el catálogo de datos, debe haber iniciado sesión con una cuenta de usuario de Azure Active Directory (Azure AD).

Azure AD proporciona una manera sencilla para la identidad de negocio toomanage y acceso, tanto en la nube de Hola y local. Los usuarios pueden utilizar una sola cuenta profesional o educativa para tooany de inicio de sesión único en la nube y local de aplicación web. El catálogo de datos usa inicio de sesión en Azure AD tooauthenticate. más información, consulte toolearn [¿qué es Azure Active Directory?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> Mediante el uso de hello [portal de Azure](http://portal.azure.com/), puede iniciar sesión cuenta con una cuenta Microsoft personal o Azure Active Directory profesional o educativa. tooset el catálogo de datos mediante el uso de Hola o portal de Azure o hello [portal del catálogo de datos](http://www.azuredatacatalog.com), debe iniciar sesión con una cuenta de Azure Active Directory, no una cuenta personal.
>
>

## <a name="active-directory-policy-configuration"></a>Configuración de directivas de Active Directory
Puede darse el caso donde puede iniciar sesión en el portal del catálogo de datos de toohello, pero al intentar toosign en la herramienta de registro de origen de datos de toohello, recibirá un mensaje de error que le impide el inicio de sesión. Podría producirse un comportamiento de este problema solo cuando se encuentra en la red de empresa de Hola o puede ocurrir sólo cuando se conecta desde la red de empresa de hello fuera.

herramienta de registro de origen de datos de Hello utiliza autenticación mediante formularios toovalidate sus credenciales de usuario en Active Directory. toohelp que iniciar sesión correctamente, un administrador de Active Directory debe habilitar la autenticación de formularios de hello directiva de autenticación Global.

En la directiva de autenticación Global de hello, métodos de autenticación pueden ser conexiones habilitadas por separado para la intranet y extranet, tal y como se muestra en la siguiente captura de pantalla de Hola. Errores de inicio de sesión pueden ocurrir si la autenticación de formularios no está habilitada para red de Hola desde el que se está conectando.

 ![Directiva de autenticación global de Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea [Configuración de directivas de autenticación](https://technet.microsoft.com/library/dn486781.aspx).
