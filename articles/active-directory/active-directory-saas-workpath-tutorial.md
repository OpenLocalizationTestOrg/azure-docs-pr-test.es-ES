---
title: "Tutorial: integración de Azure Active Directory con Workpath | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="772ba-103">Tutorial: integración de Azure Active Directory con Workpath</span><span class="sxs-lookup"><span data-stu-id="772ba-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="772ba-104">En este tutorial, aprenderá cómo toointegrate Workpath con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="772ba-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="772ba-105">Integración Workpath con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="772ba-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="772ba-106">Puede controlar en Azure AD que tenga acceso tooWorkpath</span><span class="sxs-lookup"><span data-stu-id="772ba-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="772ba-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkpath (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="772ba-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="772ba-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="772ba-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="772ba-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="772ba-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="772ba-110">Prerequisites</span></span>

<span data-ttu-id="772ba-111">integración de Azure AD con Workpath tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="772ba-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="772ba-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="772ba-113">Una suscripción habilitada para el inicio de sesión único en Workpath</span><span class="sxs-lookup"><span data-stu-id="772ba-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="772ba-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="772ba-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="772ba-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="772ba-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="772ba-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="772ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="772ba-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="772ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="772ba-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="772ba-118">Scenario description</span></span>
<span data-ttu-id="772ba-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="772ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="772ba-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="772ba-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="772ba-121">Agregar Workpath desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="772ba-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="772ba-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="772ba-123">Agregar Workpath desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="772ba-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="772ba-124">integración de hello tooconfigure de Workpath en Azure AD, deberá tooadd Workpath de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="772ba-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="772ba-125">**tooadd Workpath de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="772ba-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="772ba-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="772ba-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="772ba-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="772ba-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="772ba-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="772ba-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="772ba-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="772ba-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="772ba-133">En el cuadro de búsqueda de hello, escriba **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="772ba-133">In hello search box, type **Workpath**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="772ba-135">En el panel de resultados de hello, seleccione **Workpath**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="772ba-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="772ba-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="772ba-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workpath con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="772ba-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="772ba-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workpath es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="772ba-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="772ba-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workpath debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="772ba-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="772ba-141">En Workpath, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="772ba-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="772ba-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Workpath, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="772ba-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="772ba-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="772ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="772ba-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="772ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="772ba-145">**[Crear un usuario de prueba Workpath](#creating-a-workpath-test-user)**  -toohave un equivalente de Britta Simon en Workpath que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="772ba-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="772ba-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="772ba-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="772ba-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="772ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="772ba-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="772ba-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Workpath.</span><span class="sxs-lookup"><span data-stu-id="772ba-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="772ba-150">**inicio de sesión único en Azure AD tooconfigure con Workpath, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="772ba-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="772ba-151">En el portal de Azure, en Hola Hola **Workpath** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="772ba-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="772ba-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="772ba-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="772ba-155">En hello **Workpath dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="772ba-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="772ba-157">a.</span><span class="sxs-lookup"><span data-stu-id="772ba-157">a.</span></span> <span data-ttu-id="772ba-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="772ba-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="772ba-159">b.</span><span class="sxs-lookup"><span data-stu-id="772ba-159">b.</span></span> <span data-ttu-id="772ba-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="772ba-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="772ba-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="772ba-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="772ba-162">Si desea que aplicación de hello tooconfigure en **SP** inicia el modo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="772ba-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="772ba-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="772ba-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="772ba-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="772ba-165">These values are not real.</span></span> <span data-ttu-id="772ba-166">Actualizar estos valores con la URL de inicio de sesión real de hello, el identificador y la dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="772ba-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="772ba-167">Póngase en contacto con [equipo de soporte técnico de Workpath](https://help.workpath.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="772ba-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="772ba-168">Aplicación de Workpath espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="772ba-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="772ba-169">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="772ba-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="772ba-170">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="772ba-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="772ba-171">Hola siguiente captura de pantalla muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="772ba-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="772ba-173">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="772ba-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="772ba-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="772ba-174">Attribute Name</span></span> | <span data-ttu-id="772ba-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="772ba-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="772ba-176">first_name</span><span class="sxs-lookup"><span data-stu-id="772ba-176">first_name</span></span> | <span data-ttu-id="772ba-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="772ba-177">user.givenname</span></span> |
    | <span data-ttu-id="772ba-178">last_name</span><span class="sxs-lookup"><span data-stu-id="772ba-178">last_name</span></span> | <span data-ttu-id="772ba-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="772ba-179">user.surname</span></span> |
    
    <span data-ttu-id="772ba-180">a.</span><span class="sxs-lookup"><span data-stu-id="772ba-180">a.</span></span> <span data-ttu-id="772ba-181">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="772ba-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="772ba-183">b.</span><span class="sxs-lookup"><span data-stu-id="772ba-183">b.</span></span> <span data-ttu-id="772ba-184">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="772ba-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="772ba-186">c.</span><span class="sxs-lookup"><span data-stu-id="772ba-186">c.</span></span> <span data-ttu-id="772ba-187">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="772ba-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="772ba-188">d.</span><span class="sxs-lookup"><span data-stu-id="772ba-188">d.</span></span> <span data-ttu-id="772ba-189">Deje hello **Namespace** cuadro de texto en blanco.</span><span class="sxs-lookup"><span data-stu-id="772ba-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="772ba-190">e.</span><span class="sxs-lookup"><span data-stu-id="772ba-190">e.</span></span> <span data-ttu-id="772ba-191">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="772ba-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="772ba-192">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="772ba-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="772ba-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="772ba-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="772ba-196">En hello **Workpath configuración** sección, haga clic en **configurar Workpath** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="772ba-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="772ba-197">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="772ba-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="772ba-199">tooconfigure inicio de sesión único en **Workpath** lado, necesita hello toosend descargado **Metadata XML**, **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[equipo de soporte técnico de Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="772ba-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="772ba-200">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="772ba-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="772ba-201">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="772ba-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="772ba-202">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="772ba-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="772ba-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="772ba-204">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="772ba-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="772ba-206">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="772ba-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="772ba-207">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="772ba-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="772ba-209">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="772ba-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="772ba-211">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="772ba-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="772ba-213">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="772ba-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="772ba-215">a.</span><span class="sxs-lookup"><span data-stu-id="772ba-215">a.</span></span> <span data-ttu-id="772ba-216">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="772ba-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="772ba-217">b.</span><span class="sxs-lookup"><span data-stu-id="772ba-217">b.</span></span> <span data-ttu-id="772ba-218">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="772ba-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="772ba-219">c.</span><span class="sxs-lookup"><span data-stu-id="772ba-219">c.</span></span> <span data-ttu-id="772ba-220">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="772ba-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="772ba-221">d.</span><span class="sxs-lookup"><span data-stu-id="772ba-221">d.</span></span> <span data-ttu-id="772ba-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="772ba-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="772ba-223">Creación de un usuario de prueba de Workpath</span><span class="sxs-lookup"><span data-stu-id="772ba-223">Creating a Workpath test user</span></span>

<span data-ttu-id="772ba-224">Workpath admite aprovisionamiento de usuarios Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="772ba-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="772ba-225">Después de la autenticación a los usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="772ba-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="772ba-226">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="772ba-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="772ba-227">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkpath.</span><span class="sxs-lookup"><span data-stu-id="772ba-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="772ba-229">**tooassign Britta Simon tooWorkpath, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="772ba-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="772ba-230">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="772ba-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="772ba-232">En la lista de aplicaciones de hello, seleccione **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="772ba-232">In hello applications list, select **Workpath**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="772ba-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="772ba-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="772ba-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="772ba-236">Click **Add** button.</span></span> <span data-ttu-id="772ba-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="772ba-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="772ba-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="772ba-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="772ba-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="772ba-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="772ba-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="772ba-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="772ba-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="772ba-242">Testing single sign-on</span></span>

<span data-ttu-id="772ba-243">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="772ba-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="772ba-244">Al hacer clic en icono de Workpath Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Workpath aplicación.</span><span class="sxs-lookup"><span data-stu-id="772ba-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="772ba-245">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="772ba-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="772ba-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="772ba-246">Additional resources</span></span>

* [<span data-ttu-id="772ba-247">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="772ba-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="772ba-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="772ba-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

