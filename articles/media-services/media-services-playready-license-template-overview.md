---
title: "Introducción de plantilla de licencia de PlayReady de los servicios de aaaMedia"
description: "En este tema se ofrece una visión general de una plantilla de licencia de PlayReady que usa tooconfigure licencias de PlayReady."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="4c780-103">Información general de plantillas de licencias de PlayReady de Media Services</span><span class="sxs-lookup"><span data-stu-id="4c780-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="4c780-104">Servicios multimedia de Azure proporciona un servicio para entregar licencias de Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="4c780-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="4c780-105">Cuando el Reproductor del usuario final hello (por ejemplo, Silverlight) intenta tooplay contenido protegido con la PlayReady, una solicitud es enviado toohello licencia entrega servicio tooobtain una licencia.</span><span class="sxs-lookup"><span data-stu-id="4c780-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="4c780-106">Si el servicio de licencias de hello aprueba la solicitud de hello, que emite la licencia de Hola que es enviado toohello cliente y puede ser usado toodecrypt y play Hola contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="4c780-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="4c780-107">Servicios multimedia también proporciona API que permiten configurar sus licencias de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="4c780-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="4c780-108">Las licencias contienen los derechos de Hola y restricciones que desea para hello tooenforce en tiempo de ejecución de DRM de PlayReady cuando un usuario trate de tooplayback contenido protegido.</span><span class="sxs-lookup"><span data-stu-id="4c780-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="4c780-109">A continuación se muestran algunos ejemplos de restricciones de licencia de PlayReady que puede especificar:</span><span class="sxs-lookup"><span data-stu-id="4c780-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="4c780-110">fecha y hora de Hola desde qué Hola licencia es válida.</span><span class="sxs-lookup"><span data-stu-id="4c780-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="4c780-111">valor de fecha y hora cuando expira la licencia de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="4c780-112">Para toobe de licencia de hello guardada en un almacenamiento persistente en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="4c780-113">Las licencias persistentes son utilizados normalmente tooallow sin conexión reproducción de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="4c780-114">Hola nivel mínimo de seguridad que debe tener un reproductor tooplay su contenido.</span><span class="sxs-lookup"><span data-stu-id="4c780-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="4c780-115">Hola de salida de nivel de protección para los controles de salida de hello para el contenido de audio/vídeo.</span><span class="sxs-lookup"><span data-stu-id="4c780-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="4c780-116">Para obtener más información, vea controles de salida de hello (3.5) hello en la sección [reglas de compatibilidad de PlayReady](https://www.microsoft.com/playready/licensing/compliance/) documento.</span><span class="sxs-lookup"><span data-stu-id="4c780-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="4c780-117">Actualmente, solo se puede configurar hello PlayRight de licencia de PlayReady de hello (este derecho es necesario).</span><span class="sxs-lookup"><span data-stu-id="4c780-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="4c780-118">Hola PlayRight le ofrece a cliente hello contenido de hello capacidad tooplayback Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="4c780-119">Hola PlayRight también permite configurar restricciones específicas tooplayback.</span><span class="sxs-lookup"><span data-stu-id="4c780-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="4c780-120">Para obtener más información, consulte [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="4c780-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="4c780-121">tooconfigure licencias de PlayReady con servicios multimedia, debe configurar la plantilla de licencia de PlayReady de servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="4c780-122">plantilla de Hola se define en XML.</span><span class="sxs-lookup"><span data-stu-id="4c780-122">hello template is defined in XML.</span></span>

<span data-ttu-id="4c780-123">Hello en el ejemplo siguiente se muestra hello más sencilla (y más común) plantilla que configura una licencia básica de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="4c780-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="4c780-124">Con esta licencia, los clientes sería capaz de tooplayback contenido protegido con la PlayReady.</span><span class="sxs-lookup"><span data-stu-id="4c780-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="4c780-125">Hola XML cumple el esquema toohello PlayReady licencia plantilla XML definido en la plantilla de licencia de PlayReady de hello sección de esquema XML.</span><span class="sxs-lookup"><span data-stu-id="4c780-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="4c780-126">Servicios multimedia también define un conjunto de clases de .NET que puede ser usado tooserialized y tooand deserializado de hello XML.</span><span class="sxs-lookup"><span data-stu-id="4c780-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="4c780-127">Para obtener una descripción de las clases principales, vea [Clases .NET de Media Services](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="4c780-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="4c780-128">que son plantillas de licencia de uso tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="4c780-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="4c780-129">Para un ejemplo de extremo a extremo que utiliza .NET clases de plantilla de licencia de PlayReady tooconfigure hello, consulte [usar cifrado dinámico PlayReady y del servicio de entrega de licencias](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="4c780-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="4c780-130"><a id="classes"></a>Clases de .NET de los servicios multimedia son plantillas de licencia de uso tooconfigure</span><span class="sxs-lookup"><span data-stu-id="4c780-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="4c780-131">siguiente Hola es clases .NET principales de hello son plantillas de licencia de PlayReady de servicios multimedia de tooconfigure usado.</span><span class="sxs-lookup"><span data-stu-id="4c780-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="4c780-132">Estas clases asignan los tipos de toohello definidos en [esquema XML de plantilla de licencia de PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="4c780-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="4c780-133">Hola [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) clase es tooserialize usado y deserializar tooand de plantilla de licencia de servicios multimedia de hello XML.</span><span class="sxs-lookup"><span data-stu-id="4c780-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="4c780-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="4c780-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="4c780-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -esta clase representa la plantilla de hello para la respuesta de hello envía toohello back-end usuario.</span><span class="sxs-lookup"><span data-stu-id="4c780-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="4c780-136">Contiene un campo de una cadena de datos personalizados entre el servidor de licencias de Hola y la aplicación hello (pueden ser útiles para la lógica de aplicación personalizada), así como una lista de uno o más plantillas de licencia.</span><span class="sxs-lookup"><span data-stu-id="4c780-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="4c780-137">Se trata de clase de "nivel superior" hello en la jerarquía de plantillas de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="4c780-138">Lo que significa que la plantilla de respuesta de hello incluye una lista de plantillas de licencia y plantillas de licencia de hello incluyen (directa o indirectamente) todos Hola otras clases que constituyen Hola plantilla datos toobe serializado.</span><span class="sxs-lookup"><span data-stu-id="4c780-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="4c780-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="4c780-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="4c780-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -clase hello representa una plantilla de licencia para crear toobe de licencias de PlayReady devuelve los usuarios finales de toohello.</span><span class="sxs-lookup"><span data-stu-id="4c780-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="4c780-141">Contiene datos de tipo hello en la clave de contenido de hello en licencias de Hola y cualquier toobe derechos o restricciones exige hello en tiempo de ejecución de DRM de PlayReady al usar la clave de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="4c780-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="4c780-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="4c780-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -esta clase representa hello PlayRight de una licencia de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="4c780-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="4c780-144">Concede Hola usuario Hola capacidad tooplayback Hola contenido sujeto toohello cero o más restricciones configuradas en la licencia de Hola y en hello PlayRight (para reproducir una directiva específica).</span><span class="sxs-lookup"><span data-stu-id="4c780-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="4c780-145">Gran parte de la directiva de hello en hello PlayRight tiene toodo con las restricciones de salida que controlan Hola tipos de salidas que puede reproducirse el contenido de Hola y las restricciones que se deben incluir en su lugar al usar una salida específica.</span><span class="sxs-lookup"><span data-stu-id="4c780-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="4c780-146">Por ejemplo, si se habilita DigitalVideoOnlyContentRestriction, el Hola Hola, a continuación, en tiempo de ejecución DRM solo permitirá hello toobe vídeo muestre en salidas digitales (salidas de vídeo analógicas no podrán contenido de hello toopass).</span><span class="sxs-lookup"><span data-stu-id="4c780-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c780-147">Estos tipos de restricciones pueden ser muy eficaces, pero también pueden afectar a la experiencia del consumidor Hola.</span><span class="sxs-lookup"><span data-stu-id="4c780-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="4c780-148">Si las protecciones de salida de hello están configuradas demasiado restrictiva, contenido de hello podría no reproducirse en algunos clientes.</span><span class="sxs-lookup"><span data-stu-id="4c780-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="4c780-149">Para obtener más información, vea hello [reglas de compatibilidad de PlayReady](https://www.microsoft.com/playready/licensing/compliance/) documento.</span><span class="sxs-lookup"><span data-stu-id="4c780-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="4c780-150">Para ver un ejemplo de los niveles de protección que admite Silverlight, consulte: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="4c780-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="4c780-151"><a id="schema"></a>Esquema XML de la plantilla de licencia de PlayReady</span><span class="sxs-lookup"><span data-stu-id="4c780-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="4c780-152">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="4c780-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4c780-153">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="4c780-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

