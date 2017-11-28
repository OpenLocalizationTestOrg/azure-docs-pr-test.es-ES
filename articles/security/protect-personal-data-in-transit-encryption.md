---
title: "datos personales aaaProtect en tránsito con el cifrado en Azure | Documentos de Microsoft"
description: Mediante el cifrado en Azure tooprotect los datos personales
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a><span data-ttu-id="d5c98-103">Tecnologías de cifrado de Azure: protección de datos personales en tránsito con cifrado</span><span class="sxs-lookup"><span data-stu-id="d5c98-103">Azure encryption technologies: Protect personal data in transit with encryption</span></span>

<span data-ttu-id="d5c98-104">En este artículo le ayudará a comprender y usar datos de toosecure de tecnologías de cifrado de Azure en tránsito.</span><span class="sxs-lookup"><span data-stu-id="d5c98-104">This article will help you understand and use Azure encryption technologies toosecure data in transit.</span></span> 

<span data-ttu-id="d5c98-105">Privacidad de hello protección de datos personales que viajan a través de la red de hello es una parte esencial de una estrategia de seguridad varias capas de defensa en profundidad.</span><span class="sxs-lookup"><span data-stu-id="d5c98-105">Protecting hello privacy of personal data as it travels across hello network is an essential part of a multi-layered defense-in-depth security strategy.</span></span> <span data-ttu-id="d5c98-106">El cifrado en tránsito es diseñada tooprevent si un atacante intercepta las transmisiones de ser capaz de datos de hello tooview o el uso.</span><span class="sxs-lookup"><span data-stu-id="d5c98-106">Encryption in transit is designed tooprevent an attacker who intercepts transmissions from being able tooview or use hello data.</span></span>

## <a name="scenario"></a><span data-ttu-id="d5c98-107">Escenario</span><span class="sxs-lookup"><span data-stu-id="d5c98-107">Scenario</span></span>

<span data-ttu-id="d5c98-108">Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas.</span><span class="sxs-lookup"><span data-stu-id="d5c98-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="d5c98-109">toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas que encuentre en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="d5c98-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="d5c98-110">la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="d5c98-111">Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global.</span><span class="sxs-lookup"><span data-stu-id="d5c98-111">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="d5c98-112">También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="d5c98-112">It also includes traditional Human Resource information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="d5c98-113">línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.</span><span class="sxs-lookup"><span data-stu-id="d5c98-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="d5c98-114">Datos personales de los clientes se escribe en la base de datos de Hola de oficinas remotas de la compañía de Hola y de agentes de viaje situados alrededor de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="d5c98-114">Personal data of customers is entered in hello database from hello company’s remote offices and from travel agents located around hello world.</span></span> <span data-ttu-id="d5c98-115">Los documentos que contienen información del cliente se transfieren a través de almacenamiento de la red tooAzure Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-115">Documents containing customer information are transferred across hello network tooAzure storage.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="d5c98-116">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="d5c98-116">Problem statement</span></span>

<span data-ttu-id="d5c98-117">empresa Hola debe proteger la privacidad de Hola de los clientes y datos personales de los empleados mientras están en tránsito tooand desde servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c98-117">hello company must protect hello privacy of customers’ and employees’ personal data while it is in transit tooand from Azure services.</span></span>

## <a name="company-goal"></a><span data-ttu-id="d5c98-118">Objetivo de la empresa</span><span class="sxs-lookup"><span data-stu-id="d5c98-118">Company goal</span></span>

<span data-ttu-id="d5c98-119">Hola tooensure de objetivo de empresa que se cifran los datos personales al desactivar el disco.</span><span class="sxs-lookup"><span data-stu-id="d5c98-119">hello company goal tooensure that personal data is encrypted when off disk.</span></span> <span data-ttu-id="d5c98-120">Si las personas no autorizadas interceptan datos personales de hello desactivar el disco, debe ser en un formulario que se representará ilegible.</span><span class="sxs-lookup"><span data-stu-id="d5c98-120">If unauthorized persons intercept hello off-disk personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="d5c98-121">La aplicación del cifrado debería ser fácil o totalmente transparente tanto para los usuarios como para los administradores.</span><span class="sxs-lookup"><span data-stu-id="d5c98-121">Applying encryption should be easy, or completely transparent, for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="d5c98-122">Soluciones</span><span class="sxs-lookup"><span data-stu-id="d5c98-122">Solutions</span></span>

<span data-ttu-id="d5c98-123">Los servicios de Azure proporcionan varios toohelp herramientas y tecnologías de proteger los datos personales en tránsito.</span><span class="sxs-lookup"><span data-stu-id="d5c98-123">Azure services provide multiple tools and technologies toohelp you protect personal data in transit.</span></span>

### <a name="azure-storage"></a><span data-ttu-id="d5c98-124">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d5c98-124">Azure Storage</span></span>

<span data-ttu-id="d5c98-125">Datos que se almacenan en la nube de hello deben viajar desde el cliente hello, que puede estar ubicado físicamente en cualquier lugar de Hola a todos, toohello centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c98-125">Data that is stored in hello cloud must travel from hello client, which can be physically located anywhere in hello world, toohello Azure data center.</span></span> <span data-ttu-id="d5c98-126">Cuando esos datos se recuperan los usuarios, pasa de nuevo, en hello dirección opuesta.</span><span class="sxs-lookup"><span data-stu-id="d5c98-126">When that data is retrieved by users, it travels again, in hello opposite direction.</span></span> <span data-ttu-id="d5c98-127">Datos que están en tránsito a través de Hola Internet pública siempre está en riesgo de interceptación por los atacantes.</span><span class="sxs-lookup"><span data-stu-id="d5c98-127">Data that is in transit over hello public Internet is always at risk of interception by attackers.</span></span> <span data-ttu-id="d5c98-128">Es privacidad de hello tooprotect importante de los datos personales mediante el uso de toosecure de cifrado de nivel de transporte tal como se mueve entre ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="d5c98-128">It is important tooprotect hello privacy of personal data by using transport-level encryption toosecure it as it moves between locations.</span></span>

<span data-ttu-id="d5c98-129">Hola protocolo HTTPS proporciona un canal de comunicaciones cifradas seguras a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-129">hello HTTPS protocol provides a secure, encrypted communications channel over hello Internet.</span></span> <span data-ttu-id="d5c98-130">HTTPS debe ser objetos de tooaccess usado en el almacenamiento de Azure y al llamar a las API de REST.</span><span class="sxs-lookup"><span data-stu-id="d5c98-130">HTTPS should be used tooaccess objects in Azure Storage and when calling REST APIs.</span></span> <span data-ttu-id="d5c98-131">Exigir el uso del protocolo HTTPS de Hola al usar [firmas de acceso compartido](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) objetos de almacenamiento (SAS) toodelegate acceso tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d5c98-131">You enforce use of hello HTTPS protocol when using [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure Storage objects.</span></span> <span data-ttu-id="d5c98-132">Hay dos tipos de SAS: SAS de servicio y SAS de cuenta.</span><span class="sxs-lookup"><span data-stu-id="d5c98-132">There are two types of SAS: Service SAS and Account SAS.</span></span>

#### <a name="how-do-i-construct-a-service-sas"></a><span data-ttu-id="d5c98-133">¿Cómo se puede crear una SAS de servicio?</span><span class="sxs-lookup"><span data-stu-id="d5c98-133">How do I construct a Service SAS?</span></span>

<span data-ttu-id="d5c98-134">Un servicio SAS delegados acceso tooa recurso en solo uno de los servicios de almacenamiento de hello (servicio blob, cola, tabla o archivo).</span><span class="sxs-lookup"><span data-stu-id="d5c98-134">A Service SAS delegates access tooa resource in just one of hello storage services (blob, queue, table or file service).</span></span> <span data-ttu-id="d5c98-135">Hola tooconstruct una SAS de servicio siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5c98-135">tooconstruct a Service SAS, do hello following:</span></span>

1. <span data-ttu-id="d5c98-136">Especificar Hola Signed campo de versión</span><span class="sxs-lookup"><span data-stu-id="d5c98-136">Specify hello Signed Version Field</span></span>

2. <span data-ttu-id="d5c98-137">Especificar Hola Signed recursos (Blob y archivo de servicio solo)</span><span class="sxs-lookup"><span data-stu-id="d5c98-137">Specify hello Signed Resource (Blob and File Service Only)</span></span>

3. <span data-ttu-id="d5c98-138">Especificar encabezados de respuesta de tooOverride de parámetros de consulta (servicio de Blob y archivo de servicio solo)</span><span class="sxs-lookup"><span data-stu-id="d5c98-138">Specify Query Parameters tooOverride Response Headers (Blob Service and File Service Only)</span></span>

4. <span data-ttu-id="d5c98-139">Especificar hello (solo servicio de tabla) el nombre de tabla</span><span class="sxs-lookup"><span data-stu-id="d5c98-139">Specify hello Table Name (Table Service Only)</span></span>

5. <span data-ttu-id="d5c98-140">Especificar Hola directiva de acceso</span><span class="sxs-lookup"><span data-stu-id="d5c98-140">Specify hello Access Policy</span></span>

6. <span data-ttu-id="d5c98-141">Especificar Hola intervalo de validez de firma</span><span class="sxs-lookup"><span data-stu-id="d5c98-141">Specify hello Signature Validity Interval</span></span>

8. <span data-ttu-id="d5c98-142">Especifique los permisos</span><span class="sxs-lookup"><span data-stu-id="d5c98-142">Specify Permissions</span></span>

9. <span data-ttu-id="d5c98-143">Especifique la dirección IP o el intervalo IP</span><span class="sxs-lookup"><span data-stu-id="d5c98-143">Specify IP Address or IP Range</span></span>

10. <span data-ttu-id="d5c98-144">Especificar Hola protocolo HTTP</span><span class="sxs-lookup"><span data-stu-id="d5c98-144">Specify hello HTTP Protocol</span></span>

11. <span data-ttu-id="d5c98-145">Especifique los intervalos de acceso a la tabla</span><span class="sxs-lookup"><span data-stu-id="d5c98-145">Specify Table Access Ranges</span></span>

12. <span data-ttu-id="d5c98-146">Especificar Hola identificador firmado</span><span class="sxs-lookup"><span data-stu-id="d5c98-146">Specify hello Signed Identifier</span></span>

13. <span data-ttu-id="d5c98-147">Especificar Hola firma</span><span class="sxs-lookup"><span data-stu-id="d5c98-147">Specify hello Signature</span></span>

<span data-ttu-id="d5c98-148">Para obtener instrucciones más detalladas, consulte [Creación de una SAS de servicio](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="d5c98-148">For more detailed instructions, see [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).</span></span>

#### <a name="how-do-i-construct-an-account-sas"></a><span data-ttu-id="d5c98-149">¿Cómo se puede crear una SAS de cuenta?</span><span class="sxs-lookup"><span data-stu-id="d5c98-149">How do I construct an Account SAS?</span></span>

<span data-ttu-id="d5c98-150">Una SAS de cuenta delega tooresources de acceso en uno o varios de los servicios de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-150">An Account SAS delegates access tooresources in one or more of hello storage services.</span></span> <span data-ttu-id="d5c98-151">También puede delegar el acceso tooread, escritura y las operaciones de eliminación en contenedores de blobs, tablas, colas y recursos compartidos de archivos que no se permiten con un servicio de SAS.</span><span class="sxs-lookup"><span data-stu-id="d5c98-151">You can also delegate access tooread, write, and delete operations on blob containers, tables, queues, and file shares that are not permitted with a service SAS.</span></span> <span data-ttu-id="d5c98-152">Construcción de una cuenta SA es toothat similar de una SAS de servicio.</span><span class="sxs-lookup"><span data-stu-id="d5c98-152">Construction of an Account SAS is similar toothat of a Service SAS.</span></span> <span data-ttu-id="d5c98-153">Para obtener instrucciones detalladas, consulte [Creación de una SAS de cuenta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="d5c98-153">For detailed instructions, see [Constructing an Account SAS.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)</span></span>

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a><span data-ttu-id="d5c98-154">¿Cómo se puede aplicar HTTPS al llamar a API de REST?</span><span class="sxs-lookup"><span data-stu-id="d5c98-154">How do I enforce HTTPS when calling REST APIs?</span></span>

<span data-ttu-id="d5c98-155">tooenforce el uso de Hola de HTTPS al llamar a objetos de las API de REST tooaccess en cuentas de almacenamiento, puede habilitar la transferencia segura necesaria Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d5c98-155">tooenforce hello use of HTTPS when calling REST APIs tooaccess objects in storage accounts, you can enable Secure Transfer Required for hello storage account.</span></span> 

1. <span data-ttu-id="d5c98-156">Hola portal de Azure, seleccione **crear cuenta de almacenamiento**, o para una cuenta de almacenamiento existente, seleccione **configuración** y, a continuación, **configuración**.</span><span class="sxs-lookup"><span data-stu-id="d5c98-156">In hello Azure portal, select **Create Storage Account**, or for an existing storage account, select **Settings** and then **Configuration**.</span></span>

2. <span data-ttu-id="d5c98-157">En **Se requiere transferencia segura**, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="d5c98-157">Under **Secure Transfer Required**, select **Enabled**.</span></span>

![Creación de una cuenta de almacenamiento](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

<span data-ttu-id="d5c98-159">Para obtener más instrucciones, incluido cómo tooenable seguros transferir necesarios mediante programación, vea [requieren Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span><span class="sxs-lookup"><span data-stu-id="d5c98-159">For more detailed instructions, including how tooenable Secure Transfer Required programmatically, see [Require Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).</span></span>

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a><span data-ttu-id="d5c98-160">¿Cómo se pueden cifrar datos en Azure File Storage?</span><span class="sxs-lookup"><span data-stu-id="d5c98-160">How do I encrypt data in Azure File Storage?</span></span>

<span data-ttu-id="d5c98-161">tooencrypt datos en tránsito con [almacenamiento de archivos de Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), puede usar SMB 3.x con Windows 8, 8.1 y 10 y Windows Server 2012 R2 y Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d5c98-161">tooencrypt data in transit with [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), you can use SMB 3.x with Windows 8, 8.1, and 10 and with Windows Server 2012 R2 and Windows Server 2016.</span></span> <span data-ttu-id="d5c98-162">Cuando se usa el servicio de archivos de Azure de hello, se produce un error en cualquier conexión sin cifrado cuando "Proteger la transferencia requerida" está habilitada.</span><span class="sxs-lookup"><span data-stu-id="d5c98-162">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="d5c98-163">Esto incluye escenarios con algunos tipos de hello cliente Linux SMB, SMB 2.1 y SMB 3.0 sin cifrado.</span><span class="sxs-lookup"><span data-stu-id="d5c98-163">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span>

#### <a name="azure-client-side-encryption"></a><span data-ttu-id="d5c98-164">Cifrado de cliente de Azure</span><span class="sxs-lookup"><span data-stu-id="d5c98-164">Azure Client-Side Encryption</span></span>

<span data-ttu-id="d5c98-165">Otra opción para proteger datos personales mientras se transfieren entre una aplicación cliente y Azure Storage es [Cifrado de cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span><span class="sxs-lookup"><span data-stu-id="d5c98-165">Another option for protecting personal data while it’s being transferred between a client application and Azure Storage is [Client-side Encryption](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).</span></span> <span data-ttu-id="d5c98-166">Hola datos se cifran antes de que se transfieren al almacenamiento de Azure y cuando se recuperan datos de Hola desde el almacenamiento de Azure, se descifran datos Hola tras su recepción en el lado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-166">hello data is encrypted before being transferred into Azure Storage and when you retrieve hello data from Azure Storage, hello data is decrypted after it is received on hello client side.</span></span>

### <a name="azure-site-to-site-vpn"></a><span data-ttu-id="d5c98-167">VPN de sitio a sitio de Azure</span><span class="sxs-lookup"><span data-stu-id="d5c98-167">Azure Site-to-Site VPN</span></span>

<span data-ttu-id="d5c98-168">Un modo eficaz tooprotect personal los datos en tránsito entre una red corporativa o un usuario y Hola red virtual de Azure están toouse una [sitio a sitio](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) o [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) red privada Virtual (VPN).</span><span class="sxs-lookup"><span data-stu-id="d5c98-168">An effective way tooprotect personal data in transit between a corporate network or user and hello Azure virtual network is toouse a [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) or [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) Virtual Private Network (VPN).</span></span> <span data-ttu-id="d5c98-169">Una conexión VPN crea un túnel cifrado seguro a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-169">A VPN connection creates a secure encrypted tunnel across hello Internet.</span></span>

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a><span data-ttu-id="d5c98-170">¿Cómo se puede crear una conexión VPN de sitio a sitio?</span><span class="sxs-lookup"><span data-stu-id="d5c98-170">How do I create a site-to-site VPN connection?</span></span>

<span data-ttu-id="d5c98-171">Una VPN de sitio a sitio conecta a varios usuarios en hello tooAzure de red corporativa.</span><span class="sxs-lookup"><span data-stu-id="d5c98-171">A site-to-site VPN connects multiple users on hello corporate network tooAzure.</span></span> <span data-ttu-id="d5c98-172">toocreate una conexión de sitio a sitio en el portal de Azure, Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5c98-172">toocreate a site-to-site connection in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="d5c98-173">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d5c98-173">Create a virtual network.</span></span>

2. <span data-ttu-id="d5c98-174">Especifique un servidor DNS</span><span class="sxs-lookup"><span data-stu-id="d5c98-174">Specify a DNS server.</span></span>

3. <span data-ttu-id="d5c98-175">Crear una subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-175">Create hello gateway subnet.</span></span>

4. <span data-ttu-id="d5c98-176">Crear puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-176">Create hello VPN gateway.</span></span> 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. <span data-ttu-id="d5c98-177">Crear puerta de enlace de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-177">Create hello local network gateway.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. <span data-ttu-id="d5c98-178">Configure el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="d5c98-178">Configure your VPN device.</span></span>

7. <span data-ttu-id="d5c98-179">Crear la conexión de VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-179">Create hello VPN connection.</span></span>

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. <span data-ttu-id="d5c98-180">Compruebe la conexión de VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-180">Verify hello VPN connection.</span></span>

<span data-ttu-id="d5c98-181">Para obtener instrucciones detalladas sobre cómo conexión toocreate un sitio a sitio en hello Azure portal, vea [crear un sitio a sitio de conexión en hello Portal de Azure]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="d5c98-181">For more detailed instructions on how toocreate a site-to-site connection in hello Azure portal, see [Create a Site-to-Site  connection in hello Azure Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)</span></span>

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a><span data-ttu-id="d5c98-182">¿Cómo se puede crear una conexión VPN de punto a sitio?</span><span class="sxs-lookup"><span data-stu-id="d5c98-182">How do I create a point-to-site VPN connection?</span></span>

<span data-ttu-id="d5c98-183">Una VPN de sitio a punto, crea una conexión segura en una red virtual de la tooa de equipos cliente individuales.</span><span class="sxs-lookup"><span data-stu-id="d5c98-183">A Point-to-Site VPN creates a secure connection from an individual client computer tooa virtual network.</span></span> <span data-ttu-id="d5c98-184">Esto es útil cuando se desea tooconnect tooAzure desde una ubicación remota, como desde el centro principal o de un hotel o conferencia.</span><span class="sxs-lookup"><span data-stu-id="d5c98-184">This is useful when you  want tooconnect tooAzure from a remote location, such as from home or a hotel or conference center.</span></span> <span data-ttu-id="d5c98-185">toocreate una conexión punto a sitio en hello portal de Azure,</span><span class="sxs-lookup"><span data-stu-id="d5c98-185">toocreate a point-to-site  connection in hello Azure portal,</span></span>

1. <span data-ttu-id="d5c98-186">Cree una red virtual.</span><span class="sxs-lookup"><span data-stu-id="d5c98-186">Create a virtual network.</span></span>

2. <span data-ttu-id="d5c98-187">Agregue una subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d5c98-187">Add a gateway subnet.</span></span>

3. <span data-ttu-id="d5c98-188">Especifique un servidor DNS</span><span class="sxs-lookup"><span data-stu-id="d5c98-188">Specify a DNS server.</span></span> <span data-ttu-id="d5c98-189">(opcional).</span><span class="sxs-lookup"><span data-stu-id="d5c98-189">(optional)</span></span>

4. <span data-ttu-id="d5c98-190">Cree una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="d5c98-190">Create a virtual network gateway.</span></span>

5. <span data-ttu-id="d5c98-191">Genere certificados.</span><span class="sxs-lookup"><span data-stu-id="d5c98-191">Generate certificates.</span></span>

6. <span data-ttu-id="d5c98-192">Agregar grupo de direcciones de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-192">Add hello client address pool.</span></span>

7. <span data-ttu-id="d5c98-193">Cargar datos de certificado público del certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-193">Upload hello root certificate public certificate data.</span></span>

8. <span data-ttu-id="d5c98-194">Generar e instalar el paquete de configuración de cliente VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5c98-194">Generate and install hello VPN client configuration package.</span></span>

9. <span data-ttu-id="d5c98-195">Instale un certificado de cliente exportado.</span><span class="sxs-lookup"><span data-stu-id="d5c98-195">Install an exported client certificate.</span></span>

10. <span data-ttu-id="d5c98-196">Conectar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d5c98-196">Connect tooAzure.</span></span>

11. <span data-ttu-id="d5c98-197">Compruebe la conexión.</span><span class="sxs-lookup"><span data-stu-id="d5c98-197">Verify your connection.</span></span>

<span data-ttu-id="d5c98-198">Para obtener instrucciones detalladas, consulte [configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado: Portal de Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span><span class="sxs-lookup"><span data-stu-id="d5c98-198">For more detailed instructions, see [Configure a Point-to-Site connection tooa VNet using certificate authentication: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)</span></span>

### <a name="ssltls"></a><span data-ttu-id="d5c98-199">SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="d5c98-199">SSL/TLS</span></span>

<span data-ttu-id="d5c98-200">Microsoft recomienda que siempre que usan los datos de tooexchange de protocolos SSL/TLS en diferentes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="d5c98-200">Microsoft recommends that you always use SSL/TLS protocols tooexchange data across different locations.</span></span> <span data-ttu-id="d5c98-201">Las organizaciones que elija toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grandes conjuntos de datos mediante un vínculo WAN de alta velocidad dedicado también puede cifrar los datos de hello en hello mediante TLS/SSL u otros protocolos para una mayor protección de nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5c98-201">Organizations that choose toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove large data sets over a dedicated high-speed WAN link can also encrypt hello data at hello application-level using SSL/TLS or other protocols for added protection.</span></span>

### <a name="encryption-by-default"></a><span data-ttu-id="d5c98-202">Cifrado de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="d5c98-202">Encryption by default</span></span>

<span data-ttu-id="d5c98-203">Microsoft utiliza los datos de tooprotect de cifrado en tránsito entre los clientes y los servicios de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c98-203">Microsoft uses encryption tooprotect data in transit between customers and Azure cloud services.</span></span> <span data-ttu-id="d5c98-204">Si interactúa con el almacenamiento de Azure a través de hello Portal de Azure, todas las transacciones se producen a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d5c98-204">If you are interacting with Azure Storage through hello Azure Portal, all transactions occur via HTTPS.</span></span>

<span data-ttu-id="d5c98-205">[Seguridad de la capa de transporte](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) es el protocolo de Hola que los centros de datos de Microsoft intentará toonegotiate con sistemas de cliente que se conectan tooMicrosoft servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="d5c98-205">[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is hello protocol that Microsoft data centers will attempt toonegotiate with client systems that connect tooMicrosoft cloud services.</span></span> <span data-ttu-id="d5c98-206">TLS proporciona una autenticación sólida, privacidad de mensajes e integridad (lo que permite la detección de la manipulación, interceptación y falsificación de mensajes), interoperabilidad, flexibilidad de algoritmo y facilidad de implementación y uso.</span><span class="sxs-lookup"><span data-stu-id="d5c98-206">TLS provides strong authentication, message privacy, and integrity (enables detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, ease of deployment and use.</span></span>

<span data-ttu-id="d5c98-207">[Confidencialidad directa total](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) también se emplea para que cada conexión entre los sistemas cliente de los clientes y los servicios en la nube de Microsoft use claves únicas.</span><span class="sxs-lookup"><span data-stu-id="d5c98-207">[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) is also employed so that each connection between customers’ client systems and Microsoft’s cloud services use unique keys.</span></span> <span data-ttu-id="d5c98-208">Servicios en la nube tooMicrosoft conexiones también sacar partido de cifrado de 2048 bits RSA según longitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="d5c98-208">Connections tooMicrosoft cloud services also take advantage of RSA based 2,048-bit encryption key lengths.</span></span> <span data-ttu-id="d5c98-209">Hola combinación de TLS, longitudes de clave de RSA 2048 bits, y PFS hace mucho más difícil para un usuario toointercept y acceso a datos que están en tránsito entre servicios de nube de Microsoft y los clientes.</span><span class="sxs-lookup"><span data-stu-id="d5c98-209">hello combination of TLS, RSA 2,048-bit key lengths, and PFS makes it much  more difficult for someone toointercept and access data that is in transit between Microsoft cloud services and customers.</span></span>

<span data-ttu-id="d5c98-210">Los datos en tránsito siempre se cifran en [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span><span class="sxs-lookup"><span data-stu-id="d5c98-210">Data in transit is always encrypted in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview).</span></span> <span data-ttu-id="d5c98-211">Por otra parte media toopersistent de tooencrypting datos toostoring anterior, Hola datos están protegidos también siempre a través de HTTPS en tránsito.</span><span class="sxs-lookup"><span data-stu-id="d5c98-211">In addition tooencrypting data prior toostoring toopersistent media, hello data is also always secured in transit by using HTTPS.</span></span> <span data-ttu-id="d5c98-212">HTTPS es Hola único protocolo admitido para hello que REST de almacén de datos Lake interfaces.</span><span class="sxs-lookup"><span data-stu-id="d5c98-212">HTTPS is hello only protocol that is supported for hello Data Lake Store REST interfaces.</span></span>

## <a name="summary"></a><span data-ttu-id="d5c98-213">Resumen</span><span class="sxs-lookup"><span data-stu-id="d5c98-213">Summary</span></span>

<span data-ttu-id="d5c98-214">empresa Hola puede lograr su objetivo de proteger la privacidad hello y datos personal de tales datos exigir HTTPS conexiones tooAzure almacenamiento, mediante firmas de acceso compartido y habilitar la transferencia segura necesaria hello en cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d5c98-214">hello company can accomplish its goal of protecting personal data and hello privacy of such data by enforcing HTTPS connections tooAzure Storage, using Shared Access Signatures and enabling Secure Transfer Required on hello storage accounts.</span></span> <span data-ttu-id="d5c98-215">También puede proteger datos personales mediante conexiones SMB 3.0 e implementando cifrado de cliente.</span><span class="sxs-lookup"><span data-stu-id="d5c98-215">They can also protect personal data by using SMB 3.0 connections and implementing client-side encryption.</span></span> <span data-ttu-id="d5c98-216">Hola a las conexiones VPN de sitio a sitio de red corporativa toohello red virtual de Azure y conexiones de point-to-site VPN de los usuarios individuales crean un túnel seguro a través del cual pueden viajar forma segura los datos personales.</span><span class="sxs-lookup"><span data-stu-id="d5c98-216">Site-to-site VPN connections from hello corporate network toohello Azure virtual network and point-to-site VPN connections from individual users will create a secure tunnel through which personal data can securely travel.</span></span> <span data-ttu-id="d5c98-217">Prácticas de cifrado predeterminado de Microsoft protegerá aún más la privacidad de Hola de los datos personales.</span><span class="sxs-lookup"><span data-stu-id="d5c98-217">Microsoft’s default encryption practices will further protect hello privacy of personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5c98-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5c98-218">Next steps</span></span>

- [<span data-ttu-id="d5c98-219">Procedimientos recomendados de cifrado y seguridad de datos en Azure</span><span class="sxs-lookup"><span data-stu-id="d5c98-219">Azure Data Security and Encryption Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [<span data-ttu-id="d5c98-220">Planeamiento y diseño de VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="d5c98-220">Planning and design for VPN Gateway</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [<span data-ttu-id="d5c98-221">Preguntas más frecuentes sobre VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="d5c98-221">VPN Gateway FAQ</span></span>](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [<span data-ttu-id="d5c98-222">Compra y configuración de un certificado SSL para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d5c98-222">Buy and configure an SSL Certificate for your Azure App Service</span></span>](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
