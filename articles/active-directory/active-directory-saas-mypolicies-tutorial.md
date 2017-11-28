---
title: "Tutorial: Integración de Azure Active Directory con myPolicies | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="dcdf6-103">Tutorial: Integración de Azure Active Directory con myPolicies</span><span class="sxs-lookup"><span data-stu-id="dcdf6-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="dcdf6-104">En este tutorial, aprenderá cómo toointegrate myPolicies con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dcdf6-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dcdf6-105">Integración myPolicies con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dcdf6-106">Puede controlar en Azure AD que tenga acceso toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="dcdf6-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="dcdf6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión toomyPolicies (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dcdf6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="dcdf6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dcdf6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dcdf6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcdf6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dcdf6-110">Prerequisites</span></span>

<span data-ttu-id="dcdf6-111">integración de Azure AD con myPolicies tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="dcdf6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dcdf6-113">Una suscripción habilitada para el inicio de sesión único en myPolicies</span><span class="sxs-lookup"><span data-stu-id="dcdf6-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dcdf6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dcdf6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dcdf6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dcdf6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dcdf6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dcdf6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="dcdf6-118">Scenario description</span></span>
<span data-ttu-id="dcdf6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dcdf6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dcdf6-121">Agregar myPolicies desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="dcdf6-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="dcdf6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="dcdf6-123">Agregar myPolicies desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="dcdf6-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="dcdf6-124">integración de hello tooconfigure de myPolicies en Azure AD, deberá tooadd myPolicies de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dcdf6-125">**tooadd myPolicies de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dcdf6-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcdf6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dcdf6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dcdf6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="dcdf6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="dcdf6-133">En el cuadro de búsqueda de hello, escriba **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-133">In hello search box, type **myPolicies**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="dcdf6-135">En el panel de resultados de hello, seleccione **myPolicies**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dcdf6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dcdf6-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con myPolicies con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dcdf6-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dcdf6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en myPolicies es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="dcdf6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en myPolicies debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="dcdf6-141">En myPolicies, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dcdf6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con myPolicies, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dcdf6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dcdf6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dcdf6-145">**[Crear un usuario de prueba myPolicies](#creating-a-mypolicies-test-user)**  -toohave un equivalente de Britta Simon en myPolicies que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dcdf6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dcdf6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dcdf6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dcdf6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación myPolicies.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="dcdf6-150">**inicio de sesión único en Azure AD tooconfigure con myPolicies, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dcdf6-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcdf6-151">En el portal de Azure, en Hola Hola **myPolicies** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="dcdf6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="dcdf6-155">En hello **myPolicies dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="dcdf6-157">a.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-157">a.</span></span> <span data-ttu-id="dcdf6-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="dcdf6-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="dcdf6-159">b.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-159">b.</span></span> <span data-ttu-id="dcdf6-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="dcdf6-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dcdf6-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-161">These values are not real.</span></span> <span data-ttu-id="dcdf6-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="dcdf6-163">Póngase en contacto con [equipo de soporte técnico myPolicies](mailto:support@mypolicies.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="dcdf6-164">aplicación de Hello myPolicies espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="dcdf6-165">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="dcdf6-166">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="dcdf6-167">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="dcdf6-169">Haga clic en **ver y editar todos los demás atributos de usuario** checkbox en hello **atributos de usuario** sección atributos de hello tooexpand.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="dcdf6-170">Realizar Hola siguiendo los pasos en cada uno de los atributos de muestra de Hola-</span><span class="sxs-lookup"><span data-stu-id="dcdf6-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="dcdf6-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="dcdf6-171">Attribute Name</span></span> | <span data-ttu-id="dcdf6-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="dcdf6-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="dcdf6-173">givenname</span><span class="sxs-lookup"><span data-stu-id="dcdf6-173">givenname</span></span> | <span data-ttu-id="dcdf6-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="dcdf6-174">user.givenname</span></span> |
    | <span data-ttu-id="dcdf6-175">surname</span><span class="sxs-lookup"><span data-stu-id="dcdf6-175">surname</span></span> | <span data-ttu-id="dcdf6-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="dcdf6-176">user.surname</span></span> |
    | <span data-ttu-id="dcdf6-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="dcdf6-177">emailaddress</span></span> | <span data-ttu-id="dcdf6-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="dcdf6-178">user.mail</span></span> |
    | <span data-ttu-id="dcdf6-179">name</span><span class="sxs-lookup"><span data-stu-id="dcdf6-179">name</span></span> | <span data-ttu-id="dcdf6-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="dcdf6-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="dcdf6-181">a.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-181">a.</span></span> <span data-ttu-id="dcdf6-182">Haga clic en Hola de hello atributo tooopen **Editar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="dcdf6-184">b.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-184">b.</span></span> <span data-ttu-id="dcdf6-185">Eliminar el valor de dirección URL de Hola de hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="dcdf6-186">c.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-186">c.</span></span> <span data-ttu-id="dcdf6-187">Haga clic en **Aceptar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="dcdf6-188">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="dcdf6-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="dcdf6-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="dcdf6-192">En hello **myPolicies configuración** sección, haga clic en **configurar myPolicies** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dcdf6-193">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="dcdf6-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="dcdf6-195">inicio de sesión único en tooconfigure en **myPolicies** lado, necesita hello toosend descargado **Certificate(Base64)** y **SAML Single Sign-On dirección URL del servicio** demasiado[equipo de soporte técnico myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="dcdf6-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="dcdf6-196">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="dcdf6-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dcdf6-197">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dcdf6-198">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dcdf6-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dcdf6-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="dcdf6-200">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="dcdf6-202">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dcdf6-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcdf6-203">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dcdf6-205">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dcdf6-207">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dcdf6-209">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="dcdf6-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dcdf6-211">a.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-211">a.</span></span> <span data-ttu-id="dcdf6-212">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dcdf6-213">b.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-213">b.</span></span> <span data-ttu-id="dcdf6-214">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dcdf6-215">c.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-215">c.</span></span> <span data-ttu-id="dcdf6-216">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dcdf6-217">d.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-217">d.</span></span> <span data-ttu-id="dcdf6-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="dcdf6-219">Creación de un usuario de prueba de myPolicies</span><span class="sxs-lookup"><span data-stu-id="dcdf6-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="dcdf6-220">En esta sección, se crea un usuario denominado Britta Simon en myPolicies.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="dcdf6-221">Trabajar con [equipo de soporte técnico myPolicies](mailto:support@mypolicies.com) para agregar usuarios de hello en la plataforma de myPolicies Hola.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="dcdf6-222">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dcdf6-223">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcdf6-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dcdf6-224">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso toomyPolicies.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="dcdf6-226">**tooassign Britta Simon toomyPolicies, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="dcdf6-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcdf6-227">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="dcdf6-229">En la lista de aplicaciones de hello, seleccione **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-229">In hello applications list, select **myPolicies**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="dcdf6-231">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="dcdf6-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-233">Click **Add** button.</span></span> <span data-ttu-id="dcdf6-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="dcdf6-236">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dcdf6-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dcdf6-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dcdf6-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="dcdf6-239">Testing single sign-on</span></span>

<span data-ttu-id="dcdf6-240">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dcdf6-241">Al hacer clic en hello myPolicies el icono Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour myPolicies aplicación.</span><span class="sxs-lookup"><span data-stu-id="dcdf6-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="dcdf6-242">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dcdf6-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dcdf6-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="dcdf6-243">Additional resources</span></span>

* [<span data-ttu-id="dcdf6-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcdf6-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dcdf6-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dcdf6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

