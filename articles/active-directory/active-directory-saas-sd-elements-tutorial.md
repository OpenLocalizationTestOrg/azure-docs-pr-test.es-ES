---
title: "Tutorial: Integración de Azure Active Directory con SD Elements | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y los elementos de SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="9e652-103">Tutorial: Integración de Azure Active Directory con SD Elements</span><span class="sxs-lookup"><span data-stu-id="9e652-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="9e652-104">En este tutorial, aprenderá cómo toointegrate elementos SD con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e652-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e652-105">Integrar los elementos de SD con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9e652-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9e652-106">Puede controlar en Azure AD que tenga acceso tooSD elementos</span><span class="sxs-lookup"><span data-stu-id="9e652-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="9e652-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión con tooSD elementos (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e652-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9e652-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9e652-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e652-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e652-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9e652-110">Prerequisites</span></span>

<span data-ttu-id="9e652-111">integración de Azure AD con elementos de SD tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9e652-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="9e652-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e652-113">Una suscripción habilitada para el inicio de sesión único en SD Elements</span><span class="sxs-lookup"><span data-stu-id="9e652-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e652-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9e652-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e652-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9e652-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e652-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9e652-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e652-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e652-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e652-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9e652-118">Scenario description</span></span>
<span data-ttu-id="9e652-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9e652-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e652-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9e652-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e652-121">Adición de SD de elementos de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9e652-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="9e652-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="9e652-123">Adición de SD de elementos de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9e652-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="9e652-124">integración de hello tooconfigure de elementos de SD en Azure AD, deberá tooadd SD elementos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9e652-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9e652-125">**tooadd SD elementos de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e652-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e652-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9e652-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e652-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9e652-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9e652-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e652-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9e652-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e652-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9e652-133">En el cuadro de búsqueda de hello, escriba **SD elementos**.</span><span class="sxs-lookup"><span data-stu-id="9e652-133">In hello search box, type **SD Elements**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="9e652-135">En el panel de resultados de hello, seleccione **SD elementos**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9e652-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e652-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e652-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SD Elements con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9e652-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e652-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en elementos de SD es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e652-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="9e652-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en elementos de SD debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9e652-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="9e652-141">SD de elementos, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e652-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9e652-142">tooconfigure y prueba de inicio de sesión único en Azure AD con elementos de SD, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9e652-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9e652-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9e652-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9e652-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e652-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e652-145">**[Crear un usuario de prueba de elementos de SD](#creating-a-sd-elements-test-user)**  -toohave un equivalente de Britta Simon en elementos de SD es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9e652-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e652-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9e652-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e652-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9e652-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e652-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e652-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de elementos de SD.</span><span class="sxs-lookup"><span data-stu-id="9e652-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="9e652-150">**inicio de sesión único en tooconfigure Azure AD con elementos de SD, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e652-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e652-151">En el portal de Azure, en Hola Hola **SD elementos** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9e652-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9e652-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9e652-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="9e652-155">En hello **SD elementos dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9e652-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="9e652-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e652-157">a.</span></span> <span data-ttu-id="9e652-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="9e652-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="9e652-159">b.</span><span class="sxs-lookup"><span data-stu-id="9e652-159">b.</span></span> <span data-ttu-id="9e652-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="9e652-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e652-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9e652-161">These values are not real.</span></span> <span data-ttu-id="9e652-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="9e652-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9e652-163">Póngase en contacto con [equipo de soporte técnico de los elementos de SD](mailto:support@sdelements.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9e652-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="9e652-164">Aplicación de elementos de SD espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="9e652-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9e652-165">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e652-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="9e652-166">Puede administrar valores de hello de estos atributos de hello **"Atributo de usuario"** pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9e652-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="9e652-167">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="9e652-167">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="9e652-169">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9e652-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="9e652-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="9e652-170">Attribute Name</span></span> | <span data-ttu-id="9e652-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="9e652-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9e652-172">email</span><span class="sxs-lookup"><span data-stu-id="9e652-172">email</span></span> |<span data-ttu-id="9e652-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="9e652-173">user.mail</span></span> |
    | <span data-ttu-id="9e652-174">firstname</span><span class="sxs-lookup"><span data-stu-id="9e652-174">firstname</span></span> |<span data-ttu-id="9e652-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9e652-175">user.givenname</span></span> |
    | <span data-ttu-id="9e652-176">lastname</span><span class="sxs-lookup"><span data-stu-id="9e652-176">lastname</span></span> |<span data-ttu-id="9e652-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="9e652-177">user.surname</span></span> |

    <span data-ttu-id="9e652-178">a.</span><span class="sxs-lookup"><span data-stu-id="9e652-178">a.</span></span> <span data-ttu-id="9e652-179">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e652-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="9e652-182">b.</span><span class="sxs-lookup"><span data-stu-id="9e652-182">b.</span></span> <span data-ttu-id="9e652-183">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="9e652-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="9e652-184">c.</span><span class="sxs-lookup"><span data-stu-id="9e652-184">c.</span></span> <span data-ttu-id="9e652-185">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="9e652-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="9e652-186">d.</span><span class="sxs-lookup"><span data-stu-id="9e652-186">d.</span></span> <span data-ttu-id="9e652-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9e652-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="9e652-188">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9e652-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="9e652-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9e652-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9e652-192">En hello **SD elementos de configuración** sección, haga clic en **configurar elementos de SD** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9e652-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9e652-193">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9e652-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="9e652-195">tooget inicio de sesión único habilitado, póngase en contacto con su [equipo de soporte técnico SD elementos](mailto:support@sdelements.com) y proporcióneles con archivo de certificado descargado hello.</span><span class="sxs-lookup"><span data-stu-id="9e652-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="9e652-196">En otra ventana del explorador, inquilino de SD elementos tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="9e652-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="9e652-197">En el menú de hello en la parte superior de hello, haga clic en **System**y, a continuación, **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9e652-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="9e652-199">En hello **configuración de inicio de sesión único** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9e652-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="9e652-201">a.</span><span class="sxs-lookup"><span data-stu-id="9e652-201">a.</span></span> <span data-ttu-id="9e652-202">Como **Tipo de inicio de sesión único**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e652-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="9e652-203">b.</span><span class="sxs-lookup"><span data-stu-id="9e652-203">b.</span></span> <span data-ttu-id="9e652-204">Hola **Id. de entidad de proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e652-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="9e652-205">c.</span><span class="sxs-lookup"><span data-stu-id="9e652-205">c.</span></span> <span data-ttu-id="9e652-206">Hola **servicio proveedor de identidad Single Sign-On** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e652-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="9e652-207">d.</span><span class="sxs-lookup"><span data-stu-id="9e652-207">d.</span></span> <span data-ttu-id="9e652-208">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9e652-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9e652-209">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9e652-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9e652-210">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9e652-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9e652-211">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e652-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e652-212">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e652-213">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9e652-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9e652-215">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e652-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e652-216">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9e652-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e652-218">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9e652-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e652-220">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e652-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e652-222">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9e652-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e652-224">a.</span><span class="sxs-lookup"><span data-stu-id="9e652-224">a.</span></span> <span data-ttu-id="9e652-225">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e652-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e652-226">b.</span><span class="sxs-lookup"><span data-stu-id="9e652-226">b.</span></span> <span data-ttu-id="9e652-227">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e652-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e652-228">c.</span><span class="sxs-lookup"><span data-stu-id="9e652-228">c.</span></span> <span data-ttu-id="9e652-229">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9e652-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9e652-230">d.</span><span class="sxs-lookup"><span data-stu-id="9e652-230">d.</span></span> <span data-ttu-id="9e652-231">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9e652-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="9e652-232">Creación de un usuario de prueba de SD Elements</span><span class="sxs-lookup"><span data-stu-id="9e652-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="9e652-233">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en elementos de SD.</span><span class="sxs-lookup"><span data-stu-id="9e652-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="9e652-234">En caso de hello de SD elementos, la creación de elementos de SD usuarios es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9e652-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="9e652-235">**toocreate Britta Simon SD de elementos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e652-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e652-236">En una ventana del explorador web, sitio de la empresa de inicio de sesión tooyour SD elementos como administrador.</span><span class="sxs-lookup"><span data-stu-id="9e652-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="9e652-237">En el menú de hello en la parte superior de hello, haga clic en **administración de usuarios**y, a continuación, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9e652-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="9e652-239">Haga clic en **Add New User**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="9e652-239">Click **Add New User**.</span></span>
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="9e652-241">En hello **Agregar nuevo usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9e652-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="9e652-243">a.</span><span class="sxs-lookup"><span data-stu-id="9e652-243">a.</span></span> <span data-ttu-id="9e652-244">Hola **correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="9e652-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="9e652-245">b.</span><span class="sxs-lookup"><span data-stu-id="9e652-245">b.</span></span> <span data-ttu-id="9e652-246">Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="9e652-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="9e652-247">c.</span><span class="sxs-lookup"><span data-stu-id="9e652-247">c.</span></span> <span data-ttu-id="9e652-248">Hola **Last Name** cuadro de texto, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9e652-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="9e652-249">d.</span><span class="sxs-lookup"><span data-stu-id="9e652-249">d.</span></span> <span data-ttu-id="9e652-250">Como **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="9e652-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="9e652-251">e.</span><span class="sxs-lookup"><span data-stu-id="9e652-251">e.</span></span> <span data-ttu-id="9e652-252">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="9e652-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9e652-253">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e652-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9e652-254">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSD elementos.</span><span class="sxs-lookup"><span data-stu-id="9e652-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9e652-256">**tooassign Britta Simon tooSD elementos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9e652-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e652-257">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9e652-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9e652-259">En la lista de aplicaciones de hello, seleccione **SD elementos**.</span><span class="sxs-lookup"><span data-stu-id="9e652-259">In hello applications list, select **SD Elements**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="9e652-261">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9e652-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9e652-263">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9e652-263">Click **Add** button.</span></span> <span data-ttu-id="9e652-264">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9e652-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9e652-266">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e652-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9e652-267">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9e652-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e652-268">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9e652-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e652-269">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9e652-269">Testing single sign-on</span></span>

<span data-ttu-id="9e652-270">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9e652-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="9e652-271">Al hacer clic en hello SD elementos disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación SD elementos.</span><span class="sxs-lookup"><span data-stu-id="9e652-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e652-272">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9e652-272">Additional resources</span></span>

* [<span data-ttu-id="9e652-273">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e652-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e652-274">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e652-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

