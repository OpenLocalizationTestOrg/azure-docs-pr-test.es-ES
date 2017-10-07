---
title: "Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y un área de trabajo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="3c20e-103">Tutorial: integración de Azure Active Directory con Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="3c20e-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="3c20e-104">En este tutorial, aprenderá cómo toointegrate al área de trabajo Facebook con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3c20e-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c20e-105">Integración al área de trabajo Facebook con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3c20e-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3c20e-106">Puede controlar en Azure AD que tenga acceso tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="3c20e-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="3c20e-107">Puede permitir a los usuarios tooautomatically obtener firmado en tooWorkplace Facebook (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c20e-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3c20e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c20e-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="3c20e-109">Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c20e-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c20e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3c20e-110">Prerequisites</span></span>

<span data-ttu-id="3c20e-111">integración de Azure AD con un área de trabajo Facebook tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3c20e-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="3c20e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c20e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c20e-113">Una suscripción habilitada para inicio de sesión único (SSO) de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="3c20e-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="3c20e-114">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3c20e-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="3c20e-115">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3c20e-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c20e-116">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c20e-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c20e-117">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3c20e-117">Scenario description</span></span>
<span data-ttu-id="3c20e-118">En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3c20e-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="3c20e-119">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3c20e-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c20e-120">Agregar un área de trabajo Facebook de hello Galería.</span><span class="sxs-lookup"><span data-stu-id="3c20e-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="3c20e-121">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c20e-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="3c20e-122">Agregar un área de trabajo Facebook de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3c20e-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="3c20e-123">integración de hello tooconfigure del área de trabajo Facebook en Azure AD, agregue al área de trabajo Facebook de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3c20e-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="3c20e-124">Hola [portal de Azure](https://portal.azure.com), en el panel izquierdo de Hola, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="3c20e-126">Examinar demasiado**aplicaciones empresariales** > **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="3c20e-128">tooadd Hola nueva aplicación, seleccione **nueva aplicación** en la parte superior de Hola Hola del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c20e-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="3c20e-130">En el cuadro de búsqueda de hello, escriba **al área de trabajo Facebook**y seleccione **al área de trabajo Facebook** de resultados.</span><span class="sxs-lookup"><span data-stu-id="3c20e-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="3c20e-131">A continuación, seleccione **agregar**, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3c20e-131">Then select **Add**, tooadd hello application.</span></span>

    ![Área de trabajo Facebook en la lista de resultados de Hola](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3c20e-133">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c20e-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3c20e-134">En esta sección podrá configurar y probar el SSO de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3c20e-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3c20e-135">Para toowork SSO, Azure AD necesita tooknow qué usuario equivalente de hello en lugar de trabajo Facebook es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c20e-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="3c20e-136">En otras palabras, se debe establecer una relación entre un usuario de Azure AD y el usuario relacionado de hello en lugar de trabajo Facebook vinculada.</span><span class="sxs-lookup"><span data-stu-id="3c20e-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="3c20e-137">Establecer esta relación mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en lugar de trabajo Facebook.</span><span class="sxs-lookup"><span data-stu-id="3c20e-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3c20e-138">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c20e-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3c20e-139">En esta sección, se habilita el SSO de Azure AD en hello portal de Azure y configurar SSO en el área de trabajo por la aplicación de Facebook.</span><span class="sxs-lookup"><span data-stu-id="3c20e-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="3c20e-140">En el portal de Azure, en Hola Hola **al área de trabajo Facebook** página de integración de aplicaciones, seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="3c20e-142">Hola **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="3c20e-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="3c20e-144">Hola **al área de trabajo por dominio de Facebook y las direcciones URL** sección, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c20e-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="3c20e-145">a.</span><span class="sxs-lookup"><span data-stu-id="3c20e-145">a.</span></span> <span data-ttu-id="3c20e-146">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL que utiliza Hola siguiente patrón:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="3c20e-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="3c20e-147">b.</span><span class="sxs-lookup"><span data-stu-id="3c20e-147">b.</span></span> <span data-ttu-id="3c20e-148">Hola **identificador** cuadro de texto, escriba una dirección URL que utiliza Hola siguiente patrón:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="3c20e-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="3c20e-149">Estos valores son solo un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3c20e-149">These values are an example only.</span></span> <span data-ttu-id="3c20e-150">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="3c20e-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="3c20e-151">Póngase en contacto con hello [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="3c20e-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="3c20e-152">Hola **el certificado de firma de SAML** sección, seleccione **certificado (Base64)**y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3c20e-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="3c20e-154">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-154">Select **Save**.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3c20e-156">Hola **al área de trabajo por la configuración de Facebook** sección, seleccione **al área de trabajo configurar Facebook** tooopen hello **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3c20e-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="3c20e-157">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **referencia rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="3c20e-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configuración de Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="3c20e-159">En una ventana del explorador web diferente, inicie sesión en tooyour al área de trabajo por sitio de la compañía de Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="3c20e-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="3c20e-160">Como parte del proceso de autenticación de SAML de hello, al área de trabajo puede utilizar cadenas de consulta de seguridad too2.5 kilobytes de tamaño en orden toopass parámetros tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="3c20e-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="3c20e-161">Hola **empresa panel**, vaya toohello **autenticación** ficha.</span><span class="sxs-lookup"><span data-stu-id="3c20e-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="3c20e-162">En **autenticación SAML**, seleccione **SSO sólo** desde la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c20e-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="3c20e-163">Escriba los valores de hello copiados de hello **al área de trabajo por la configuración de Facebook** sección del portal de Azure en los campos correspondientes de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="3c20e-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="3c20e-164">En el **dirección URL SAML** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único**, que haya copiado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c20e-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="3c20e-165">En el **dirección URL del emisor de SAML** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c20e-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="3c20e-166">En **SAML Logout redirigir (opcional)**, pegue el valor de Hola de **dirección URL de cierre de sesión**, que haya copiado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c20e-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="3c20e-167">Abra su **certificado codificado en base 64** en el Bloc de notas, descarga desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c20e-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="3c20e-168">Copie el contenido de hello del mismo en el Portapapeles y, a continuación, péguelo toothe **certificado SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3c20e-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="3c20e-169">Es posible que tenga la audiencia de hello tooenter dirección URL, dirección URL de destinatario y ACS (servicio de consumidor de aserción) URL, aparecen en hello **configuración de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="3c20e-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="3c20e-170">Desplácese toohello inferior de la sección de Hola y seleccione **prueba SSO**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="3c20e-171">Aparece una ventana emergente, página de inicio de sesión de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c20e-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="3c20e-172">tooauthenticate, escriba sus credenciales de forma habitual.</span><span class="sxs-lookup"><span data-stu-id="3c20e-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="3c20e-173">Asegúrese de dirección de correo electrónico de hello devuelto desde Azure AD es Hola igual Hola cuenta de empresa que haya iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="3c20e-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="3c20e-174">Si prueba Hola ha finalizado correctamente, desplazar toohello inferior de la página de Hola y seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="3c20e-175">A todo el que use Workplace se le presentará la página de inicio de sesión de Azure AD para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="3c20e-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="3c20e-176">Puede elegir tooconfigure un cierre de sesión SAML dirección URL, que puede ser toopoint utilizado en la página de cierre de sesión de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c20e-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="3c20e-177">Cuando esta opción está habilitada y configurada, el usuario de Hola ya no es página de cierre de sesión de toohello dirigida al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3c20e-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="3c20e-178">En su lugar, usuario de hello es dirección URL redirigida toohello que se agregó en la configuración de redireccionamiento de cierre de sesión de SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c20e-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="3c20e-179">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3c20e-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="3c20e-180">Después de agregar esta aplicación de hello **Active Directory** > **aplicaciones empresariales** sección, simplemente seleccione hello **Single Sign-On** hello de acceso y de pestaña incrusta documentación a través de hello **configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3c20e-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3c20e-181">Puede leer más acerca de la característica de documentación de embedded Hola Hola [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3c20e-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="3c20e-182">Configuración de la frecuencia de reautenticación</span><span class="sxs-lookup"><span data-stu-id="3c20e-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="3c20e-183">Puede configurar tooprompt al área de trabajo para una comprobación SAML cada día, tres días, una semana, dos semanas, un mes o nunca.</span><span class="sxs-lookup"><span data-stu-id="3c20e-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="3c20e-184">Hello valor mínimo para la comprobación SAML de hello en aplicaciones móviles se establece tooone semana.</span><span class="sxs-lookup"><span data-stu-id="3c20e-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="3c20e-185">También puede forzar un restablecimiento de SAML para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3c20e-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="3c20e-186">toodo, Hola uso **la autenticación de SAML requiere para todos los usuarios ahora** botón.</span><span class="sxs-lookup"><span data-stu-id="3c20e-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3c20e-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c20e-187">Create an Azure AD test user</span></span>
<span data-ttu-id="3c20e-188">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c20e-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

1. <span data-ttu-id="3c20e-190">Hola **portal de Azure**, en el panel izquierdo de Hola, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c20e-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y seleccione **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c20e-194">Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c20e-196">Hola **usuario** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c20e-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c20e-198">a.</span><span class="sxs-lookup"><span data-stu-id="3c20e-198">a.</span></span> <span data-ttu-id="3c20e-199">Hola **nombre** cuadro de texto, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c20e-200">b.</span><span class="sxs-lookup"><span data-stu-id="3c20e-200">b.</span></span> <span data-ttu-id="3c20e-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3c20e-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c20e-202">c.</span><span class="sxs-lookup"><span data-stu-id="3c20e-202">c.</span></span> <span data-ttu-id="3c20e-203">Seleccione **Mostrar contraseña** y anótela.</span><span class="sxs-lookup"><span data-stu-id="3c20e-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="3c20e-204">d.</span><span class="sxs-lookup"><span data-stu-id="3c20e-204">d.</span></span> <span data-ttu-id="3c20e-205">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="3c20e-206">Creación de un usuario de prueba de Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="3c20e-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="3c20e-207">En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="3c20e-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="3c20e-208">Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3c20e-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="3c20e-209">El usuario no tiene que hacer nada en esta sección.</span><span class="sxs-lookup"><span data-stu-id="3c20e-209">There is no action for you in this section.</span></span> <span data-ttu-id="3c20e-210">Si un usuario no existe en el área de trabajo Facebook, una nueva se crea cuando intente tooaccess al área de trabajo Facebook.</span><span class="sxs-lookup"><span data-stu-id="3c20e-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="3c20e-211">Si necesita un usuario toocreate manualmente, póngase en contacto con hello [al área de trabajo al equipo de soporte técnico de cliente de Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="3c20e-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3c20e-212">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c20e-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3c20e-213">En esta sección, se habilita Britta Simon toouse Azure SSO concediendo acceso tooWorkplace Facebook.</span><span class="sxs-lookup"><span data-stu-id="3c20e-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Asignar usuario][200] 

1. <span data-ttu-id="3c20e-215">Hola Azure ver aplicaciones de portal, abra Hola.</span><span class="sxs-lookup"><span data-stu-id="3c20e-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="3c20e-216">Ir a vista del directorio toohello, vaya demasiado**aplicaciones empresariales**y, a continuación, seleccione **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3c20e-218">En la lista de aplicaciones de hello, seleccione **al área de trabajo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Hola al área de trabajo por el vínculo de Facebook en la lista de aplicaciones de Hola](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="3c20e-220">En el menú de Hola Hola izquierda, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="3c20e-222">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-222">Select **Add**.</span></span> <span data-ttu-id="3c20e-223">A continuación, en hello **Agregar asignación** panel, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="3c20e-225">Hola **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c20e-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="3c20e-226">Hola **usuarios y grupos** cuadro de diálogo, seleccione **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="3c20e-227">Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.</span><span class="sxs-lookup"><span data-stu-id="3c20e-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3c20e-228">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="3c20e-228">Test single sign-on</span></span>

<span data-ttu-id="3c20e-229">Si desea tootest la configuración de SSO, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3c20e-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="3c20e-230">Para obtener más información, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c20e-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3c20e-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c20e-231">Next steps</span></span>

* <span data-ttu-id="3c20e-232">Vea hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="3c20e-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="3c20e-233">Consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c20e-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="3c20e-234">Más información acerca de cómo demasiado[configurar aprovisionamiento de usuario](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3c20e-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

