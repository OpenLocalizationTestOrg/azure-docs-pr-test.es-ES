---
title: Archivo de prueba de Sipi | Documentos de Microsoft
description: Probar las dependencias de archivo toocheck ReadyForTest
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a>Archivo de prueba de Sipi

Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos. Cuando haya terminado, la aplicación se registra para su uso en el inquilino de hello Azure B2C.

## <a name="prerequisites"></a>Requisitos previos

toobuild una aplicación que acepta consumidor registrarse e iniciar sesión, necesita primero la aplicación de hello tooregister con un inquilino de Azure Active Directory B2C. Obtener su propio inquilino mediante el uso de pasos de hello descritos en [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).

Aplicaciones creadas a partir de la hoja de Azure AD B2C Hola Hola portal de Azure deben administrarse desde Hola misma ubicación. Si edita las aplicaciones de B2C Hola con PowerShell u otro portal, que se convierten en no compatibles y no funcionan con Azure AD B2C. Ver detalles de hello [errores en aplicaciones](#faulted-apps) sección. 

## <a name="navigate-toob2c-settings"></a>Desplácese tooB2C configuración

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como Hola administrador Global del inquilino de hello B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Elija los pasos siguientes en función de tipo de aplicación Hola que va a registrar:
