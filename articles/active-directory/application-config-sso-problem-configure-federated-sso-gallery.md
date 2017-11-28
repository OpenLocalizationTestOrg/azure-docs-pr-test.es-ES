---
title: "aaaProblem configuración federada inicio de sesión único para una aplicación de la Galería de Azure AD | Documentos de Microsoft"
description: "Resolver algunos problemas comunes de Hola que pueden producirse al configurar federado única sesión con SAML para las aplicaciones que se enumeran en hello Galería de aplicaciones de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="da322-103">Problemas en la configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="da322-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="da322-104">Si se produce un problema al configurar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="da322-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="da322-105">Compruebe que ha seguido todos los pasos de hello en el tutorial de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="da322-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="da322-106">En configuración de la aplicación hello, dispone de documentación en línea en cómo tooconfigure Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="da322-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="da322-107">Además, puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones paso a paso detallados.</span><span class="sxs-lookup"><span data-stu-id="da322-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="da322-108">No se puede agregar otra instancia de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="da322-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="da322-109">tooadd una segunda instancia de una aplicación, necesita toobe capaz de:</span><span class="sxs-lookup"><span data-stu-id="da322-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="da322-110">Configurar un identificador único para la segunda instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="da322-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="da322-111">No será hello tooconfigure pueda mismo identificador utilizado para primera instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="da322-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="da322-112">Configurar un certificado diferente Hola uno utilizado para la primera instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="da322-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="da322-113">Si hello aplicación no admite cualquiera de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="da322-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="da322-114">A continuación, no será capaz de tooconfigure una segunda instancia.</span><span class="sxs-lookup"><span data-stu-id="da322-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="da322-115">No se puede agregar Hola identificador u Hola dirección URL de respuesta</span><span class="sxs-lookup"><span data-stu-id="da322-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="da322-116">Si no es capaz de tooconfigure Hola identificador u Hola dirección URL de respuesta, confirme Hola identificador y los valores de dirección URL de respuesta coincidan con modelos de hello configurados previamente para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="da322-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="da322-117">patrones de hello tooknow configurados previamente para la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="da322-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="da322-118">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.** Vaya toostep 7.</span><span class="sxs-lookup"><span data-stu-id="da322-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="da322-119">Si ya está en la hoja de configuración de aplicaciones de hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da322-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="da322-120">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="da322-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="da322-121">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="da322-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="da322-122">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da322-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="da322-123">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da322-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="da322-124">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado** Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="da322-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="da322-125">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="da322-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="da322-126">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="da322-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="da322-127">Seleccione **sesión basado en SAML** de hello **modo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="da322-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="da322-128">Vaya toohello **identificador** o **dirección URL de respuesta** cuadro de texto, en hello **sección de dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="da322-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="da322-129">Hay tres formas de patrones de hello admitida tooknow para la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="da322-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="da322-130">En el cuadro de texto hello, vea Hola admiten patrones como un marcador de posición *ejemplo:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="da322-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="da322-131">Si no se admite el patrón de hello, verá una marca de exclamación roja cuando intente tooenter valor de hello en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="da322-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="da322-132">Si se mantenga el mouse sobre la marca de exclamación rojo hello, verá patrones Hola compatible.</span><span class="sxs-lookup"><span data-stu-id="da322-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="da322-133">En el tutorial de hello para la aplicación hello, también puede obtener información sobre los patrones de hello admite.</span><span class="sxs-lookup"><span data-stu-id="da322-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="da322-134">En hello **inicio de sesión único en configurar Azure AD** sección.</span><span class="sxs-lookup"><span data-stu-id="da322-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="da322-135">Vaya toohello paso para los valores de hello configurado en hello **dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="da322-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="da322-136">Si los valores de hello no coinciden con los patrones de hello configurados previamente en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da322-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="da322-137">Puede:</span><span class="sxs-lookup"><span data-stu-id="da322-137">You can:</span></span>

-   <span data-ttu-id="da322-138">Trabajar con valores de tooget de proveedor de aplicación de Hola que coinciden con el patrón de hello configurado previamente en Azure AD</span><span class="sxs-lookup"><span data-stu-id="da322-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="da322-139">O bien, puede ponerse en contacto con el equipo de Azure AD en < aadapprequest@microsoft.com > o deje un comentario en la actualización de Hola Hola toorequest tutorial de patrones de hello compatible para la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="da322-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="da322-140">Donde se puede establecer formato de hello EntityID (identificador de usuario)</span><span class="sxs-lookup"><span data-stu-id="da322-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="da322-141">No será formato de tooselect capaz de hello EntityID (identificador de usuario) que Azure AD envía toohello aplicación en respuesta Hola después de la autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="da322-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="da322-142">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="da322-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="da322-143">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en la sección de hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="da322-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="da322-144">No se puede encontrar la configuración hello Azure AD metadatos toocomplete Hola con la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="da322-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="da322-145">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="da322-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="da322-146">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="da322-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="da322-147">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="da322-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="da322-148">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="da322-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="da322-149">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da322-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="da322-150">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="da322-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="da322-151">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado** Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="da322-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="da322-152">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="da322-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="da322-153">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="da322-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="da322-154">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="da322-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="da322-155">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="da322-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="da322-156">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="da322-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="da322-157">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="da322-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="da322-158">No sabe cómo envían notificaciones SAML toocustomize los tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="da322-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="da322-159">toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="da322-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da322-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="da322-160">Next steps</span></span>
[<span data-ttu-id="da322-161">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da322-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
