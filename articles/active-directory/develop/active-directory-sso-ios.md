---
title: "aaaHow tooenable SSO de aplicación cruzado en iOS mediante AAL | Documentos de Microsoft"
description: "¿Cómo toouse características de Hola de Hola SDK AAL tooenable inicio de sesión único a través de las aplicaciones. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="6b259-103">¿Cómo tooenable SSO de aplicación cruzado en iOS mediante AAL</span><span class="sxs-lookup"><span data-stu-id="6b259-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="6b259-104">Ahora se espera que proporciona el inicio de sesión único (SSO) para que los usuarios solo necesitan tooenter sus credenciales una vez y tienen esas credenciales profesional automáticamente en todas las aplicaciones por los clientes.</span><span class="sxs-lookup"><span data-stu-id="6b259-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="6b259-105">dificultad Hola escribir su nombre de usuario y contraseña en una pantalla pequeña, a menudo veces se combinan con un factor adicional (2FA) como una llamada de teléfono o un código de mensajes de texto, resultados de insatisfacción rápido si un usuario tiene toodo esto más de una vez para el producto.</span><span class="sxs-lookup"><span data-stu-id="6b259-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="6b259-106">Además, si aplica una plataforma de identidad que pueden utilizar otras aplicaciones como Microsoft Accounts o una cuenta profesional de Office 365, los clientes esperan que dichos toouse disponible toobe de credenciales en todas sus aplicaciones ya no importa proveedor Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="6b259-107">Hello plataforma de Microsoft Identity, junto con nuestro SDK de identidad de Microsoft funciona todo esto disco duro para usted y proporciona Hola capacidad toodelight con SSO, ya sea dentro de su propio conjunto de aplicaciones o, como los clientes con nuestro agente capacidad y el autenticador aplicaciones, a través de dispositivo completo Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="6b259-108">Este tutorial le indicará cómo tooconfigure nuestro SDK dentro de su aplicación tooprovide esta tooyour beneficio que los clientes.</span><span class="sxs-lookup"><span data-stu-id="6b259-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="6b259-109">Este tutorial se aplica a:</span><span class="sxs-lookup"><span data-stu-id="6b259-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="6b259-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b259-110">Azure Active Directory</span></span>
* <span data-ttu-id="6b259-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="6b259-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="6b259-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="6b259-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="6b259-113">Acceso condicional de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b259-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="6b259-114">documento de Hello anterior se supone que sabe cómo demasiado[aprovisionar aplicaciones en portal heredado de Hola para Azure Active Directory](active-directory-how-to-integrate.md) y la aplicación integrada con hello [SDK de iOS de Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="6b259-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="6b259-115">Conceptos de SSO en hello plataforma de identidad de Microsoft</span><span class="sxs-lookup"><span data-stu-id="6b259-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="6b259-116">Agentes de Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="6b259-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="6b259-117">Microsoft proporciona a las aplicaciones para todas las plataformas móviles que permiten Hola puentes de credenciales en todas las aplicaciones de diferentes proveedores y admite características mejoradas especiales que requieren un único lugar seguro desde donde toovalidate credenciales.</span><span class="sxs-lookup"><span data-stu-id="6b259-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="6b259-118">A estas aplicaciones las llamamos **agentes**.</span><span class="sxs-lookup"><span data-stu-id="6b259-118">We call these **brokers**.</span></span> <span data-ttu-id="6b259-119">En iOS y Android estos agentes se proporcionan a través de aplicaciones que se pueden descargar que los clientes instalación de forma independiente o se pueden insertar toohello dispositivo por una compañía que administra algunos o todos los dispositivos de Hola para sus empleados.</span><span class="sxs-lookup"><span data-stu-id="6b259-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="6b259-120">Estos agentes admiten la administración de seguridad solo para algunas aplicaciones o dispositivo completo hello en función de lo que los administradores de TI desea.</span><span class="sxs-lookup"><span data-stu-id="6b259-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="6b259-121">En Windows, esta funcionalidad se proporciona mediante un selector de la cuenta integrada en el sistema de operativo toohello, técnicamente conocido como Hola Broker de autenticación Web.</span><span class="sxs-lookup"><span data-stu-id="6b259-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="6b259-122">Para obtener más información acerca de cómo se utilizan estos agentes y cómo los clientes pueden verlas en su flujo de inicio de sesión para la plataforma de Microsoft Identity Hola de lectura en.</span><span class="sxs-lookup"><span data-stu-id="6b259-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="6b259-123">Patrones para iniciar sesión en dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="6b259-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="6b259-124">Toocredentials de acceso en los dispositivos siga dos patrones básicos para la plataforma de Microsoft Identity hello:</span><span class="sxs-lookup"><span data-stu-id="6b259-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="6b259-125">Inicios de sesión no asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="6b259-126">Inicios de sesión asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="6b259-127">Inicios de sesión no asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-127">Non-broker assisted logins</span></span>
<span data-ttu-id="6b259-128">Los inicios de sesión del agente no asistidas son experiencias de inicio de sesión que se realizan en línea con la aplicación hello y usar el almacenamiento local de hello en dispositivo Hola para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="6b259-129">Este almacenamiento puede compartirse en todas las aplicaciones pero credenciales Hola están estrechamente toohello aplicación o conjunto de aplicaciones con esa credencial.</span><span class="sxs-lookup"><span data-stu-id="6b259-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="6b259-130">Probablemente ha experimentado esto en muchas aplicaciones móviles al escribir un nombre de usuario y contraseña en la propia aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="6b259-131">Estos inicios de sesión tienen Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6b259-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="6b259-132">Experiencia del usuario existe completamente dentro de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6b259-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="6b259-133">Las credenciales se pueden compartir entre las aplicaciones que están firmadas por hello mismo certificado, lo que proporciona un conjunto de tooyour de la experiencia de inicio de sesión único de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b259-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="6b259-134">Control alrededor de la experiencia de hello del inicio de sesión se proporciona toohello aplicación antes y después del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6b259-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="6b259-135">Estos inicios de sesión tienen Hola siguientes desventajas:</span><span class="sxs-lookup"><span data-stu-id="6b259-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="6b259-136">El usuario no puede experimentar el inicio de sesión único entre todas las aplicaciones que usan una identidad de Microsoft Identity, solo en aquellas identidades de Microsoft Identity que su aplicación ha configurado.</span><span class="sxs-lookup"><span data-stu-id="6b259-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="6b259-137">La aplicación no se puede usar con las características más avanzadas de negocios como acceso condicional o use Hola InTune conjunto de productos.</span><span class="sxs-lookup"><span data-stu-id="6b259-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="6b259-138">La aplicación no admite la autenticación basada en certificados para usuarios empresariales.</span><span class="sxs-lookup"><span data-stu-id="6b259-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="6b259-139">Aquí es una representación de cómo funcionan los SDK de identidad de Microsoft hello con almacenamiento de hello compartido de su tooenable aplicaciones SSO:</span><span class="sxs-lookup"><span data-stu-id="6b259-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="6b259-140">Inicios de sesión asistidos por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-140">Broker assisted logins</span></span>
<span data-ttu-id="6b259-141">Asistido por el agente de inicios de sesión son experiencias de inicio de sesión que se producen dentro de la aplicación de broker de hello y utilizar almacenamiento de Hola y seguridad de credenciales de hello broker tooshare en todas las aplicaciones en dispositivos de Hola que se aplican de la plataforma de Microsoft Identity Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="6b259-142">Esto significa que las aplicaciones dependen de los usuarios de hello broker toosign en.</span><span class="sxs-lookup"><span data-stu-id="6b259-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="6b259-143">En iOS y Android estos agentes se proporcionan a través de aplicaciones que se pueden descargar que los clientes instalación de forma independiente o se pueden insertar toohello dispositivo por una compañía que administra el dispositivo de hello para el usuario.</span><span class="sxs-lookup"><span data-stu-id="6b259-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="6b259-144">Un ejemplo de este tipo de aplicación es la aplicación de Microsoft Authenticator hello en iOS.</span><span class="sxs-lookup"><span data-stu-id="6b259-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="6b259-145">En Windows, esta funcionalidad se proporciona mediante un selector de la cuenta integrada en el sistema de operativo toohello, técnicamente conocido como Hola Broker de autenticación Web.</span><span class="sxs-lookup"><span data-stu-id="6b259-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="6b259-146">experiencia de Hello varía según la plataforma y a veces puede ser perjudiciales toousers si no administra correctamente.</span><span class="sxs-lookup"><span data-stu-id="6b259-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="6b259-147">Es probablemente más familiarizado con este patrón si tiene instalada la aplicación de Facebook de Hola y usar Facebook Connect desde otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="6b259-148">Hello usa de la plataforma de Microsoft Identity Hola mismo patrón.</span><span class="sxs-lookup"><span data-stu-id="6b259-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="6b259-149">Para iOS Esto conduce animación de "transición" tooa donde la aplicación se envía a toohello fondo mientras las aplicaciones de Microsoft Authenticator Hola procede de primer plano de toohello para hello usuario tooselect qué cuenta preferirían toosign con.</span><span class="sxs-lookup"><span data-stu-id="6b259-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="6b259-150">Android y Windows cuenta Hola selector se muestra encima de la aplicación que es menos problemática toohello al usuario.</span><span class="sxs-lookup"><span data-stu-id="6b259-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="6b259-151">¿Cómo se invoca broker Hola</span><span class="sxs-lookup"><span data-stu-id="6b259-151">How hello broker gets invoked</span></span>
<span data-ttu-id="6b259-152">Si está instalado un agente compatible en dispositivos de hello, que configurará automáticamente y Hola aplicación Microsoft Authenticator, Hola SDK de identidad de Microsoft Hola trabajo de invocar broker Hola automáticamente cuando un usuario indica que hubieran querido toolog con cualquier cuenta de plataforma de Microsoft Identity Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="6b259-153">Esta cuenta podría tratarse de una cuenta personal de Microsoft, una cuenta profesional o educativa o una cuenta que especifique y hospede en Azure mediante nuestros productos B2C y B2B.</span><span class="sxs-lookup"><span data-stu-id="6b259-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="6b259-154">Cómo garantizamos que la aplicación hello es válido</span><span class="sxs-lookup"><span data-stu-id="6b259-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="6b259-155">identidad de Hello necesidad tooensure Hola de un agente de Hola de llamada de aplicación es toohello fundamental para la seguridad por que se proporcionan en los inicios de sesión de agente asistida.</span><span class="sxs-lookup"><span data-stu-id="6b259-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="6b259-156">IOS ni Android exige identificadores únicos que solo son válidos para una aplicación determinada, por lo que pueden "Suplantar" identificador de la aplicación legítimo y reciben los testigos de hello destinados a la aplicación legítima Hola aplicaciones malintencionadas.</span><span class="sxs-lookup"><span data-stu-id="6b259-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="6b259-157">tooensure que siempre se comunica con la aplicación correcta de hello en tiempo de ejecución, le pedimos Hola developer tooprovide un redirectURI personalizado al registrar su aplicación con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6b259-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="6b259-158">**A continuación se describe cómo los desarrolladores deben diseñar este URI de redirección.**</span><span class="sxs-lookup"><span data-stu-id="6b259-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="6b259-159">Este redirectURI personalizado contiene Hola identificador de paquete de aplicación hello y está garantizada toobe toohello única aplicación por hello App Store de Apple.</span><span class="sxs-lookup"><span data-stu-id="6b259-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="6b259-160">Cuando un agente de Hola de llamadas de aplicación, agente de hello solicita Hola iOS tooprovide de sistema de operativo Hola con Id. del lote que llama broker Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="6b259-161">broker de Hello proporciona esta tooMicrosoft Id. del lote en el sistema de identidades de hello llamada tooour.</span><span class="sxs-lookup"><span data-stu-id="6b259-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="6b259-162">Si Hola identificador de paquete de aplicación hello no coincide con Id. del lote proporcionado toous desarrollador Hola durante el registro de hello, se denegará el acceso toohello tokens para hello recursos Hola aplicación está solicitando.</span><span class="sxs-lookup"><span data-stu-id="6b259-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="6b259-163">Esta comprobación garantiza que sólo las aplicación hello registrada por el desarrollador de hello recibe los tokens.</span><span class="sxs-lookup"><span data-stu-id="6b259-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="6b259-164">**desarrollador de Hello tiene elección Hola de si Hola SDK de Microsoft Identity llama a broker Hola o usa flujo asistida de hello no es del agente.**</span><span class="sxs-lookup"><span data-stu-id="6b259-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="6b259-165">Sin embargo si el desarrollador de hello elige no flujo asistidas por el agente de Hola de toouse pierden ventaja de hello del uso de credenciales de SSO que el usuario Hola puedas haber agregado ya en el dispositivo de Hola e impide que su aplicación que se va a usar con las características de business Microsoft proporciona a los clientes, como el acceso condicional y capacidades de administración de Intune, autenticación basada en certificados.</span><span class="sxs-lookup"><span data-stu-id="6b259-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="6b259-166">Estos inicios de sesión tienen Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6b259-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="6b259-167">Usuario experimenta SSO a través de todas sus aplicaciones, independientemente del proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="6b259-168">La aplicación puede utilizar las características más avanzadas de negocio, como el acceso condicional o conjunto de productos de hello InTune.</span><span class="sxs-lookup"><span data-stu-id="6b259-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="6b259-169">La aplicación puede admitir la autenticación basada en certificados para los usuarios empresariales.</span><span class="sxs-lookup"><span data-stu-id="6b259-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="6b259-170">Inicio de sesión mucho más segura de experimentar como identidad de Hola de aplicación hello y usuario Hola se comprobó por aplicación de broker de hello con algoritmos de seguridad adicional y el cifrado.</span><span class="sxs-lookup"><span data-stu-id="6b259-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="6b259-171">Estos inicios de sesión tienen Hola siguientes desventajas:</span><span class="sxs-lookup"><span data-stu-id="6b259-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="6b259-172">En iOS usuario Hola pasa fuera de la experiencia de su aplicación mientras se eligen las credenciales.</span><span class="sxs-lookup"><span data-stu-id="6b259-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="6b259-173">Pérdida de inicio de sesión de hello capacidad toomanage Hola experiencia para sus clientes dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="6b259-174">Aquí es una representación de cómo de trabajo del SDK de identidad de Microsoft de hello con hello broker tooenable aplicaciones SSO:</span><span class="sxs-lookup"><span data-stu-id="6b259-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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

<span data-ttu-id="6b259-175">Gracias a esta información debe ser capaz de toobetter comprender e implementar SSO dentro de la aplicación con la plataforma de Microsoft Identity hello y SDK.</span><span class="sxs-lookup"><span data-stu-id="6b259-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="6b259-176">Habilitación del SSO entre aplicaciones mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="6b259-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="6b259-177">Aquí usamos hello, iOS AAL SDK para:</span><span class="sxs-lookup"><span data-stu-id="6b259-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="6b259-178">Activar el SSO no asistido por agente para su conjunto de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6b259-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="6b259-179">Activar la compatibilidad para el SSO asistido por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="6b259-180">Activación del SSO para el SSO no asistido por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="6b259-181">Para no es del agente asistida SSO en todas las aplicaciones Hola SDK de identidad de Microsoft administra gran parte de la complejidad de Hola de SSO por usted.</span><span class="sxs-lookup"><span data-stu-id="6b259-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="6b259-182">Esto incluye Buscar usuario hello en memoria caché de Hola y mantiene una lista de usuarios tooquery ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="6b259-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="6b259-183">tooenable SSO en todas las aplicaciones que usted es el propietario que debe hello toodo después de:</span><span class="sxs-lookup"><span data-stu-id="6b259-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="6b259-184">Asegúrese de todos los el saludo del usuario aplicaciones mismo Id. de cliente o el identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="6b259-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="6b259-185">Asegúrese de que todos los Hola de recurso compartido de aplicaciones misma firma de certificado de Apple para que puedan compartir llaves</span><span class="sxs-lookup"><span data-stu-id="6b259-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="6b259-186">Solicitar Hola mismo derecho de cadena de claves para cada una de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b259-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="6b259-187">Explíquenos SDK de identidad de Microsoft de Hola Hola compartido llaveros que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="6b259-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="6b259-188">Usar Hola mismo Id. de cliente / Id. de aplicación para todas las aplicaciones en el conjunto de aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="6b259-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="6b259-189">Para tooknow de plataforma de Microsoft Identity Hola que se permite tooshare símbolos (tokens) a través de las aplicaciones, cada una de las aplicaciones necesitará tooshare Hola mismo Id. de cliente o el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="6b259-190">Se trata de un identificador único de Hola que se proporcionó tooyou cuando registra su primera aplicación de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="6b259-191">Quizás se pregunte cómo identificará las diferentes aplicaciones toohello servicio de Microsoft Identity si utiliza Hola el mismo identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="6b259-192">es la respuesta a Hola con hello **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="6b259-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="6b259-193">Cada aplicación puede tener varios URI de redireccionamiento registrado en el portal de incorporación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="6b259-194">Cada una de las aplicaciones de su conjunto tendrá diferentes URI de redirección.</span><span class="sxs-lookup"><span data-stu-id="6b259-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="6b259-195">A continuación se muestra un ejemplo típico de su aspecto:</span><span class="sxs-lookup"><span data-stu-id="6b259-195">An example of how this looks is below:</span></span>

<span data-ttu-id="6b259-196">URI de redirección de la aplicación 1: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="6b259-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="6b259-197">URI de redirección de la aplicación 2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="6b259-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="6b259-198">URI de redirección de la aplicación 3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="6b259-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="6b259-199">....</span><span class="sxs-lookup"><span data-stu-id="6b259-199">....</span></span>

<span data-ttu-id="6b259-200">Estos se anidan debajo de Hola el mismo Id. de cliente / volver toous en la configuración del SDK de URI de redireccionamiento de Id. de aplicación y buscada Hola según.</span><span class="sxs-lookup"><span data-stu-id="6b259-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="6b259-201">*Tenga en cuenta que el formato de estos URI de redireccionamiento de Hola se explican a continuación. Puede usar cualquier URI de redireccionamiento a menos que se desea que el agente de hello toosupport, en cuyo caso debe ser similar a Hola anterior*</span><span class="sxs-lookup"><span data-stu-id="6b259-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="6b259-202">Permitir el uso compartido de llaveros entre aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6b259-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="6b259-203">Habilitar uso compartido está más allá del ámbito de Hola de este documento y cubierto por Apple en el documento [agregar capacidades](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="6b259-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="6b259-204">Lo importante es que decidir la acción que realizará su toobe de cadena de claves denominado y agregar esa capacidad a través de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b259-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="6b259-205">Cuando el usuario tiene derechos configurados correctamente, deberían ver un archivo en el directorio del proyecto titulada " `entitlements.plist` que contiene algo similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="6b259-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="6b259-206">Una vez que tiene derechos de cadena de claves de hello habilitado en cada una de las aplicaciones, y está listo toouse SSO, explíquenos Hola SDK de Microsoft Identity su cadena de claves mediante el uso de hello después de la configuración en su `ADAuthenticationSettings` con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="6b259-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="6b259-207">Cuando se comparte una cadena de claves a través de las aplicaciones de cualquier aplicación puede eliminar usuarios o lo que es peor eliminar todos los tokens de Hola a través de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="6b259-208">Esto es especialmente desastroso si tiene aplicaciones que se basan en el trabajo en segundo plano toodo Hola símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="6b259-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="6b259-209">Uso compartido de una cadena de claves significa que debe ser mucho cuidado en todos los quite las operaciones a través de SDK de identidad de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="6b259-210">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="6b259-210">That's it!</span></span> <span data-ttu-id="6b259-211">Hola SDK de Microsoft Identity ahora compartirán las credenciales en todas sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b259-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="6b259-212">lista de usuarios de Hello también se compartirán entre instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="6b259-213">Activación del SSO para el SSO asistido por agente</span><span class="sxs-lookup"><span data-stu-id="6b259-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="6b259-214">Hola la posibilidad de que un toouse de aplicación es cualquier agente que está instalada en el dispositivo de hello **está desactivada de forma predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="6b259-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="6b259-215">En Ordenar toouse su aplicación con el agente de hello debe hacer alguna configuración adicional y agregar alguna aplicación tooyour de código.</span><span class="sxs-lookup"><span data-stu-id="6b259-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="6b259-216">Hola pasos toofollow son:</span><span class="sxs-lookup"><span data-stu-id="6b259-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="6b259-217">Habilitar el modo de broker en toohello de llamada del código de la aplicación MS SDK.</span><span class="sxs-lookup"><span data-stu-id="6b259-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="6b259-218">Establecer un nuevo URI de redireccionamiento y proporcionar esa aplicación de hello tooboth y el registro de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b259-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="6b259-219">Registrar un esquema de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="6b259-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="6b259-220">compatibilidad con iOS9: agregar un archivo info.plist de tooyour de permisos.</span><span class="sxs-lookup"><span data-stu-id="6b259-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="6b259-221">Paso 1: Habilitar el modo de agente en la aplicación</span><span class="sxs-lookup"><span data-stu-id="6b259-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="6b259-222">capacidad de Hello para el agente de hello toouse de aplicación está activado cuando creas Hola "context" o la instalación inicial de su objeto de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6b259-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="6b259-223">Para ello, configure el tipo de credenciales en el código:</span><span class="sxs-lookup"><span data-stu-id="6b259-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="6b259-224">Hola `AD_CREDENTIALS_AUTO` configuración permitirá Hola SDK de Microsoft Identity tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` evitará Hola SDK de Microsoft Identity de la llamada a toohello broker.</span><span class="sxs-lookup"><span data-stu-id="6b259-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="6b259-225">Paso 2: Registrar un esquema de dirección URL</span><span class="sxs-lookup"><span data-stu-id="6b259-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="6b259-226">plataforma de Microsoft Identity Hello usa broker de direcciones URL tooinvoke hello y control vuelva atrás tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="6b259-227">toofinish que necesita un esquema de dirección URL de ida y registrado para la aplicación que Hola conoce plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="6b259-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="6b259-228">Esto puede ser además tooany otros esquemas de aplicación puede haber registrado previamente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="6b259-229">Se recomienda realizar Hola posibilidades de Hola de dirección URL esquema toominimize bastante único de otra aplicación usando Hola mismo esquema de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="6b259-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="6b259-230">Apple no exigir la exclusividad de Hola de esquemas de direcciones URL que están registrados en la tienda de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="6b259-231">A continuación, se muestra un ejemplo del aspecto que podría tener esto en la configuración de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="6b259-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="6b259-232">También es posible hacerlo en XCode del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6b259-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="6b259-233">Paso 3: Establecer un nuevo URI de redirección con el esquema de dirección URL</span><span class="sxs-lookup"><span data-stu-id="6b259-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="6b259-234">En orden tooensure que devolvemos siempre credenciales Hola tokens toohello de aplicación correcto, necesitamos toomake seguro que se devuelva la llamada puede comprobar la aplicación tooyour de forma que Hola de sistema operativo iOS.</span><span class="sxs-lookup"><span data-stu-id="6b259-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="6b259-235">Hola iOS sistema operativo informes toohello Microsoft broker aplicaciones Hola identificador de paquete de aplicación hello llamarlo.</span><span class="sxs-lookup"><span data-stu-id="6b259-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="6b259-236">Este sistema no se puede suplantar por ninguna aplicación malintencionada.</span><span class="sxs-lookup"><span data-stu-id="6b259-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="6b259-237">Por lo tanto, hemos aprovechado esto junto con el URI de nuestro tooensure de aplicación de agente que los tokens de Hola se devuelvan toohello correcta aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="6b259-238">Es necesario tooestablish este tanto en la aplicación y se establece el URI de redireccionamiento único como un URI de redireccionamiento en nuestro portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="6b259-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="6b259-239">El URI de redireccionamiento debe ser en forma adecuada de Hola de:</span><span class="sxs-lookup"><span data-stu-id="6b259-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="6b259-240">Por ejemplo, *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="6b259-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="6b259-241">Este URI de redireccionamiento debe toobe especificado en el registro de aplicación con hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6b259-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="6b259-242">Para más información sobre el registro de aplicaciones de Azure AD, consulte [Integración con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="6b259-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="6b259-243">Paso 3a: agregar un URI de redirección de la autenticación basada en certificados de portal toosupport aplicación y desarrollo</span><span class="sxs-lookup"><span data-stu-id="6b259-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="6b259-244">toosupport autenticación basada en certificado una segunda "msauth" necesita toobe registrado en la aplicación y hello [portal de Azure](https://portal.azure.com/) toohandle de autenticación de certificado si desea tooadd que se admiten en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="6b259-245">Por ejemplo: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="6b259-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="6b259-246">Paso 4: iOS9: agregar una aplicación de tooyour del parámetro de configuración</span><span class="sxs-lookup"><span data-stu-id="6b259-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="6b259-247">AAL usa: Canopenur: toocheck si el agente de hello está instalado en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6b259-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="6b259-248">En iOS 9, Apple ha bloqueado los esquemas que puede consultar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="6b259-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="6b259-249">Necesitará tooadd "msauth" toohello LSApplicationQueriesSchemes sección de su `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="6b259-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="6b259-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="6b259-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="6b259-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="6b259-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="6b259-252">Ya ha configurado el SSO.</span><span class="sxs-lookup"><span data-stu-id="6b259-252">You've configured SSO!</span></span>
<span data-ttu-id="6b259-253">Ahora Hola SDK de Microsoft Identity usarán automáticamente tanto comparte las credenciales a través de sus aplicaciones e invocarán a broker Hola si está presente en su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b259-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

