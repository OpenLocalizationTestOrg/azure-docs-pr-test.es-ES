---
title: "aaaSet de un dispositivo Windows 10 con Azure AD desde configuración | Documentos de Microsoft"
description: "Explica cómo los usuarios pueden unirse tooAzure AD a través del menú de configuración de Hola."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Configuración de un dispositivo de Windows 10 con Azure AD desde Configuración
Si ya está usando Windows 7 o Windows 8 y el equipo o dispositivo se ha actualizado tooWindows 10, puede combinar tooAzure Active Directory (Azure AD) a través del menú de configuración de Hola.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD desde el menú de configuración de Hola
1. De hello **iniciar** menú, haga clic en hello **configuración** acceso.
2. En **Configuración**, seleccione **Sistema**->**Acerca de**->**Unirse a Azure AD**.
   
   <center>
   ![Unirse a Azure AD desde el menú de configuración de hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Haga clic en **continuar** en la ventana de mensaje de Hola Azure AD Join.
   
   <center>
   ![Ventana de mensaje de Unirse a Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Proporcione sus credenciales de inicio de sesión. Esta experiencia de inicio de sesión incluirá todos los pasos de hello toocomplete requiere autenticación. Si forma parte de un inquilino federado, el administrador le proporcionará experiencia de federación de Hola que está alojado en su organización.
   <center>
   ![Proporcionar credenciales de inicio de sesión](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Si su organización ha configurado la autenticación multifactor Azure para combinar tooAzure AD, proporcione el segundo factor de hello antes de continuar.
6. Haga clic en **Accept** en hello **permitir este toobe dispositivo administrado** pantalla.
7. Debería ver el mensaje de saludo "el dispositivo ya está combinadas tooyour organización en Azure AD".

## <a name="additional-information"></a>Información adicional
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)
* [Autenticación de identidades sin contraseñas a través de Microsoft Passport](active-directory-azureadjoin-passport.md)

