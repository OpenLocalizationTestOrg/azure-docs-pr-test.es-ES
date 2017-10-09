---
title: "Tutorial: integración de Azure Active Directory con BetterWorks | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="b3973-103">Tutorial: Integración de Azure Active Directory con BetterWorks</span><span class="sxs-lookup"><span data-stu-id="b3973-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="b3973-104">En este tutorial, aprenderá cómo toointegrate BetterWorks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3973-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3973-105">Integración BetterWorks con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b3973-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3973-106">Puede controlar en Azure AD que tenga acceso tooBetterWorks</span><span class="sxs-lookup"><span data-stu-id="b3973-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="b3973-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBetterWorks (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3973-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b3973-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b3973-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3973-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3973-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b3973-110">Prerequisites</span></span>

<span data-ttu-id="b3973-111">integración de Azure AD con BetterWorks tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b3973-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="b3973-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3973-113">Una suscripción habilitada para inicio de sesión único en BetterWorks</span><span class="sxs-lookup"><span data-stu-id="b3973-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3973-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b3973-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3973-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b3973-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3973-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b3973-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3973-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3973-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3973-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b3973-118">Scenario description</span></span>
<span data-ttu-id="b3973-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b3973-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3973-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="b3973-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3973-121">Agregar BetterWorks desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b3973-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="b3973-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="b3973-123">Agregar BetterWorks desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b3973-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="b3973-124">integración de hello tooconfigure de BetterWorks en Azure AD, deberá tooadd BetterWorks de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3973-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3973-125">**tooadd BetterWorks de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b3973-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3973-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b3973-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3973-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b3973-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3973-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b3973-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b3973-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b3973-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b3973-133">En el cuadro de búsqueda de hello, escriba **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="b3973-133">In hello search box, type **BetterWorks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="b3973-135">En el panel de resultados de hello, seleccione **BetterWorks**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b3973-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3973-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3973-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BetterWorks con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b3973-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3973-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en BetterWorks es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3973-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="b3973-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BetterWorks debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="b3973-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="b3973-141">En BetterWorks, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3973-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b3973-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BetterWorks, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b3973-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3973-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="b3973-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3973-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b3973-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3973-145">**[Crear un usuario de prueba BetterWorks](#creating-a-betterworks-test-user)**  -toohave un equivalente de Britta Simon en BetterWorks que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b3973-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3973-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b3973-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3973-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b3973-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3973-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3973-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="b3973-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="b3973-150">**inicio de sesión único en Azure AD tooconfigure con BetterWorks, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b3973-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3973-151">En el portal de Azure, en Hola Hola **BetterWorks** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b3973-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b3973-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b3973-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="b3973-155">En hello **BetterWorks dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**:</span><span class="sxs-lookup"><span data-stu-id="b3973-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="b3973-157">a.</span><span class="sxs-lookup"><span data-stu-id="b3973-157">a.</span></span> <span data-ttu-id="b3973-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="b3973-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="b3973-159">b.</span><span class="sxs-lookup"><span data-stu-id="b3973-159">b.</span></span> <span data-ttu-id="b3973-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="b3973-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="b3973-161">En hello **BetterWorks dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b3973-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="b3973-163">a.</span><span class="sxs-lookup"><span data-stu-id="b3973-163">a.</span></span> <span data-ttu-id="b3973-164">Haga clic en hello **mostrar avanzadas de configuración de la URL**.</span><span class="sxs-lookup"><span data-stu-id="b3973-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="b3973-165">b.</span><span class="sxs-lookup"><span data-stu-id="b3973-165">b.</span></span> <span data-ttu-id="b3973-166">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="b3973-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3973-167">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="b3973-167">These are not real values.</span></span> <span data-ttu-id="b3973-168">Actualizar estos valores con hello URL de respuesta, identificador y el inicio de sesión en dirección URL real.</span><span class="sxs-lookup"><span data-stu-id="b3973-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="b3973-169">Póngase en contacto con [equipo de soporte técnico BetterWorks](mailto:support@betterworks.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="b3973-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="b3973-170">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b3973-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="b3973-172">Aplicación de BetterWorks espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="b3973-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b3973-173">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3973-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="b3973-174">Puede administrar valores de hello de estos atributos de Hola "**atributo**" pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b3973-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="b3973-175">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="b3973-175">hello following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="b3973-177">En hello **atributos de token SAML** cuadro de diálogo, para cada fila se muestra en la tabla de Hola a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b3973-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="b3973-178">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="b3973-178">Attribute Name</span></span> | <span data-ttu-id="b3973-179">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="b3973-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="b3973-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="b3973-180">saml_token</span></span>     | <span data-ttu-id="b3973-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="b3973-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="b3973-182">a.</span><span class="sxs-lookup"><span data-stu-id="b3973-182">a.</span></span> <span data-ttu-id="b3973-183">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b3973-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="b3973-186">b.</span><span class="sxs-lookup"><span data-stu-id="b3973-186">b.</span></span> <span data-ttu-id="b3973-187">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="b3973-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="b3973-188">c.</span><span class="sxs-lookup"><span data-stu-id="b3973-188">c.</span></span> <span data-ttu-id="b3973-189">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="b3973-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="b3973-190">d.</span><span class="sxs-lookup"><span data-stu-id="b3973-190">d.</span></span> <span data-ttu-id="b3973-191">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b3973-191">Click **Ok**.</span></span>

7. <span data-ttu-id="b3973-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b3973-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b3973-194">tooconfigure inicio de sesión único en **BetterWorks** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="b3973-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="b3973-195">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="b3973-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3973-196">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="b3973-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3973-197">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3973-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3973-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3973-199">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="b3973-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b3973-201">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b3973-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3973-202">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b3973-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3973-204">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b3973-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3973-206">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3973-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3973-208">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="b3973-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3973-210">a.</span><span class="sxs-lookup"><span data-stu-id="b3973-210">a.</span></span> <span data-ttu-id="b3973-211">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3973-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3973-212">b.</span><span class="sxs-lookup"><span data-stu-id="b3973-212">b.</span></span> <span data-ttu-id="b3973-213">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b3973-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3973-214">c.</span><span class="sxs-lookup"><span data-stu-id="b3973-214">c.</span></span> <span data-ttu-id="b3973-215">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b3973-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b3973-216">d.</span><span class="sxs-lookup"><span data-stu-id="b3973-216">d.</span></span> <span data-ttu-id="b3973-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b3973-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="b3973-218">Creación de un usuario de prueba en BetterWorks</span><span class="sxs-lookup"><span data-stu-id="b3973-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="b3973-219">En esta sección, creará un usuario llamado Britta Simon en BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="b3973-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="b3973-220">Trabajar con [equipo de soporte técnico BetterWorks](mailto:support@betterworks.com) a los usuarios de tooadd hello en la plataforma de BetterWorks Hola.</span><span class="sxs-lookup"><span data-stu-id="b3973-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b3973-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3973-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b3973-222">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBetterWorks.</span><span class="sxs-lookup"><span data-stu-id="b3973-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b3973-224">**tooassign Britta Simon tooBetterWorks, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b3973-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3973-225">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b3973-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b3973-227">En la lista de aplicaciones de hello, seleccione **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="b3973-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="b3973-229">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b3973-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b3973-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b3973-231">Click **Add** button.</span></span> <span data-ttu-id="b3973-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b3973-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b3973-234">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3973-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3973-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b3973-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3973-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b3973-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3973-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b3973-237">Testing single sign-on</span></span>

<span data-ttu-id="b3973-238">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b3973-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3973-239">Al hacer clic en hello BetterWorks el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour BetterWorks aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3973-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3973-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b3973-240">Additional resources</span></span>

* [<span data-ttu-id="b3973-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3973-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3973-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3973-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

