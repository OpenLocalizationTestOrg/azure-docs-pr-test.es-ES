---
title: "Tutorial: Integración de Azure Active Directory con ServiceChannel | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="399cb-103">Tutorial: Integración de Azure Active Directory con ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="399cb-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="399cb-104">En este tutorial, aprenderá cómo toointegrate ServiceChannel con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="399cb-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="399cb-105">Integración de ServiceChannel con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="399cb-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="399cb-106">Puede controlar en Azure AD que tenga acceso tooServiceChannel</span><span class="sxs-lookup"><span data-stu-id="399cb-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="399cb-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooServiceChannel (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="399cb-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="399cb-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="399cb-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="399cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="399cb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="399cb-110">Prerequisites</span></span>

<span data-ttu-id="399cb-111">integración de Azure AD con ServiceChannel tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="399cb-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="399cb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="399cb-113">Una suscripción habilitada para inicio de sesión único en ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="399cb-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="399cb-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="399cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="399cb-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="399cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="399cb-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="399cb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="399cb-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="399cb-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="399cb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="399cb-118">Scenario description</span></span>
<span data-ttu-id="399cb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="399cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="399cb-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="399cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="399cb-121">Agregar ServiceChannel desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="399cb-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="399cb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="399cb-123">Agregar ServiceChannel desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="399cb-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="399cb-124">integración de hello tooconfigure de ServiceChannel en Azure AD, deberá tooadd ServiceChannel de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="399cb-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="399cb-125">**tooadd ServiceChannel de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="399cb-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="399cb-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="399cb-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="399cb-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="399cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="399cb-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="399cb-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="399cb-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="399cb-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="399cb-133">En el cuadro de búsqueda de hello, escriba **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="399cb-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="399cb-135">En el panel de resultados de hello, seleccione **ServiceChannel**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="399cb-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="399cb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="399cb-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con ServiceChannel con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="399cb-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="399cb-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ServiceChannel es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="399cb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="399cb-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ServiceChannel debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="399cb-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="399cb-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="399cb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="399cb-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ServiceChannel, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="399cb-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="399cb-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="399cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="399cb-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="399cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="399cb-145">**[Crear un usuario de prueba de ServiceChannel](#creating-a-servicechannel-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="399cb-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="399cb-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="399cb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="399cb-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="399cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="399cb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="399cb-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="399cb-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="399cb-150">**inicio de sesión único en Azure AD tooconfigure con ServiceChannel, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="399cb-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="399cb-151">En el portal de administración de Azure de hello, en hello **ServiceChannel** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="399cb-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="399cb-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="399cb-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="399cb-155">En hello **ServiceChannel dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="399cb-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="399cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="399cb-157">a.</span></span> <span data-ttu-id="399cb-158">Hola **identificador** cuadro de texto, valor de tipo hello como:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="399cb-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="399cb-159">b.</span><span class="sxs-lookup"><span data-stu-id="399cb-159">b.</span></span> <span data-ttu-id="399cb-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="399cb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="399cb-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="399cb-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="399cb-162">Tener tooupdate estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="399cb-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="399cb-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="399cb-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="399cb-164">Póngase en contacto con [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="399cb-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="399cb-165">La aplicación de ServiceChannel espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="399cb-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="399cb-166">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="399cb-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="399cb-167">**NameIdentifier (identificador de usuario)** es Hola solo notificación obligatoria y es el valor predeterminado de hello **user.userprincipalname** pero ServiceChannel espera este toobe asignado con **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="399cb-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="399cb-168">Si tiene previsto aprovisionamiento de usuarios solo en tiempo de tooenable, debe agregar Hola después notificaciones tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="399cb-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="399cb-169">**Rol** notificación necesita toobe asignado demasiado**user.assignedroles** que contiene la función de saludo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="399cb-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="399cb-170">Puede consultar la guía de ServiceChannel [aquí](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) para obtener más información sobre las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="399cb-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="399cb-172">Haga clic en [aquí](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow cómo tooconfigure **rol** en Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="399cb-173">En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="399cb-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="399cb-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="399cb-174">Attribute Name</span></span> | <span data-ttu-id="399cb-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="399cb-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="399cb-176">Rol</span><span class="sxs-lookup"><span data-stu-id="399cb-176">Role</span></span>| <span data-ttu-id="399cb-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="399cb-177">user.assignedroles</span></span> |

    <span data-ttu-id="399cb-178">a.</span><span class="sxs-lookup"><span data-stu-id="399cb-178">a.</span></span> <span data-ttu-id="399cb-179">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="399cb-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="399cb-182">b.</span><span class="sxs-lookup"><span data-stu-id="399cb-182">b.</span></span> <span data-ttu-id="399cb-183">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="399cb-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="399cb-184">c.</span><span class="sxs-lookup"><span data-stu-id="399cb-184">c.</span></span> <span data-ttu-id="399cb-185">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="399cb-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="399cb-186">d.</span><span class="sxs-lookup"><span data-stu-id="399cb-186">d.</span></span> <span data-ttu-id="399cb-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="399cb-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="399cb-188">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="399cb-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="399cb-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="399cb-190">Click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="399cb-192">En hello **configuración de ServiceChannel** sección, haga clic en **configurar ServiceChannel** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="399cb-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="399cb-193">Tenga en cuenta que hello **SAML Entity ID** de hello **referencia rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="399cb-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="399cb-194">tooconfigure inicio de sesión único en **ServiceChannel** lado, necesita hello toosend descargado **certificado (Base64)** y **Id. de entidad SAML** demasiado[ Equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="399cb-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="399cb-195">Configurará esto Hola de toohave orden configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="399cb-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="399cb-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="399cb-197">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="399cb-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="399cb-199">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="399cb-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="399cb-200">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="399cb-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="399cb-202">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="399cb-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="399cb-204">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="399cb-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="399cb-206">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="399cb-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="399cb-208">a.</span><span class="sxs-lookup"><span data-stu-id="399cb-208">a.</span></span> <span data-ttu-id="399cb-209">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="399cb-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="399cb-210">b.</span><span class="sxs-lookup"><span data-stu-id="399cb-210">b.</span></span> <span data-ttu-id="399cb-211">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="399cb-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="399cb-212">c.</span><span class="sxs-lookup"><span data-stu-id="399cb-212">c.</span></span> <span data-ttu-id="399cb-213">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="399cb-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="399cb-214">d.</span><span class="sxs-lookup"><span data-stu-id="399cb-214">d.</span></span> <span data-ttu-id="399cb-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="399cb-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="399cb-216">Crear un usuario de prueba de ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="399cb-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="399cb-217">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="399cb-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="399cb-218">Para el aprovisionamiento de usuario completo, póngase en contacto con el [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="399cb-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="399cb-219">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="399cb-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="399cb-220">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooServiceChannel de acceso.</span><span class="sxs-lookup"><span data-stu-id="399cb-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="399cb-222">**tooassign Britta Simon tooServiceChannel, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="399cb-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="399cb-223">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="399cb-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="399cb-225">En la lista de aplicaciones de hello, seleccione **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="399cb-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="399cb-227">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="399cb-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="399cb-229">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="399cb-229">Click **Add** button.</span></span> <span data-ttu-id="399cb-230">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="399cb-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="399cb-232">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="399cb-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="399cb-233">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="399cb-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="399cb-234">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="399cb-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="399cb-235">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="399cb-235">Testing single sign-on</span></span>

<span data-ttu-id="399cb-236">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="399cb-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="399cb-237">Al hacer clic en icono de ServiceChannel Hola Hola Panel de acceso, deberá obtener aplicaciones de ServiceChannel tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="399cb-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="399cb-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="399cb-238">Additional resources</span></span>

* [<span data-ttu-id="399cb-239">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="399cb-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="399cb-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="399cb-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png