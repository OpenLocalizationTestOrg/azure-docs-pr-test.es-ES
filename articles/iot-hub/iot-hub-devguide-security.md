---
title: seguridad de Azure IoT Hub aaaUnderstand | Documentos de Microsoft
description: "Guía para desarrolladores - cómo toocontrol acceso tooIoT concentrador para aplicaciones de dispositivos y aplicaciones de back-end. Además, incluye información sobre los tokens de seguridad y la compatibilidad con certificados X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="cc769-104">Controlar el acceso tooIoT concentrador</span><span class="sxs-lookup"><span data-stu-id="cc769-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="cc769-105">En este artículo se describe las opciones de Hola para proteger su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="cc769-106">Centro de IoT usa *permisos* toogrant punto de conexión de acceso tooeach IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cc769-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="cc769-107">Permisos de limitan el centro de IoT tooan Hola acceso basado en la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="cc769-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="cc769-108">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="cc769-108">This article describes:</span></span>

* <span data-ttu-id="cc769-109">Hola distintos permisos que puede conceder tooa dispositivos o aplicaciones back-end tooaccess su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="cc769-110">Hola tokens hello y proceso de autenticación utiliza tooverify permisos.</span><span class="sxs-lookup"><span data-stu-id="cc769-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="cc769-111">¿Cómo tooscope credenciales toolimit acceder a los recursos de toospecific.</span><span class="sxs-lookup"><span data-stu-id="cc769-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="cc769-112">IoT Hub admite los certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="cc769-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="cc769-113">Los mecanismos de autenticación de dispositivo personalizado que utilizan los registros de identidad de dispositivo o los esquemas de autenticación.</span><span class="sxs-lookup"><span data-stu-id="cc769-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="cc769-114">Cuando toouse</span><span class="sxs-lookup"><span data-stu-id="cc769-114">When toouse</span></span>

<span data-ttu-id="cc769-115">Debe tener los permisos adecuados tooaccess cualquiera de los extremos del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="cc769-116">Por ejemplo, un dispositivo debe incluir un símbolo (token) que contiene las credenciales de seguridad junto con cada mensaje que envía tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="cc769-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="cc769-117">Permisos y control del acceso</span><span class="sxs-lookup"><span data-stu-id="cc769-117">Access control and permissions</span></span>

<span data-ttu-id="cc769-118">Puede conceder [permisos](#iot-hub-permissions) Hola siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="cc769-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="cc769-119">**Directivas de acceso compartido de nivel de centro de IoT**.</span><span class="sxs-lookup"><span data-stu-id="cc769-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="cc769-120">Las directivas de acceso compartido pueden conceder cualquier combinación de los [permisos](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="cc769-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="cc769-121">Las directivas se pueden definir en hello [portal de Azure][lnk-management-portal], o mediante programación usando hello [API de REST de proveedor de recursos de centro de IoT][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="cc769-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="cc769-122">Un centro de IoT recién creado tiene Hola siguiendo las directivas predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="cc769-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="cc769-123">**iothubowner**: directiva con todos los permisos.</span><span class="sxs-lookup"><span data-stu-id="cc769-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="cc769-124">**service**: directiva con el permiso **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="cc769-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="cc769-125">**device**: directiva con el permiso **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="cc769-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="cc769-126">**registryRead**: directiva con el permiso **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="cc769-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="cc769-127">**registryReadWrite**: directiva con los permisos **RegistryRead** y RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="cc769-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="cc769-128">**Credenciales de seguridad de cada dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="cc769-128">**Per-device security credentials**.</span></span> <span data-ttu-id="cc769-129">Cada centro de IoT contiene un [registro de identidades][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="cc769-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="cc769-130">Para cada dispositivo en este registro de identidad, puede configurar las credenciales de seguridad que concedan **DeviceConnect** toohello puntos de conexión de dispositivo correspondientes del ámbito de permisos.</span><span class="sxs-lookup"><span data-stu-id="cc769-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="cc769-131">Por ejemplo en una solución típica de IoT:</span><span class="sxs-lookup"><span data-stu-id="cc769-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="cc769-132">componente de administración de dispositivos de Hello usa hello *registryReadWrite* directiva.</span><span class="sxs-lookup"><span data-stu-id="cc769-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="cc769-133">componente del procesador de eventos de Hello usa hello *servicio* directiva.</span><span class="sxs-lookup"><span data-stu-id="cc769-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="cc769-134">componente de lógica de negocios de Hello dispositivo de tiempo de ejecución utiliza hello *servicio* directiva.</span><span class="sxs-lookup"><span data-stu-id="cc769-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="cc769-135">Dispositivos individuales se conectan mediante las credenciales almacenadas en el registro de la identidad del centro de IoT de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="cc769-136">Para más detalles, vea [Permisos](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="cc769-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="cc769-137">Autenticación</span><span class="sxs-lookup"><span data-stu-id="cc769-137">Authentication</span></span>

<span data-ttu-id="cc769-138">Centro de IoT de Azure, se concede acceso tooendpoints comprobando un token con las directivas de acceso compartido de Hola y credenciales de identidad de seguridad del registro.</span><span class="sxs-lookup"><span data-stu-id="cc769-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="cc769-139">Las credenciales de seguridad, como las claves simétricas, nunca se envían a través de la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="cc769-140">Hello proveedor de recursos de centro de IoT de Azure se protege mediante la suscripción de Azure, igual que todos los proveedores de hello [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="cc769-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="cc769-141">Para obtener más información acerca de cómo tooconstruct y use tokens de seguridad, vea [tokens de seguridad del centro de IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="cc769-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="cc769-142">Detalles específicos de protocolo</span><span class="sxs-lookup"><span data-stu-id="cc769-142">Protocol specifics</span></span>

<span data-ttu-id="cc769-143">Cada protocolo admitido, como MQTT, AMQP y HTTP, transporta tokens de diferentes maneras.</span><span class="sxs-lookup"><span data-stu-id="cc769-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="cc769-144">Cuando se usa MQTT, paquete de saludo conectar tiene deviceId Hola Hola ClientId, {iothubhostname} / {deviceId} en el campo de nombre de usuario de Hola y un token SAS en el campo de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="cc769-145">{iothubhostname} debe ser Hola CName completa del centro de IoT hello (por ejemplo, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="cc769-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="cc769-146">Al usar [AMQP][lnk-amqp], IoT Hub admite [SASL PLAIN][lnk-sasl-plain] y [seguridad basada en notificaciones AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="cc769-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="cc769-147">Si usa AMQP notificaciones según-seguridad, Hola estándar especifica cómo tootransmit estos tokens.</span><span class="sxs-lookup"><span data-stu-id="cc769-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="cc769-148">Para SASL sin formato, Hola **nombre de usuario** puede ser:</span><span class="sxs-lookup"><span data-stu-id="cc769-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="cc769-149">`{policyName}@sas.root.{iothubName}` si usa tokens de nivel de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="cc769-150">`{deviceId}@sas.{iothubname}` si usa tokens de ámbito por el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="cc769-151">En ambos casos, campo de contraseña de Hola contiene el token de hello, como se describe en [tokens de seguridad del centro de IoT][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="cc769-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="cc769-152">HTTP implementa la autenticación mediante la inclusión de un token válido en hello **autorización** encabezado de solicitud.</span><span class="sxs-lookup"><span data-stu-id="cc769-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="cc769-153">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cc769-153">Example</span></span>

<span data-ttu-id="cc769-154">Nombre de usuario (DeviceId distingue entre mayúsculas y minúsculas): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="cc769-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="cc769-155">Contraseña (token de SAS generar con hello [explorer dispositivo] [ lnk-device-explorer] herramienta):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="cc769-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="cc769-156">Hola [SDK de Azure IoT] [ lnk-sdks] automáticamente generar tokens cuando se conecta el servicio toohello.</span><span class="sxs-lookup"><span data-stu-id="cc769-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="cc769-157">En algunos casos, hello Azure IoT SDK no son compatibles con todos los protocolos de Hola o todos los métodos de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="cc769-158">Consideraciones especiales para SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="cc769-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="cc769-159">Cuando se usa sin formato SASL con AMQP, un cliente que se conecta el centro de IoT tooan puede usar un token único para cada conexión TCP.</span><span class="sxs-lookup"><span data-stu-id="cc769-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="cc769-160">Cuando expira el token de hello, Hola conexión TCP se desconecta del servicio de Hola y desencadena una reconexión.</span><span class="sxs-lookup"><span data-stu-id="cc769-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="cc769-161">Este comportamiento, aunque no problemático para una aplicación back-end, es perjudicial para una aplicación de dispositivo para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="cc769-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="cc769-162">Las puertas de enlace normalmente se conectan en nombre de muchos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cc769-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="cc769-163">Cuando se usa sin formato SASL, tienen toocreate una conexión TCP distinta para cada dispositivo que se conecta el centro de IoT tooan.</span><span class="sxs-lookup"><span data-stu-id="cc769-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="cc769-164">Este escenario considerablemente aumenta el consumo de hello potencia y recursos de red y aumenta la latencia de Hola de cada conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="cc769-165">Dispositivos de recursos restringidos se ven afectados negativamente mediante el uso de hello aumentado de recursos tooreconnect después de cada vencimiento del token.</span><span class="sxs-lookup"><span data-stu-id="cc769-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="cc769-166">Restricción de las credenciales de nivel de centro de IoT</span><span class="sxs-lookup"><span data-stu-id="cc769-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="cc769-167">Puede restringir el ámbito de las directivas de seguridad de nivel de centro de IoT mediante la creación de tokens con un URI de recurso restringido.</span><span class="sxs-lookup"><span data-stu-id="cc769-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="cc769-168">Por ejemplo, mensajes de Hola extremo toosend dispositivo a la nube desde un dispositivo es **/devices/ {deviceId} / mensajes y eventos**.</span><span class="sxs-lookup"><span data-stu-id="cc769-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="cc769-169">También puede utilizar una directiva de acceso compartido de nivel del centro de IoT con **DeviceConnect** permisos toosign un token es cuyo resourceURI **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="cc769-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="cc769-170">Este método crea un símbolo (token) que solo se puede usar toosend mensajes en nombre de dispositivo **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="cc769-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="cc769-171">Este mecanismo es similar toohello [directiva de edición de los centros de eventos][lnk-event-hubs-publisher-policy]y permite los métodos de autenticación personalizados de tooimplement.</span><span class="sxs-lookup"><span data-stu-id="cc769-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="cc769-172">Tokens de seguridad</span><span class="sxs-lookup"><span data-stu-id="cc769-172">Security tokens</span></span>

<span data-ttu-id="cc769-173">Centro de IoT utiliza la seguridad de tokens tooauthenticate dispositivos y servicios tooavoid envío de claves en el cable Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="cc769-174">Además, los tokens de seguridad están limitados en cuanto al ámbito y el período de validez.</span><span class="sxs-lookup"><span data-stu-id="cc769-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="cc769-175">Los [SDK IoT de Azure][lnk-sdks] generan automáticamente tokens sin necesidad de ninguna configuración especial.</span><span class="sxs-lookup"><span data-stu-id="cc769-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="cc769-176">Algunos escenarios requieren toogenerate y utilizar directamente los tokens de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cc769-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="cc769-177">Entre los escenarios se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="cc769-177">Such scenarios include:</span></span>

* <span data-ttu-id="cc769-178">uso directo de Hola de superficies de hello MQTT, AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc769-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="cc769-179">Hola implementación del modelo de servicio de token de hello, como se explica en [autenticación de dispositivo personalizada][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="cc769-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="cc769-180">Centro de IoT también permite tooauthenticate de dispositivos con el centro de IoT con [certificados X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="cc769-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="cc769-181">Estructura del token de seguridad</span><span class="sxs-lookup"><span data-stu-id="cc769-181">Security token structure</span></span>

<span data-ttu-id="cc769-182">Usar seguridad tokens toogrant acceso limitado de tiempo toodevices toospecific funcionalidad de servicios y en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="cc769-183">tooget autorización tooconnect tooIoT concentrador, dispositivos y servicios deben enviar los tokens de seguridad firmados con un acceso compartido o una clave simétrica.</span><span class="sxs-lookup"><span data-stu-id="cc769-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="cc769-184">Dichas claves están almacenadas con una identidad de dispositivo en el registro de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="cc769-185">Un token firmado con una funcionalidad de hello acceso compartido clave concede acceso tooall asociada con permisos de directiva de acceso de hello compartido.</span><span class="sxs-lookup"><span data-stu-id="cc769-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="cc769-186">Un token firmado con hello de concesiones única clave simétrica de la identidad de dispositivo **DeviceConnect** permiso para hello asociados identidad del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="cc769-187">token de seguridad de Hello tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="cc769-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="cc769-188">Estos son los valores esperados hello:</span><span class="sxs-lookup"><span data-stu-id="cc769-188">Here are hello expected values:</span></span>

| <span data-ttu-id="cc769-189">Valor</span><span class="sxs-lookup"><span data-stu-id="cc769-189">Value</span></span> | <span data-ttu-id="cc769-190">Description</span><span class="sxs-lookup"><span data-stu-id="cc769-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc769-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="cc769-191">{signature}</span></span> |<span data-ttu-id="cc769-192">Una cadena de firma de HMAC-SHA256 del formulario de hello: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="cc769-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="cc769-193">**Importante**: clave hello es descodificar de base64 y se utiliza como clave tooperform cálculo de hello HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="cc769-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="cc769-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="cc769-194">{resourceURI}</span></span> |<span data-ttu-id="cc769-195">Prefijo URI (por segmento) de los puntos de conexión de Hola que puede tener acceso a este token, empezando por el nombre de host del centro de IoT hello (ningún protocolo).</span><span class="sxs-lookup"><span data-stu-id="cc769-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="cc769-196">Por ejemplo: `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="cc769-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="cc769-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="cc769-197">{expiry}</span></span> |<span data-ttu-id="cc769-198">UTF8 cadenas para el número de segundos transcurridos desde la época de hello 00:00:00 hora UTC de 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="cc769-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="cc769-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="cc769-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="cc769-200">Cuanto menor sea caso codificación de direcciones URL de URI de recurso de minúsculas Hola</span><span class="sxs-lookup"><span data-stu-id="cc769-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="cc769-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="cc769-201">{policyName}</span></span> |<span data-ttu-id="cc769-202">nombre de Hola de hello compartido toowhich de directiva de acceso que hace referencia este token.</span><span class="sxs-lookup"><span data-stu-id="cc769-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="cc769-203">Está ausente if token Hola hace referencia a las credenciales de registro toodevice.</span><span class="sxs-lookup"><span data-stu-id="cc769-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="cc769-204">**Tenga en cuenta en el prefijo**: prefijo URI de Hola se calcula por segmento y no por carácter.</span><span class="sxs-lookup"><span data-stu-id="cc769-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="cc769-205">Por ejemplo `/a/b` es un prefijo de `/a/b/c` pero `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="cc769-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="cc769-206">Hello Node.js fragmento siguiente muestra una función denominada **generateSasToken** que calcula Hola símbolo (token) de entradas de hello `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="cc769-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="cc769-207">Hola siguiente se detallan cómo tooinitialize Hola diferentes entradas token distinto de hello utilizar casos.</span><span class="sxs-lookup"><span data-stu-id="cc769-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="cc769-208">Como comparación, Hola toogenerate equivalente de código de Python que es un token de seguridad:</span><span class="sxs-lookup"><span data-stu-id="cc769-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="cc769-209">Puesto que el periodo de validez de Hola de token de Hola se valida en equipos de centro de IoT, una desviación de hello en reloj Hola de máquina de Hola que genera el token de hello debe ser mínima.</span><span class="sxs-lookup"><span data-stu-id="cc769-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="cc769-210">Uso de tokens de SAS en una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="cc769-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="cc769-211">Hay tooobtain de dos maneras **DeviceConnect** permisos con el centro de IoT con tokens de seguridad: usar un [clave simétrica dispositivo desde el registro de la identidad de hello](#use-a-symmetric-key-in-the-identity-registry), o usar un [declavedeaccesocompartido](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="cc769-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="cc769-212">Recuerde que puede acceder a toda la funcionalidad desde los dispositivos expuestos por diseño en los puntos de conexión con el prefijo `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="cc769-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc769-213">Hola única manera de que el centro de IoT autentica un dispositivo específico está usando la clave simétrica de identidad de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="cc769-214">En casos cuando una directiva de acceso compartido es tooaccess usa funcionalidad del dispositivo, solución de hello debe tener en cuenta componente Hola emisión de token de seguridad de Hola como un subcomponente de confianza.</span><span class="sxs-lookup"><span data-stu-id="cc769-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="cc769-215">los puntos de conexión del dispositivo de Hello son (independientemente del protocolo de hello):</span><span class="sxs-lookup"><span data-stu-id="cc769-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="cc769-216">Extremo</span><span class="sxs-lookup"><span data-stu-id="cc769-216">Endpoint</span></span> | <span data-ttu-id="cc769-217">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="cc769-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="cc769-218">Envío de mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="cc769-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="cc769-219">Recepción de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="cc769-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="cc769-220">Usar una clave simétrica en el registro de la identidad de Hola</span><span class="sxs-lookup"><span data-stu-id="cc769-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="cc769-221">Cuando se usa toogenerate clave simétrica un token de una identidad dispositivo, Hola policyName (`skn`) se omite el elemento de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="cc769-222">Por ejemplo, crea un token de tooaccess toda la funcionalidad de dispositivo debe haber Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="cc769-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="cc769-223">URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="cc769-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="cc769-224">clave de firma: cualquier clave simétrica para hello `{device id}` identidad,</span><span class="sxs-lookup"><span data-stu-id="cc769-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="cc769-225">ningún nombre de directiva,</span><span class="sxs-lookup"><span data-stu-id="cc769-225">no policy name,</span></span>
* <span data-ttu-id="cc769-226">cualquier fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="cc769-226">any expiration time.</span></span>

<span data-ttu-id="cc769-227">Un ejemplo de cómo utilizar Hola anterior Node.js función sería:</span><span class="sxs-lookup"><span data-stu-id="cc769-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="cc769-228">resultado de Hello, que concede acceso a la funcionalidad de tooall para dispositivo1, sería:</span><span class="sxs-lookup"><span data-stu-id="cc769-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="cc769-229">Es posible toogenerate un token SAS mediante .NET hello [explorador del dispositivo] [ lnk-device-explorer] herramienta u Hola multiplataforma, basado en nodos [el centro de IOT explorador] [ lnk-iothub-explorer] utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="cc769-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="cc769-230">Uso de una directiva de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="cc769-230">Use a shared access policy</span></span>

<span data-ttu-id="cc769-231">Cuando se crea un símbolo (token) de una directiva de acceso compartido, establezca hello `skn` toohello nombre del campo de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="cc769-232">Esta directiva debe conceder hello **DeviceConnect** permiso.</span><span class="sxs-lookup"><span data-stu-id="cc769-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="cc769-233">Hola dos escenarios principales para usar la funcionalidad de dispositivo de tooaccess de directivas de acceso compartido son:</span><span class="sxs-lookup"><span data-stu-id="cc769-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="cc769-234">[puertas de enlace del protocolo en la nube][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="cc769-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="cc769-235">[Servicios de tokens] [ lnk-custom-auth] utiliza esquemas de autenticación personalizados de tooimplement.</span><span class="sxs-lookup"><span data-stu-id="cc769-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="cc769-236">Desde Hola directiva de acceso compartido puede potencialmente conceder acceso tooconnect como cualquier dispositivo, es importante toouse Hola correcta URI del recurso al crear tokens de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cc769-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="cc769-237">Esta opción es especialmente importante para los servicios de token, que tienen con el URI de recurso de hello tooscope hello tooa token específico dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="cc769-238">Este punto es menos relevante para puertas de enlace de protocolo, puesto que ya están mediando el tráfico para todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cc769-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="cc769-239">Por ejemplo, un servicio de token con hello creado previamente compartido llama a la directiva de acceso **dispositivo** crearía un token con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="cc769-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="cc769-240">URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="cc769-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="cc769-241">clave de firma: una de las claves de Hola de hello `device` directiva,</span><span class="sxs-lookup"><span data-stu-id="cc769-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="cc769-242">nombre de la directiva: `device`,</span><span class="sxs-lookup"><span data-stu-id="cc769-242">policy name: `device`,</span></span>
* <span data-ttu-id="cc769-243">cualquier fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="cc769-243">any expiration time.</span></span>

<span data-ttu-id="cc769-244">Un ejemplo de cómo utilizar Hola anterior Node.js función sería:</span><span class="sxs-lookup"><span data-stu-id="cc769-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="cc769-245">resultado de Hello, que concede acceso a la funcionalidad de tooall para dispositivo1, sería:</span><span class="sxs-lookup"><span data-stu-id="cc769-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="cc769-246">Una puerta de enlace de protocolo podría utilizar Hola mismo símbolo (token) para todos los dispositivos que simplemente establecer Hola URI de recurso demasiado`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="cc769-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="cc769-247">Uso de tokens de seguridad de los componentes de servicio</span><span class="sxs-lookup"><span data-stu-id="cc769-247">Use security tokens from service components</span></span>

<span data-ttu-id="cc769-248">Componentes del servicio solo pueden generar tokens de seguridad mediante las directivas de acceso compartido para conceder los permisos adecuados de hello tal y como se ha explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cc769-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="cc769-249">Aquí está expuestas en los puntos de conexión de hello las funciones de servicios de hello:</span><span class="sxs-lookup"><span data-stu-id="cc769-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="cc769-250">Extremo</span><span class="sxs-lookup"><span data-stu-id="cc769-250">Endpoint</span></span> | <span data-ttu-id="cc769-251">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="cc769-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="cc769-252">Creación, actualización, recuperación y eliminación de las identidades del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="cc769-253">Recepción de mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="cc769-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="cc769-254">Recepción de comentarios para los mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="cc769-255">Envío de mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="cc769-256">Por ejemplo, un servicio que se genera utilizando Hola creado previamente compartido llama a la directiva de acceso **registryRead** crearía un token con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="cc769-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="cc769-257">URI de recurso: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="cc769-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="cc769-258">clave de firma: una de las claves de Hola de hello `registryRead` directiva,</span><span class="sxs-lookup"><span data-stu-id="cc769-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="cc769-259">nombre de la directiva: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="cc769-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="cc769-260">cualquier fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="cc769-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="cc769-261">resultado de Hello, que le concede acceso tooread todas las identidades del dispositivo, sería:</span><span class="sxs-lookup"><span data-stu-id="cc769-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="cc769-262">Certificados X.509 compatibles</span><span class="sxs-lookup"><span data-stu-id="cc769-262">Supported X.509 certificates</span></span>

<span data-ttu-id="cc769-263">Puede usar cualquier tooauthenticate de certificado X.509 un dispositivo con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="cc769-264">Los certificados incluyen:</span><span class="sxs-lookup"><span data-stu-id="cc769-264">Certificates include:</span></span>

* <span data-ttu-id="cc769-265">**Un certificado X.509 existente**.</span><span class="sxs-lookup"><span data-stu-id="cc769-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="cc769-266">Puede que un dispositivo ya tenga un certificado X.509 asociado.</span><span class="sxs-lookup"><span data-stu-id="cc769-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="cc769-267">dispositivo de Hello puede usar este certificado tooauthenticate con centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="cc769-268">**Un certificado X-509 autofirmado y generado automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="cc769-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="cc769-269">Un fabricante del dispositivo o implementador interna puede generar estos certificados y almacenar Hola clave privada correspondiente (y el certificado) en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="cc769-270">Puede usar herramientas como [OpenSSL][lnk-openssl] y la utilidad [Windows SelfSignedCertificate][lnk-selfsigned] para este propósito.</span><span class="sxs-lookup"><span data-stu-id="cc769-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="cc769-271">**Certificado X.509 firmado por una CA**.</span><span class="sxs-lookup"><span data-stu-id="cc769-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="cc769-272">tooidentify un dispositivo y autenticar con el centro de IoT, puede usar un certificado X.509 generado y firmado por una entidad de certificación (CA).</span><span class="sxs-lookup"><span data-stu-id="cc769-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="cc769-273">Centro de IoT solo comprueba esa huella digital de hello presentado coincide con la huella digital de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="cc769-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="cc769-274">El centro de IOT no valida la cadena de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="cc769-275">Un dispositivo puede usar un token de seguridad o un certificado X.509 para realizar la autenticación, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="cc769-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="cc769-276">Registro de certificados X.509 en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="cc769-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="cc769-277">Hola [SDK del servicio de IoT de Azure para C#] [ lnk-service-sdk] (versión 1.0.8+) admite registrar un dispositivo que usa un certificado X.509 para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="cc769-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="cc769-278">Otras API como la importación y exportación de dispositivos también admiten este tipo de certificados.</span><span class="sxs-lookup"><span data-stu-id="cc769-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="cc769-279">Compatibilidad con C\#</span><span class="sxs-lookup"><span data-stu-id="cc769-279">C\# Support</span></span>

<span data-ttu-id="cc769-280">Hola **RegistryManager** clase proporciona un mecanismo de programación tooregister un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="cc769-281">En concreto, Hola **AddDeviceAsync** y **UpdateDeviceAsync** métodos permiten tooregister y actualizar un dispositivo en hello del registro de identidad de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="cc769-282">Estos dos métodos toman una instancia **Device** como entrada.</span><span class="sxs-lookup"><span data-stu-id="cc769-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="cc769-283">Hola **dispositivo** clase incluye una **autenticación** propiedad que permite toospecify principales y secundarias X.509 huellas digitales de certificado.</span><span class="sxs-lookup"><span data-stu-id="cc769-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="cc769-284">huella digital de Hello representa un hash SHA-1 del certificado X.509 de hello (almacenada mediante codificación DER binaria).</span><span class="sxs-lookup"><span data-stu-id="cc769-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="cc769-285">Tiene la opción de Hola de especificar una huella digital del principal o una huella digital del secundaria o ambos.</span><span class="sxs-lookup"><span data-stu-id="cc769-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="cc769-286">Huellas digitales principales y secundarias son escenarios de sustitución de certificados toohandle admitidos.</span><span class="sxs-lookup"><span data-stu-id="cc769-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="cc769-287">Centro de IoT no requiere ni almacenar certificado X.509 completo hello, sólo huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="cc769-288">Este es un ejemplo C\# un dispositivo mediante un certificado X.509 de tooregister de fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="cc769-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="cc769-289">Uso de certificados X.509 durante las operaciones en entorno de ejecución</span><span class="sxs-lookup"><span data-stu-id="cc769-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="cc769-290">Hola [dispositivos de IoT de Azure SDK para .NET] [ lnk-client-sdk] (versión 1.0.11+) admite el uso de Hola de certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="cc769-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="cc769-291">Compatibilidad con C\#</span><span class="sxs-lookup"><span data-stu-id="cc769-291">C\# Support</span></span>

<span data-ttu-id="cc769-292">Hola clase **DeviceAuthenticationWithX509Certificate** admite Hola creación de **DeviceClient** instancias mediante un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="cc769-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="cc769-293">certificado X.509 de Hello debe estar en formato PFX (también llamado PKCS #12) de Hola que incluye la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="cc769-294">A continuación, veremos un fragmento de código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cc769-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="cc769-295">Personalización de la autenticación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="cc769-295">Custom device authentication</span></span>

<span data-ttu-id="cc769-296">Puede usar hello centro de IoT [del registro de identidad] [ lnk-identity-registry] las credenciales de seguridad de tooconfigure por dispositivo y control de acceso usando [tokens] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="cc769-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="cc769-297">Si una solución de IoT ya tiene un esquema de registro o la autenticación de identidad personalizado, considere la posibilidad de crear un *del servicio de token* toointegrate esta infraestructura con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="cc769-298">De este modo, puede usar otras características de IoT en la solución.</span><span class="sxs-lookup"><span data-stu-id="cc769-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="cc769-299">Un servicio de token es un servicio en la nube personalizado.</span><span class="sxs-lookup"><span data-stu-id="cc769-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="cc769-300">Usa un centro de IoT *directiva de acceso compartido* con **DeviceConnect** permisos toocreate *centrada en el dispositivo* símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="cc769-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="cc769-301">Estos tokens habilitar un centro de IoT de dispositivo tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="cc769-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Pasos del modelo de servicio de token de Hola][img-tokenservice]

<span data-ttu-id="cc769-303">Estos son Hola pasos principales del modelo de servicio de token de hello:</span><span class="sxs-lookup"><span data-stu-id="cc769-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="cc769-304">Cree una directiva de acceso compartido de IoT Hub con permisos **DeviceConnect** para IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cc769-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="cc769-305">Puede crear esta directiva en hello [portal de Azure] [ lnk-management-portal] o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="cc769-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="cc769-306">servicio de token de Hello usa esta directiva toosign Hola símbolos (tokens) crea.</span><span class="sxs-lookup"><span data-stu-id="cc769-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="cc769-307">Cuando un dispositivo necesita tooaccess su centro de IoT, solicita un token firmado de su servicio de token.</span><span class="sxs-lookup"><span data-stu-id="cc769-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="cc769-308">dispositivo de Hola puede autenticar con la identidad del dispositivo identidad personalizada del registro/autenticación esquema toodetermine Hola que el servicio de token de hello utiliza símbolo (token) de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="cc769-309">servicio de token de Hello devuelve un token.</span><span class="sxs-lookup"><span data-stu-id="cc769-309">hello token service returns a token.</span></span> <span data-ttu-id="cc769-310">Hello símbolo (token) se crea utilizando `/devices/{deviceId}` como `resourceURI`, con `deviceId` como dispositivo de Hola que se va a autenticar.</span><span class="sxs-lookup"><span data-stu-id="cc769-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="cc769-311">servicio de token de Hello usa Hola acceso compartido directiva tooconstruct Hola símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="cc769-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="cc769-312">dispositivo de Hello usa token Hola directamente con el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="cc769-313">Puede utilizar la clase de .NET de hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] u Hola clase Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate un token en el servicio de token.</span><span class="sxs-lookup"><span data-stu-id="cc769-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="cc769-314">servicio de token de Hello puede establecer caducidad del testigo Hola según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cc769-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="cc769-315">Cuando expira el token de hello, centro de IoT Hola servidores de conexión del dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="cc769-316">A continuación, Hola debe solicitar un nuevo token de servicio de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="cc769-317">Una hora de expiración corto aumenta la carga de hello en dispositivo de Hola y el servicio de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="cc769-318">Para un concentrador de tooyour tooconnect de dispositivo, deberá agregar también se toohello del registro de identidad de centro de IoT: aunque Hola dispositivo usa un token y no un tooconnect de clave de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="cc769-319">Por lo tanto, puede seguir el control de acceso por dispositivo toouse habilitando o deshabilitando las identidades del dispositivo en hello [del registro de identidad][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="cc769-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="cc769-320">Este enfoque mitiga los riesgos de hello del uso de tokens con tiempos de expiración largos.</span><span class="sxs-lookup"><span data-stu-id="cc769-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="cc769-321">Comparación con una puerta de enlace personalizada</span><span class="sxs-lookup"><span data-stu-id="cc769-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="cc769-322">modelo de servicio de token de Hello es Hola recomienda tooimplement forma un esquema de registro/autenticación de identidad personalizada con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="cc769-323">Este patrón se recomienda porque el centro de IoT sigue toohandle la mayor parte del tráfico de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="cc769-324">Sin embargo, si el esquema de autenticación personalizado de Hola por lo que es entrelazado con protocolo de hello, puede requerir un *puerta de enlace personalizado* tooprocess todos Hola tráfico.</span><span class="sxs-lookup"><span data-stu-id="cc769-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="cc769-325">Un ejemplo de escenario de este tipo es la [seguridad de la capa de transporte (TLS) y las claves previamente compartidas (PSK)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="cc769-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="cc769-326">Para obtener más información, vea hello [puerta de enlace de protocolo] [ lnk-protocols] tema.</span><span class="sxs-lookup"><span data-stu-id="cc769-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="cc769-327">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="cc769-327">Reference topics:</span></span>

<span data-ttu-id="cc769-328">Hello temas de referencia siguientes proporcionan más información sobre el centro de IoT de controlar acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="cc769-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="cc769-329">Permisos de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cc769-329">IoT Hub permissions</span></span>

<span data-ttu-id="cc769-330">Hello tabla siguiente enumera los permisos de hello puede usar Centro de IoT de toocontrol acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="cc769-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="cc769-331">Permiso</span><span class="sxs-lookup"><span data-stu-id="cc769-331">Permission</span></span> | <span data-ttu-id="cc769-332">Notas</span><span class="sxs-lookup"><span data-stu-id="cc769-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="cc769-333">**RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="cc769-333">**RegistryRead**</span></span> |<span data-ttu-id="cc769-334">Registro de identidad de toohello de concede acceso de lectura.</span><span class="sxs-lookup"><span data-stu-id="cc769-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="cc769-335">Para más información, consulte [Registro de identidad][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="cc769-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="cc769-336">Este permiso se usa en servicios de back-end en la nube.</span><span class="sxs-lookup"><span data-stu-id="cc769-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="cc769-337">**RegistryReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="cc769-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="cc769-338">Concede acceso de lectura y escritura toohello del registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="cc769-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="cc769-339">Para más información, consulte [Registro de identidad][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="cc769-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="cc769-340">Este permiso se usa en servicios de back-end en la nube.</span><span class="sxs-lookup"><span data-stu-id="cc769-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="cc769-341">**ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="cc769-341">**ServiceConnect**</span></span> |<span data-ttu-id="cc769-342">Concede acceso toocloud orientada a servicios comunicación y supervisión de los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="cc769-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="cc769-343">Concede permiso tooreceive dispositivo a la nube mensajes, enviar mensajes en la nube al dispositivo y Hola recuperar correspondientes confirmaciones de entrega.</span><span class="sxs-lookup"><span data-stu-id="cc769-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="cc769-344">Confirmaciones de entrega de tooretrieve concede permiso para el archivo de carga.</span><span class="sxs-lookup"><span data-stu-id="cc769-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="cc769-345">Concede permiso tooaccess dispositivo: los gemelos tooupdate etiquetas y propiedades que desee, recuperar las propiedades de informes y ejecutar consultas.</span><span class="sxs-lookup"><span data-stu-id="cc769-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="cc769-346">Este permiso se usa en servicios de back-end en la nube.</span><span class="sxs-lookup"><span data-stu-id="cc769-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="cc769-347">**DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="cc769-347">**DeviceConnect**</span></span> |<span data-ttu-id="cc769-348">Concede acceso a extremos de acceso toodevice.</span><span class="sxs-lookup"><span data-stu-id="cc769-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="cc769-349">Concede permiso toosend dispositivo a la nube los mensajes y recibir mensajes en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="cc769-350">Concede permiso tooperform la carga de archivos desde un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc769-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="cc769-351">Concede permiso tooreceive gemelas deseado propiedad las notificaciones del dispositivo y el dispositivo de actualización de dos propiedades notificados.</span><span class="sxs-lookup"><span data-stu-id="cc769-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="cc769-352">Carga el archivo tooperform de concesiones de permisos.</span><span class="sxs-lookup"><span data-stu-id="cc769-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="cc769-353">Este permiso lo usan los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cc769-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="cc769-354">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="cc769-354">Additional reference material</span></span>

<span data-ttu-id="cc769-355">Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:</span><span class="sxs-lookup"><span data-stu-id="cc769-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="cc769-356">[Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.</span><span class="sxs-lookup"><span data-stu-id="cc769-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="cc769-357">[Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola y comportamientos que se aplican toohello servicio del centro de IoT de limitación.</span><span class="sxs-lookup"><span data-stu-id="cc769-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="cc769-358">[SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cc769-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="cc769-359">[Lenguaje de consulta de centro de IoT] [ lnk-query] describe el lenguaje de consulta de Hola que puede utilizar información tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.</span><span class="sxs-lookup"><span data-stu-id="cc769-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="cc769-360">[Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="cc769-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc769-361">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc769-361">Next steps</span></span>

<span data-ttu-id="cc769-362">Ahora que ha aprendido cómo toocontrol tener acceso a centro de IoT, es posible que interesa Hola temas de guía para desarrolladores de centro de IoT siguientes:</span><span class="sxs-lookup"><span data-stu-id="cc769-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="cc769-363">[Usar el estado del dispositivo: los gemelos toosynchronize y configuraciones][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="cc769-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="cc769-364">[Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="cc769-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="cc769-365">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="cc769-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="cc769-366">Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola centro de IoT tutoriales:</span><span class="sxs-lookup"><span data-stu-id="cc769-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="cc769-367">[Introducción a Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="cc769-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="cc769-368">[Cómo mensajes toosend en la nube al dispositivo con el centro de IoT][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="cc769-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="cc769-369">[¿Cómo tooprocess mensajes del dispositivo a la nube de centro de IoT][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="cc769-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
