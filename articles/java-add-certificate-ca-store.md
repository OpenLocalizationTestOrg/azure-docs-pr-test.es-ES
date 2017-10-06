---
title: "un almacén de CA de Java de certificados toohello aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd un certificado de entidad emisora de certificados de Java de toohello (cacerts) de certificados emisora de certificados (CA) certificado almacén para servicio de Twilio o Service Bus de Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Agregar un almacén de certificados de CA de Java de toohello de certificado
Hola siguientes pasos muestra cómo tooadd un certificado de entidad emisora de certificados de Java de toohello de certificado emisora de certificados (CA) certificado (cacerts) almacén. Hello en el ejemplo se usa para el certificado de entidad emisora de certificados de hello requiere hello Twilio servicio. La información proporcionada más adelante en el tema de hello describe cómo tooinstall Hola CA de certificados para hello Azure Service Bus. 

Puede usar keytool tooadd Hola CA certificado anterior toozipping el JDK y agregar tooyour proyecto de Azure **approot** carpeta, o bien puede ejecutar una tarea de inicio de Azure que utiliza certificados de keytool tooadd Hola. En este ejemplo se da por supuesto que va a agregar un certificado de entidad emisora de certificados anterior toohello JDK que se va a comprimir. Además, se usará un certificado de CA específico en hello (ejemplo), pero los pasos de Hola de obtención de un certificado de CA diferente e importándolos a Hola cacerts tienda serían similar.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>almacenar un cacerts toohello de certificado de tooadd
1. En una ventana del símbolo del sistema se establece del JDK tooyour **jdk\jre\lib\security** carpeta, ejecute hello después toosee qué certificados están instalados:
   
    `keytool -list -keystore cacerts`
   
    Se le pedirá de contraseña del almacén de Hola. es la contraseña predeterminada de Hello **cambiarlo**. (Si desea que la contraseña de hello toochange, consulte la documentación de keytool hello en <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) En este ejemplo se da por supuesto ese certificado Hola con 67:CB:9 de huella digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 no aparece, y que desea tooimport TI (Hola servicio Twilio API necesita este certificado concreto).
2. Obtener certificado de hello en lista de Hola de certificados que se muestran en [GeoTrust raíz certificados](http://www.geotrust.com/resources/root-certificates/). Haga clic en el vínculo de hello certificado Hola con número de serie 35:DE:F4:CF y guárdelo toohello **jdk\jre\lib\security** carpeta. Para fines de este ejemplo, se ha guardado con el nombre de archivo de tooa **Equifax\_seguro\_certificado\_Authority.cer**.
3. Importar el certificado de Hola a través de hello siguiente comando:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Cuando se le pregunte tootrust este certificado, si el certificado de hello tiene 67:CB:9 de huella digital MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, responden escribiendo **y**.
4. Hola ejecución después de certificado de CA hello tooensure comando se ha importado correctamente:
   
    `keytool -list -keystore cacerts`
5. Código postal Hola JDK y agregar tooyour proyecto de Azure **approot** carpeta.

Para más información acerca de keytool, consulte <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Certificados raíz de Azure
Las aplicaciones que usan los servicios de Azure (por ejemplo, Azure Service Bus) necesitan certificado Baltimore CyberTrust Root de tootrust Hola. (A partir del 15 de abril de 2013, Azure empezó a migrar desde Hola GTE CyberTrust Root Global toohello Baltimore CyberTrust Root. Esta migración llevó a cabo varias toocomplete meses.)

Hello Baltimore certificado ya podría estar instalado en el almacén cacerts, por tanto, recuerde hello toorun **keytool-lista** comando toosee primero si ya existe.

Si necesita tooadd Hola Baltimore CyberTrust Root, tiene 02:00:00:b9 de número de serie y SHA1 huella digital d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74. Se puede descargar desde <https://cacert.omniroot.com/bc2025.crt>, guarda el archivo local tooa con extensión **.cer**y, a continuación, importar mediante **keytool** como se indicó anteriormente.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los certificados raíz de hello usa Azure, consulte [migración de certificados raíz de Azure](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Para más información sobre Java, consulte [Azure para desarrolladores de Java](/java/azure).

