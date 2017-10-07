---
title: "Tutorial: Integración de Azure Active Directory con Evidence.com | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="7b6fa-103">Tutorial: Integración de Azure Active Directory con Evidence.com</span><span class="sxs-lookup"><span data-stu-id="7b6fa-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="7b6fa-104">En este tutorial, aprenderá cómo toointegrate Evidence.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b6fa-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b6fa-105">Integración Evidence.com con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b6fa-106">Puede controlar en Azure AD que tenga acceso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="7b6fa-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEvidence.com (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7b6fa-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7b6fa-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b6fa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b6fa-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b6fa-110">Prerequisites</span></span>

<span data-ttu-id="7b6fa-111">integración de Azure AD con Evidence.com tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="7b6fa-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b6fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b6fa-113">Una suscripción habilitada para el inicio de sesión único en Evidence.com</span><span class="sxs-lookup"><span data-stu-id="7b6fa-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b6fa-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b6fa-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b6fa-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b6fa-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b6fa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b6fa-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7b6fa-118">Scenario description</span></span>
<span data-ttu-id="7b6fa-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b6fa-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b6fa-121">Agregar Evidence.com desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7b6fa-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="7b6fa-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b6fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="7b6fa-123">Agregar Evidence.com desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7b6fa-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="7b6fa-124">integración de hello tooconfigure de Evidence.com en Azure AD, deberá tooadd Evidence.com de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b6fa-125">**tooadd Evidence.com de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b6fa-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="7b6fa-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b6fa-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="7b6fa-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="7b6fa-133">En el cuadro de búsqueda de hello, escriba **Evidence.com**, seleccione **Evidence.com** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com en la lista de resultados de Hola](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b6fa-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b6fa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7b6fa-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Evidence.com con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7b6fa-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b6fa-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Evidence.com es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="7b6fa-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Evidence.com debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="7b6fa-139">En Evidence.com, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b6fa-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Evidence.com, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b6fa-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b6fa-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b6fa-143">**[Crear un usuario de prueba Evidence.com](#create-a-evidencecom-test-user)**  -toohave un equivalente de Britta Simon en Evidence.com que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b6fa-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b6fa-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b6fa-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b6fa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b6fa-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="7b6fa-148">**inicio de sesión único en Azure AD tooconfigure con Evidence.com, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b6fa-149">En el portal de Azure, en Hola Hola **Evidence.com** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="7b6fa-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="7b6fa-153">En hello **Evidence.com dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="7b6fa-155">a.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-155">a.</span></span> <span data-ttu-id="7b6fa-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="7b6fa-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="7b6fa-157">b.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-157">b.</span></span> <span data-ttu-id="7b6fa-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="7b6fa-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b6fa-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-159">These values are not real.</span></span> <span data-ttu-id="7b6fa-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7b6fa-161">Póngase en contacto con [equipo de soporte técnico de cliente de Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="7b6fa-162">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="7b6fa-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7b6fa-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b6fa-166">En hello **Evidence.com configuración** sección, haga clic en **configurar Evidence.com** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b6fa-167">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="7b6fa-169">En una ventana del explorador web independiente, tooyour Evidence.com de inicio de sesión como administrador de inquilinos y navegue demasiado**administración** ficha</span><span class="sxs-lookup"><span data-stu-id="7b6fa-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="7b6fa-170">Haga clic en **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="7b6fa-171">Seleccione **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="7b6fa-172">Hola copia **Id. de entidad SAML**, **SAML Single Sign-On dirección URL del servicio** y **dirección URL de cierre de sesión** valores que se muestran en hello portal de Azure y los campos correspondientes toohello Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="7b6fa-173">Abra el archivo Certificate(Base64) descargado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado de seguridad** cuadro.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="7b6fa-174">Guardar configuración de hello en Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="7b6fa-175">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7b6fa-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b6fa-176">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b6fa-177">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b6fa-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b6fa-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b6fa-178">Create an Azure AD test user</span></span>

<span data-ttu-id="7b6fa-179">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="7b6fa-181">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b6fa-182">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7b6fa-184">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7b6fa-186">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7b6fa-188">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7b6fa-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7b6fa-190">a.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-190">a.</span></span> <span data-ttu-id="7b6fa-191">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b6fa-192">b.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-192">b.</span></span> <span data-ttu-id="7b6fa-193">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7b6fa-194">c.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-194">c.</span></span> <span data-ttu-id="7b6fa-195">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7b6fa-196">d.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-196">d.</span></span> <span data-ttu-id="7b6fa-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="7b6fa-198">Creación de un usuario de prueba de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="7b6fa-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="7b6fa-199">Para Azure AD a los usuarios toobe puede toosign en, se les deben aprovisionar para obtener acceso dentro de hello Evidence.com aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="7b6fa-200">Esta sección describe cómo las cuentas de usuario de Azure AD toocreate dentro de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="7b6fa-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="7b6fa-201">**una cuenta de usuario en Evidence.com tooprovision:**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="7b6fa-202">En una ventana del explorador web, inicie sesión en el sitio de la compañía en Evidence.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="7b6fa-203">Navegue demasiado**administración** ficha.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="7b6fa-204">Haga clic en **Add User**(Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="7b6fa-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="7b6fa-205">Haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="7b6fa-206">Hola **dirección de correo electrónico** de hello agrega el usuario debe coincidir con el nombre de usuario de Hola de usuarios de hello en Azure AD que deseen toogive acceso.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="7b6fa-207">Si la dirección de correo electrónico y el nombre de usuario de hello no son hello mismo valor en su organización, puede usar hello **Evidence.com > atributos > Single Sign-On** sección de hello toochange portal Azure hello nameidenitifer enviado dirección de correo electrónico de tooEvidence.com toobe Hola.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7b6fa-208">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b6fa-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7b6fa-209">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="7b6fa-211">**tooassign Britta Simon tooEvidence.com, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7b6fa-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b6fa-212">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7b6fa-214">En la lista de aplicaciones de hello, seleccione **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-214">In hello applications list, select **Evidence.com**.</span></span>

    ![vínculo de Evidence.com Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="7b6fa-216">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="7b6fa-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-218">Click **Add** button.</span></span> <span data-ttu-id="7b6fa-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="7b6fa-221">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b6fa-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b6fa-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b6fa-224">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="7b6fa-224">Test single sign-on</span></span>

<span data-ttu-id="7b6fa-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b6fa-226">Al hacer clic en icono de Evidence.com Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Evidence.com aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b6fa-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="7b6fa-227">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b6fa-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b6fa-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7b6fa-228">Additional resources</span></span>

* [<span data-ttu-id="7b6fa-229">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b6fa-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b6fa-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b6fa-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

