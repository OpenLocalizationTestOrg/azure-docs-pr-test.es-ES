---
title: "aaaSet de un dispositivo nuevo con Azure AD durante la instalación | Documentos de Microsoft"
description: "Un tema que explica cómo los usuarios pueden configurar Azure AD Join durante su configuración rápida."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Configuración de un dispositivo nuevo con Azure AD durante la configuración
En Windows 10, los usuarios pueden combinarse su tooAzure dispositivos Active Directory (Azure AD) de experiencia de primera ejecución hello (FRX). Esto permite a los empleados de las organizaciones toodistribute dispositivos reducidas tootheir o estudiantes o que les permite elegir sus propios dispositivos (CYOD).
Si las ediciones de Windows 10 Professional o Windows 10 Enterprise está instalado en un dispositivo, Hola experimentar proceso de instalación de toohello los valores predeterminados de dispositivos de empresa.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin un tooAzure dispositivo AD
1. Cuando encienda el dispositivo nuevo e inicie el proceso de instalación de hello, debería ver Hola **preparar** mensaje. Siga tooset de mensajes de Hola del dispositivo.
2. Para comenzar, personalice su región e idioma. A continuación, acepte los términos de licencia del Software de Microsoft de Hola.
   ![Personalizar para la región](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Seleccione red Hola desea toouse para conectar toohello Internet.
4. Seleccione si usa un dispositivo personal o un dispositivo propiedad de la empresa. Si es propiedad de la empresa, haga clic en **este dispositivo pertenece organización toomy**. Esto inicia la experiencia de Azure AD Join Hola. La siguiente pantalla aparece si usa Windows 10 Professional.
   <center>
   ![Pantalla ¿A quién pertenece el equipo?](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Escriba las credenciales de Hola que se proporcionaron tooyou por su organización.
   <center>
   ![Pantalla de inicio de sesión](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Después de que escriba su nombre de usuario, se coloca un inquilino coincidente en Azure AD. Si está en un dominio federado, es posible que servidor de servicio de Token seguro (STS) local de tooyour redirigida: por ejemplo, Active Directory Federation Services (AD FS).
7. Si es un usuario en un dominio no federadas, escriba sus credenciales directamente en hello página AD hospedado de Azure. Si se ha configurado la personalización de la marca, también verá el logotipo de la organización y texto complementario.
8. A continuación, encontrará un desafío de Multi-factor Authentication. Este desafío puede configurarlo un administrador de TI.
9. Azure AD comprobará si este usuario/dispositivo requiere la inscripción en la administración de dispositivos móviles.
10. Windows registra el dispositivo de Hola Hola del directorio de organización en Azure AD e inscribe en administración de dispositivos móviles, si procede.
11. Si es un usuario administrado, Windows realiza toohello escritorio mediante el proceso de inicio de sesión automático de Hola.
12. Si es un usuario federado, se le dirigirá toohello inicio de sesión de Windows pantalla tooenter sus credenciales.

> [!NOTE]
> Unirse a un dominio de Windows Server Active Directory local de Windows hello de rápida no se admite. Por lo tanto, si tiene previsto toojoin un dominio tooa del equipo, debe seleccionar el vínculo de hello **configurar Windows con una cuenta local** en su lugar. A continuación, puede unirse a dominio Hola de configuración de hello en el equipo tal y como hizo antes.
> 
> 

## <a name="additional-information"></a>Información adicional
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticación de identidades sin contraseñas a través de Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

