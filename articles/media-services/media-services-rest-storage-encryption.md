---
title: aaaEncrypting su contenido con cifrado de almacenamiento mediante la API de REST de AMS
description: "Obtenga información acerca de cómo tooencrypt su contenido con cifrado de almacenamiento mediante las API de REST de AMS."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="ff0cc-103">Cifrado del contenido con cifrado de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ff0cc-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="ff0cc-104">Se recomienda encarecidamente tooencrypt el contenido localmente con AES-256 bits cifrado y, a continuación, cargarlo tooAzure almacenamiento donde se almacenarán cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="ff0cc-105">Este artículo ofrece una visión general del cifrado de almacenamiento de AMS y muestra cómo de contenido cifrado de almacenamiento de Hola tooupload:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="ff0cc-106">Cree una clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-106">Create a content key.</span></span>
* <span data-ttu-id="ff0cc-107">Cree un recurso.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-107">Create an Asset.</span></span> <span data-ttu-id="ff0cc-108">Establecer hello AssetCreationOption tooStorageEncryption al crear Hola activo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="ff0cc-109">Los recursos cifrados tienen toobe asociado con las claves de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="ff0cc-110">Recurso de vínculo hello toohello de clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="ff0cc-111">Establecer parámetros en entidades de AssetFile Hola relacionadas con el cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="ff0cc-112">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="ff0cc-112">Considerations</span></span> 

<span data-ttu-id="ff0cc-113">Si desea toodeliver un recurso cifrado de almacenamiento, debe configurar la directiva de entrega del activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="ff0cc-114">Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="ff0cc-115">Para obtener más información, consulte [Configuración de directivas de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="ff0cc-116">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ff0cc-117">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="ff0cc-118">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="ff0cc-118">Connect tooMedia Services</span></span>

<span data-ttu-id="ff0cc-119">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ff0cc-120">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ff0cc-121">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="ff0cc-122">Información general del cifrado de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ff0cc-122">Storage encryption overview</span></span>
<span data-ttu-id="ff0cc-123">se aplica el cifrado de almacenamiento de Hello AMS **AES-CTR** toohello todo archivo de cifrado de modo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="ff0cc-124">El modo AES-CTR es un cifrado de bloques que puede cifrar los datos de longitud arbitraria sin necesidad de relleno.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="ff0cc-125">Funciona mediante el cifrado de un bloque de contador con el algoritmo AES de hello y, a continuación, la salida de hello de ing XOR de AES con hello datos tooencrypt o descifrar.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="ff0cc-126">bloque de contador de Hello usado se crea copiando valor Hola de hello InitializationVector toobytes 0 too7 del valor de contador de Hola y too15 de 8 bytes del valor de contador de Hola se establecen toozero.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="ff0cc-127">Del bloque de contador de 16 bytes de hello, too15 de 8 bytes (es decir, Hola los bytes menos significativos) se usan como un entero sin signo de 64 bits simple que se incrementa en uno para cada bloque de datos procesada posterior y es que se mantiene en el orden de bytes de red.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="ff0cc-128">Tenga en cuenta que si este entero alcanza el valor máximo de hello (0xFFFFFFFFFFFFFFFF) incrementarlo, a continuación, restablece Hola bloque contador toozero (8 bytes too15) sin que afecte a Hola otro 64 bits del contador de hello (es decir, too7 bytes 0).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="ff0cc-129">En orden toomaintain Hola de seguridad de cifrado de modo de hello CTR AES, hello InitializationVector valor para un determinado identificador de clave para cada clave de contenido debe ser único para cada archivo y archivos deben ser inferior a 2 ^ 64 bloques de longitud.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="ff0cc-130">Se trata de tooensure que un valor de contador nunca se reutilizan con una clave determinada.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="ff0cc-131">Para obtener más información acerca del modo CTR hello, consulte [esta página wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (artículo de wiki de hello usa el término Hola "Nonce" en lugar de "InitializationVector").</span><span class="sxs-lookup"><span data-stu-id="ff0cc-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="ff0cc-132">Use **cifrado de almacenamiento** tooencrypt el contenido no localmente mediante AES-256 bits cifrado y, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ff0cc-133">Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="ff0cc-134">caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure sitúe los archivos multimedia de entrada de gran calidad con cifrado de alta seguridad en disco.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="ff0cc-135">En orden toodeliver un recurso cifrado de almacenamiento, debe configurar Directiva de entrega del activo de Hola para que Servicios multimedia sepa cómo desea toodeliver su contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="ff0cc-136">Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega (por ejemplo, AES, cifrado común o sin cifrado).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="ff0cc-137">Creación de ContentKeys para el cifrado</span><span class="sxs-lookup"><span data-stu-id="ff0cc-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="ff0cc-138">Los recursos cifrados tienen toobe asociado a la clave de cifrado de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="ff0cc-139">Debe crear hello toobe clave contenido usado para el cifrado antes de crear archivos de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="ff0cc-140">Esta sección se describe cómo toocreate una clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="ff0cc-141">Hello siguientes son pasos generales para la generación de claves de contenido que se asociará con activos que desea toobe cifrado.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="ff0cc-142">Para el cifrado de almacenamiento, genere de forma aleatoria una clave AES de 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="ff0cc-143">Se trata de clave de contenido de hello para el recurso, lo que significa que todos los archivos asociados a ese recurso se necesita toouse Hola misma clave de contenido durante el descifrado.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="ff0cc-144">Llamar a hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) y [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget métodos Hola certificado X.509 correcto que debe ser tooencrypt usa la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="ff0cc-145">Cifrar la clave de contenido con clave pública de Hola de hello certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="ff0cc-146">SDK de .NET de servicios multimedia usa RSA con OAEP al realizar el cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="ff0cc-147">Puede ver un ejemplo de .NET en hello [EncryptSymmetricKeyData función](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="ff0cc-148">Crear un valor de suma de comprobación calculado mediante el identificador de clave de Hola y clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="ff0cc-149">Hola siguiente ejemplo .NET calcula la suma de comprobación de hello mediante Hola GUID parte del identificador de clave de Hola y Hola borrar la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. <span data-ttu-id="ff0cc-150">Crear clave de contenido de hello con hello **EncryptedContentKey** (convierte la cadena codificada en toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, y **suma de comprobación** valores recibidos en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="ff0cc-151">Para el cifrado de almacenamiento, hello siguientes propiedades se deben incluir en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="ff0cc-152">Propiedad del cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="ff0cc-152">Request body property</span></span>    | <span data-ttu-id="ff0cc-153">Description</span><span class="sxs-lookup"><span data-stu-id="ff0cc-153">Description</span></span>
    ---|---
    <span data-ttu-id="ff0cc-154">Id</span><span class="sxs-lookup"><span data-stu-id="ff0cc-154">Id</span></span> | <span data-ttu-id="ff0cc-155">Hello identificador de ContentKey que generamos desarrollamos con hello después de dar formato, "NB:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="ff0cc-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="ff0cc-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="ff0cc-156">ContentKeyType</span></span> | <span data-ttu-id="ff0cc-157">Este es el tipo de clave contenido de Hola como un número entero para esta clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="ff0cc-158">Pasamos el valor de hello 1 para el cifrado de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="ff0cc-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="ff0cc-159">EncryptedContentKey</span></span> | <span data-ttu-id="ff0cc-160">Creamos un valor de clave de contenido que es un valor de 256 bits (32 bytes).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="ff0cc-161">clave de Hola se cifra mediante el certificado X.509 de cifrado de almacenamiento de Hola que recuperamos de servicios multimedia de Microsoft Azure mediante la ejecución de una solicitud HTTP GET hello GetProtectionKeyId y GetProtectionKey métodos.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="ff0cc-162">Por ejemplo, vea Hola después código .NET: Hola **EncryptSymmetricKeyData** método definido [aquí](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="ff0cc-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ff0cc-163">ProtectionKeyId</span></span> | <span data-ttu-id="ff0cc-164">Esto es Hola Id. de clave de protección para el certificado X.509 de cifrado de almacenamiento de Hola que estaba tooencrypt usa la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="ff0cc-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="ff0cc-165">ProtectionKeyType</span></span> | <span data-ttu-id="ff0cc-166">Se trata de un tipo de cifrado de hello para la clave de protección de Hola que fue utilizado tooencrypt Hola contenido clave.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="ff0cc-167">Este valor es StorageEncryption(1) en nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="ff0cc-168">Checksum</span><span class="sxs-lookup"><span data-stu-id="ff0cc-168">Checksum</span></span> |<span data-ttu-id="ff0cc-169">Hola MD5 suma de comprobación calculada Hola clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="ff0cc-170">Se calcula mediante el cifrado de contenido de hello identificador con clave de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="ff0cc-171">código de ejemplo de Hola muestra cómo toocalculate Hola suma de comprobación.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="ff0cc-172">Recuperar hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ff0cc-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="ff0cc-173">Hola de ejemplo siguiente muestra cómo tooretrieve Hola ProtectionKeyId, una huella digital del certificado, debe usar al cifrar la clave de contenido de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="ff0cc-174">Realice este toomake paso que ya ha certificado adecuado de hello en su equipo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="ff0cc-175">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="ff0cc-176">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-176">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="ff0cc-177">Recuperar hello ProtectionKey para hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ff0cc-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="ff0cc-178">Hello en el ejemplo siguiente se muestra cómo certificado X.509 de hello tooretrieve mediante hello ProtectionKeyId haya recibido en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="ff0cc-179">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="ff0cc-180">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-180">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a><span data-ttu-id="ff0cc-181">Crear clave de contenido de Hola</span><span class="sxs-lookup"><span data-stu-id="ff0cc-181">Create hello content key</span></span>
<span data-ttu-id="ff0cc-182">Después de haber recuperado el certificado X.509 de Hola y usa su tooencrypt de clave pública de la clave de contenido, crear un **ContentKey** entidad y establezca su propiedad valores según corresponda.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="ff0cc-183">Uno de los valores de hello que debe establecer al crear contenido clave es de tipo Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="ff0cc-184">En el caso de cifrado de almacenamiento de hello, el valor de hello es '1'.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="ff0cc-185">Hola siguiente ejemplo se muestra cómo toocreate una **ContentKey** con un **ContentKeyType** establecido para el cifrado de almacenamiento ("1") y hello **ProtectionKeyType** establecido demasiado "0" tooindicate que Hola Id de la clave de protección es la huella digital del certificado de hello X.509.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="ff0cc-186">Solicitud</span><span class="sxs-lookup"><span data-stu-id="ff0cc-186">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="ff0cc-187">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-187">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="ff0cc-188">Creación de un recurso</span><span class="sxs-lookup"><span data-stu-id="ff0cc-188">Create an asset</span></span>
<span data-ttu-id="ff0cc-189">Hola siguiente ejemplo se muestra cómo toocreate un activo.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="ff0cc-190">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="ff0cc-190">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="ff0cc-191">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="ff0cc-191">**HTTP Response**</span></span>

<span data-ttu-id="ff0cc-192">Si se realiza correctamente, se devuelve el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-192">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="ff0cc-193">Asociar hello ContentKey a un activo</span><span class="sxs-lookup"><span data-stu-id="ff0cc-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="ff0cc-194">Después de crear hello ContentKey, asociarla a su activo mediante la operación de hello $links, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="ff0cc-195">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-195">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="ff0cc-196">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="ff0cc-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="ff0cc-197">Creación de AssetFile</span><span class="sxs-lookup"><span data-stu-id="ff0cc-197">Create an AssetFile</span></span>
<span data-ttu-id="ff0cc-198">Hola [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidad representa un archivo de vídeo o audio que se almacena en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="ff0cc-199">Un archivo de recursos siempre está asociado a un recurso y un recurso puede contener uno o varios archivos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="ff0cc-200">se produce un error en la tarea de codificador de servicios multimedia de Hello si un objeto de archivo de recursos no está asociado a un archivo digital de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="ff0cc-201">Tenga en cuenta que hello **AssetFile** instancia y archivo de hello multimedia real son dos objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="ff0cc-202">instancia de AssetFile Hola contiene metadatos sobre archivo multimedia de hello, mientras que el archivo de medios de hello contiene contenido multimedia real de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff0cc-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="ff0cc-203">Después de cargar el archivo multimedia digital en un contenedor de blobs, usará hello **mezcla** tooupdate hello AssetFile HTTP solicitud con información sobre el archivo de medios (no se muestra en este tema).</span><span class="sxs-lookup"><span data-stu-id="ff0cc-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="ff0cc-204">**Solicitud HTTP**</span><span class="sxs-lookup"><span data-stu-id="ff0cc-204">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="ff0cc-205">**Respuesta HTTP**</span><span class="sxs-lookup"><span data-stu-id="ff0cc-205">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
