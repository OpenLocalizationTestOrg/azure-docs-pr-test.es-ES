---
title: "Depuración del inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory  "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="b6fa0-103">Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6fa0-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="b6fa0-104">Cuando se depura una integración de la aplicación basada en SAML, a menudo resulta útil usar una herramienta como [Fiddler](http://www.telerik.com/fiddler) para ver la solicitud SAML, la respuesta de SAML y el token SAML real que se emite a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6fa0-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="b6fa0-105">Mediante el examen del token SAML, puede asegurarse de que todos los atributos necesarios, el nombre de usuario del SAML Subject y el URI del emisor se logren del modo esperado.</span><span class="sxs-lookup"><span data-stu-id="b6fa0-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="b6fa0-106">Normalmente, la respuesta de Azure AD que contiene el token SAML es la que se produce después de un redireccionamiento HTTP 302 desde https://login.windows.net, y se envía a la **URL de respuesta** configurada de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6fa0-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="b6fa0-107">Para ver el token SAML, seleccione esta línea y, luego, seleccione la pestaña **Inspectors > WebForms** (Inspectores > WebForms) en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="b6fa0-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="b6fa0-108">Desde ahí, haga clic con el botón derecho en el valor **SAMLResponse** y seleccione **Send to TextWizard** (Enviar a TextWizard).</span><span class="sxs-lookup"><span data-stu-id="b6fa0-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="b6fa0-109">Después, seleccione **From Base64** (De Base64) en el menú **Transform** (Transformar) para descodificar el token y ver su contenido.</span><span class="sxs-lookup"><span data-stu-id="b6fa0-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="b6fa0-110">**Nota**: Para ver el contenido de esta solicitud HTTP, es posible que Fiddler le solicite configurar el cifrado del tráfico HTTPS, que tendrá que llevar a cabo.</span><span class="sxs-lookup"><span data-stu-id="b6fa0-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b6fa0-111">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="b6fa0-111">Related Articles</span></span>
* [<span data-ttu-id="b6fa0-112">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6fa0-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="b6fa0-113">Configuración del inicio de sesión único en aplicaciones que no están en la Galería de aplicaciones de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6fa0-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="b6fa0-114">Personalización de notificaciones emitidas en el token SAML para aplicaciones previamente integradas en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6fa0-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png