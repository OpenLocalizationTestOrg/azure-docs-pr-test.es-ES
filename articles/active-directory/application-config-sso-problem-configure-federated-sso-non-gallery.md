---
title: "aaaProblem configuración federada inicio de sesión único para una aplicación no Galería | Documentos de Microsoft"
description: "Resolver algunos problemas comunes de Hola que puede surgir al configurar aplicación SAML personalizada tooyour de inicio de sesión único federado no aparece en la Galería de aplicaciones de Azure AD de Hola"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="58e97-103">Problemas en la configuración del inicio de sesión único federado para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="58e97-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="58e97-104">Si se produce un problema al configurar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="58e97-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="58e97-105">Compruebe que ha seguido todos los pasos de hello en el artículo hello [configurar tooapplications de inicio de sesión único que no están en la Galería de aplicaciones de Azure Active Directory Hola.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="58e97-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="58e97-106">No se puede agregar otra instancia de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="58e97-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="58e97-107">tooadd una segunda instancia de una aplicación, necesita toobe capaz de:</span><span class="sxs-lookup"><span data-stu-id="58e97-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="58e97-108">Configurar un identificador único para la segunda instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="58e97-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="58e97-109">No será hello tooconfigure pueda mismo identificador utilizado para primera instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="58e97-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="58e97-110">Configurar un certificado diferente Hola uno utilizado para la primera instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="58e97-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="58e97-111">Si hello aplicación no admite cualquiera de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="58e97-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="58e97-112">A continuación, no será capaz de tooconfigure una segunda instancia.</span><span class="sxs-lookup"><span data-stu-id="58e97-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="58e97-113">Donde se puede establecer formato de hello EntityID (identificador de usuario)</span><span class="sxs-lookup"><span data-stu-id="58e97-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="58e97-114">No será formato de tooselect capaz de hello EntityID (identificador de usuario) que Azure AD envía toohello aplicación en respuesta Hola después de la autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="58e97-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="58e97-115">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="58e97-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="58e97-116">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en la sección de hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="58e97-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="58e97-117">¿Dónde puedo conseguir metadatos de la aplicación de Hola o certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="58e97-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="58e97-118">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="58e97-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="58e97-119">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="58e97-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="58e97-120">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="58e97-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="58e97-121">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="58e97-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="58e97-122">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58e97-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="58e97-123">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="58e97-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="58e97-124">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado** Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="58e97-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="58e97-125">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="58e97-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="58e97-126">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="58e97-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="58e97-127">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="58e97-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="58e97-128">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="58e97-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="58e97-129">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="58e97-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="58e97-130">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="58e97-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="58e97-131">No sabe cómo envían notificaciones SAML toocustomize los tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="58e97-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="58e97-132">toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="58e97-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58e97-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="58e97-133">Next steps</span></span>
[<span data-ttu-id="58e97-134">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58e97-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
