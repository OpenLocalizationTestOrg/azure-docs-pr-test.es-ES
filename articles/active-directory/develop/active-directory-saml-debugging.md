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
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="e2b62-103">¿Cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2b62-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="e2b62-104">Cuando se depura una integración de aplicaciones basado en SAML, es a menudo útil toouse una herramienta como [Fiddler](http://www.telerik.com/fiddler) toosee Hola solicitud, respuesta de SAML de Hola y token SAML real Hola emitido toohello aplicación de SAML.</span><span class="sxs-lookup"><span data-stu-id="e2b62-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="e2b62-105">Mediante el examen de token SAML de hello, puede Asegúrese de que todos Hola requiera atributos, Hola nombre de usuario de sujeto SAML de Hola y Hola a emisor URI está entrando en según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="e2b62-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="e2b62-106">Hello respuesta de Azure AD que contiene el token SAML de hello suele ser Hola uno que tiene lugar después de una redirección HTTP 302 de https://login.windows.net y se ha configurado toohello enviado **dirección URL de respuesta** de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e2b62-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="e2b62-107">Puede ver el token SAML de hello seleccionando esta línea y, a continuación, seleccionando hello **inspectores > WebForms** ficha en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2b62-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="e2b62-108">Desde allí, haga clic en hello **SAMLResponse** valor y seleccione **enviar tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="e2b62-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="e2b62-109">A continuación, seleccione **de Base64** de hello **transformar** menú toodecode Hola símbolo (token) y ver su contenido.</span><span class="sxs-lookup"><span data-stu-id="e2b62-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="e2b62-110">**Tenga en cuenta**: solicitud de contenido de hello toosee de este HTTP, Fiddler puede solicitarle que tooconfigure el descifrado de tráfico HTTPS, que tendrá toodo.</span><span class="sxs-lookup"><span data-stu-id="e2b62-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="e2b62-111">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="e2b62-111">Related Articles</span></span>
* [<span data-ttu-id="e2b62-112">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2b62-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="e2b62-113">Configurar tooapplications de inicio de sesión único que no están en la Galería de aplicaciones de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="e2b62-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="e2b62-114">Cómo se emiten las notificaciones tooCustomize en hello Token de SAML para aplicaciones Pre-Integrated</span><span class="sxs-lookup"><span data-stu-id="e2b62-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png