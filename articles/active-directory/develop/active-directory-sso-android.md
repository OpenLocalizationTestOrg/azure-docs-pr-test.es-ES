---
title: "Habilitación del inicio de sesión único entre aplicaciones en Android mediante ADAL | Microsoft Docs"
description: "Cómo utilizar las características del SDK de ADAL para habilitar el inicio de sesión único entre las aplicaciones. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="d7ec5-103">Habilitación de SSO entre aplicaciones en Android mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="d7ec5-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="d7ec5-104">Los clientes esperan que se proporcione un inicio de sesión único (SSO) para que los usuarios solo tengan que escribir sus credenciales una sola vez y esas credenciales automáticamente funcionen en otras aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="d7ec5-105">La dificultad de escribir el nombre de usuario y contraseña en una pantalla pequeña, a menudo combinado con un factor adicional (2FA) como una llamada de teléfono o un código de mensaje de texto, provoca una rápida insatisfacción si el usuario tiene que hacer esto más de una vez para su producto.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="d7ec5-106">Además, si aplica una plataforma de identidad que puedan usar otras aplicaciones, como cuentas Microsoft o una cuenta de trabajo de Office 365, los clientes esperan que las credenciales estén disponibles para todas sus aplicaciones, independientemente del proveedor.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="d7ec5-107">La plataforma de Microsoft Identity, junto con los SDK correspondientes, se ocupa de este trabajo ingrato y le ofrece la posibilidad de satisfacer a sus clientes con el inicio de sesión único, ya sea dentro de su propio conjunto de aplicaciones o, como sucede con nuestra funcionalidad de agente y las aplicaciones de Authenticator, en todo el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="d7ec5-108">Este tutorial le indicará cómo configurar nuestro SDK dentro de la aplicación para proporcionar esta ventaja a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="d7ec5-109">Este tutorial se aplica a:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="d7ec5-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7ec5-110">Azure Active Directory</span></span>
* <span data-ttu-id="d7ec5-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d7ec5-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="d7ec5-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d7ec5-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="d7ec5-113">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7ec5-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="d7ec5-114">En el documento anterior se considera que tiene conocimientos acerca de cómo [aprovisionar aplicaciones en el portal heredado para Azure Active Directory](active-directory-how-to-integrate.md) y que ha integrado su aplicación con el [SDK de Android de Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="d7ec5-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="d7ec5-115">Conceptos de inicio de sesión único en la plataforma de Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="d7ec5-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="d7ec5-116">Agentes de Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="d7ec5-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="d7ec5-117">Microsoft proporciona aplicaciones para todas las plataformas móviles que permiten el traspaso de credenciales entre aplicaciones de distintos proveedores, y habilita características mejoradas especiales que requieren un único lugar seguro desde el que validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="d7ec5-118">A estas aplicaciones las llamamos **agentes**.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-118">We call these **brokers**.</span></span> <span data-ttu-id="d7ec5-119">En iOS y Android, estos agentes se consiguen a través de aplicaciones descargables que los clientes instalan de forma independiente o bien se insertan en el dispositivo gracias a una empresa que administra el dispositivo de manera total o parcial para sus empleados.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="d7ec5-120">Gracias a estos agentes, es posible administrar la seguridad de solo unas aplicaciones o bien del dispositivo en su totalidad, en función de lo que decidan los administradores de TI.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="d7ec5-121">En Windows, esta funcionalidad se proporciona mediante un selector de cuentas integrado en el sistema operativo, que se conoce técnicamente como agente de autenticación web.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="d7ec5-122">Para más información sobre el uso que hacemos de estos agentes y la percepción que tendrán de ellos sus clientes durante el proceso de inicio de sesión para la plataforma Microsoft Identity, siga leyendo.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="d7ec5-123">Patrones para iniciar sesión en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="d7ec5-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="d7ec5-124">El acceso a credenciales en los dispositivos sigue dos patrones básicos para la plataforma Microsoft Identity:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="d7ec5-125">Inicios de sesión no asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="d7ec5-126">Inicios de sesión asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="d7ec5-127">Inicios de sesión no asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-127">Non-broker assisted logins</span></span>
<span data-ttu-id="d7ec5-128">Los inicios de sesión no asistidos por agente son experiencias de inicio de sesión que ocurren en línea con la aplicación y usan el almacenamiento local en el dispositivo para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="d7ec5-129">Este almacenamiento puede compartirse entre las aplicaciones, pero las credenciales están estrechamente vinculadas a la aplicación o al conjunto de aplicaciones que usan esa credencial.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="d7ec5-130">Probablemente haya experimentado esto en muchas aplicaciones móviles en las que escribe un nombre de usuario y una contraseña en la propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="d7ec5-131">Estos inicios de sesión tienen las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="d7ec5-132">La experiencia de usuario se desarrolla por completo dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="d7ec5-133">Las credenciales se pueden compartir entre aplicaciones que estén firmadas por el mismo certificado, proporcionando una experiencia de inicio de sesión único para el conjunto de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="d7ec5-134">Se proporciona el control de la experiencia de inicio de sesión a la aplicación antes y después del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="d7ec5-135">Estos inicios de sesión tienen las siguientes desventajas:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="d7ec5-136">El usuario no puede experimentar el inicio de sesión único entre todas las aplicaciones que usan una identidad de Microsoft Identity, solo en aquellas identidades de Microsoft Identity que su aplicación ha configurado.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="d7ec5-137">La aplicación no se puede usar con las características empresariales más avanzadas, como el acceso condicional, ni utilizar el conjunto de aplicaciones de InTune.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="d7ec5-138">La aplicación no admite la autenticación basada en certificados para usuarios empresariales.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="d7ec5-139">A continuación se representa el funcionamiento de los SDK de Microsoft Identity con el almacenamiento compartido de sus aplicaciones para habilitar el inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="d7ec5-140">Inicios de sesión asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-140">Broker assisted logins</span></span>
<span data-ttu-id="d7ec5-141">Los inicios de sesión asistidos por agente son experiencias de inicio de sesión que se producen dentro de la aplicación del agente y usan el almacenamiento y la seguridad del agente para compartir las credenciales entre todas las aplicaciones del dispositivo que se aplican a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="d7ec5-142">Esto significa que las aplicaciones dependen del agente para que los usuarios inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="d7ec5-143">En iOS y Android, estos agentes se consiguen a través de aplicaciones descargables que los clientes instalan de forma independiente o bien se insertan en el dispositivo gracias a una empresa que administra el dispositivo para sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="d7ec5-144">Un ejemplo de este tipo de aplicación es la aplicación Microsoft Authenticator en iOS.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="d7ec5-145">En Windows, esta funcionalidad se proporciona mediante un selector de cuentas integrado en el sistema operativo, que se conoce técnicamente como agente de autenticación web.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="d7ec5-146">La experiencia varía según la plataforma y a veces puede ser problemática para los usuarios si no se administra correctamente.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="d7ec5-147">Quizá este modelo le resulte más familiar si tiene instalada la aplicación Facebook y usa Facebook Connect desde otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="d7ec5-148">La plataforma Microsoft Identity utiliza este mismo modelo.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="d7ec5-149">En el caso de iOS, esto da lugar a una animación de "transición" en la que la aplicación se envía a un segundo plano y las aplicaciones de Microsoft Authenticator vienen al primer plano para que el usuario seleccione la cuenta en la que quiere iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="d7ec5-150">En el caso de Android y Windows, el selector de cuentas se muestra sobre la aplicación, lo cual interrumpe menos la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="d7ec5-151">¿Cómo se invoca el agente?</span><span class="sxs-lookup"><span data-stu-id="d7ec5-151">How the broker gets invoked</span></span>
<span data-ttu-id="d7ec5-152">Si se instala un agente compatible en el dispositivo, como la aplicación Microsoft Authenticator, los SDK de Microsoft Identity se ocuparán automáticamente de la tarea de invocar al agente cuando un usuario indique que quiere iniciar sesión con alguna de las cuentas de la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="d7ec5-153">Esta cuenta podría tratarse de una cuenta personal de Microsoft, una cuenta profesional o educativa o una cuenta que especifique y hospede en Azure mediante nuestros productos B2C y B2B.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="d7ec5-154">Cómo se garantiza que la aplicación es válida</span><span class="sxs-lookup"><span data-stu-id="d7ec5-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="d7ec5-155">La necesidad de asegurar la identidad de una llamada de la aplicación al agente es fundamental para la seguridad que proporcionamos en los inicios de sesión asistidos por agente.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="d7ec5-156">Ni IOS ni Android exigen identificadores únicos que solo son válidos para una aplicación determinada, por lo que aplicaciones malintencionadas pueden "suplantar" un identificador de la aplicación legítima y recibir los tokens destinados a la aplicación legítima.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="d7ec5-157">Para asegurarse de que siempre se comunica con la aplicación correcta en tiempo de ejecución, le pedimos al desarrollador que proporcione un redirectURI personalizado al registrar su aplicación con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="d7ec5-158">**A continuación se describe cómo deben diseñar los desarrolladores este URI de redirección.**</span><span class="sxs-lookup"><span data-stu-id="d7ec5-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="d7ec5-159">Este URI de redirección personalizado contiene la huella digital del certificado de la aplicación y se asegura de que es único para la aplicación por Google Play Store.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="d7ec5-160">Cuando una aplicación llama el agente, este solicita al sistema de operativo Android que le proporcione la huella digital del certificado que llama el agente.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="d7ec5-161">El agente proporciona esta huella digital del certificado a Microsoft en la llamada a nuestro sistema de identidad.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="d7ec5-162">Si la huella digital del certificado de la aplicación no coincide con la huella digital del certificado proporcionada por el desarrollador durante el registro, se denegará el acceso a los tokens para el recurso que está solicitando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="d7ec5-163">Esta comprobación asegura que solo la aplicación registrada por el desarrollador recibe los tokens.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="d7ec5-164">**El desarrollador tiene la opción de elegir si el SDK de Microsoft Identity llama al agente o usa el flujo sin asistencia del agente.**</span><span class="sxs-lookup"><span data-stu-id="d7ec5-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="d7ec5-165">Sin embargo, si el desarrollador decide no usar el flujo asistido por agente, no podrá beneficiarse del uso de las credenciales de SSO que el usuario puede ya haber agregado en el dispositivo; además, impide que la aplicación se use con las características empresariales que Microsoft proporciona a sus clientes, como el acceso condicional, las funcionalidades de administración de Intune y la autenticación basada en certificados.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="d7ec5-166">Estos inicios de sesión tienen las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="d7ec5-167">El usuario experimenta el inicio de sesión único en todas sus aplicaciones, con independencia del proveedor.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="d7ec5-168">La aplicación puede usar las características empresariales más avanzadas, como el acceso condicional, o usar el conjunto de productos de InTune.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="d7ec5-169">La aplicación puede admitir la autenticación basada en certificados para los usuarios empresariales.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="d7ec5-170">La experiencia de inicio de sesión es mucho más segura, ya que tanto la identidad de la aplicación como el usuario se verifican por parte de la aplicación de agente con algoritmos de seguridad y sistemas de cifrado adicionales.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="d7ec5-171">Estos inicios de sesión tienen las siguientes desventajas:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="d7ec5-172">En iOS, el usuario pasa por un proceso externo a la experiencia de la aplicación mientras se eligen las credenciales.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="d7ec5-173">Se pierde la capacidad de administrar la experiencia de inicio de sesión para los clientes dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="d7ec5-174">A continuación se representa el funcionamiento de los SDK de Microsoft Identity con las aplicaciones de agente para habilitar el inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="d7ec5-175">Una vez que disponga de toda esta información, probablemente pueda entender e implementar mejor el inicio de sesión único en la aplicación mediante los SDK y la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="d7ec5-176">Habilitación del SSO entre aplicaciones mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="d7ec5-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="d7ec5-177">Ahora vamos a usar el SDK de Android de ADAL para:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="d7ec5-178">Activar el SSO no asistido por agente para su conjunto de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d7ec5-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="d7ec5-179">Activar la compatibilidad para el SSO asistido por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="d7ec5-180">Activación del SSO para el SSO no asistido por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="d7ec5-181">En el caso del SSO entre aplicaciones no asistido por agente, los SDK de Microsoft Identity administran automáticamente gran parte de la complejidad que entraña este proceso.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="d7ec5-182">Esto incluye la búsqueda del usuario adecuado en la memoria caché y el mantenimiento de una lista de usuarios que han iniciado sesión en la que se pueden realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="d7ec5-183">Para habilitar el SSO entre aplicaciones de las que es el propietario debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="d7ec5-184">Garantizar que todas las aplicaciones utilizan el mismo identificador de cliente o aplicación</span><span class="sxs-lookup"><span data-stu-id="d7ec5-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="d7ec5-185">Garantizar que todas las aplicaciones tienen el mismo conjunto de SharedUserID.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="d7ec5-186">Garantizar que todas las aplicaciones comparten el mismo certificado de firma de Google Play Store para que puedan compartir el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="d7ec5-187">Paso 1: Uso del mismo identificador de cliente o aplicación para todas las aplicaciones de su conjunto</span><span class="sxs-lookup"><span data-stu-id="d7ec5-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="d7ec5-188">A fin de que la plataforma Microsoft Identity sepa que puede compartir tokens entre las aplicaciones, es necesario que todas ellas compartan el mismo identificador de cliente o aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="d7ec5-189">Se trata del identificador único que se le suministró al registrar su primera aplicación en el portal.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="d7ec5-190">Quizás se pregunte cómo se puede identificar a las diferentes aplicaciones en el servicio Microsoft Identity si todas utilizan el mismo identificador.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="d7ec5-191">Pues bien, esto es posible gracias a los **URI de redirección**.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="d7ec5-192">Cada aplicación puede tener varios URI de redirección registrados en el portal de incorporación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="d7ec5-193">Cada una de las aplicaciones de su conjunto tendrá diferentes URI de redirección.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="d7ec5-194">A continuación se muestra un ejemplo típico de su aspecto:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-194">An example of how this looks is below:</span></span>

<span data-ttu-id="d7ec5-195">URI de redirección de la aplicación 1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="d7ec5-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="d7ec5-196">URI de redirección de la aplicación 2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="d7ec5-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="d7ec5-197">URI de redirección de la aplicación 3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="d7ec5-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="d7ec5-198">....</span><span class="sxs-lookup"><span data-stu-id="d7ec5-198">....</span></span>

<span data-ttu-id="d7ec5-199">Estos están anidados en el mismo identificador de cliente o aplicación y se consultan en función del URI de redirección que nos devuelve en su configuración del SDK.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="d7ec5-200">*Tenga en cuenta que el formato de estos URI de redirección se explica a continuación. Puede usar cualquier URI de redirección, a menos que desee utilizar el agente, en cuyo caso debe tener un aspecto como el anterior*</span><span class="sxs-lookup"><span data-stu-id="d7ec5-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="d7ec5-201">Paso 2: Configuración del almacenamiento compartido en Android</span><span class="sxs-lookup"><span data-stu-id="d7ec5-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="d7ec5-202">La definición de `SharedUserID` está fuera del ámbito de este documento, pero se puede aprender en la documentación de Google Android, en el [Manifiesto](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="d7ec5-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="d7ec5-203">Lo importante es que decida cómo desea llamar a su sharedUserID y usar ese nombre en todas sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="d7ec5-204">Una vez que tiene `SharedUserID` en todas las aplicaciones, estará listo para utilizar SSO.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="d7ec5-205">Cuando se comparte un almacenamiento entre aplicaciones, cualquiera de ellas puede eliminar usuarios o, peor aún, eliminar todos los tokens de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="d7ec5-206">Esto puede resultar especialmente problemático si tiene aplicaciones que dependen de los tokens para hacer el trabajo en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="d7ec5-207">Compartir un almacenamiento implica ser muy cuidadoso en todas y cada una de las operaciones de eliminación realizadas a través de los SDK de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="d7ec5-208">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-208">That's it!</span></span> <span data-ttu-id="d7ec5-209">El SDK de Microsoft Identity ahora compartirá las credenciales entre todas sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="d7ec5-210">La lista de usuarios también se compartirá entre las instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="d7ec5-211">Activación del SSO para el SSO asistido por agente</span><span class="sxs-lookup"><span data-stu-id="d7ec5-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="d7ec5-212">La capacidad de una aplicación de usar cualquier agente que esté instalado en el dispositivo está **desactivada de forma predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="d7ec5-213">Para poder utilizar la aplicación con el agente debe realizar algunos pasos de configuración adicionales y agregar código a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="d7ec5-214">Los pasos que debe seguir son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-214">The steps to follow are:</span></span>

1. <span data-ttu-id="d7ec5-215">Habilitar el modo de agente en la llamada al código de la aplicación para el SDK de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d7ec5-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="d7ec5-216">Establecer un nuevo URI de redirección e indicarlo tanto en la aplicación como en el registro de la aplicación</span><span class="sxs-lookup"><span data-stu-id="d7ec5-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="d7ec5-217">Configurar los permisos correctos en el manifiesto de Android</span><span class="sxs-lookup"><span data-stu-id="d7ec5-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="d7ec5-218">Paso 1: Habilitar el modo de agente en la aplicación</span><span class="sxs-lookup"><span data-stu-id="d7ec5-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="d7ec5-219">La capacidad de la aplicación de utilizar el agente se activa al crear la configuración inicial de la instancia de autenticación.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="d7ec5-220">Para ello, configure el tipo de ApplicationSettings en el código:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="d7ec5-221">Paso 2: Establecer un nuevo URI de redirección con el esquema de dirección URL</span><span class="sxs-lookup"><span data-stu-id="d7ec5-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="d7ec5-222">Para garantizar que siempre se devuelvan los tokens de credencial a la aplicación correcta, es necesario asegurarse de que se llama a la aplicación de tal manera que el sistema operativo Android pueda verificarla.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="d7ec5-223">El sistema operativo Android utiliza el hash del certificado en Google Play Store.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="d7ec5-224">Este sistema no se puede suplantar por ninguna aplicación malintencionada.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="d7ec5-225">Por lo tanto, se aprovecha este elemento junto con el URI de la aplicación de agente para garantizar que los tokens se devuelven a la aplicación correcta.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="d7ec5-226">Es necesario establecer este URI de redirección único en la aplicación y configurarlo como URI de redirección en nuestro portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="d7ec5-227">Para ser correcto, el URI de redirección debe presentar el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="d7ec5-228">Por ejemplo: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="d7ec5-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="d7ec5-229">Este URI de redirección debe especificarse en el registro de la aplicación mediante [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d7ec5-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d7ec5-230">Para más información sobre el registro de aplicaciones de Azure AD, consulte [Integración con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="d7ec5-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="d7ec5-231">Paso 3: Configurar los permisos correctos en la aplicación</span><span class="sxs-lookup"><span data-stu-id="d7ec5-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="d7ec5-232">Nuestra aplicación de agente en Android utiliza la característica de administrador de cuentas del SO Android para administrar las credenciales entre aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="d7ec5-233">Para utilizar el agente en Android el manifiesto de la aplicación debe tener permisos para usar cuentas del administrador de cuentas.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="d7ec5-234">Esto se explica en detalle en la [documentación de Google para el administrador de cuentas que puede encontrar aquí](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="d7ec5-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="d7ec5-235">En concreto, estos permisos son:</span><span class="sxs-lookup"><span data-stu-id="d7ec5-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="d7ec5-236">Ya ha configurado el SSO.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-236">You've configured SSO!</span></span>
<span data-ttu-id="d7ec5-237">Ahora, el SDK de Microsoft Identity compartirá automáticamente las credenciales entre las aplicaciones e invocará al agente si está presente en su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7ec5-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

