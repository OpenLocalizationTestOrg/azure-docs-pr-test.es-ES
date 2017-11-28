---
title: "Tutorial: Integración de Azure Active Directory con Procore SSO | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO Procore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="45273-103">Tutorial: Integración de Azure Active Directory con Procore SSO</span><span class="sxs-lookup"><span data-stu-id="45273-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="45273-104">En este tutorial, aprenderá cómo toointegrate Procore SSO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="45273-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45273-105">Integración de SSO Procore con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="45273-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45273-106">Puede controlar en Azure AD que tenga acceso tooProcore SSO</span><span class="sxs-lookup"><span data-stu-id="45273-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="45273-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooProcore SSO (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45273-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="45273-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="45273-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45273-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="45273-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="45273-110">Prerequisites</span></span>

<span data-ttu-id="45273-111">integración de Azure AD con SSO Procore tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="45273-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="45273-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45273-113">Una suscripción habilitada para el inicio de sesión único en Procore SSO</span><span class="sxs-lookup"><span data-stu-id="45273-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45273-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="45273-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45273-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="45273-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45273-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="45273-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="45273-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45273-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45273-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="45273-118">Scenario description</span></span>
<span data-ttu-id="45273-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="45273-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45273-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="45273-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45273-121">Agregar SSO Procore desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="45273-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="45273-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="45273-123">Agregar SSO Procore desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="45273-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="45273-124">integración de hello tooconfigure de SSO Procore en Azure AD, deberá tooadd SSO Procore de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="45273-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45273-125">**tooadd Procore SSO de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="45273-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45273-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="45273-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45273-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="45273-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45273-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="45273-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="45273-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45273-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="45273-133">En el cuadro de búsqueda de hello, escriba **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="45273-133">In hello search box, type **Procore SSO**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="45273-135">En el panel de resultados de hello, seleccione **SSO Procore**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="45273-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45273-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45273-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Procore SSO con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="45273-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="45273-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SSO Procore es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45273-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="45273-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SSO Procore debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="45273-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="45273-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="45273-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="45273-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SSO Procore, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="45273-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45273-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="45273-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45273-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="45273-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="45273-145">**[Crear un usuario de prueba de SSO Procore](#creating-a-procore-sso-test-user)**  -toohave un equivalente de Britta Simon en Procore SSO que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="45273-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="45273-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="45273-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="45273-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="45273-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45273-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45273-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación SSO Procore.</span><span class="sxs-lookup"><span data-stu-id="45273-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="45273-150">**inicio de sesión único en tooconfigure Azure AD con SSO Procore, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="45273-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="45273-151">En el portal de administración de Azure de hello, en hello **SSO Procore** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="45273-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="45273-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="45273-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="45273-155">En hello **Procore de SSO de dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="45273-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="45273-157">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="45273-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="45273-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="45273-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="45273-161">En hello **Procore configuración de SSO** sección, haga clic en **configurar SSO Procore** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="45273-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="45273-162">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="45273-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="45273-164">inicio de sesión único en tooconfigure en **Procore SSO** lado, un sitio de empresa procore tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="45273-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="45273-165">De colocación del cuadro de herramientas de hello hacia abajo, haga clic en **administración** página de configuración de SSO de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="45273-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="45273-167">Describen los valores de hello pegar Hola que en los cuadros siguientes:</span><span class="sxs-lookup"><span data-stu-id="45273-167">Paste hello values in hello boxes as described below-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="45273-169">a.</span><span class="sxs-lookup"><span data-stu-id="45273-169">a.</span></span> <span data-ttu-id="45273-170">Hola **único inicio de sesión en dirección URL del emisor** cuadro, pegue Hola Id. de entidad SAML copiado de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="45273-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="45273-171">b.</span><span class="sxs-lookup"><span data-stu-id="45273-171">b.</span></span> <span data-ttu-id="45273-172">Hola **SAML inicio de sesión en dirección URL de destino** cuadro, pegue Hola SAML Single Sign-On dirección URL del servicio se copian de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="45273-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="45273-173">c.</span><span class="sxs-lookup"><span data-stu-id="45273-173">c.</span></span> <span data-ttu-id="45273-174">Ahora, abra hello **Metadata XML** descargado anteriormente de hello portal de Azure y copia certificados de hello en etiqueta Hola denominado **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="45273-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="45273-175">Hola pegar copia valor en hello **Single Sign On x509 certificado** cuadro.</span><span class="sxs-lookup"><span data-stu-id="45273-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="45273-176">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="45273-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="45273-177">Después de esta configuración, debe hello toosend **nombre de dominio** (por ejemplo **contoso.com**) a través de que está iniciando en toohello Procore [equipo de soporte técnico Procore](https://support.procore.com/) y Activar SSO federado para ese dominio.</span><span class="sxs-lookup"><span data-stu-id="45273-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45273-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="45273-179">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="45273-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="45273-181">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="45273-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45273-182">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="45273-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45273-184">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="45273-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45273-186">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="45273-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45273-188">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="45273-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45273-190">a.</span><span class="sxs-lookup"><span data-stu-id="45273-190">a.</span></span> <span data-ttu-id="45273-191">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45273-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45273-192">b.</span><span class="sxs-lookup"><span data-stu-id="45273-192">b.</span></span> <span data-ttu-id="45273-193">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="45273-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45273-194">c.</span><span class="sxs-lookup"><span data-stu-id="45273-194">c.</span></span> <span data-ttu-id="45273-195">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="45273-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45273-196">d.</span><span class="sxs-lookup"><span data-stu-id="45273-196">d.</span></span> <span data-ttu-id="45273-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="45273-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="45273-198">Creación de un usuario de prueba de Procore SSO</span><span class="sxs-lookup"><span data-stu-id="45273-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="45273-199">Siga Hola por debajo de los pasos toocreate un usuario de prueba Procore en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="45273-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="45273-200">Sitio de empresa procore de tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="45273-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="45273-201">De colocación del cuadro de herramientas de hello hacia abajo, haga clic en **Directory** página del directorio de la compañía de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="45273-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="45273-203">Haga clic en **agregar una persona** opción tooopen formulario de Hola y escriba realizar las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="45273-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="45273-205">a.</span><span class="sxs-lookup"><span data-stu-id="45273-205">a.</span></span> <span data-ttu-id="45273-206">Hola **nombre** cuadro de texto Nombre del usuario de tipo como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="45273-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="45273-207">b.</span><span class="sxs-lookup"><span data-stu-id="45273-207">b.</span></span> <span data-ttu-id="45273-208">Hola **apellidos** cuadro de texto, apellido del usuario de tipo como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="45273-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="45273-209">c.</span><span class="sxs-lookup"><span data-stu-id="45273-209">c.</span></span> <span data-ttu-id="45273-210">Hola **dirección de correo electrónico** como dirección de correo electrónico del usuario del tipo de cuadro de texto,  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="45273-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="45273-211">d.</span><span class="sxs-lookup"><span data-stu-id="45273-211">d.</span></span> <span data-ttu-id="45273-212">Seleccione **Permission Template** (Plantilla de permisos) como **Apply Permission Template Later** (Aplicar plantilla de permisos más tarde).</span><span class="sxs-lookup"><span data-stu-id="45273-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="45273-213">e.</span><span class="sxs-lookup"><span data-stu-id="45273-213">e.</span></span> <span data-ttu-id="45273-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="45273-214">Click **Create**.</span></span>

4. <span data-ttu-id="45273-215">Comprobar y actualizar los detalles de Hola Hola recién agregado contacto.</span><span class="sxs-lookup"><span data-stu-id="45273-215">Check and update hello details for hello newly added contact.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="45273-217">Haga clic en **guardar y Enviar invitación** (si se requiere una invitación por correo electrónico) o **guardar** (guardar directamente) registro de usuario de toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="45273-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45273-219">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="45273-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45273-220">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooProcore acceso SSO.</span><span class="sxs-lookup"><span data-stu-id="45273-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="45273-222">**tooassign Britta Simon tooProcore SSO, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="45273-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="45273-223">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="45273-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="45273-225">En la lista de aplicaciones de hello, seleccione **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="45273-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="45273-227">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="45273-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="45273-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="45273-229">Click **Add** button.</span></span> <span data-ttu-id="45273-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="45273-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="45273-232">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="45273-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45273-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="45273-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45273-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="45273-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45273-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="45273-235">Testing single sign-on</span></span>

<span data-ttu-id="45273-236">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="45273-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="45273-237">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="45273-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="45273-238">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="45273-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="45273-239">Al hacer clic en icono de SSO Procore Hola Hola Panel de acceso, deberá obtener la aplicación de SSO Procore tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="45273-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45273-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="45273-240">Additional resources</span></span>

* [<span data-ttu-id="45273-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45273-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45273-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45273-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

