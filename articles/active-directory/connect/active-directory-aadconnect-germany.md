---
title: aaaAzure AD Connect en Microsoft Cloud Alemania
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite tooprovide una identidad común para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD."
keywords: "Introducción tooAzure AD Connect, información general de Azure AD Connect, ¿qué es Azure AD Connect, instalar active directory, Alemania, bosque negro"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Azure AD Connect en Microsoft Cloud Germany- Versión preliminar pública
## <a name="introduction"></a>Introducción
Azure AD Connect proporciona sincronización entre instancias de Active Directory y Azure Active Directory locales.
Actualmente, muchos de los escenarios de hello en [Alemania Microsoft Cloud](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) debe realizarla de operador de Hola. Al usar Microsoft Cloud Alemania, debe tener en cuenta los siguiente hello:

* Hola que direcciones URL siguientes deben estar abiertas en un servidor proxy para sincronización toooccur correctamente:
  
  * *. microsoftonline.de
  * *.windows.net
  * * Listas de revocación de certificados
* Al iniciar sesión en el directorio de Azure AD tooyour, debe usar una cuenta de dominio de onmicrosoft.de Hola.
* Hola siguientes características no está disponible:
  * Azure AD Connect Health
  * Actualizaciones automáticas
 
## <a name="download"></a>Descargar
Puede descargar Azure AD Connect de hoja de Azure AD Connect hello en el portal de Hola.  Siga las instrucciones de Hola por debajo de la hoja de toolocate hello Azure AD Connect.

### <a name="hello-azure-ad-connect-blade"></a>Hola hoja de Connect de Azure AD
Una vez que haya iniciado sesión toohello portal de Azure, Hola siguientes:

1. Vaya tooBrowse
2. Seleccione Azure Active Directory.
3. Después, seleccione Azure AD Connect.

Debería ver Hola siguiente:

![Hoja Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

Hello tabla siguiente describen características de Hola se muestra en la hoja de Hola.

| Título | Description |
| --- | --- |
| ESTADO DE SINCRONIZACIÓN |Le permite saber si la sincronización está habilitada o no. |
| ÚLTIMA SINCRONIZACIÓN |Hola última vez una sincronización correcta completada. |
| DOMINIOS FEDERADOS |Muestra el número de Hola de dominios federados configurado actualmente. |

## <a name="installation"></a>Instalación
tooinstall Azure AD Connect, puede usar la documentación de hello [aquí](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Características avanzadas e información adicional
Para obtener información adicional e instrucciones sobre la configuración personalizada o configuraciones avanzadas, empiece con la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).  Esta página proporciona información y vínculos tooadditional instrucciones.

