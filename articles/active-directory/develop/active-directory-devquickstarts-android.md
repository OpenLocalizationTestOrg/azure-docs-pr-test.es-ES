---
title: "Introducción a Azure AD Android | Microsoft Docs"
description: "Cómo crear una aplicación Android que se integra con Azure AD para el inicio de sesión y llama a las API protegidas de Azure AD mediante OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="7d42a-103">Integración de Azure AD en una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="7d42a-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="7d42a-104">Pruebe la versión preliminar de nuestro nuevo [portal para desarrolladores](https://identity.microsoft.com/Docs/Android), que le ayudará a empezar a trabajar con Azure AD en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7d42a-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="7d42a-105">El portal para desarrolladores lo guiará a través del proceso de registro de una aplicación y de integración de Azure AD en el código.</span><span class="sxs-lookup"><span data-stu-id="7d42a-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="7d42a-106">Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.</span><span class="sxs-lookup"><span data-stu-id="7d42a-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="7d42a-107">Si está desarrollando una aplicación de escritorio, Azure Active Directory (Azure AD) le facilita la autenticación de los usuarios mediante sus cuentas de Active Directory locales.</span><span class="sxs-lookup"><span data-stu-id="7d42a-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="7d42a-108">También permite a la aplicación consumir con seguridad cualquier API web protegida por Azure AD, como las API de Office 365 o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d42a-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="7d42a-109">Para los clientes de Android que necesitan tener acceso a recursos protegidos, Azure AD proporciona la Biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="7d42a-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="7d42a-110">El único propósito de ADAL es facilitar a su aplicación la obtención de tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="7d42a-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="7d42a-111">Para demostrar lo fácil que es, crearemos una aplicación Android de lista de tareas pendientes que permita realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7d42a-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="7d42a-112">Obtener tokens de acceso para llamar a la API de lista de tareas pendientes utilizando el [protocolo de autenticación OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d42a-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="7d42a-113">Obtener listas de tareas pendientes de un usuario.</span><span class="sxs-lookup"><span data-stu-id="7d42a-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="7d42a-114">Desconectar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7d42a-114">Signs out users.</span></span>

<span data-ttu-id="7d42a-115">Para comenzar, necesitará a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="7d42a-116">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7d42a-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="7d42a-117">Paso 1: descargue y ejecute el servidor de ejemplos TODO de la API de REST de Node.js</span><span class="sxs-lookup"><span data-stu-id="7d42a-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="7d42a-118">Este servidor de ejemplos TODO de la API de REST de Node.js está escrito específicamente para que funcione con nuestro ejemplo existente para crear una API de REST To-Do de un solo inquilino para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d42a-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="7d42a-119">Se trata de un requisito previo para el Inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="7d42a-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="7d42a-120">Para obtener información sobre cómo configurarlo, consulte los ejemplos existentes en [Servicio de API de REST de ejemplo de Microsoft Azure Active Directory para Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7d42a-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="7d42a-121">Paso 2: registre la API web con el inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d42a-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="7d42a-122">Active Directory permite agregar dos tipos de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="7d42a-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="7d42a-123">API web que ofrecen servicios a los usuarios</span><span class="sxs-lookup"><span data-stu-id="7d42a-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="7d42a-124">Aplicaciones (que se ejecutan en la Web o en un dispositivo) que tienen acceso a esas API web</span><span class="sxs-lookup"><span data-stu-id="7d42a-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="7d42a-125">En este paso, va a registrar la API web que se ejecuta localmente para probar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="7d42a-126">Normalmente, esta API web es un servicio de REST que ofrece la funcionalidad a la que desea que acceda una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="7d42a-127">Azure AD puede ayudar a proteger cualquier punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="7d42a-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="7d42a-128">Aquí suponemos que va a registrar la API de REST TODO mencionada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7d42a-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="7d42a-129">No obstante, este procedimiento este procedimiento sirve para cualquier API web que desee que Azure Active Directory ayude a proteger.</span><span class="sxs-lookup"><span data-stu-id="7d42a-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="7d42a-130">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d42a-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7d42a-131">En la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="7d42a-131">On the top bar, click your account.</span></span> <span data-ttu-id="7d42a-132">En la lista **Directorio**, elija el inquilino de Azure AD donde desea registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="7d42a-133">Haga clic en **Más servicios** en el panel izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7d42a-134">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="7d42a-135">Escriba un nombre descriptivo para la aplicación (por ejemplo, **TodoListService**), seleccione **Aplicación web y/o API web** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="7d42a-136">Para la URL de inicio de sesión, escriba la dirección URL base para el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="7d42a-137">De manera predeterminada, será `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="7d42a-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="7d42a-138">Haga clic en **Aceptar** para completar el registro.</span><span class="sxs-lookup"><span data-stu-id="7d42a-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="7d42a-139">Mientras sigue en Azure Portal, vaya a la página de la aplicación, busque el valor del id. de aplicación y cópielo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="7d42a-140">Lo necesitará más adelante cuando configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="7d42a-141">En la página **Configuración** -> **Propiedades**, actualice la aplicación del URI del identificador de aplicación y escriba `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="7d42a-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="7d42a-142">Reemplace `<your_tenant_name>` por el nombre de su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d42a-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="7d42a-143">Paso 3: registre la aplicación de cliente nativo de Android de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7d42a-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="7d42a-144">Debe registrar la aplicación web en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-144">You must register your web application in this sample.</span></span> <span data-ttu-id="7d42a-145">Esto permite a su aplicación comunicarse con la recién registrada API web.</span><span class="sxs-lookup"><span data-stu-id="7d42a-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="7d42a-146">Azure AD rechazará incluso que la aplicación pueda solicitar el inicio de sesión, a menos que esté registrada.</span><span class="sxs-lookup"><span data-stu-id="7d42a-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="7d42a-147">Eso forma parte de la seguridad del modelo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-147">That's part of the security of the model.</span></span>

<span data-ttu-id="7d42a-148">Aquí suponemos que va a registrar la aplicación de ejemplo mencionada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7d42a-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="7d42a-149">No obstante, este procedimiento sirve para cualquier aplicación que esté desarrollando.</span><span class="sxs-lookup"><span data-stu-id="7d42a-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="7d42a-150">Es posible que se pregunte por qué poner una aplicación y una API web en un mismo inquilino.</span><span class="sxs-lookup"><span data-stu-id="7d42a-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="7d42a-151">Como posiblemente haya intuido, puede crear una aplicación con acceso a una API externa registrada en Azure AD desde otro inquilino.</span><span class="sxs-lookup"><span data-stu-id="7d42a-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="7d42a-152">Si lo hace, se pedirá a los clientes que acepten el uso de la API en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="7d42a-153">La Biblioteca de autenticación de Active Directory para iOS se encarga de este consentimiento por usted.</span><span class="sxs-lookup"><span data-stu-id="7d42a-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="7d42a-154">A medida que exploremos características más avanzadas, verá que se trata de una parte importante del trabajo necesario para tener acceso al conjunto de API de Microsoft desde Azure y Office, así como cualquier otro proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="7d42a-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="7d42a-155">Por ahora, como ha registrado su API web y la aplicación en el mismo inquilino, no verá ninguna petición de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="7d42a-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="7d42a-156">Este suele ser el caso si va a desarrollar una aplicación solo para que la use su propia empresa.</span><span class="sxs-lookup"><span data-stu-id="7d42a-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="7d42a-157">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d42a-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7d42a-158">En la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="7d42a-158">On the top bar, click your account.</span></span> <span data-ttu-id="7d42a-159">En la lista **Directorio**, elija el inquilino de Azure AD donde desea registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="7d42a-160">Haga clic en **Más servicios** en el panel izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7d42a-161">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="7d42a-162">Escriba un nombre descriptivo para la aplicación (por ejemplo **TodoListClient-Android**), seleccione **Aplicación de cliente nativo** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="7d42a-163">Para el URI de redirección, escriba `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="7d42a-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="7d42a-164">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="7d42a-164">Click **Finish**.</span></span>
7. <span data-ttu-id="7d42a-165">En la página de la aplicación, busque el valor de identificador de la aplicación y cópielo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="7d42a-166">Lo necesitará más adelante cuando configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="7d42a-167">En la página **Configuración**, seleccione **Permisos necesarios** y, a continuación, **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="7d42a-168">Busque y seleccione TodoListService y agregue el permiso **Access TodoListService** en **Permisos delegados**; luego, haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="7d42a-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="7d42a-169">Para compilar con Maven, puede utilizar pom.xml en el nivel superior:</span><span class="sxs-lookup"><span data-stu-id="7d42a-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="7d42a-170">Clone este repositorio en el directorio que desee:</span><span class="sxs-lookup"><span data-stu-id="7d42a-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="7d42a-171">Siga los pasos descritos en los [requisitos previos para configurar el entorno Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="7d42a-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="7d42a-172">Configure el emulador con SDK 19.</span><span class="sxs-lookup"><span data-stu-id="7d42a-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="7d42a-173">Vaya a la carpeta raíz donde ha clonado el repositorio.</span><span class="sxs-lookup"><span data-stu-id="7d42a-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="7d42a-174">Ejecute este comando: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="7d42a-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="7d42a-175">Cambie el directorio al ejemplo de inicio rápido: `cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="7d42a-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="7d42a-176">Ejecute este comando: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="7d42a-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="7d42a-177">La aplicación debería iniciarse.</span><span class="sxs-lookup"><span data-stu-id="7d42a-177">You should see the app starting.</span></span>
8. <span data-ttu-id="7d42a-178">Escriba las credenciales del usuario de prueba para probarlas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="7d42a-179">Los paquetes JAR se enviarán junto con el paquete AAR.</span><span class="sxs-lookup"><span data-stu-id="7d42a-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="7d42a-180">Paso 4: descargue ADAL de Android y agréguelo al área de trabajo de Eclipse</span><span class="sxs-lookup"><span data-stu-id="7d42a-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="7d42a-181">Ahora tiene varias opciones para usar ADAL en el proyecto Android:</span><span class="sxs-lookup"><span data-stu-id="7d42a-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="7d42a-182">Puede usar el código fuente para importar esta biblioteca en Eclipse y vincularla a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="7d42a-183">Si utiliza Android Studio, puede usar el formato de paquete AAR y hacer referencia a los archivos binarios.</span><span class="sxs-lookup"><span data-stu-id="7d42a-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="7d42a-184">Opción 1: origen a través de ZIP</span><span class="sxs-lookup"><span data-stu-id="7d42a-184">Option 1: Source Zip</span></span>
<span data-ttu-id="7d42a-185">Para descargar una copia del código fuente, haga clic en **Descargar ZIP** en el lado derecho de la página.</span><span class="sxs-lookup"><span data-stu-id="7d42a-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="7d42a-186">También puede [descargarla desde GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="7d42a-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="7d42a-187">Opción 2: origen a través de Git</span><span class="sxs-lookup"><span data-stu-id="7d42a-187">Option 2: Source via Git</span></span>
<span data-ttu-id="7d42a-188">Para obtener el código fuente del SDK mediante Git, escriba:</span><span class="sxs-lookup"><span data-stu-id="7d42a-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="7d42a-189">Opción 3: binarios a través de Gradle</span><span class="sxs-lookup"><span data-stu-id="7d42a-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="7d42a-190">Puede obtener los archivos binarios desde el repositorio central de Maven.</span><span class="sxs-lookup"><span data-stu-id="7d42a-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="7d42a-191">El paquete AAR puede incluirse de la siguiente forma en el proyecto en Android Studio:</span><span class="sxs-lookup"><span data-stu-id="7d42a-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="7d42a-192">Opción 4: AAR a través de Maven</span><span class="sxs-lookup"><span data-stu-id="7d42a-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="7d42a-193">Si utiliza el complemento M2Eclipse, puede especificar la dependencia en el archivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="7d42a-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="7d42a-194">Opción 5: paquete JAR dentro de la carpeta libs</span><span class="sxs-lookup"><span data-stu-id="7d42a-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="7d42a-195">Puede obtener el archivo JAR desde el repositorio de Maven y colocarlo en la carpeta **libs** del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7d42a-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="7d42a-196">También deberá copiar los recursos necesarios en el proyecto, ya que los paquetes JAR no los incluyen.</span><span class="sxs-lookup"><span data-stu-id="7d42a-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="7d42a-197">Paso 5: agregue referencias a ADAL de Android en el proyecto</span><span class="sxs-lookup"><span data-stu-id="7d42a-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="7d42a-198">Agregue una referencia al proyecto y especifíquela como una biblioteca de Android.</span><span class="sxs-lookup"><span data-stu-id="7d42a-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="7d42a-199">Si no está seguro de cómo hacerlo, puede obtener más información en el [sitio de Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="7d42a-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="7d42a-200">Agregue la dependencia de proyecto para la depuración en la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7d42a-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="7d42a-201">Actualice el archivo del proyecto AndroidManifest.xml para incluir:</span><span class="sxs-lookup"><span data-stu-id="7d42a-201">Update your project's AndroidManifest.xml file to include:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="7d42a-202">Cree una instancia de AuthenticationContext en la actividad principal.</span><span class="sxs-lookup"><span data-stu-id="7d42a-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="7d42a-203">Los detalles de esta llamada quedan fuera del ámbito de este tema, pero puede empezar a trabajar examinando el [ejemplo del cliente nativo de Android](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="7d42a-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="7d42a-204">En el ejemplo siguiente, SharedPreferences es la memoria caché predeterminada y Authority se presenta con el formato de `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="7d42a-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="7d42a-205">Copie este bloque de código para controlar el final de AuthenticationActivity después de que el usuario escriba las credenciales y reciba el código de autorización:</span><span class="sxs-lookup"><span data-stu-id="7d42a-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="7d42a-206">Para solicitar un token, defina una devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="7d42a-206">To ask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="7d42a-207">Por último, solicite un token mediante esa devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="7d42a-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="7d42a-208">A continuación, se proporciona una explicación de los parámetros:</span><span class="sxs-lookup"><span data-stu-id="7d42a-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="7d42a-209">Hay que especificar *resource*, que es el recurso al que está intentando acceder.</span><span class="sxs-lookup"><span data-stu-id="7d42a-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="7d42a-210">*clientid* es necesario. Su valor procede de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d42a-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="7d42a-211">No es necesario que se proporcione *RedirectUri* para la llamada a acquireToken.</span><span class="sxs-lookup"><span data-stu-id="7d42a-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="7d42a-212">Se puede configurar como el nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="7d42a-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="7d42a-213">*PromptBehavior* ayuda a pedir las credenciales para omitir la memoria caché y la cookie.</span><span class="sxs-lookup"><span data-stu-id="7d42a-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="7d42a-214">Se llamará a *callback* una vez que se intercambie el código de autorización para un token.</span><span class="sxs-lookup"><span data-stu-id="7d42a-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="7d42a-215">La devolución de llamada tiene un objeto de AuthenticationResult que tiene acceso al token, fecha de caducidad e información sobre el token del identificador.</span><span class="sxs-lookup"><span data-stu-id="7d42a-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="7d42a-216">*acquireTokenSilent* es opcional.</span><span class="sxs-lookup"><span data-stu-id="7d42a-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="7d42a-217">Puede llamarlo para controlar el almacenamiento en caché y la actualización del token.</span><span class="sxs-lookup"><span data-stu-id="7d42a-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="7d42a-218">También proporciona la versión de sincronización.</span><span class="sxs-lookup"><span data-stu-id="7d42a-218">It also provides the sync version.</span></span> <span data-ttu-id="7d42a-219">Acepta *userId* como parámetro.</span><span class="sxs-lookup"><span data-stu-id="7d42a-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="7d42a-220">Con este procedimiento, debe contar con todo lo necesario para lograr una integración correcta con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d42a-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="7d42a-221">Para obtener más ejemplos de este trabajo, visite el repositorio AzureADSamples/ en GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d42a-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="7d42a-222">Información importante</span><span class="sxs-lookup"><span data-stu-id="7d42a-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="7d42a-223">Personalización</span><span class="sxs-lookup"><span data-stu-id="7d42a-223">Customization</span></span>
<span data-ttu-id="7d42a-224">Los recursos de la aplicación pueden sobrescribir a los recursos del proyecto de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7d42a-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="7d42a-225">Esto sucede cuando la aplicación se está generando.</span><span class="sxs-lookup"><span data-stu-id="7d42a-225">This happens when your app is being built.</span></span> <span data-ttu-id="7d42a-226">Por este motivo, puede personalizar el diseño de la actividad de autenticación del modo que desee.</span><span class="sxs-lookup"><span data-stu-id="7d42a-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="7d42a-227">Asegúrese de conservar el identificador de los controles que use ADAL (WebView).</span><span class="sxs-lookup"><span data-stu-id="7d42a-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="7d42a-228">Agente</span><span class="sxs-lookup"><span data-stu-id="7d42a-228">Broker</span></span>
<span data-ttu-id="7d42a-229">La aplicación de portal de empresa de Microsoft Intune proporciona el componente del agente.</span><span class="sxs-lookup"><span data-stu-id="7d42a-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="7d42a-230">La cuenta se crea en el administrador de cuentas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-230">The account is created in AccountManager.</span></span> <span data-ttu-id="7d42a-231">El tipo de cuenta es "com.microsoft.workaccount".</span><span class="sxs-lookup"><span data-stu-id="7d42a-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="7d42a-232">El administrador de cuentas únicamente permite una sola cuenta SSO.</span><span class="sxs-lookup"><span data-stu-id="7d42a-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="7d42a-233">Después de completar el desafío del dispositivo para una de las aplicaciones, creará una cookie de SSO para el usuario.</span><span class="sxs-lookup"><span data-stu-id="7d42a-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="7d42a-234">ADAL usará la cuenta del agente si en este autenticador hay creada una cuenta de usuario y decide no omitirla.</span><span class="sxs-lookup"><span data-stu-id="7d42a-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="7d42a-235">Puede omitir el usuario del agente mediante:</span><span class="sxs-lookup"><span data-stu-id="7d42a-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="7d42a-236">Debe registrar un RedirectUri especial para el uso del agente.</span><span class="sxs-lookup"><span data-stu-id="7d42a-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="7d42a-237">RedirectUri tiene el formato `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="7d42a-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="7d42a-238">Puede obtener un RedirectUri para su aplicación mediante el script brokerRedirectPrint.ps1. También puede usar la llamada de API mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="7d42a-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="7d42a-239">La firma está relacionada con los certificados de firma.</span><span class="sxs-lookup"><span data-stu-id="7d42a-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="7d42a-240">El modelo de agente actual es para un usuario.</span><span class="sxs-lookup"><span data-stu-id="7d42a-240">The current broker model is for one user.</span></span> <span data-ttu-id="7d42a-241">AuthenticationContext proporciona un método de API para obtener el usuario del agente.</span><span class="sxs-lookup"><span data-stu-id="7d42a-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="7d42a-242">El manifiesto de aplicación debe tener los siguientes permisos para usar cuentas del administrador de cuentas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="7d42a-243">Para más información, consulte la [información del administrador de cuentas en el sitio de Android](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="7d42a-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="7d42a-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="7d42a-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="7d42a-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="7d42a-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="7d42a-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="7d42a-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="7d42a-247">AD FS y URL de la autoridad</span><span class="sxs-lookup"><span data-stu-id="7d42a-247">Authority URL and AD FS</span></span>
<span data-ttu-id="7d42a-248">Active Directory Federation Services (AD FS) no se reconoce como STS de producción, por lo que debe desactivar el descubrimiento de la instancia y pasar el valor "false" al constructor de AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="7d42a-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="7d42a-249">La dirección URL de la autoridad necesita la instancia de STS y un [nombre de inquilino](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="7d42a-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="7d42a-250">Consulta de los elementos en caché</span><span class="sxs-lookup"><span data-stu-id="7d42a-250">Querying cache items</span></span>
<span data-ttu-id="7d42a-251">ADAL proporciona memoria caché predeterminada en SharedPreferences con algunas características sencillas para hacer consultas sobre los elementos en caché.</span><span class="sxs-lookup"><span data-stu-id="7d42a-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="7d42a-252">Puede obtener la memoria caché actual de AuthenticationContext mediante:</span><span class="sxs-lookup"><span data-stu-id="7d42a-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="7d42a-253">También puede proporcionar su implementación de la memoria caché, si desea personalizarla.</span><span class="sxs-lookup"><span data-stu-id="7d42a-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="7d42a-254">Comportamiento de la petición</span><span class="sxs-lookup"><span data-stu-id="7d42a-254">Prompt behavior</span></span>
<span data-ttu-id="7d42a-255">ADAL permite especificar el comportamiento de la petición.</span><span class="sxs-lookup"><span data-stu-id="7d42a-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="7d42a-256">PromptBehavior.Auto mostrará la interfaz de usuario si el token de actualización no es válido y se necesitan credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="7d42a-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="7d42a-257">PromptBehavior.Always omitirá el uso de la memoria caché y mostrará siempre la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="7d42a-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="7d42a-258">Solicitud de token silenciosa desde la memoria caché y actualización</span><span class="sxs-lookup"><span data-stu-id="7d42a-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="7d42a-259">Una solicitud de token silenciosa no utiliza la interfaz de usuario emergente ni requiere una actividad.</span><span class="sxs-lookup"><span data-stu-id="7d42a-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="7d42a-260">Devuelve un token de la memoria caché si está disponible.</span><span class="sxs-lookup"><span data-stu-id="7d42a-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="7d42a-261">Si el token ha caducado, este método intenta actualizarlo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="7d42a-262">Si el token de actualización está caducado o falla por cualquier motivo, devuelve AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="7d42a-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="7d42a-263">También puede hacer una llamada de sincronización con este método.</span><span class="sxs-lookup"><span data-stu-id="7d42a-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="7d42a-264">Puede establecer null para la devolución de llamada o usar acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="7d42a-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="7d42a-265">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="7d42a-265">Diagnostics</span></span>
<span data-ttu-id="7d42a-266">Estas son las principales fuentes de información para diagnosticar problemas:</span><span class="sxs-lookup"><span data-stu-id="7d42a-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="7d42a-267">Excepciones</span><span class="sxs-lookup"><span data-stu-id="7d42a-267">Exceptions</span></span>
* <span data-ttu-id="7d42a-268">Registros</span><span class="sxs-lookup"><span data-stu-id="7d42a-268">Logs</span></span>
* <span data-ttu-id="7d42a-269">Seguimientos de red</span><span class="sxs-lookup"><span data-stu-id="7d42a-269">Network traces</span></span>

<span data-ttu-id="7d42a-270">Tenga en cuenta que los identificadores de correlación son fundamentales para el diagnóstico en la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7d42a-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="7d42a-271">Puede establecer los identificadores de correlación sujetos a solicitud si desea establecer una correlación de ADAL con otras operaciones en el código.</span><span class="sxs-lookup"><span data-stu-id="7d42a-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="7d42a-272">Si no establece un identificador de correlación, ADAL generará uno aleatorio.</span><span class="sxs-lookup"><span data-stu-id="7d42a-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="7d42a-273">A continuación, todos los mensajes de registro y llamadas de red se marcarán con el identificador de correlación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="7d42a-274">El identificador generado automáticamente se modifica con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="7d42a-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="7d42a-275">Excepciones</span><span class="sxs-lookup"><span data-stu-id="7d42a-275">Exceptions</span></span>
<span data-ttu-id="7d42a-276">Las excepciones son el primer diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7d42a-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="7d42a-277">Intentamos ofrecerle mensajes de error útiles.</span><span class="sxs-lookup"><span data-stu-id="7d42a-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="7d42a-278">Si encuentra alguno que no sea útil, genere un caso y háganoslo saber.</span><span class="sxs-lookup"><span data-stu-id="7d42a-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="7d42a-279">Proporcione también información sobre el dispositivo, por ejemplo, el modelo y el número de SDK.</span><span class="sxs-lookup"><span data-stu-id="7d42a-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="7d42a-280">Registros</span><span class="sxs-lookup"><span data-stu-id="7d42a-280">Logs</span></span>
<span data-ttu-id="7d42a-281">Puede configurar la biblioteca para que genere mensajes de registro que podrá utilizar para diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="7d42a-282">Configure el registro mediante la siguiente llamada para configurar una devolución de llamada que ADAL usará para entregar los mensajes de registro a medida que se generen.</span><span class="sxs-lookup"><span data-stu-id="7d42a-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="7d42a-283">Los mensajes pueden escribirse en un archivo de registro personalizado, tal como se muestra en el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="7d42a-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="7d42a-284">Por desgracia, no hay ninguna manera estándar de obtener los registros de un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="7d42a-285">Hay algunos servicios que pueden ayudar con esta tarea.</span><span class="sxs-lookup"><span data-stu-id="7d42a-285">There are some services that can help you with this.</span></span> <span data-ttu-id="7d42a-286">También puede "inventar" sus propios métodos, como enviar el archivo a un servidor.</span><span class="sxs-lookup"><span data-stu-id="7d42a-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="7d42a-287">Estos son los niveles de registro:</span><span class="sxs-lookup"><span data-stu-id="7d42a-287">These are the logging levels:</span></span>
* <span data-ttu-id="7d42a-288">Error (excepciones)</span><span class="sxs-lookup"><span data-stu-id="7d42a-288">Error (exceptions)</span></span>
* <span data-ttu-id="7d42a-289">Warn (advertencia)</span><span class="sxs-lookup"><span data-stu-id="7d42a-289">Warn (warning)</span></span>
* <span data-ttu-id="7d42a-290">Info (información)</span><span class="sxs-lookup"><span data-stu-id="7d42a-290">Info (information purposes)</span></span>
* <span data-ttu-id="7d42a-291">Verbose (más detalles)</span><span class="sxs-lookup"><span data-stu-id="7d42a-291">Verbose (more details)</span></span>

<span data-ttu-id="7d42a-292">El nivel de registro se define de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="7d42a-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="7d42a-293">Todos los mensajes de registro se envían a logcat, además de las devoluciones de llamada de registro personalizadas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="7d42a-294">Es posible obtener un registro a un archivo de logcat como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="7d42a-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="7d42a-295">Para más información acerca de los comandos de adb, consulte la [información de logcat en el sitio de Android](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="7d42a-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="7d42a-296">Seguimientos de red</span><span class="sxs-lookup"><span data-stu-id="7d42a-296">Network traces</span></span>
<span data-ttu-id="7d42a-297">Puede usar varias herramientas para capturar el tráfico HTTP que genera ADAL.</span><span class="sxs-lookup"><span data-stu-id="7d42a-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="7d42a-298">Esto es muy útil si está familiarizado con el protocolo OAuth o si necesita proporcionar información de diagnóstico a Microsoft o a otros canales de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="7d42a-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="7d42a-299">Fiddler es la herramienta de seguimiento de HTTP más sencilla.</span><span class="sxs-lookup"><span data-stu-id="7d42a-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="7d42a-300">Utilice los vínculos siguientes para configurarla para que registre correctamente el tráfico de red de ADAL.</span><span class="sxs-lookup"><span data-stu-id="7d42a-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="7d42a-301">Para que una herramienta de seguimiento como Fiddler o Charles surta efecto, debe configurarla para registrar tráfico SSL sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="7d42a-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="7d42a-302">Los seguimientos generados de esta manera pueden contener información altamente privilegiada, como tokens de acceso, nombres de usuario y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="7d42a-303">Si utiliza cuentas de producción, no comparta esta información con terceras partes.</span><span class="sxs-lookup"><span data-stu-id="7d42a-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="7d42a-304">Si necesita transmitir el seguimiento a alguien para obtener soporte técnico, reproduzca el problema con una cuenta temporal con nombres de usuario y contraseñas que no le importe compartir.</span><span class="sxs-lookup"><span data-stu-id="7d42a-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="7d42a-305">En el sitio web de Telerik, consulte cómo [configurar Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid).</span><span class="sxs-lookup"><span data-stu-id="7d42a-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="7d42a-306">En GitHub, consulte cómo [configurar reglas de Fiddler para ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler).</span><span class="sxs-lookup"><span data-stu-id="7d42a-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="7d42a-307">Modo de diálogo</span><span class="sxs-lookup"><span data-stu-id="7d42a-307">Dialog mode</span></span>
<span data-ttu-id="7d42a-308">El método acquireToken sin actividad es compatible con el modo de cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="7d42a-309">Cifrado</span><span class="sxs-lookup"><span data-stu-id="7d42a-309">Encryption</span></span>
<span data-ttu-id="7d42a-310">ADAL cifra los tokens y los almacena en SharedPreferences de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7d42a-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="7d42a-311">Puede consultar la clase StorageHelper para ver los detalles.</span><span class="sxs-lookup"><span data-stu-id="7d42a-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="7d42a-312">Android introdujo el almacenamiento seguro de claves privadas AndroidKeyStore 4.3 (API18).</span><span class="sxs-lookup"><span data-stu-id="7d42a-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="7d42a-313">ADAL lo utiliza para API 18 y las versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="7d42a-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="7d42a-314">Si desea usar ADAL para las versiones inferiores de SDK, deberá proporcionar una clave secreta en AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="7d42a-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="7d42a-315">Desafío de portador de Oauth2</span><span class="sxs-lookup"><span data-stu-id="7d42a-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="7d42a-316">La clase AuthenticationParameters proporciona funcionalidad para obtener el authorization_uri a partir del desafío de portador de OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7d42a-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="7d42a-317">Cookies de sesión en WebView</span><span class="sxs-lookup"><span data-stu-id="7d42a-317">Session cookies in WebView</span></span>
<span data-ttu-id="7d42a-318">Android WebView no elimina las cookies de sesión después de cerrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d42a-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="7d42a-319">Esto puede controlarse mediante el siguiente código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7d42a-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="7d42a-320">Para más información acerca de las cookies, consulte la [información sobre CookieSyncManager en el sitio de Android](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="7d42a-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="7d42a-321">Reemplazos de recursos</span><span class="sxs-lookup"><span data-stu-id="7d42a-321">Resource overrides</span></span>
<span data-ttu-id="7d42a-322">La biblioteca de ADAL incluye cadenas en inglés para mensajes de ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="7d42a-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="7d42a-323">La aplicación debe sobrescribirlas si desea ver las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="7d42a-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="7d42a-324">Cuadro de diálogo NTLM</span><span class="sxs-lookup"><span data-stu-id="7d42a-324">NTLM dialog box</span></span>
<span data-ttu-id="7d42a-325">La versión 1.1.0 de ADAL admite el cuadro de diálogo NTLM que se procesa a través del evento onReceivedHttpAuthRequest desde WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="7d42a-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="7d42a-326">Puede personalizar el diseño y las cadenas del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d42a-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="7d42a-327">SSO entre aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7d42a-327">Cross-app SSO</span></span>
<span data-ttu-id="7d42a-328">Obtenga información sobre la [Habilitación de SSO entre aplicaciones en Android mediante ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="7d42a-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
