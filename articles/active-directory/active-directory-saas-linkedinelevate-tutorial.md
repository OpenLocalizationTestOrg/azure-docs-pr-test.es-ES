---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Elevate | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y elevar LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="a13a0-103">Tutorial: Integración de Azure Active Directory con LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="a13a0-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="a13a0-104">En este tutorial, aprenderá cómo elevar los toointegrate LinkedIn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a13a0-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a13a0-105">Integración elevar LinkedIn con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a13a0-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a13a0-106">Puede controlar en Azure AD que tenga acceso tooLinkedIn elevar</span><span class="sxs-lookup"><span data-stu-id="a13a0-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="a13a0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLinkedIn elevar (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a13a0-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="a13a0-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="a13a0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a13a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a13a0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a13a0-110">Prerequisites</span></span>

<span data-ttu-id="a13a0-111">tooconfigure integración de Azure AD con elevar LinkedIn, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a13a0-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="a13a0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a13a0-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="a13a0-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a13a0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a13a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a13a0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a13a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a13a0-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a13a0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a13a0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a13a0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a13a0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a13a0-118">Scenario description</span></span>
<span data-ttu-id="a13a0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a13a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a13a0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a13a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a13a0-121">Agregar LinkedIn elevar desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a13a0-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="a13a0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="a13a0-123">Agregar LinkedIn elevar desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a13a0-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="a13a0-124">integración de hello tooconfigure de LinkedIn elevar en Azure AD, deberá tooadd LinkedIn elevar de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a13a0-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a13a0-125">**tooadd LinkedIn elevar el nivel de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a13a0-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a13a0-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a13a0-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a13a0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a13a0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a13a0-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a13a0-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a13a0-133">En el cuadro de búsqueda de hello, escriba **LinkedIn elevar**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="a13a0-134">En el panel de resultados, haga clic en **LinkedIn elevar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a13a0-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a13a0-136">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a13a0-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Elevate utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a13a0-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a13a0-138">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en elevar LinkedIn es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a13a0-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="a13a0-139">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LinkedIn elevar debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="a13a0-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="a13a0-140">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en LinkedIn elevar sus privilegios.</span><span class="sxs-lookup"><span data-stu-id="a13a0-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="a13a0-141">tooconfigure y prueba de inicio de sesión único en Azure AD con elevar LinkedIn, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a13a0-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a13a0-142">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="a13a0-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a13a0-143">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a13a0-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a13a0-144">**[Crear un usuario de prueba LinkedIn elevar](#creating-a-linkedin-elevate-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a13a0-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="a13a0-145">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a13a0-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a13a0-146">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a13a0-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a13a0-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a13a0-148">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación LinkedIn elevar sus privilegios.</span><span class="sxs-lookup"><span data-stu-id="a13a0-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="a13a0-149">**inicio de sesión único en tooconfigure Azure AD con elevar LinkedIn, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a13a0-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="a13a0-150">En el portal de administración de Azure de hello, en hello **LinkedIn elevar** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a13a0-152">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a13a0-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="a13a0-154">En una ventana del explorador web diferente, inicio de sesión tooyour LinkedIn elevar inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="a13a0-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="a13a0-155">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="a13a0-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="a13a0-156">Además, seleccione **elevar - elevar prueba de AAD** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="a13a0-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="a13a0-158">Haga clic en **o haga clic aquí tooload y copie los campos individuales de formulario de hello** y copie **Id. de entidad** y **dirección Url de acceso de consumidor de aserción (ACS)**</span><span class="sxs-lookup"><span data-stu-id="a13a0-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="a13a0-160">En el Portal de Azure, en **LinkedIn elevar dominio y las direcciones URL**, realizar Hola siguientes pasos si desea tooconfigure SSO en **iniciado por IdP** modo</span><span class="sxs-lookup"><span data-stu-id="a13a0-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="a13a0-162">a.</span><span class="sxs-lookup"><span data-stu-id="a13a0-162">a.</span></span> <span data-ttu-id="a13a0-163">Hola **identificador** cuadro de texto, escriba Hola **Id. de entidad** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="a13a0-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="a13a0-164">b.</span><span class="sxs-lookup"><span data-stu-id="a13a0-164">b.</span></span> <span data-ttu-id="a13a0-165">Hola **dirección URL de respuesta** cuadro de texto, escriba Hola **dirección Url de acceso de consumidor de aserción (ACS)** copiados desde el LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="a13a0-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="a13a0-166">Si desea que tooconfigure SSO en **iniciado en SP**, a continuación, haga clic en la opción Mostrar URL avanzada en la sección de configuración de Hola y configurar inicio de sesión de hello en dirección URL con hello siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="a13a0-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="a13a0-168">La aplicación LinkedIn elevar espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="a13a0-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="a13a0-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="a13a0-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="a13a0-170">Hola valor predeterminado de **identificador de usuario** es **user.userprincipalname** pero LinkedIn elevar espera este toobe asignado con la dirección de correo electrónico del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a13a0-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="a13a0-171">Para que puede usar **user.mail** de atributo de la lista de Hola o usar el valor de atributo apropiado de hello según la configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="a13a0-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="a13a0-173">En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a13a0-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="a13a0-174">Necesita tooadd otra notificación denominado **departamento** y valor de hello debe toobe asignado demasiado**user.department**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="a13a0-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="a13a0-175">Attribute Name</span></span> | <span data-ttu-id="a13a0-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="a13a0-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="a13a0-177">department</span><span class="sxs-lookup"><span data-stu-id="a13a0-177">department</span></span>| <span data-ttu-id="a13a0-178">user.department</span><span class="sxs-lookup"><span data-stu-id="a13a0-178">user.department</span></span> |

      ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="a13a0-180">a.</span><span class="sxs-lookup"><span data-stu-id="a13a0-180">a.</span></span> <span data-ttu-id="a13a0-181">Haga clic en la página de detalles de atributo de Agregar atributo tooopen Hola Agregar atributo de departamento Hola tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a13a0-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="a13a0-183">b.</span><span class="sxs-lookup"><span data-stu-id="a13a0-183">b.</span></span> <span data-ttu-id="a13a0-184">Haga clic en **Aceptar** atributo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="a13a0-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="a13a0-185">c.</span><span class="sxs-lookup"><span data-stu-id="a13a0-185">c.</span></span> <span data-ttu-id="a13a0-186">Cambiar el nombre del atributo de Hola Hola **emailaddress** demasiado**correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="a13a0-187">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a13a0-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="a13a0-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-189">Click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="a13a0-191">Vaya demasiado**configuración de administración de LinkedIn** sección.</span><span class="sxs-lookup"><span data-stu-id="a13a0-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="a13a0-192">Cargar archivo XML de Hola que acaba de descargar de hello portal de Azure haciendo clic en hello opción de archivo de cargar XML.</span><span class="sxs-lookup"><span data-stu-id="a13a0-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="a13a0-194">Haga clic en **en** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="a13a0-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="a13a0-195">Estado SSO cambiará de **no conectado** demasiado**conectado**</span><span class="sxs-lookup"><span data-stu-id="a13a0-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a13a0-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="a13a0-198">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="a13a0-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a13a0-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a13a0-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a13a0-201">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="a13a0-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a13a0-203">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a13a0-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a13a0-205">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a13a0-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a13a0-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="a13a0-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a13a0-209">a.</span><span class="sxs-lookup"><span data-stu-id="a13a0-209">a.</span></span> <span data-ttu-id="a13a0-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a13a0-211">b.</span><span class="sxs-lookup"><span data-stu-id="a13a0-211">b.</span></span> <span data-ttu-id="a13a0-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a13a0-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a13a0-213">c.</span><span class="sxs-lookup"><span data-stu-id="a13a0-213">c.</span></span> <span data-ttu-id="a13a0-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a13a0-215">d.</span><span class="sxs-lookup"><span data-stu-id="a13a0-215">d.</span></span> <span data-ttu-id="a13a0-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="a13a0-217">Creación de un usuario de prueba de LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="a13a0-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="a13a0-218">Aplicación de elevar vinculado admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a13a0-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="a13a0-219">Página de configuración de administración de hello en el conmutador de hello LinkedIn elevar Hola voltear portal **asignar automáticamente licencias** tooactive tooenable sólo en tiempo de aprovisionamiento y esto también asignarán a un usuario de toohello licencia.</span><span class="sxs-lookup"><span data-stu-id="a13a0-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a13a0-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a13a0-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a13a0-222">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooLinkedIn acceso elevar.</span><span class="sxs-lookup"><span data-stu-id="a13a0-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a13a0-224">**tooassign Britta Simon tooLinkedIn elevar, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="a13a0-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="a13a0-225">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a13a0-227">En la lista de aplicaciones de hello, seleccione **LinkedIn elevar**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="a13a0-229">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a13a0-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-231">Click **Add** button.</span></span> <span data-ttu-id="a13a0-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a13a0-234">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="a13a0-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a13a0-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a13a0-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a13a0-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a13a0-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a13a0-237">Testing single sign-on</span></span>

<span data-ttu-id="a13a0-238">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a13a0-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a13a0-239">Al hacer clic en icono de LinkedIn elevar Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión Azure hello y en después de la sesión correctamente, deberá obtener en la aplicación LinkedIn elevar sus privilegios.</span><span class="sxs-lookup"><span data-stu-id="a13a0-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a13a0-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a13a0-240">Additional resources</span></span>

* [<span data-ttu-id="a13a0-241">Tutorial: configuración de LinkedIn Elevate para el aprovisionamiento automático de usuarios con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a13a0-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="a13a0-242">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a13a0-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a13a0-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a13a0-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
