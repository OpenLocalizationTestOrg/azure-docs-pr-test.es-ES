---
title: "Autenticación basada en encabezados con PingAccess para el proxy de la aplicación de Azure AD | Microsoft Docs"
description: "Publique aplicaciones con PingAccess y el proxy de la aplicación que admitan la autenticación basada en encabezados."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="360e5-103">Autenticación basada en el encabezado para el inicio de sesión único con el proxy de aplicación y PingAccess</span><span class="sxs-lookup"><span data-stu-id="360e5-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="360e5-104">El proxy de la aplicación Azure Active Directory y PingAccess se han asociado para proporcionar a los clientes de Azure Active Directory acceso a más aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="360e5-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="360e5-105">PingAccess expande las [ofertas actuales del proxy de aplicación](active-directory-application-proxy-get-started.md) para incluir el acceso de inicio sesión único a las aplicaciones que utilicen encabezados para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="360e5-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="360e5-106">¿Qué es PingAccess para Azure AD?</span><span class="sxs-lookup"><span data-stu-id="360e5-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="360e5-107">PingAccess para Azure Active Directory es una oferta de PingAccess que permite conceder acceso a los usuarios y el inicio de sesión único a las aplicaciones que utilizan encabezados para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="360e5-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="360e5-108">El proxy de la aplicación trata estas aplicaciones como a las demás, usa Azure AD para autenticar el acceso y, después, pasa el tráfico a través del servicio de conector.</span><span class="sxs-lookup"><span data-stu-id="360e5-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="360e5-109">PingAccess se coloca delante de las aplicaciones y convierte el token de acceso de Azure AD en un encabezado, con el fin de que la aplicación reciba la autenticación en un formato que pueda leer.</span><span class="sxs-lookup"><span data-stu-id="360e5-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="360e5-110">Los usuarios no notarán ninguna diferencia al iniciar sesión para usar las aplicaciones corporativas.</span><span class="sxs-lookup"><span data-stu-id="360e5-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="360e5-111">Podrán seguir trabajando desde cualquier lugar y en cualquier dispositivo.</span><span class="sxs-lookup"><span data-stu-id="360e5-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="360e5-112">Dado que los conectores del proxy de la aplicación dirigen el tráfico remoto a todas las aplicaciones, independientemente de su tipo de autenticación, seguirán equilibrando la carga de forma automática.</span><span class="sxs-lookup"><span data-stu-id="360e5-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="360e5-113">¿Cómo puedo obtener acceso?</span><span class="sxs-lookup"><span data-stu-id="360e5-113">How do I get access?</span></span>

<span data-ttu-id="360e5-114">Dado que este escenario se ofrece a través de una asociación entre Azure Active Directory y PingAccess, se necesitarán licencias de ambos servicios.</span><span class="sxs-lookup"><span data-stu-id="360e5-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="360e5-115">Sin embargo, las suscripciones Premium de Azure Active Directory incluyen una licencia básica de PingAccess que abarca hasta 20 aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="360e5-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="360e5-116">Si tiene que publicar más de 20 aplicaciones basadas en el encabezado, puede adquirir una licencia adicional de PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="360e5-117">Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="360e5-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="360e5-118">Publicación de una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="360e5-118">Publish your application in Azure</span></span>

<span data-ttu-id="360e5-119">Este artículo va dirigido a quienes publican por primera vez una aplicación con este escenario.</span><span class="sxs-lookup"><span data-stu-id="360e5-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="360e5-120">Es una guía a través de cómo empezar a trabajar con Application y PingAccess, además de explicar los pasos de la publicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="360e5-121">Si ya configuró ambos servicios, pero desea revisar los pasos de publicación, puede omitir la instalación del conector y pasar a [agregar la aplicación a Azure AD con el proxy de aplicación](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="360e5-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="360e5-122">Dado que este escenario es una asociación entre Azure AD y PingAccess, algunas de las instrucciones se encuentran en el sitio de Ping Identity.</span><span class="sxs-lookup"><span data-stu-id="360e5-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="360e5-123">Instalación de un conector del proxy de la aplicación</span><span class="sxs-lookup"><span data-stu-id="360e5-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="360e5-124">Si ya tiene habilitado el proxy de aplicación y tiene instalado un conector, puede omitir esta sección y pasar a [agregar la aplicación a Azure AD con el proxy de aplicación](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="360e5-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="360e5-125">El conector del proxy de la aplicación es un servicio de Windows Server que dirige el tráfico de los empleados remotos a las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="360e5-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="360e5-126">Para más información acerca de las instrucciones de instalación, consulte [Habilitación del proxy de aplicación en Azure Portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="360e5-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="360e5-127">Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="360e5-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="360e5-128">Seleccione **Azure Active Directory** > **Proxy de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="360e5-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="360e5-129">Seleccione **Download Connector** (Descargar conector) para iniciar la descarga de conector del proxy de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="360e5-130">Siga las instrucciones de instalación.</span><span class="sxs-lookup"><span data-stu-id="360e5-130">Follow the installation instructions.</span></span>

   ![Habilitar el proxy de la aplicación y descargar el conector](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="360e5-132">La descarga del conector debería habilitar automáticamente el proxy de la aplicación en el directorio, pero si no lo hace, puede seleccionar **Habilitar el proxy de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="360e5-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="360e5-133">Incorporación de la aplicación a Azure AD con el proxy de la aplicación</span><span class="sxs-lookup"><span data-stu-id="360e5-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="360e5-134">Hay dos acciones que se deben tomar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="360e5-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="360e5-135">En primer lugar, debe publicar la aplicación con el proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="360e5-136">Después, debe recopilar información acerca de la aplicación que puede usar en los pasos de PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="360e5-137">Siga estos pasos para publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="360e5-138">Para obtener un tutorial más detallado de los pasos 1 a 8, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="360e5-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="360e5-139">Si no lo hizo en la sección anterior, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="360e5-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="360e5-140">Seleccione **Azure Active Directory** > **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="360e5-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="360e5-141">Seleccione **Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="360e5-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="360e5-142">Seleccione **Aplicación local**.</span><span class="sxs-lookup"><span data-stu-id="360e5-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="360e5-143">Rellene los campos requeridos con la información de la aplicación nueva.</span><span class="sxs-lookup"><span data-stu-id="360e5-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="360e5-144">Utilice las siguientes instrucciones para realizar la configuración:</span><span class="sxs-lookup"><span data-stu-id="360e5-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="360e5-145">**Dirección URL interna**: normalmente, especifica la dirección URL que lleva a la página de inicio de sesión la aplicación cuando esté en la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="360e5-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="360e5-146">En este escenario, el conector tiene que tratar el proxy de PingAccess como la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="360e5-147">Use este formato: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="360e5-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="360e5-148">El puerto predeterminado es 3000, pero puedo configurar uno distinto en PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="360e5-149">**Método de autenticación previa**: Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="360e5-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="360e5-150">**Traducir URL en encabezados**: No.</span><span class="sxs-lookup"><span data-stu-id="360e5-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="360e5-151">Si esta es su primera aplicación, utilice el puerto 3000 para empezar y regrese para actualizar este valor si cambia la configuración de PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="360e5-152">Si no es la primera, tendrá que coincidir con la escucha que ha configurado en PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="360e5-153">Obtenga más información sobre [escucha en PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="360e5-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="360e5-154">Seleccione **Agregar** en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="360e5-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="360e5-155">Se agrega la aplicación y se abre el menú de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="360e5-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="360e5-156">En dicho menú, seleccione **Asignar un usuario para las pruebas**  y agregue al menos un usuario a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="360e5-157">Asegúrese de que esta cuenta de prueba tiene acceso a la aplicación local.</span><span class="sxs-lookup"><span data-stu-id="360e5-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="360e5-158">Seleccione **Asignar** para guardar la asignación del usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="360e5-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="360e5-159">En la hoja de administración de la aplicación, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="360e5-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="360e5-160">Elija **Header-based sign-on** (Inicio de sesión basado en encabezado) en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="360e5-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="360e5-161">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="360e5-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="360e5-162">Si se trata de la primera vez que usa el inicio de sesión único basado en el encabezado, debe instalar PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="360e5-163">Para asegurarse de que su suscripción de Azure se asocia automáticamente con la instalación de PingAccess, utilice el vínculo de esta página de inicio de sesión único para descargar PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="360e5-164">Puede abrir el sitio de descarga ahora o volver a esta página más adelante.</span><span class="sxs-lookup"><span data-stu-id="360e5-164">You can open the download site now, or come back to this page later.</span></span> 

   ![Selección del inicio de sesión basado en encabezados](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="360e5-166">Cierre la hoja Aplicaciones empresariales o desplácese completamente hacia la izquierda para volver al menú de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="360e5-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="360e5-167">Seleccione **App registrations** (Registros de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="360e5-167">Select **App registrations**.</span></span>

   ![Selección de los registros de aplicaciones](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="360e5-169">Seleccione la aplicación que se acaba de agregar y seleccione **Direcciones URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="360e5-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![Selección de las direcciones URL de respuesta](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="360e5-171">Compruebe si la dirección URL externa que asignó a la aplicación en el paso 5 se encuentra en la lista de direcciones URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="360e5-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="360e5-172">Si no está, agréguela ahora.</span><span class="sxs-lookup"><span data-stu-id="360e5-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="360e5-173">En la hoja de configuración de la aplicación, seleccione **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="360e5-173">On the app settings blade, select **Required permissions**.</span></span>

  ![Selección de los permisos necesarios](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="360e5-175">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="360e5-175">Select **Add**.</span></span> <span data-ttu-id="360e5-176">Para la API, elija **Microsoft Azure Active Directory** y, después, **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="360e5-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="360e5-177">Para los permisos, elija **Read and write all applications** (Leer y escribir en todas las aplicaciones) y **Sign in and read user profile** (Iniciar sesión y leer perfil de usuario), luego **Seleccionar** y, finalmente, **Listo**.</span><span class="sxs-lookup"><span data-stu-id="360e5-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Selección de permisos](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="360e5-179">Recopilación de información para los pasos de PingAccess</span><span class="sxs-lookup"><span data-stu-id="360e5-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="360e5-180">En la hoja de configuración de la aplicación, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="360e5-180">On your app settings blade, select **Properties**.</span></span> 

  ![Selección de las propiedades](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="360e5-182">Guarde el valor de **Id. de la aplicación**,</span><span class="sxs-lookup"><span data-stu-id="360e5-182">Save the **Application Id** value.</span></span> <span data-ttu-id="360e5-183">ya que se usa para el identificador de cliente cuando se configura PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="360e5-184">En la misma hoja, seleccione **Claves**.</span><span class="sxs-lookup"><span data-stu-id="360e5-184">On the app settings blade, select **Keys**.</span></span>

  ![Selección de las claves](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="360e5-186">Cree una clave, para lo que debe escribir una descripción de la misma y elegir una fecha de expiración en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="360e5-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="360e5-187">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="360e5-187">Select **Save**.</span></span> <span data-ttu-id="360e5-188">Aparece un GUID en el campo **Valor**.</span><span class="sxs-lookup"><span data-stu-id="360e5-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="360e5-189">Guarde este valor, ya que no lo volverá a ver una vez que cierre esta ventana.</span><span class="sxs-lookup"><span data-stu-id="360e5-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Creación de una nueva clave](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="360e5-191">Cierre la hoja Registros de aplicaciones o desplácese completamente hacia la izquierda para volver al menú de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="360e5-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="360e5-192">Seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="360e5-192">Select **Properties**.</span></span>
8. <span data-ttu-id="360e5-193">Guarde el GUID de **Id. de directorio**.</span><span class="sxs-lookup"><span data-stu-id="360e5-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="360e5-194">Opcional: actualice GraphAPI para enviar los campos personalizados</span><span class="sxs-lookup"><span data-stu-id="360e5-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="360e5-195">Para obtener una lista de los tokens de seguridad que Azure AD envía para la autenticación, consulte la [referencia de tokens de Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="360e5-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="360e5-196">Si necesita una notificación personalizada que enviar a otros tokens, use GraphAPI para establecer el campo de la aplicación *acceptMappedClaims* en **True**.</span><span class="sxs-lookup"><span data-stu-id="360e5-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="360e5-197">Puede utilizar el Explorador de Azure AD Graph o MS Graph para hacer esta configuración.</span><span class="sxs-lookup"><span data-stu-id="360e5-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="360e5-198">En este ejemplo se usa el Explorador de Graph:</span><span class="sxs-lookup"><span data-stu-id="360e5-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="360e5-199">Descarga de PingAccess y configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="360e5-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="360e5-200">Ahora que ha completado todos los pasos de instalación de Azure Active Directory, puede pasar a configurar PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="360e5-201">Los pasos detallados de la parte de PingAccess de este escenario se pueden encontrar en la documentación de Ping Identity, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html) (Configuración de PingAccess para Azure AD).</span><span class="sxs-lookup"><span data-stu-id="360e5-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="360e5-202">Dichos pasos le guiarán a través del proceso de obtención de una cuenta de PingAccess, en caso de que aún no la tenga, instalación del servidor de PingAccess y creación de una conexión de proveedor de OIDC de Azure AD con el Id. de directorio que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="360e5-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="360e5-203">A continuación, utilice los valores de Id. de la aplicación y Clave para crear una sesión Web en PingAccess.</span><span class="sxs-lookup"><span data-stu-id="360e5-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="360e5-204">Después, puede configurar la asignación de identidades y crear un host virtual, un sitio y una aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="360e5-205">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="360e5-205">Test your app</span></span>

<span data-ttu-id="360e5-206">Cuando haya completado todos los pasos, la aplicación debería estar en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="360e5-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="360e5-207">Para probarla, abra un explorador y navegue a la dirección URL externa que creó al publicar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="360e5-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="360e5-208">Inicie sesión con la cuenta de prueba que asignó a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="360e5-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="360e5-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="360e5-209">Next steps</span></span>

- [<span data-ttu-id="360e5-210">Configuración de PingAccess para Azure AD</span><span class="sxs-lookup"><span data-stu-id="360e5-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="360e5-211">¿Cómo permite el proxy de aplicación de Azure AD el inicio de sesión único?</span><span class="sxs-lookup"><span data-stu-id="360e5-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="360e5-212">Solucionar problemas de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="360e5-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
