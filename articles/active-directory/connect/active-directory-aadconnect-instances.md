---
title: "Azure AD Connect: instancias de servicio de sincronización | Microsoft Docs"
description: "Esta página documenta las consideraciones especiales para instancias de Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: consideraciones especiales para instancias
Azure AD Connect se utiliza normalmente con la instancia de todo el mundo Hola de Azure AD y Office 365. Pero también hay otras instancias y estas tienen requisitos diferentes para las direcciones URL y otras consideraciones especiales.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Germany
Hola [Alemania Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) es una nube soberano operada por un usuario de confianza de alemán de datos.

| Tooopen de direcciones URL en el servidor proxy |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| +Listas de revocación de certificados |

Al iniciar sesión en el inquilino de Azure AD tooyour, debe usar una cuenta de dominio de onmicrosoft.de Hola.

Características actualmente no está presentes en hello Microsoft Cloud Alemania:

* **Azure AD Connect Health** no está disponible.
* Las **actualizaciones automáticas** no están disponibles.
* La **escritura diferida de contraseñas** está disponible en versión preliminar con Azure AD Connect versión 1.1.570.0 y posteriores.
* Otros servicios de Azure AD Premium no están disponibles.

## <a name="microsoft-azure-government-cloud"></a>Microsoft Azure Government Cloud
Hola [nube de Microsoft Azure Government](https://azure.microsoft.com/features/gov/) es una nube de gobierno de Estados Unidos.

Esta nube ha sido compatible con versiones anteriores de DirSync. De compilación 1.1.180 de Azure AD Connect, Hola siguiente generación de nube de hello es compatible. Esta generación utiliza los puntos de conexión según solo Estados Unidos y tiene una lista de direcciones URL tooopen diferentes en el servidor proxy.

| Tooopen de direcciones URL en el servidor proxy |
| --- |
| \*.microsoftonline.com |
| \*.microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| +Listas de revocación de certificados |

Azure AD Connect no es capaz de tooautomatically detectar que el inquilino de Azure AD se encuentra en la nube de gobierno Hola. En su lugar debe hello tootake las siguientes acciones cuando instalar Azure AD Connect.

1. Iniciar instalación de Azure AD Connect Hola.
2. Cuando vea la primera página de Hola se supone que tooaccept Hola términos de licencia, no continúe pero dejar el Asistente para la instalación Hola ejecutar.
3. Inicie regedit y cambie la clave del registro de hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valor `2`.
4. Volver al Asistente para la instalación de toohello AD Azure Connect, acepte Hola términos de licencia y continuar. Durante la instalación, asegúrese de que hello toouse **configuración personalizada** instalación ruta de acceso (y no Express). A continuación, continuar instalación hello como de costumbre.

Características actualmente no está presentes en la nube de Microsoft Azure Government hello:

* **Azure AD Connect Health** no está disponible.
* Las **actualizaciones automáticas** no están disponibles.
* La **escritura diferida de contraseñas** está disponible en versión preliminar con Azure AD Connect versión 1.1.570.0 y posteriores.
* Otros servicios de Azure AD Premium no están disponibles.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
