---
title: aaaCryptography - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Marco de seguridad: Criptografía | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Aplicación web** | <ul><li>[Use solamente los cifrados de bloques simétricos y longitudes de clave aprobados](#cipher-length)</li><li>[Use modos aprobados de cifrado de bloques y vectores de inicialización apropiados para los cifrados simétricos](#vector-ciphers)</li><li>[Use algoritmos asimétricos, longitudes de clave y rellenos aprobados](#padding)</li><li>[Use generadores de números aleatorios aprobados](#numgen)</li><li>[No use cifrados de flujo simétricos](#stream-ciphers)</li><li>[Use los algoritmos hash con clave MAC o HMAC aprobados](#mac-hash)</li><li>[Use solamente las funciones hash criptográficas aprobadas](#hash-functions)</li></ul> |
| **Base de datos** | <ul><li>[Usar datos de tooencrypt de algoritmos de cifrado de alta seguridad en la base de datos de Hola](#strong-db)</li><li>[Los paquetes SSIS deben cifrarse y firmarse digitalmente](#ssis-signed)</li><li>[Agregar elementos protegibles de base de datos de toocritical de firma digital](#securables-db)</li><li>[Utilizar claves de cifrado de SQL server EKM tooprotect](#ekm-keys)</li><li>[Usar la característica de AlwaysEncrypted si las claves de cifrado no deben tooDatabase revelados motor](#keys-engine)</li></ul> |
| **Dispositivo de IoT** | <ul><li>[Almacene las claves criptográficas de forma segura en dispositivos IoT](#keys-iot)</li></ul> | 
| **Puerta de enlace de nube de IoT** | <ul><li>[Generar una clave simétrica aleatoria de longitud suficiente para autenticación tooIoT concentrador](#random-hub)</li></ul> | 
| **Cliente para dispositivos móviles de Dynamics CRM** | <ul><li>[Asegúrese de que hay una directiva de administración de dispositivos que requiere el uso de un PIN y permite el borrado remoto](#pin-remote)</li></ul> | 
| **Cliente de Outlook de Dynamics CRM** | <ul><li>[Asegúrese de que hay una directiva de administración de dispositivos que requiere un bloqueo automático con PIN o contraseña, y cifra todos los datos (por ejemplo, Bitlocker)](#bitlocker)</li></ul> | 
| **Identity Server** | <ul><li>[Asegúrese de que las claves de firma se sustituyen cuando se usa Identity Server](#rolled-server)</li><li>[Asegúrese de que se usan un identificador de cliente y un secreto de cliente de alta seguridad criptográfica en Identity Server](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Use solamente los cifrados de bloques simétricos y longitudes de clave aprobados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Productos deben usar solo los cifrados de bloques simétrico y longitudes de clave asociadas que se han aprobado explícitamente por hello Crypto asesor en su organización. Los algoritmos simétricos aprobados de Microsoft incluyen hello siguiendo los cifrados de bloques:</p><ul><li>Para el nuevo código son aceptables AES-128, AES-192 y AES-256</li><li>Para mantener la compatibilidad con el código existente, el algoritmo 3DES de tres claves es aceptable</li><li>Para los productos con cifrados de bloques simétricos:<ul><li>El estándar de cifrado avanzado (AES) es necesario para el nuevo código</li><li>El estándar de cifrado de datos triple (3DES) con tres claves está permitido en el código existente para proporcionar la compatibilidad con versiones anteriores</li><li>Todos los demás cifrados de bloques, como RC2, DES, 3DES de dos claves, DESX y Skipjack, solo pueden usarse para descifrar datos antiguos y tienen que reemplazarse si se usan para el cifrado</li></ul></li><li>Para los algoritmos de cifrado de bloques simétrico, se requiere una longitud de clave mínima de 128 bits. Hola solo el algoritmo de cifrado de bloques se recomienda para nuevo código es AES (AES-128, AES-192 y AES-256 son aceptables)</li><li>Tres clave 3DES es actualmente aceptable si ya está en uso en el código existente; se recomienda tooAES de transición. DES, DESX, RC2 y Skipjack ya no se consideran seguros. Estos algoritmos sólo pueden utilizarse para descifrar los datos existentes para simplificar Hola compatibilidad con versiones anteriores y datos se deben volver a cifrar mediante un cifrado por bloques recomendada</li></ul><p>Tenga en cuenta que todos los cifrados de bloques simétricos tienen que usarse con un modo de cifrado aprobado, lo que requiere el uso de un vector de inicialización (IV) adecuado. Un vector de inicialización adecuado, suele ser un número aleatorio y nunca un valor constante</p><p>uso de Hola de heredado o de otra manera de los algoritmos criptográficos no aprobados y longitudes de clave más pequeñas para leer los datos existentes (como toowriting lugar nuevos datos) puede permitirse después de revisar el panel de la clave criptográfica de su organización. Sin embargo, debe solicitar una excepción en contra de este requisito. Además, en las implementaciones empresariales, productos deben considerar los administradores de advertencia cuando criptografía no segura datos tooread usado. Dichas advertencias deben ser explicativas y prácticas. En algunos casos, puede ser adecuado toohave uso de Hola de control de directiva de grupo de criptografía no segura</p><p>Algoritmos .NET permitidos para criptografía personal administrada (en orden de preferencia)</p><ul><li>AesCng (compatible con FIPS)</li><li>AuthenticatedAesCng (compatible con FIPS)</li><li>AESCryptoServiceProvider (compatible con FIPS)</li><li>AESManaged (no compatible con FIPS)</li></ul><p>Tenga en cuenta que ninguno de estos algoritmos se pueden especificar a través de hello `SymmetricAlgorithm.Create` o `CryptoConfig.CreateFromName` métodos sin realizar el archivo machine.config de toohello de cambios. Además, tenga en cuenta que se denomina AES en las versiones de too.NET anteriores de .NET 3.5 `RijndaelManaged`, y `AesCng` y `AuthenticatedAesCng` son > disponible a través de CodePlex y requieren CNG en hello subyacente SO</p>

## <a id="vector-ciphers"></a>Use modos aprobados de cifrado de bloques y vectores de inicialización apropiados para los cifrados simétricos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Todos los cifrados de bloques simétricos tienen que utilizarse con un modo de cifrado simétrico aprobado. modos de Hello solo aprobado son CBC y CTS. En concreto, debería evitarse modo de funcionamiento de hello código electrónica (ECB) del libro; uso de ECB requiere revisión de panel de criptografía de su organización. Todo posible uso de OFB, CFB, CTR, CCM y GCM o cualquier otro modo de cifrado tiene que revisarlo la junta de criptografía de su organización. Reutilizar Hola mismo vector de inicialización (IV) con el cifrado de bloques en "streaming cifrados de los modos," como CTR, puede provocar toobe datos cifrados revelada. Todos los cifrados de bloques simétricos tienen que utilizarse también con un vector de inicialización (IV) adecuado. Un vector de inicialización adecuado es un número aleatorio de alta seguridad criptográfica y nunca un valor constante. |

## <a id="padding"></a>Use algoritmos asimétricos, longitudes de clave y rellenos aprobados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>uso de Hola de algoritmos criptográficos prohibidos presenta un riesgo significativo tooproduct seguridad y debe evitarse. Los productos tienen que usar solo los algoritmos criptográficos, las longitudes de clave y los rellenos que la junta de criptografía de su organización haya aprobado explícitamente.</p><ul><li>**RSA:** puede utilizarse para el cifrado, el intercambio de claves y la firma. El cifrado RSA debe usar solo Hola OAEP o RSA-KEM modos de relleno. El código existente puede utilizar el modo de relleno PKCS #1 v1.5 solo si es necesario para garantizar la compatibilidad. El uso de relleno nulo está explícitamente prohibido. El nuevo código requiere claves de 2048 bits o más. El código existente puede admitir claves de menos de 2048 bits solamente para garantizar la compatibilidad con versiones anteriores, y después de una revisión por parte de la junta de criptografía de su organización. La claves de menos de 1024 bits se pueden usar únicamente para descifrar o verificar datos antiguos, y tienen que remplazarse si se utilizan para operaciones de cifrado o firma</li><li>**ECDSA:** puede utilizarse solo para la firma. El nuevo código requiere ECDSA con claves de 256 bits o más. Las firmas basadas en ECDSA deben usar uno de curvas NIST aprobado Hola tres (p-256, p-384 o P521). Las curvas que se han analizado exhaustivamente pueden utilizarse solo después de una revisión por parte de la junta de criptografía de su organización.</li><li>**ECDH:** puede utilizarse solamente para el intercambio de claves. El nuevo código requiere ECDH con claves de 256 bits o más. Intercambio de claves de ECDH debe usar uno de curvas NIST aprobado Hola tres (p-256, p-384 o P521). Las curvas que se han analizado exhaustivamente pueden utilizarse solo después de una revisión por parte de la junta de criptografía de su organización.</li><li>**DSA:** puede ser aceptable después de la revisión y aprobación por parte de la junta de criptografía de su organización. Póngase en contacto con su tooschedule de Asesor de seguridad revisión de la placa de criptografía de su organización. Si se aprueba el uso de DSA, tenga en cuenta que necesitará tooprohibit uso de claves de menos de 2048 bits de longitud. CNG admite longitudes de clave de 2048 bits y superiores a partir de Windows 8.</li><li>**Diffie-Hellman:** se puede usar para la administración de claves de sesión únicamente. El nuevo código requiere claves con una longitud de 2048 bits o más. El código existente puede admitir claves con una longitud inferior a 2048 bits solo para garantizar la compatibilidad con versiones anteriores y después de una revisión por parte de la junta de criptografía de la organización. La claves de menos de 1024 no se pueden usar.</li><ul>

## <a id="numgen"></a>Use generadores de números aleatorios aprobados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Los productos tienen que usar generadores de números aleatorios aprobados. Funciones pseudoaleatorios como rand de función en tiempo de ejecución de C de hello, clase de .NET Framework de hello System.Random o funciones del sistema como GetTickCount no deben, por lo tanto, nunca se usará en este código. Se prohíbe el uso de hello dual curva elíptica aleatorio algoritmo generador de números (DUAL_EC_DRBG)</p><ul><li>**CNG -** BCryptGenRandom (uso de hello BCRYPT_USE_SYSTEM_PREFERRED_RNG marca recomendada a menos que el llamador de hello pudiera ejecutarse en cualquier IRQL mayor que 0 [es decir, PASSIVE_LEVEL])</li><li>**CAPI:** cryptGenRandom</li><li>**Win32/64:** RtlGenRandom (las implementaciones nuevas deben utilizar BCryptGenRandom o CryptGenRandom) * rand_s * SystemPrng (para el modo de kernel)</li><li>**.NET:** RNGCryptoServiceProvider o RNGCng</li><li>**Aplicaciones de la Tienda Windows:** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom o .GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (SecRandomRef aleatorio, recuento de size_t, uint8_t *bytes)</li><li>**Apple OS X (< 10.7)-** Use / tooretrieve dev/aleatoria de números aleatorios</li><li>**Java (incluido código Google Android Java) -** java.security.SecureRandom clase. Tenga en cuenta que para Android 4.3 (jalea Bean), los desarrolladores deben siga Hola Android recomienda solución alternativa y actualizar su aplicaciones tooexplicitly inicializar hello PRNG con entropía de /dev/urandom o/dev/Random</li></ul>|

## <a id="stream-ciphers"></a>No use cifrados de flujo simétricos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | No pueden usarse cifrados de flujos simétricos, como RC4. En lugar de cifrados de flujos simétricos, los productos deberían utilizar un cifrado por bloques, específicamente AES con una longitud de clave de 128 bits como mínimo. |

## <a id="mac-hash"></a>Use los algoritmos hash con clave MAC o HMAC aprobados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Los productos deben usar solo los algoritmos aprobados de código de autenticación de mensajes (MAC) o código de autenticación de mensajes basado en hash (HMAC).</p><p>Un código de autenticación de mensajes (MAC) es un fragmento del mensaje de tooa adjunto de información que permite que su destinatario tooverify tanto autenticidad de hello del remitente de Hola y la integridad de Hola de mensaje hello mediante una clave secreta. Hola de uso de un MAC basado en hash ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) o [MAC basados en el cifrado de bloques](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) está permitida como hash de todas las subyacente o algoritmos de cifrado simétricos también están aprobados para su uso; actualmente esto incluye Hola HMAC SHA2 funciones (HMAC-SHA256, SHA384 HMAC y HMAC-SHA512) y hello CMAC/OMAC1 y OMAC2 bloquean Mac basada en cifrado (se basan en AES).</p><p>Uso de HMAC-SHA1 puede estar autorizada para la compatibilidad con plataformas, pero se pueden toofile requiere un procedimiento de toothis de excepción y realizarse revisión de cifrado de su organización. No se permite el truncamiento de HMAC que no requiere herramientas de 128 bits. Utilizando métodos de cliente toohash una clave y los datos no se ha aprobado y debe someterse a toouse de su organización Crypto panel revisión anterior.</p>|

## <a id="hash-functions"></a>Use solamente las funciones hash criptográficas aprobadas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Productos deben utilizar la familia de hello SHA-2 de algoritmos de hash (SHA256, SHA384 y SHA512). Si se necesita un hash más corto, por ejemplo, una longitud de 128 bits salida en orden toofit una estructura de datos diseñada con el hash de MD5 más corto de hello en mente, los equipos del producto pueden truncar uno de los valores de hash de hello SHA2 (normalmente SHA256). Tenga en cuenta que SHA384 es una versión truncada de SHA512. No se permite el truncamiento de los algoritmos hash criptográficos para la seguridad con fines que no requiere herramientas de 128 bits. Nuevo código no debe utilizar los algoritmos de hash MD2, MD4, MD5, SHA-0, SHA-1 o RIPEMD Hola. Las colisiones de hash son factibles desde el punto de vista computacional para estos algoritmos, lo que de forma efectiva supone su ruptura.</p><p>Algoritmos hash de .NET permitidos para criptografía personal administrada (en orden de preferencia):</p><ul><li>SHA512Cng (compatible con FIPS)</li><li>SHA384Cng (compatible con FIPS)</li><li>SHA256Cng (compatible con FIPS)</li><li>SHA512Managed (no compatible FIPS) (use SHA512 como nombre del algoritmo en llamadas tooHashAlgorithm.Create o CryptoConfig.CreateFromName)</li><li>SHA384Managed (no compatible FIPS) (use SHA384 como nombre del algoritmo en llamadas tooHashAlgorithm.Create o CryptoConfig.CreateFromName)</li><li>SHA256Managed (no compatible FIPS) (use SHA256 como nombre del algoritmo en llamadas tooHashAlgorithm.Create o CryptoConfig.CreateFromName)</li><li>SHA512CryptoServiceProvider (compatible con FIPS)</li><li>SHA256CryptoServiceProvider (compatible con FIPS)</li><li>SHA384CryptoServiceProvider (compatible con FIPS)</li></ul>| 

## <a id="strong-db"></a>Usar datos de tooencrypt de algoritmos de cifrado de alta seguridad en la base de datos de Hola

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Elegir un algoritmo de cifrado](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Pasos** | Los algoritmos de cifrado definen las transformaciones de datos que los usuarios no autorizados no pueden revertir fácilmente. SQL Server permite a los administradores y desarrolladores toochoose entre varios algoritmos, incluidos DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 de 128 bits, DESX, AES de 128 bits, AES de 192 bits y AES de 256 bits |

## <a id="ssis-signed"></a>Los paquetes SSIS deben cifrarse y firmarse digitalmente

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Identificar el origen de los paquetes con firmas digitales de hello](https://msdn.microsoft.com/library/ms141174.aspx), [mitigar amenazas y vulnerabilidades (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Pasos** | origen de Hola de un paquete es Hola individual u organización que creó el paquete de saludo. Ejecutar un paquete desde un origen desconocido o en el que no se confía puede ser arriesgado. tooprevent no autorizados alteren los paquetes SSIS, se deben utilizar firmas digitales. Además, confidencialidad de hello tooensure de paquetes de Hola durante el tránsito/almacenamiento, paquetes SSIS tienen toobe cifrada |

## <a id="securables-db"></a>Agregar elementos protegibles de base de datos de toocritical de firma digital

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [ADD SIGNATURE (Transact-SQL)](https://msdn.microsoft.com/library/ms181700)[Agregar firma (Transact-SQL)] |
| **Pasos** | En los casos en que la integridad de una base de datos crítico que se puede proteger hello toobe comprobado, deben usarse firmas digitales. Los elementos protegibles de una base de datos, como un procedimiento almacenado, una función, un ensamblado o un desencadenador pueden firmarse digitalmente. A continuación se muestra un ejemplo de cuando esto puede resultar útil: supongamos un ISV (proveedores de Software independientes) ha proporcionado soporte tooa software entregado tooone de sus clientes. Antes de proporcionar soporte técnico, Hola ISV sería aconsejable que un elemento protegible en software de Hola de base de datos no se alteró por error o por un intento malicioso de tooensure. Si Hola protegible está firmado digitalmente, Hola ISV puede comprobar la firma digital y validar su integridad.| 

## <a id="ekm-keys"></a>Utilizar claves de cifrado de SQL server EKM tooprotect

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Administración extensible de claves (EKM) de SQL Server](https://msdn.microsoft.com/library/bb895340), [Administración extensible de claves con Azure Key Vault (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **Pasos** | Administración Extensible de claves de SQL Server permite que las claves de cifrado de Hola que protegen toobe de archivos de base de datos de hello almacenado en un dispositivo externo, como una tarjeta inteligente, un dispositivo USB o un módulo EKM/HSM. Esto también habilita la protección de datos de los administradores de base de datos (exceptuando a los miembros del grupo de sysadmin de hello). Datos se pueden cifrar mediante el uso de claves de cifrado que solo hello usuario de base de datos tiene acceso tooon Hola externo EKM/HSM módulo. |

## <a id="keys-engine"></a>Usar la característica de AlwaysEncrypted si las claves de cifrado no deben tooDatabase revelados motor

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure, OnPrem |
| **Atributos**              | Versión de SQL: V12, MsSQL2016 |
| **Referencias**              | [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865) |
| **Pasos** | Always Encrypted es un característica diseñada tooprotect datos confidenciales, como números de tarjeta de crédito o números de identificación nacional (por ejemplo, Estados Unidos números de seguridad social), almacenados en las bases de datos de la base de datos de SQL Azure o SQL Server. Always Encrypted permite a los clientes tooencrypt datos confidenciales en aplicaciones de cliente y nunca revela toohello de claves de cifrado de hello motor de base de datos (base de datos SQL o SQL Server). Como resultado, Always Encrypted proporciona una separación entre aquellos que poseen los datos de hello (y pueden verlos) y aquellos usuarios que administran datos de hello (pero no deberían tener acceso) |

## <a id="keys-iot"></a>Almacene las claves criptográficas de forma segura en dispositivos IoT

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Sistema operativo del dispositivo: Windows IoT Core, Conectividad de dispositivos: SDK de dispositivo IoT de Azure |
| **Referencias**              | [TPM on Windows IoT Core](https://developer.microsoft.com/windows/iot/docs/tpm) (TPM en Windows IoT Core), [Configuración de TPM en Windows IoT Core](https://developer.microsoft.com/windows/iot/win10/setuptpm), [TPM con SDK de dispositivo IoT de Azure](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) |
| **Pasos** | Claves privadas de certificado o simétricas en un almacenamiento protegido de hardware como chips TPM o de tarjeta inteligente. Windows 10 IoT Core es compatible con usuario Hola de un TPM y hay varios TPM compatible que puede usarse: https://developer.microsoft.com/windows/iot/win10/tpm. Es recomienda toouse un Firmware o TPM discretos. Un TPM de software solo se debe usar con fines de desarrollo y prueba. Una vez que un TPM está disponible y las claves de Hola se aprovisionan en ella, debería escribir el código de hello que genera el token de hello sin codificar de forma rígida información confidencial en ella. | 

### <a name="example"></a>Ejemplo
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Como puede ver, clave principal de hello dispositivo no está presente en el código de hello. En su lugar, se almacena en hello TPM en la ranura 0. El dispositivo TPM genera una corta duración token de SAS que es, a continuación, usa tooconnect toohello centro de IoT. 

## <a id="random-hub"></a>Generar una clave simétrica aleatoria de longitud suficiente para autenticación tooIoT concentrador

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Elección de puerta de enlace: Azure IoT Hub |
| **Referencias**              | N/D  |
| **Pasos** | IoT Hub contiene un registro de identidad del dispositivo y durante el aprovisionamiento de un dispositivo genera automáticamente una clave simétrica aleatoria. Se recomienda toouse esta característica de clave de hello registro de identidad de Azure IoT Hub toogenerate Hola se usa para la autenticación. Centro de IoT también permite un toobe clave que se especificó al crear el dispositivo de Hola. Si se genera una clave fuera de centro de IoT durante el aprovisionamiento de dispositivos, es recomendable toocreate una clave simétrica aleatoria o al menos de 256 bits. |

## <a id="pin-remote"></a>Asegúrese de que hay una directiva de administración de dispositivos que requiere el uso de un PIN y permite el borrado remoto

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvil de Dynamics CRM | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que hay una directiva de administración de dispositivos que requiere el uso de un PIN y permite el borrado remoto |

## <a id="bitlocker"></a>Asegúrese de que hay una directiva de administración de dispositivos que requiere un bloqueo automático con PIN o contraseña y cifra todos los datos (por ejemplo, Bitlocker)

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Cliente de Outlook de Dynamics CRM | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que hay una directiva de administración de dispositivos que requiere un bloqueo automático con PIN o contraseña y cifra todos los datos (por ejemplo, Bitlocker) |

## <a id="rolled-server"></a>Asegúrese de que las claves de firma se sustituyen cuando se usa Identity Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Identity Server: claves, firmas y cifrado](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) |
| **Pasos** | Asegúrese de las claves de firma se sustituyen cuando se usa Identity Server. vínculo de Hello en la sección de referencias de Hola explica cómo esta acción debe planearse sin causar tooapplications interrupciones en el servidor de identidades de confianza. |

## <a id="client-server"></a>Asegúrese de que se usan un identificador de cliente y un secreto de cliente de alta seguridad criptográfica en Identity Server

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Asegúrese de que se usan un identificador de cliente y un secreto de cliente de alta seguridad criptográfica en Identity Server. Hola siguientes instrucciones se debe utilizar al generar un identificador de cliente y el secreto:</p><ul><li>Generar un GUID aleatorio como Id. de cliente hello</li><li>Generar una clave de 256 bits criptográficamente aleatoria como secreto de Hola</li></ul>|
