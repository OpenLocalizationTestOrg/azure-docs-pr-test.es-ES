---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y un área de trabajo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="8ee59-103">Tutorial: integración de Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="8ee59-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="8ee59-104">En este tutorial, aprenderá cómo toointegrate al área de trabajo Facebook con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ee59-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ee59-105">Integración al área de trabajo Facebook con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8ee59-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ee59-106">Puede controlar en Azure AD que tenga acceso tooWorkplace Facebook</span><span class="sxs-lookup"><span data-stu-id="8ee59-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="8ee59-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkplace Facebook (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ee59-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee59-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ee59-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ee59-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ee59-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ee59-110">Prerequisites</span></span>

<span data-ttu-id="8ee59-111">integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8ee59-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="8ee59-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ee59-113">Una suscripción habilitada para inicio de sesión único de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="8ee59-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ee59-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8ee59-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ee59-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8ee59-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ee59-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8ee59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ee59-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ee59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ee59-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8ee59-118">Scenario description</span></span>
<span data-ttu-id="8ee59-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8ee59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ee59-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8ee59-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ee59-121">Agregar un área de trabajo Facebook desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="8ee59-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="8ee59-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="8ee59-123">Agregar un área de trabajo Facebook desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="8ee59-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="8ee59-124">integración de hello tooconfigure del área de trabajo Facebook en Azure AD, deberá tooadd al área de trabajo Facebook de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ee59-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ee59-125">**tooadd al área de trabajo Facebook desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8ee59-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ee59-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8ee59-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ee59-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ee59-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8ee59-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ee59-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8ee59-133">En el cuadro de búsqueda de hello, escriba **al área de trabajo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="8ee59-135">En el panel de resultados de hello, seleccione **al área de trabajo Facebook**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ee59-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ee59-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ee59-138">En esta sección podrá configurar y probar el inicio de sesión único de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8ee59-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ee59-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en lugar de trabajo Facebook es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ee59-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="8ee59-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en lugar de trabajo Facebook debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8ee59-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="8ee59-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en lugar de trabajo Facebook.</span><span class="sxs-lookup"><span data-stu-id="8ee59-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="8ee59-142">tooconfigure y prueba de inicio de sesión único en Azure AD con un área de trabajo Facebook, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8ee59-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ee59-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8ee59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ee59-144">**[Configurar la frecuencia de la reautenticación](#configuring-reauthentication-frequency) ** -tooconfigure tooprompt de área de trabajo para una comprobación SAML.</span><span class="sxs-lookup"><span data-stu-id="8ee59-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="8ee59-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ee59-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="8ee59-146">**[Crear un área de trabajo por usuario de prueba de Facebook](#creating-a-workplace-by-facebook-test-user) ** -toohave un equivalente de Britta Simon en lugar de trabajo Facebook que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8ee59-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="8ee59-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8ee59-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="8ee59-148">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8ee59-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ee59-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ee59-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el área de trabajo por la aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="8ee59-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="8ee59-151">**inicio de sesión único en tooconfigure Azure AD con un área de trabajo Facebook, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8ee59-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ee59-152">En el portal de Azure, en Hola Hola **al área de trabajo Facebook** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8ee59-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8ee59-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="8ee59-156">En hello **al área de trabajo por dominio de Facebook y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8ee59-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="8ee59-158">a.</span><span class="sxs-lookup"><span data-stu-id="8ee59-158">a.</span></span> <span data-ttu-id="8ee59-159">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="8ee59-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="8ee59-160">b.</span><span class="sxs-lookup"><span data-stu-id="8ee59-160">b.</span></span> <span data-ttu-id="8ee59-161">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="8ee59-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ee59-162">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="8ee59-162">These values are not hello real.</span></span> <span data-ttu-id="8ee59-163">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="8ee59-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8ee59-164">Póngase en contacto con [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="8ee59-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="8ee59-165">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8ee59-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="8ee59-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8ee59-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ee59-169">En hello **al área de trabajo por la configuración de Facebook** sección, haga clic en **al área de trabajo configurar Facebook** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8ee59-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8ee59-170">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8ee59-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="8ee59-172">En una ventana del explorador web diferente, tooyour de inicio de sesión al área de trabajo por sitio de la compañía de Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="8ee59-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="8ee59-173">Como parte del proceso de autenticación de SAML de hello, al área de trabajo puede usar las cadenas de consulta de seguridad too2.5 kilobytes de tamaño en orden toopass parámetros tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8ee59-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="8ee59-174">Hola **empresa panel**, vaya toohello **autenticación** ficha.</span><span class="sxs-lookup"><span data-stu-id="8ee59-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="8ee59-175">En **autenticación SAML**, seleccione **SSO sólo** desde la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee59-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="8ee59-176">Los valores de entrada Hola copiados desde **al área de trabajo por la configuración de Facebook** sección del portal de Azure en los campos correspondientes de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="8ee59-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="8ee59-177">En **dirección URL SAML** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee59-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="8ee59-178">En **cuadro de texto de dirección URL del emisor de SAML**, pegue el valor de Hola de **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee59-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="8ee59-179">En **redireccionamiento de cierre de sesión de SAML** (opcional), pegue el valor de Hola de **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee59-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="8ee59-180">Abra su **certificado codificado en base 64** en el Bloc de notas descargado del portal de Azure, copie el contenido de hello del mismo en el Portapapeles y péguelo toothe **certificado SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8ee59-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="8ee59-181">Puede que necesite tooenter Hola dirección URL de la audiencia, dirección URL del destinatario, y dirección URL de ACS (servicio de consumidor de aserción) aparece en hello **configuración de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="8ee59-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="8ee59-182">Desplácese toohello inferior de la sección de Hola y haga clic en hello **prueba SSO** botón.</span><span class="sxs-lookup"><span data-stu-id="8ee59-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="8ee59-183">Como resultado aparece una ventana emergente en la que se muestra la página de inicio de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ee59-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="8ee59-184">Escriba sus credenciales en como tooauthenticate normal.</span><span class="sxs-lookup"><span data-stu-id="8ee59-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="8ee59-185">**Solución de problemas:** dirección de correo electrónico de hello Asegúrese de que se devuelve desde Azure AD es Hola igual Hola cuenta de empresa que haya iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="8ee59-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="8ee59-186">Una vez que se ha completado correctamente la prueba de hello, desplácese toohello inferior de la página de Hola y haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="8ee59-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="8ee59-187">Ahora se presentará a todos los usuarios de Workplace la página de inicio de sesión de Azure AD para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="8ee59-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="8ee59-188">**Redirigir el cierre de sesión de SAML (opcional)** -</span><span class="sxs-lookup"><span data-stu-id="8ee59-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="8ee59-189">Puede elegir toooptionally configurar una dirección de Url de cierre de sesión de SAML, que puede ser toopoint utilizado en la página de cierre de sesión de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ee59-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="8ee59-190">Cuando esta opción está habilitada y configurada, usuario de hello ya no será la página de cierre de sesión de toohello dirigida al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8ee59-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="8ee59-191">En su lugar, el usuario de hello será redirigido toohello url que se agregó en la configuración de redireccionamiento de cierre de sesión de SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee59-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="8ee59-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8ee59-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ee59-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee59-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ee59-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ee59-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="8ee59-195">Configuración de la frecuencia de reautenticación</span><span class="sxs-lookup"><span data-stu-id="8ee59-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="8ee59-196">Puede configurar tooprompt al área de trabajo para una comprobación SAML cada día, tres días, semanas, dos semanas, mes o nunca.</span><span class="sxs-lookup"><span data-stu-id="8ee59-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="8ee59-197">Hello valor mínimo para la comprobación SAML de hello en aplicaciones móviles se establece tooone semana.</span><span class="sxs-lookup"><span data-stu-id="8ee59-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="8ee59-198">También puede forzar un SAML restablecer para todos los usuarios con el botón de hello: autenticación de SAML requiere para todos los usuarios ahora.</span><span class="sxs-lookup"><span data-stu-id="8ee59-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ee59-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ee59-200">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ee59-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8ee59-202">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8ee59-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ee59-203">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8ee59-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ee59-205">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ee59-207">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee59-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ee59-209">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8ee59-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ee59-211">a.</span><span class="sxs-lookup"><span data-stu-id="8ee59-211">a.</span></span> <span data-ttu-id="8ee59-212">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ee59-213">b.</span><span class="sxs-lookup"><span data-stu-id="8ee59-213">b.</span></span> <span data-ttu-id="8ee59-214">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ee59-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ee59-215">c.</span><span class="sxs-lookup"><span data-stu-id="8ee59-215">c.</span></span> <span data-ttu-id="8ee59-216">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ee59-217">d.</span><span class="sxs-lookup"><span data-stu-id="8ee59-217">d.</span></span> <span data-ttu-id="8ee59-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="8ee59-219">Creación de un usuario de prueba de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="8ee59-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="8ee59-220">En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="8ee59-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="8ee59-221">Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8ee59-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8ee59-222">El usuario no tiene que hacer nada en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8ee59-222">There is no action for you in this section.</span></span> <span data-ttu-id="8ee59-223">Si un usuario no existe en el área de trabajo Facebook, una nueva se crea cuando intente tooaccess al área de trabajo Facebook.</span><span class="sxs-lookup"><span data-stu-id="8ee59-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="8ee59-224">Si necesita toocreate manualmente, póngase en contacto con en un usuario [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="8ee59-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ee59-225">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ee59-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ee59-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="8ee59-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8ee59-228">**tooassign tooWorkplace Britta Simon Facebook, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8ee59-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ee59-229">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8ee59-231">En la lista de aplicaciones de hello, seleccione **al área de trabajo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="8ee59-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8ee59-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-235">Click **Add** button.</span></span> <span data-ttu-id="8ee59-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8ee59-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee59-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ee59-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ee59-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8ee59-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ee59-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8ee59-241">Testing single sign-on</span></span>

<span data-ttu-id="8ee59-242">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8ee59-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="8ee59-243">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ee59-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8ee59-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8ee59-244">Additional resources</span></span>

* [<span data-ttu-id="8ee59-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ee59-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ee59-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ee59-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8ee59-247">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="8ee59-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

