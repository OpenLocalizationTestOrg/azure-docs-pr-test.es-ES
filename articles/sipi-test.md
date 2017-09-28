---
title: Archivo de prueba de Sipi | Documentos de Microsoft
description: Archivo de prueba para comprobar las dependencias de ReadyForTest
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Archivo de prueba de Sipi

Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos. Cuando haya terminado, la aplicación se habrá registrado para su uso en el inquilino de Azure B2C.

## <a name="prerequisites"></a>Requisitos previos

Para crear una aplicación que acepte registros e inicios de sesión de consumidores, primero deberá registrarla en un inquilino de Azure Active Directory B2C. Para obtener su propio inquilino, siga los pasos descritos en [Creación de un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).

Las aplicaciones creadas en la hoja de Azure AD B2C de Azure Portal se deben administrar desde la misma ubicación. Si edita las aplicaciones B2C mediante PowerShell u otro portal, dejan de ser compatibles y no funcionan con Azure AD B2C. Consulte los detalles en la sección [Aplicaciones con errores](#faulted-apps). 

## <a name="navigate-to-b2c-settings"></a>Ir a la configuración de B2C

Inicie sesión en [Azure Portal](https://portal.azure.com/) como administrador global del inquilino B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Elija los pasos siguientes en función del tipo de aplicación que vaya a registrar:
