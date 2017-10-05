---
title: "Configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD | Microsoft Docs"
description: "Cómo configurar un inicio de sesión único federado para una aplicación existente de la galería de Azure AD y usar los tutoriales para empezar a trabajar rápidamente"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="62714-103">Configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62714-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="62714-104">Todas las aplicaciones de la galería de Azure AD habilitadas con funcionalidad de Enterprise Single Sign-On tienen un tutorial paso a paso disponible.</span><span class="sxs-lookup"><span data-stu-id="62714-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="62714-105">Para instrucciones detalladas paso a paso, acceda a la [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="62714-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="62714-106">Introducción a los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="62714-106">Overview of steps required</span></span>
<span data-ttu-id="62714-107">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="62714-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="62714-108">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62714-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="62714-109">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="62714-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="62714-110">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="62714-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="62714-111">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62714-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="62714-112">Configuración de los valores de los metadatos de Azure AD en la aplicación (URL de inicio de sesión, emisor, URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="62714-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="62714-113">Asignación de usuarios a la aplicación</span><span class="sxs-lookup"><span data-stu-id="62714-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="62714-114">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62714-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="62714-115">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="62714-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="62714-116">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="62714-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="62714-117">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="62714-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="62714-118">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62714-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="62714-119">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62714-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="62714-120">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="62714-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="62714-121">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="62714-122">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="62714-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="62714-123">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="62714-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="62714-124">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="62714-125">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="62714-126">Configuración del inicio de sesión único para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62714-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="62714-127">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="62714-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="62714-128">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="62714-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="62714-129">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="62714-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="62714-130">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62714-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="62714-131">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62714-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="62714-132">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="62714-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="62714-133">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="62714-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="62714-134">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="62714-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="62714-135">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="62714-136">En la lista desplegable **Modo**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="62714-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="62714-137">Especifique los valores obligatorios en **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="62714-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="62714-138">El proveedor de la aplicación le proporcionará estos valores.</span><span class="sxs-lookup"><span data-stu-id="62714-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="62714-139">Para configurar la aplicación como SSO iniciado por el SP, la dirección URL de inicio de sesión es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="62714-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="62714-140">En algunas aplicaciones, el identificador también es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="62714-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="62714-141">Para configurar la aplicación como SSO iniciado por el IdP, la dirección URL de respuesta es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="62714-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="62714-142">En algunas aplicaciones, el identificador también es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="62714-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="62714-143">**Opcional:** haga clic en **Mostrar configuración avanzada de URL** si desea ver los valores opcionales.</span><span class="sxs-lookup"><span data-stu-id="62714-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="62714-144">En **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="62714-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="62714-145">**Opcional:** haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="62714-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="62714-146">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="62714-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="62714-147">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="62714-147">click **Add attribute**.</span></span> <span data-ttu-id="62714-148">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="62714-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="62714-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="62714-149">Click **Save.**</span></span> <span data-ttu-id="62714-150">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="62714-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="62714-151">Haga clic en **Configurar &lt;nombre de la aplicación&gt;** para acceder a documentación sobre cómo configurar el inicio de sesión único en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="62714-152">Además, tiene las direcciones URL de los metadatos y el certificado necesario para la instalación de SSO con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="62714-153">Para guardar la configuración, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="62714-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="62714-154">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="62714-155">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="62714-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="62714-156">Para seleccionar el identificador de usuario o agregar atributos de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="62714-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="62714-157">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="62714-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="62714-158">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="62714-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="62714-159">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62714-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="62714-160">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62714-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="62714-161">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="62714-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="62714-162">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="62714-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="62714-163">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="62714-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="62714-164">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="62714-165">En la sección **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="62714-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="62714-166">La opción seleccionada debe coincidir con el valor esperado de la aplicación para autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="62714-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="62714-167">AD Azure selecciona el formato del atributo NameID (Identificador de usuario) en función del valor seleccionado o del formato que solicite la aplicación en el elemento AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="62714-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="62714-168">Para más información, visite la sección NameIDPolicy del artículo [Protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="62714-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="62714-169">Para agregar atributos de usuario, haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="62714-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="62714-170">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="62714-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="62714-171">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="62714-171">click **Add attribute**.</span></span> <span data-ttu-id="62714-172">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="62714-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="62714-173">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="62714-173">Click **Save**.</span></span> <span data-ttu-id="62714-174">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="62714-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="62714-175">Descarga del certificado o los metadatos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62714-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="62714-176">Para descargar el certificado o los metadatos de la aplicación de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="62714-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="62714-177">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="62714-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="62714-178">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="62714-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="62714-179">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62714-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="62714-180">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62714-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="62714-181">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="62714-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="62714-182">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="62714-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="62714-183">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="62714-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="62714-184">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="62714-185">Vaya a la sección **Certificado de firma de SAML** y haga clic en el valor de la columna **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="62714-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="62714-186">Según lo que necesite la aplicación para configurar el inicio de sesión único, verá la opción para descargar el archivo XML de metadatos o el certificado.</span><span class="sxs-lookup"><span data-stu-id="62714-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="62714-187">Azure AD no proporciona una dirección URL para obtener los metadatos.</span><span class="sxs-lookup"><span data-stu-id="62714-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="62714-188">Solo se pueden recuperar como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="62714-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="62714-189">Asignación de usuarios a la aplicación</span><span class="sxs-lookup"><span data-stu-id="62714-189">Assign users to the application</span></span>

<span data-ttu-id="62714-190">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="62714-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="62714-191">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="62714-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="62714-192">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="62714-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="62714-193">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62714-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="62714-194">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62714-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="62714-195">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="62714-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="62714-196">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="62714-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="62714-197">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="62714-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="62714-198">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="62714-199">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="62714-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="62714-200">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="62714-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="62714-201">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="62714-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="62714-202">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="62714-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="62714-203">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="62714-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="62714-204">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="62714-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="62714-205">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62714-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="62714-206">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="62714-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="62714-207">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="62714-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="62714-208">Tras un breve período de tiempo, los usuarios seleccionados podrán iniciar estas aplicaciones mediante los métodos descritos en la sección de descripción de la solución.</span><span class="sxs-lookup"><span data-stu-id="62714-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="62714-209">Personalización de las notificaciones SAML que se han enviado a una aplicación</span><span class="sxs-lookup"><span data-stu-id="62714-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="62714-210">Para obtener información sobre cómo personalizar las notificaciones de atributo SAML que se han enviado a su aplicación, vea [Asignación de notificaciones en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping).</span><span class="sxs-lookup"><span data-stu-id="62714-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62714-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62714-211">Next steps</span></span>
[<span data-ttu-id="62714-212">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="62714-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



