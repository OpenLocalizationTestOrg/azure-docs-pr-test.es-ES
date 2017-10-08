---
title: "Tutorial: Integración de Azure Active Directory con Atlassian Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Atlassian en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="77cd9-103">Tutorial: Integración de Azure Active Directory con Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="77cd9-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="77cd9-104">En este tutorial, aprenderá cómo toointegrate Atlassian en la nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77cd9-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77cd9-105">Integración Atlassian en la nube con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="77cd9-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77cd9-106">Puede controlar en Azure AD que tenga acceso tooAtlassian en la nube</span><span class="sxs-lookup"><span data-stu-id="77cd9-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="77cd9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAtlassian en la nube (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77cd9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="77cd9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77cd9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77cd9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77cd9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="77cd9-110">Prerequisites</span></span>

<span data-ttu-id="77cd9-111">tooconfigure integración de Azure AD con Atlassian en la nube, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="77cd9-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="77cd9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77cd9-113">Una suscripción habilitada para el inicio de sesión único en Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="77cd9-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77cd9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="77cd9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77cd9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="77cd9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77cd9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="77cd9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77cd9-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77cd9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77cd9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="77cd9-118">Scenario description</span></span>
<span data-ttu-id="77cd9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="77cd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77cd9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="77cd9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77cd9-121">Agregar Atlassian en la nube desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="77cd9-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="77cd9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="77cd9-123">Agregar Atlassian en la nube desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="77cd9-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="77cd9-124">integración de hello tooconfigure de Atlassian en la nube en Azure AD, deberá tooadd Atlassian en la nube de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="77cd9-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77cd9-125">**tooadd Atlassian en la nube de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77cd9-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77cd9-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="77cd9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77cd9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77cd9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="77cd9-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77cd9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="77cd9-133">En el cuadro de búsqueda de hello, escriba **Atlassian nube**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="77cd9-135">En el panel de resultados de hello, seleccione **Atlassian nube**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="77cd9-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77cd9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77cd9-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Atlassian Cloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="77cd9-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77cd9-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en nube Atlassian es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77cd9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="77cd9-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en nube Atlassian debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="77cd9-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="77cd9-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Atlassian en la nube.</span><span class="sxs-lookup"><span data-stu-id="77cd9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="77cd9-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Atlassian en la nube, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="77cd9-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77cd9-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="77cd9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77cd9-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77cd9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77cd9-145">**[Creación de un usuario de prueba en la nube Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave un equivalente de Britta Simon en nube de Atlassian que es la representación en forma de toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="77cd9-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77cd9-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="77cd9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77cd9-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="77cd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77cd9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77cd9-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Atlassian en la nube.</span><span class="sxs-lookup"><span data-stu-id="77cd9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="77cd9-150">**inicio de sesión único en tooconfigure Azure AD con Atlassian en la nube, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77cd9-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="77cd9-151">En el portal de Azure, en Hola Hola **Atlassian nube** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="77cd9-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="77cd9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="77cd9-155">En hello **Atlassian nube dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="77cd9-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="77cd9-157">a.</span><span class="sxs-lookup"><span data-stu-id="77cd9-157">a.</span></span> <span data-ttu-id="77cd9-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="77cd9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="77cd9-159">b.</span><span class="sxs-lookup"><span data-stu-id="77cd9-159">b.</span></span> <span data-ttu-id="77cd9-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL como:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="77cd9-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="77cd9-161">Comprobar **mostrar avanzadas de configuración de direcciones URL** y realizar Hola siguiendo el paso si desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="77cd9-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="77cd9-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="77cd9-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77cd9-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="77cd9-164">These values are not real.</span></span> <span data-ttu-id="77cd9-165">Actualizar estos valores con hello real identificador y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="77cd9-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="77cd9-166">Puede obtener los valores exactos de Hola desde la pantalla de configuración de SAML de Atlassian en la nube.</span><span class="sxs-lookup"><span data-stu-id="77cd9-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="77cd9-167">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="77cd9-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="77cd9-169">En hello **configuración de la nube de Atlassian** sección, haga clic en **configurar en la nube Atlassian** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="77cd9-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77cd9-170">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="77cd9-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="77cd9-172">tooget SSO había configurado para la aplicación, inicio de sesión toohello Portal Atlassian con derechos de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="77cd9-173">En la sección de autenticación de Hola de hello barra de navegación izquierda haga clic en **dominios**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="77cd9-175">a.</span><span class="sxs-lookup"><span data-stu-id="77cd9-175">a.</span></span> <span data-ttu-id="77cd9-176">En el cuadro de texto hello, escriba el nombre de dominio y, a continuación, haga clic en **Agregar dominio**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="77cd9-178">b.</span><span class="sxs-lookup"><span data-stu-id="77cd9-178">b.</span></span> <span data-ttu-id="77cd9-179">dominio de hello tooverify, haga clic en **compruebe**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="77cd9-181">c.</span><span class="sxs-lookup"><span data-stu-id="77cd9-181">c.</span></span> <span data-ttu-id="77cd9-182">Descargar archivo de html de comprobación de dominio de hello, cargarlo toohello carpeta de raíz del sitio Web de su dominio y, a continuación, haga clic en **comprobar dominio**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="77cd9-184">d.</span><span class="sxs-lookup"><span data-stu-id="77cd9-184">d.</span></span> <span data-ttu-id="77cd9-185">Una vez que se comprueba el dominio de Hola Hola valo hello **estado** campo es **comprobado**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="77cd9-187">En la barra de navegación izquierda de hello, haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="77cd9-189">Crear una configuración de SAML y agregue la configuración del proveedor de identidades Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="77cd9-191">a.</span><span class="sxs-lookup"><span data-stu-id="77cd9-191">a.</span></span> <span data-ttu-id="77cd9-192">Hola **proveedor de identidades de Id. de entidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="77cd9-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="77cd9-193">b.</span><span class="sxs-lookup"><span data-stu-id="77cd9-193">b.</span></span> <span data-ttu-id="77cd9-194">Hola **proveedor de identidades de dirección URL SSO** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="77cd9-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="77cd9-195">c.</span><span class="sxs-lookup"><span data-stu-id="77cd9-195">c.</span></span> <span data-ttu-id="77cd9-196">Abra el certificado de hello descargado de Azure valores de hello portal y copia sin Hola Begin y finalizar las líneas y péguelo en hello **X509 público certificado** cuadro.</span><span class="sxs-lookup"><span data-stu-id="77cd9-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="77cd9-197">d.</span><span class="sxs-lookup"><span data-stu-id="77cd9-197">d.</span></span> <span data-ttu-id="77cd9-198">Haga clic en **Guardar configuración** configuración de tooSave Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="77cd9-199">Actualizar configuración de hello Azure AD toomake Asegúrese de que tiene Hola instalación corregir la dirección URL de identificación.</span><span class="sxs-lookup"><span data-stu-id="77cd9-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="77cd9-200">a.</span><span class="sxs-lookup"><span data-stu-id="77cd9-200">a.</span></span> <span data-ttu-id="77cd9-201">Hola copia **ID de identidad de SP** en hello SAML pantalla y péguelo en Azure AD como hello **identificador** valor.</span><span class="sxs-lookup"><span data-stu-id="77cd9-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="77cd9-202">b.</span><span class="sxs-lookup"><span data-stu-id="77cd9-202">b.</span></span> <span data-ttu-id="77cd9-203">Dirección URL de inicio de sesión es la dirección URL del inquilino de su nube Atlassian Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="77cd9-205">Hola portal de Azure, haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="77cd9-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="77cd9-207">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="77cd9-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77cd9-208">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77cd9-209">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77cd9-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77cd9-210">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="77cd9-211">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="77cd9-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="77cd9-213">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77cd9-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77cd9-214">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="77cd9-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77cd9-216">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77cd9-218">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77cd9-220">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="77cd9-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77cd9-222">a.</span><span class="sxs-lookup"><span data-stu-id="77cd9-222">a.</span></span> <span data-ttu-id="77cd9-223">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77cd9-224">b.</span><span class="sxs-lookup"><span data-stu-id="77cd9-224">b.</span></span> <span data-ttu-id="77cd9-225">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77cd9-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77cd9-226">c.</span><span class="sxs-lookup"><span data-stu-id="77cd9-226">c.</span></span> <span data-ttu-id="77cd9-227">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77cd9-228">d.</span><span class="sxs-lookup"><span data-stu-id="77cd9-228">d.</span></span> <span data-ttu-id="77cd9-229">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="77cd9-230">Creación de un usuario de prueba de Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="77cd9-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="77cd9-231">toolog de los usuarios de Azure AD tooenable en tooAtlassian en la nube, se les deben aprovisionar en Atlassian en la nube.</span><span class="sxs-lookup"><span data-stu-id="77cd9-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="77cd9-232">En el caso de Atlassian Cloud, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="77cd9-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="77cd9-233">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77cd9-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="77cd9-234">Hola sección de administración del sitio, haga clic en hello **usuarios** botón</span><span class="sxs-lookup"><span data-stu-id="77cd9-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Creación de un usuario de Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="77cd9-236">Haga clic en hello **Create User** botón toocreate un usuario en hello Atlassian en la nube</span><span class="sxs-lookup"><span data-stu-id="77cd9-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Creación de un usuario de Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="77cd9-238">Escriba del usuario de hello **dirección de correo electrónico**, **nombre de usuario**, y **nombre completo** y asignar acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="77cd9-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Creación de un usuario de Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="77cd9-240">Haga clic en **crear usuario** botón, enviará usuario de toohello de invitación de correo electrónico de Hola y después de aceptar usuario Hola de hello invitación estará activa en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="77cd9-241">También puede crear usuarios de forma masiva de hello haciendo clic en hello **crear de forma masiva** botón Hola sección usuarios.</span><span class="sxs-lookup"><span data-stu-id="77cd9-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77cd9-242">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="77cd9-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77cd9-243">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAtlassian en la nube.</span><span class="sxs-lookup"><span data-stu-id="77cd9-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="77cd9-245">**tooassign Britta Simon tooAtlassian en la nube, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="77cd9-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="77cd9-246">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="77cd9-248">En la lista de aplicaciones de hello, seleccione **Atlassian nube**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="77cd9-250">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="77cd9-252">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-252">Click **Add** button.</span></span> <span data-ttu-id="77cd9-253">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="77cd9-255">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="77cd9-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77cd9-256">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77cd9-257">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="77cd9-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77cd9-258">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="77cd9-258">Testing single sign-on</span></span>

<span data-ttu-id="77cd9-259">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="77cd9-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="77cd9-260">Al hacer clic en hello en la nube Atlassian el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Atlassian en la nube.</span><span class="sxs-lookup"><span data-stu-id="77cd9-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="77cd9-261">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77cd9-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="77cd9-262">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="77cd9-262">Additional resources</span></span>

* [<span data-ttu-id="77cd9-263">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77cd9-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77cd9-264">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77cd9-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

