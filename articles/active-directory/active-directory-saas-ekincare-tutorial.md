---
title: "Tutorial: integración de Azure Active Directory con eKincare | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="982f8-103">Tutorial: integración de Azure Active Directory con eKincare</span><span class="sxs-lookup"><span data-stu-id="982f8-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="982f8-104">En este tutorial, aprenderá cómo toointegrate eKincare con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="982f8-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="982f8-105">Integración eKincare con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="982f8-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="982f8-106">Puede controlar en Azure AD que tenga acceso tooeKincare</span><span class="sxs-lookup"><span data-stu-id="982f8-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="982f8-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooeKincare (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="982f8-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="982f8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="982f8-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="982f8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="982f8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="982f8-110">Prerequisites</span></span>

<span data-ttu-id="982f8-111">integración de Azure AD con eKincare tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="982f8-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="982f8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="982f8-113">Una suscripción habilitada para el inicio de sesión único en eKincare</span><span class="sxs-lookup"><span data-stu-id="982f8-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="982f8-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="982f8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="982f8-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="982f8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="982f8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="982f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="982f8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="982f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="982f8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="982f8-118">Scenario description</span></span>
<span data-ttu-id="982f8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="982f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="982f8-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="982f8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="982f8-121">Agregar eKincare desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="982f8-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="982f8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="982f8-123">Agregar eKincare desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="982f8-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="982f8-124">integración de hello tooconfigure de eKincare en Azure AD, deberá tooadd eKincare de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="982f8-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="982f8-125">**tooadd eKincare de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="982f8-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="982f8-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="982f8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="982f8-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="982f8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="982f8-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="982f8-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="982f8-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="982f8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="982f8-133">En el cuadro de búsqueda de hello, escriba **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="982f8-133">In hello search box, type **eKincare**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="982f8-135">En el panel de resultados de hello, seleccione **eKincare**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="982f8-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="982f8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="982f8-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con eKincare con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="982f8-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="982f8-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en eKincare es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="982f8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="982f8-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en eKincare debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="982f8-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="982f8-141">En eKincare, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="982f8-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="982f8-142">tooconfigure y prueba de inicio de sesión único en Azure AD con eKincare, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="982f8-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="982f8-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="982f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="982f8-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="982f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="982f8-145">**[Crear un usuario de prueba eKincare](#creating-a-ekincare-test-user)**  -toohave un equivalente de Britta Simon en eKincare que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="982f8-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="982f8-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="982f8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="982f8-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="982f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="982f8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="982f8-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación eKincare.</span><span class="sxs-lookup"><span data-stu-id="982f8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="982f8-150">**inicio de sesión único en Azure AD tooconfigure con eKincare, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="982f8-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="982f8-151">En el portal de Azure, en Hola Hola **eKincare** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="982f8-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="982f8-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="982f8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="982f8-155">En hello **eKincare dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="982f8-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="982f8-157">a.</span><span class="sxs-lookup"><span data-stu-id="982f8-157">a.</span></span> <span data-ttu-id="982f8-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="982f8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="982f8-159">b.</span><span class="sxs-lookup"><span data-stu-id="982f8-159">b.</span></span> <span data-ttu-id="982f8-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="982f8-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="982f8-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="982f8-161">These values are not real.</span></span> <span data-ttu-id="982f8-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="982f8-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="982f8-163">Póngase en contacto con [equipo de soporte técnico de eKincare](mailto:tech@ekincare.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="982f8-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="982f8-164">aplicación de eKincare espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="982f8-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="982f8-165">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="982f8-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="982f8-166">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="982f8-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="982f8-167">Hola siguiente captura de pantalla muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="982f8-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="982f8-168">Hello notificación nombre será siempre **"employeeid"** y el valor de Hola que hemos asignamos toouser.extensionattribute1, que contiene el employeeid Hola de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="982f8-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="982f8-169">Hola, por ejemplo, nombre de otros dos notificaciones</span><span class="sxs-lookup"><span data-stu-id="982f8-169">hello other two claims' name i.e</span></span> <span data-ttu-id="982f8-170">**"organizationid"** y **"organizationname"** siempre será mismo y sus valores contienen detalles de Hola de organización de saludo del usuario de hello respectivamente.</span><span class="sxs-lookup"><span data-stu-id="982f8-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="982f8-172">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="982f8-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="982f8-173">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="982f8-173">Attribute Name</span></span> | <span data-ttu-id="982f8-174">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="982f8-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="982f8-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="982f8-175">employeeid</span></span> | <span data-ttu-id="982f8-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="982f8-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="982f8-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="982f8-177">organizationid</span></span> | <span data-ttu-id="982f8-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="982f8-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="982f8-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="982f8-179">organizationname</span></span> | <span data-ttu-id="982f8-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="982f8-180">*user.companyname*</span></span> |

    <span data-ttu-id="982f8-181">a.</span><span class="sxs-lookup"><span data-stu-id="982f8-181">a.</span></span> <span data-ttu-id="982f8-182">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="982f8-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="982f8-185">b.</span><span class="sxs-lookup"><span data-stu-id="982f8-185">b.</span></span> <span data-ttu-id="982f8-186">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="982f8-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="982f8-187">c.</span><span class="sxs-lookup"><span data-stu-id="982f8-187">c.</span></span> <span data-ttu-id="982f8-188">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="982f8-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="982f8-189">d.</span><span class="sxs-lookup"><span data-stu-id="982f8-189">d.</span></span> <span data-ttu-id="982f8-190">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="982f8-190">Click **Ok**</span></span>

6. <span data-ttu-id="982f8-191">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="982f8-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="982f8-193">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="982f8-193">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="982f8-195">tooconfigure inicio de sesión único en **eKincare** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="982f8-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="982f8-196">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="982f8-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="982f8-197">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="982f8-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="982f8-198">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="982f8-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="982f8-199">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="982f8-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="982f8-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="982f8-201">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="982f8-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="982f8-203">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="982f8-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="982f8-204">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="982f8-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="982f8-206">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="982f8-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="982f8-208">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="982f8-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="982f8-210">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="982f8-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="982f8-212">a.</span><span class="sxs-lookup"><span data-stu-id="982f8-212">a.</span></span> <span data-ttu-id="982f8-213">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="982f8-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="982f8-214">b.</span><span class="sxs-lookup"><span data-stu-id="982f8-214">b.</span></span> <span data-ttu-id="982f8-215">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="982f8-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="982f8-216">c.</span><span class="sxs-lookup"><span data-stu-id="982f8-216">c.</span></span> <span data-ttu-id="982f8-217">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="982f8-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="982f8-218">d.</span><span class="sxs-lookup"><span data-stu-id="982f8-218">d.</span></span> <span data-ttu-id="982f8-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="982f8-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="982f8-220">Creación de un usuario de prueba de eKincare</span><span class="sxs-lookup"><span data-stu-id="982f8-220">Creating a eKincare test user</span></span>

<span data-ttu-id="982f8-221">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="982f8-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="982f8-222">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="982f8-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="982f8-223">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooeKincare.</span><span class="sxs-lookup"><span data-stu-id="982f8-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="982f8-225">**tooassign Britta Simon tooeKincare, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="982f8-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="982f8-226">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="982f8-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="982f8-228">En la lista de aplicaciones de hello, seleccione **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="982f8-228">In hello applications list, select **eKincare**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="982f8-230">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="982f8-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="982f8-232">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="982f8-232">Click **Add** button.</span></span> <span data-ttu-id="982f8-233">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="982f8-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="982f8-235">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="982f8-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="982f8-236">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="982f8-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="982f8-237">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="982f8-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="982f8-238">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="982f8-238">Testing single sign-on</span></span>

<span data-ttu-id="982f8-239">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="982f8-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="982f8-240">Al hacer clic en icono de eKincare Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour eKincare aplicación.</span><span class="sxs-lookup"><span data-stu-id="982f8-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="982f8-241">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="982f8-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="982f8-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="982f8-242">Additional resources</span></span>

* [<span data-ttu-id="982f8-243">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="982f8-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="982f8-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="982f8-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

