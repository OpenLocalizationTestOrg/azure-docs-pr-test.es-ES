---
title: aaaHow toodebug basado en SAML single sign-on tooapplications en Azure Active Directory | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>¿Cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory
Cuando se depura una integración de aplicaciones basado en SAML, es a menudo útil toouse una herramienta como [Fiddler](http://www.telerik.com/fiddler) toosee Hola solicitud, respuesta de SAML de Hola y token SAML real Hola emitido toohello aplicación de SAML. Mediante el examen de token SAML de hello, puede Asegúrese de que todos Hola requiera atributos, Hola nombre de usuario de sujeto SAML de Hola y Hola a emisor URI está entrando en según lo previsto.

![][1]

Hello respuesta de Azure AD que contiene el token SAML de hello suele ser Hola uno que tiene lugar después de una redirección HTTP 302 de https://login.windows.net y se ha configurado toohello enviado **dirección URL de respuesta** de aplicación hello. 

Puede ver el token SAML de hello seleccionando esta línea y, a continuación, seleccionando hello **inspectores > WebForms** ficha en el panel derecho de Hola. Desde allí, haga clic en hello **SAMLResponse** valor y seleccione **enviar tooTextWizard**. A continuación, seleccione **de Base64** de hello **transformar** menú toodecode Hola símbolo (token) y ver su contenido.

**Tenga en cuenta**: solicitud de contenido de hello toosee de este HTTP, Fiddler puede solicitarle que tooconfigure el descifrado de tráfico HTTPS, que tendrá toodo.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](../active-directory-apps-index.md)
* [Configurar tooapplications de inicio de sesión único que no están en la Galería de aplicaciones de Azure Active Directory Hola](../active-directory-saas-custom-apps.md)
* [Cómo se emiten las notificaciones tooCustomize en hello Token de SAML para aplicaciones Pre-Integrated](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png