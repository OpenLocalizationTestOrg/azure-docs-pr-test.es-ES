---
title: "Tutorial: Integración de Azure Active Directory con Zoho | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="7e1e8-103">Tutorial: Integración de Azure Active Directory con Zoho</span><span class="sxs-lookup"><span data-stu-id="7e1e8-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="7e1e8-104">En este tutorial, aprenderá cómo toointegrate Zoho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e1e8-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e1e8-105">Integración Zoho con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e1e8-106">Puede controlar en Azure AD que tenga acceso tooZoho.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="7e1e8-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZoho (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7e1e8-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7e1e8-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e1e8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e1e8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7e1e8-110">Prerequisites</span></span>

<span data-ttu-id="7e1e8-111">integración de Azure AD con Zoho tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="7e1e8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1e8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e1e8-113">Una suscripción habilitada para el inicio de sesión único en Zoho</span><span class="sxs-lookup"><span data-stu-id="7e1e8-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e1e8-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e1e8-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e1e8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e1e8-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e1e8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e1e8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7e1e8-118">Scenario description</span></span>
<span data-ttu-id="7e1e8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e1e8-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e1e8-121">Agregar Zoho desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7e1e8-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="7e1e8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1e8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="7e1e8-123">Agregar Zoho desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7e1e8-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="7e1e8-124">integración de hello tooconfigure de Zoho en Azure AD, deberá tooadd Zoho de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e1e8-125">**tooadd Zoho de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7e1e8-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1e8-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="7e1e8-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e1e8-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="7e1e8-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="7e1e8-133">En el cuadro de búsqueda de hello, escriba **Zoho**, seleccione **Zoho** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de Zoho Hola](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7e1e8-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1e8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7e1e8-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Zoho con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e1e8-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e1e8-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zoho es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="7e1e8-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zoho debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="7e1e8-139">En Zoho, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e1e8-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Zoho, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e1e8-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e1e8-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e1e8-143">**[Crear un usuario de prueba de Zoho](#create-a-zoho-test-user)**  -toohave un equivalente de Britta Simon en Zoho que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e1e8-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e1e8-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7e1e8-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1e8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7e1e8-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zoho.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="7e1e8-148">**inicio de sesión único en Azure AD tooconfigure con Zoho, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7e1e8-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1e8-149">En el portal de Azure, en Hola Hola **Zoho** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="7e1e8-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="7e1e8-153">En hello **Zoho dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="7e1e8-155">a.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-155">a.</span></span> <span data-ttu-id="7e1e8-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="7e1e8-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7e1e8-157">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-157">This value is not real.</span></span> <span data-ttu-id="7e1e8-158">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7e1e8-159">Póngase en contacto con [equipo de soporte técnico de cliente de Zoho](https://www.zoho.com/mail/contact.html) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="7e1e8-160">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="7e1e8-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7e1e8-162">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e1e8-164">En hello **configuración de Zoho** sección, haga clic en **configurar Zoho** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7e1e8-165">Hola copia **SAML Single Sign-On dirección URL del servicio, cambiar dirección URL de contraseña y dirección URL de cierre de sesión** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="7e1e8-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="7e1e8-167">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zoho Mail como administrador.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="7e1e8-168">Vaya toohello **el panel de Control**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="7e1e8-169">![Panel de control](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Panel de control")</span><span class="sxs-lookup"><span data-stu-id="7e1e8-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="7e1e8-170">Haga clic en hello **autenticación SAML** ficha.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="7e1e8-171">![Autenticación SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="7e1e8-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="7e1e8-172">Hola **detalles de la autenticación de SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7e1e8-173">![Detalles de la autenticación SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Detalles de la autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="7e1e8-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="7e1e8-174">a.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-174">a.</span></span> <span data-ttu-id="7e1e8-175">Hola **dirección URL de inicio de sesión** cuadro de texto, pegue **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7e1e8-176">b.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-176">b.</span></span> <span data-ttu-id="7e1e8-177">Hola **Logout URL** cuadro de texto, pegue **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7e1e8-178">c.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-178">c.</span></span> <span data-ttu-id="7e1e8-179">Hola **cambiar dirección URL de contraseña** cuadro de texto, pegue **cambiar dirección URL de contraseña** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="7e1e8-180">d.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-180">d.</span></span> <span data-ttu-id="7e1e8-181">Abra el certificado codificado en base 64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **PublicKey** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="7e1e8-182">e.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-182">e.</span></span> <span data-ttu-id="7e1e8-183">En **Algoritmo**, seleccione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="7e1e8-184">f.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-184">f.</span></span> <span data-ttu-id="7e1e8-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="7e1e8-186">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7e1e8-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e1e8-187">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e1e8-188">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e1e8-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7e1e8-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1e8-189">Create an Azure AD test user</span></span>

<span data-ttu-id="7e1e8-190">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="7e1e8-192">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7e1e8-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1e8-193">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7e1e8-195">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7e1e8-197">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7e1e8-199">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7e1e8-201">a.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-201">a.</span></span> <span data-ttu-id="7e1e8-202">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e1e8-203">b.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-203">b.</span></span> <span data-ttu-id="7e1e8-204">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7e1e8-205">c.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-205">c.</span></span> <span data-ttu-id="7e1e8-206">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7e1e8-207">d.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-207">d.</span></span> <span data-ttu-id="7e1e8-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="7e1e8-209">Creación de un usuario de prueba de Zoho</span><span class="sxs-lookup"><span data-stu-id="7e1e8-209">Create a Zoho test user</span></span>

<span data-ttu-id="7e1e8-210">En orden tooenable toolog de los usuarios de Azure AD en Zoho Mail, se les deben aprovisionar en Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="7e1e8-211">En caso de hello de Zoho Mail, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="7e1e8-212">Puede usar cualquier otra Zoho Mail usuario cuenta herramienta de creación o las API proporcionadas por Zoho Mail tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="7e1e8-213">tooprovision una cuenta de usuario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="7e1e8-214">Inicie sesión en tooyour **Zoho Mail** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="7e1e8-215">Vaya demasiado**el Panel de Control \> correo y documentos**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="7e1e8-216">Vaya demasiado**detalles del usuario \> Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="7e1e8-217">![Agregar usuario](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="7e1e8-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="7e1e8-218">En hello **agregar usuarios** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7e1e8-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="7e1e8-219">![Agregar usuario](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="7e1e8-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="7e1e8-220">a.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-220">a.</span></span> <span data-ttu-id="7e1e8-221">Hola **nombre** cuadro de texto, tipo hello nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="7e1e8-222">b.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-222">b.</span></span> <span data-ttu-id="7e1e8-223">Hola **Last Name** cuadro de texto, escriba Hola apellidos del usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="7e1e8-224">c.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-224">c.</span></span> <span data-ttu-id="7e1e8-225">Hola **Id. de correo electrónico** cuadro de texto, Id. de tipo hello correo electrónico del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7e1e8-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="7e1e8-226">d.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-226">d.</span></span> <span data-ttu-id="7e1e8-227">Hola **contraseña** cuadro de texto, escriba la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="7e1e8-228">e.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-228">e.</span></span> <span data-ttu-id="7e1e8-229">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="7e1e8-230">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7e1e8-231">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1e8-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7e1e8-232">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZoho.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="7e1e8-234">**tooassign Britta Simon tooZoho, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7e1e8-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1e8-235">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7e1e8-237">En la lista de aplicaciones de hello, seleccione **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-237">In hello applications list, select **Zoho**.</span></span>

    ![vínculo de Zoho Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="7e1e8-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="7e1e8-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-241">Click **Add** button.</span></span> <span data-ttu-id="7e1e8-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="7e1e8-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e1e8-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e1e8-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7e1e8-247">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="7e1e8-247">Test single sign-on</span></span>

<span data-ttu-id="7e1e8-248">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e1e8-249">Al hacer clic en icono de Zoho Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Zoho aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e1e8-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="7e1e8-250">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e1e8-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e1e8-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7e1e8-251">Additional resources</span></span>

* [<span data-ttu-id="7e1e8-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e1e8-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e1e8-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e1e8-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

