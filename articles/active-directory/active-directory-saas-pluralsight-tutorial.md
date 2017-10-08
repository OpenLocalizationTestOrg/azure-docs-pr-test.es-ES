---
title: "Tutorial: integración de Azure Active Directory con Pluralsight | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="f1490-103">Tutorial: Integración de Azure Active Directory con Pluralsight</span><span class="sxs-lookup"><span data-stu-id="f1490-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="f1490-104">En este tutorial, aprenderá cómo toointegrate Pluralsight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1490-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1490-105">Integración Pluralsight con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f1490-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1490-106">Puede controlar en Azure AD que tenga acceso tooPluralsight</span><span class="sxs-lookup"><span data-stu-id="f1490-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="f1490-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPluralsight (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1490-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f1490-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1490-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1490-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1490-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f1490-110">Prerequisites</span></span>

<span data-ttu-id="f1490-111">integración de Azure AD con Pluralsight tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f1490-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="f1490-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1490-113">Una suscripción habilitada para el inicio de sesión único en Pluralsight</span><span class="sxs-lookup"><span data-stu-id="f1490-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1490-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f1490-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1490-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f1490-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1490-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f1490-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1490-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1490-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1490-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f1490-118">Scenario description</span></span>
<span data-ttu-id="f1490-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f1490-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1490-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f1490-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1490-121">Agregar Pluralsight desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f1490-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="f1490-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="f1490-123">Agregar Pluralsight desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f1490-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="f1490-124">integración de hello tooconfigure de Pluralsight en Azure AD, deberá tooadd Pluralsight de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f1490-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1490-125">**tooadd Pluralsight desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f1490-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f1490-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1490-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f1490-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1490-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f1490-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f1490-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1490-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f1490-133">En el cuadro de búsqueda de hello, escriba **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="f1490-133">In hello search box, type **Pluralsight**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="f1490-135">En el panel de resultados de hello, seleccione **Pluralsight**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1490-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1490-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1490-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pluralsight con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f1490-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1490-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Pluralsight es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1490-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="f1490-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Pluralsight debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f1490-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="f1490-141">En Pluralsight, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1490-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f1490-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Pluralsight, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f1490-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1490-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f1490-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1490-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1490-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1490-145">**[Crear un usuario de prueba de Pluralsight](#creating-a-pluralsight-test-user)**  -toohave un equivalente de Britta Simon en Pluralsight que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f1490-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1490-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f1490-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1490-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f1490-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1490-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1490-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="f1490-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="f1490-150">**inicio de sesión único en Azure AD tooconfigure con Pluralsight, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f1490-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-151">En el portal de Azure, en Hola Hola **Pluralsight** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f1490-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f1490-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f1490-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="f1490-155">En hello **Pluralsight dominio y las direcciones URL** sección, realice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1490-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="f1490-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="f1490-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1490-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="f1490-158">This value is not real.</span></span> <span data-ttu-id="f1490-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="f1490-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f1490-160">Póngase en contacto con [equipo de soporte técnico de Pluralsight cliente](mailto:support@pluralsight.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="f1490-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="f1490-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f1490-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="f1490-163">objetivo de Hola de esta sección es tooenable Azure AD inicio de sesión único en hello portal de Azure y tooconfigure SSO en la aplicación de Pluralsight hello.</span><span class="sxs-lookup"><span data-stu-id="f1490-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="f1490-164">Hola Pluralsight aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="f1490-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="f1490-165">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="f1490-165">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="f1490-167">También puede agregar hello **"Id. exclusivo"** atributo con el valor adecuado hello como EmployeeID o cualquier otra cosa que se adapte a para su organización.</span><span class="sxs-lookup"><span data-stu-id="f1490-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="f1490-168">Tenga en cuenta que esto no es atributo requerido de hello; Sin embargo, puede agregarla demasiado identificar usuario único Hola.</span><span class="sxs-lookup"><span data-stu-id="f1490-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="f1490-169">Hola tooadd requerido **atributos de token SAML**, para cada fila se muestra en la siguiente tabla se hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f1490-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="f1490-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="f1490-170">Attribute Name</span></span> | <span data-ttu-id="f1490-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="f1490-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="f1490-172">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f1490-172">First Name</span></span> |<span data-ttu-id="f1490-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f1490-173">user.givenname</span></span> |
   | <span data-ttu-id="f1490-174">Apellidos</span><span class="sxs-lookup"><span data-stu-id="f1490-174">Last Name</span></span> |<span data-ttu-id="f1490-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="f1490-175">user.surname</span></span> |
   | <span data-ttu-id="f1490-176">Email</span><span class="sxs-lookup"><span data-stu-id="f1490-176">Email</span></span> |<span data-ttu-id="f1490-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="f1490-177">user.mail</span></span> |
   
   <span data-ttu-id="f1490-178">a.</span><span class="sxs-lookup"><span data-stu-id="f1490-178">a.</span></span> <span data-ttu-id="f1490-179">Haga clic en **Agregar atributo de usuario** tooopen hello **Agregar usuario Attribure** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1490-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="f1490-181">b.</span><span class="sxs-lookup"><span data-stu-id="f1490-181">b.</span></span> <span data-ttu-id="f1490-182">Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="f1490-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="f1490-183">c.</span><span class="sxs-lookup"><span data-stu-id="f1490-183">c.</span></span> <span data-ttu-id="f1490-184">De hello **valor del atributo** lista, el valor del atributo seleccione Hola se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="f1490-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="f1490-185">d.</span><span class="sxs-lookup"><span data-stu-id="f1490-185">d.</span></span> <span data-ttu-id="f1490-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f1490-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="f1490-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f1490-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f1490-189">tooget SSO configurado para la aplicación, póngase en contacto con [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) de equipo y proporcionar el archivo de metadatos descargado Hola.</span><span class="sxs-lookup"><span data-stu-id="f1490-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="f1490-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f1490-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1490-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f1490-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1490-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1490-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1490-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1490-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1490-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f1490-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f1490-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f1490-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1490-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f1490-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1490-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1490-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1490-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f1490-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1490-205">a.</span><span class="sxs-lookup"><span data-stu-id="f1490-205">a.</span></span> <span data-ttu-id="f1490-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1490-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1490-207">b.</span><span class="sxs-lookup"><span data-stu-id="f1490-207">b.</span></span> <span data-ttu-id="f1490-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1490-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1490-209">c.</span><span class="sxs-lookup"><span data-stu-id="f1490-209">c.</span></span> <span data-ttu-id="f1490-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f1490-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1490-211">d.</span><span class="sxs-lookup"><span data-stu-id="f1490-211">d.</span></span> <span data-ttu-id="f1490-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f1490-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="f1490-213">Creación de un usuario de prueba de Pluralsight</span><span class="sxs-lookup"><span data-stu-id="f1490-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="f1490-214">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Pluralsight toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1490-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="f1490-215">Trabaje con [equipo de soporte técnico de Pluralsight cliente](mailto:support@pluralsight.com) a los usuarios de tooadd Hola Hola Pluralsight cuenta.</span><span class="sxs-lookup"><span data-stu-id="f1490-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1490-216">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1490-217">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPluralsight.</span><span class="sxs-lookup"><span data-stu-id="f1490-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f1490-219">**tooassign Britta Simon tooPluralsight, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f1490-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f1490-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f1490-222">En la lista de aplicaciones de hello, seleccione **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="f1490-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="f1490-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f1490-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f1490-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f1490-226">Click **Add** button.</span></span> <span data-ttu-id="f1490-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f1490-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f1490-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1490-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1490-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f1490-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1490-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f1490-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1490-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f1490-232">Testing single sign-on</span></span>

<span data-ttu-id="f1490-233">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f1490-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1490-234">Al hacer clic en icono de Pluralsight Hola Hola Panel de acceso, deberá obtener aplicaciones de Pluralsight tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="f1490-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="f1490-235">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1490-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1490-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f1490-236">Additional resources</span></span>

* [<span data-ttu-id="f1490-237">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1490-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1490-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1490-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

