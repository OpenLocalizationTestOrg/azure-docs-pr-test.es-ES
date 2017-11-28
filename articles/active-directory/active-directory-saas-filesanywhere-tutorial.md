---
title: "Tutorial: Integración de Azure Active Directory con FilesAnywhere | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="4ef9d-103">Tutorial: Integración de Azure Active Directory con FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="4ef9d-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="4ef9d-104">En este tutorial, aprenderá cómo toointegrate FilesAnywhere con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ef9d-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ef9d-105">Integración FilesAnywhere con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ef9d-106">Puede controlar en Azure AD que tenga acceso tooFilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="4ef9d-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="4ef9d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFilesAnywhere (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ef9d-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="4ef9d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="4ef9d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ef9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ef9d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ef9d-110">Prerequisites</span></span>

<span data-ttu-id="4ef9d-111">integración de Azure AD con FilesAnywhere tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="4ef9d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ef9d-113">Una suscripción habilitada para el inicio de sesión único en FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="4ef9d-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="4ef9d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="4ef9d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ef9d-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4ef9d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ef9d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="4ef9d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4ef9d-118">Scenario description</span></span>
<span data-ttu-id="4ef9d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ef9d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ef9d-121">Agregar FilesAnywhere desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4ef9d-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="4ef9d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="4ef9d-123">Agregar FilesAnywhere desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4ef9d-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="4ef9d-124">integración de hello tooconfigure de FilesAnywhere en Azure AD, deberá tooadd FilesAnywhere de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ef9d-125">**tooadd FilesAnywhere de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4ef9d-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ef9d-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4ef9d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4ef9d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4ef9d-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4ef9d-133">En el cuadro de búsqueda de hello, escriba **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="4ef9d-135">En el panel de resultados de hello, seleccione **FilesAnywhere**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ef9d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ef9d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FilesAnywhere con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4ef9d-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ef9d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FilesAnywhere es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="4ef9d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FilesAnywhere debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="4ef9d-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="4ef9d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con FilesAnywhere, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ef9d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ef9d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ef9d-145">**[Crear un usuario de prueba FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave un equivalente de Britta Simon en FilesAnywhere que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="4ef9d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="4ef9d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ef9d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ef9d-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="4ef9d-150">**inicio de sesión único en Azure AD tooconfigure con FilesAnywhere, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4ef9d-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ef9d-151">En el portal de administración de Azure de hello, en hello **FilesAnywhere** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4ef9d-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="4ef9d-155">En hello **FilesAnywhere dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="4ef9d-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-157">a.</span></span> <span data-ttu-id="4ef9d-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="4ef9d-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="4ef9d-159">Tenga en cuenta ese valor hello **215** es un **clientid** y es simplemente un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="4ef9d-160">Necesita tooreplace con valor de clientid real Hola.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="4ef9d-161">En hello **FilesAnywhere dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="4ef9d-163">a.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-163">a.</span></span> <span data-ttu-id="4ef9d-164">Haga clic en hello **mostrar avanzadas de configuración de direcciones URL** opción</span><span class="sxs-lookup"><span data-stu-id="4ef9d-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="4ef9d-165">b.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-165">b.</span></span> <span data-ttu-id="4ef9d-166">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="4ef9d-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ef9d-167">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="4ef9d-168">Tener tooupdate estos valores con hello URL de dirección URL de inicio de sesión y de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="4ef9d-169">Póngase en contacto con [equipo de soporte técnico de FilesAnywhere](mailto:support@FilesAnywhere.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="4ef9d-170">Aplicación de FilesAnywhere Software espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4ef9d-171">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="4ef9d-172">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="4ef9d-173">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-173">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="4ef9d-175">Hola cuando inicia sesión a los usuarios una FilesAnywhere obtienen valor Hola de **clientid** de atributo de [FilesAnywhere equipo](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="4ef9d-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="4ef9d-176">Tener atributo de "Id. de cliente" hello tooadd con valor único de hello proporcionado por FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="4ef9d-177">Todos estos atributos mostrados anteriormente son obligatorios.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="4ef9d-178">Tenga en cuenta ese valor hello **2331** de **clientid** es simplemente un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="4ef9d-179">Necesita el valor real de tooprovide Hola.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="4ef9d-180">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4ef9d-181">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="4ef9d-181">Attribute Name</span></span> | <span data-ttu-id="4ef9d-182">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="4ef9d-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="4ef9d-183">clientid</span><span class="sxs-lookup"><span data-stu-id="4ef9d-183">clientid</span></span> | <span data-ttu-id="4ef9d-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="4ef9d-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="4ef9d-185">a.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-185">a.</span></span> <span data-ttu-id="4ef9d-186">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="4ef9d-189">b.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-189">b.</span></span> <span data-ttu-id="4ef9d-190">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4ef9d-191">c.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-191">c.</span></span> <span data-ttu-id="4ef9d-192">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4ef9d-193">d.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-193">d.</span></span> <span data-ttu-id="4ef9d-194">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-194">Click **Ok**</span></span>

7. <span data-ttu-id="4ef9d-195">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4ef9d-195">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4ef9d-197">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="4ef9d-199">En hello **FilesAnywhere configuración** sección, haga clic en **configurar FilesAnywhere** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="4ef9d-202">configuración de SSO de tooget completa de la aplicación FilesAnywhere final, póngase en contacto con [equipo de soporte técnico de FilesAnywhere](mailto:support@FilesAnywhere.com) y proporcióneles la dirección URL de inicio de sesión único (SSO) y de certificado de firma de tokens SAML de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ef9d-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ef9d-204">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4ef9d-206">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4ef9d-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ef9d-207">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ef9d-209">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ef9d-211">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ef9d-213">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4ef9d-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ef9d-215">a.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-215">a.</span></span> <span data-ttu-id="4ef9d-216">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ef9d-217">b.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-217">b.</span></span> <span data-ttu-id="4ef9d-218">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ef9d-219">c.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-219">c.</span></span> <span data-ttu-id="4ef9d-220">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4ef9d-221">d.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-221">d.</span></span> <span data-ttu-id="4ef9d-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="4ef9d-223">Creación de un usuario de prueba para FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="4ef9d-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="4ef9d-224">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4ef9d-225">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef9d-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4ef9d-226">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooFilesAnywhere de acceso.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4ef9d-228">**tooassign Britta Simon tooFilesAnywhere, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4ef9d-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ef9d-229">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4ef9d-231">En la lista de aplicaciones de hello, seleccione **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="4ef9d-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4ef9d-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-235">Click **Add** button.</span></span> <span data-ttu-id="4ef9d-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4ef9d-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4ef9d-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ef9d-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="4ef9d-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4ef9d-241">Testing single sign-on</span></span>

<span data-ttu-id="4ef9d-242">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4ef9d-243">Al hacer clic en icono de FilesAnywhere Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour FilesAnywhere aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ef9d-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4ef9d-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4ef9d-244">Additional resources</span></span>

* [<span data-ttu-id="4ef9d-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ef9d-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ef9d-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ef9d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
