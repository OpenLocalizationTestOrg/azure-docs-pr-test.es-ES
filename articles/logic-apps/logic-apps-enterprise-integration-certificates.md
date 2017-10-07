---
title: "certificados aaaUsing con paquete de integración empresarial | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse certificados con hello paquete de integración empresarial | Aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Información sobre los certificados y Enterprise Integration Pack
## <a name="overview"></a>Información general
Integración de Enterprise utiliza las comunicaciones de certificados toosecure B2B. Puede emplear dos tipos de certificados en las aplicaciones de integración de empresas:

* Certificados públicos, que deben comprarse a una entidad de certificación (CA).
* Certificados privados, que puede emitir usted mismo. A veces, estos certificados son autofirmados tooas que se hace referencia.

## <a name="what-are-certificates"></a>¿Qué son los certificados?
Los certificados son documentos digitales que comprobar la identidad de Hola de participantes de hello en comunicaciones electrónicas y que proteger las comunicaciones electrónicas.

## <a name="why-use-certificates"></a>¿Por qué se utilizan los certificados?
A veces, hay que conservar la confidencialidad de las comunicaciones B2B. Integración de Enterprise utiliza certificados toosecure estas comunicaciones de dos maneras:

* Mediante el cifrado de contenido de Hola de mensajes
* Firmando digitalmente los mensajes  

## <a name="upload-a-public-certificate"></a>Carga de un certificado público

toouse una *certificado público* en las aplicaciones lógicas con capacidades de B2B, primero necesita tooupload Hola certificado en su cuenta de integración.  

Después de cargar un certificado, está disponible toohelp proteger los mensajes B2B al definir sus propiedades en hello [contratos](logic-apps-enterprise-integration-agreements.md) creados por usted.  

Presentamos Hola pasos detallados para cargar los certificados públicos en su cuenta de integración después de iniciar sesión en toohello portal de Azure:

1. Seleccione **más servicios** y escriba **integración** en el cuadro de búsqueda del filtro de Hola. Seleccione **cuentas de integración** desde la lista de resultados de Hola     
![Seleccionar Examinar](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Seleccione Hola integración cuenta toowhich desea tooadd Hola certificado.  
![Seleccione Hola integración cuenta toowhich desea tooadd Hola certificado](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Seleccione hello **certificados** icono.  
![Icono de hello seleccione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. Hola **certificados** hoja que se abre, seleccione hello **agregar** botón.   
![Seleccione el botón de agregar Hola](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Escriba un **nombre** para el certificado y hello, a continuación, seleccione el tipo de certificado como **público** de lista desplegable de Hola.  
6. Icono de carpeta de hello seleccione lado derecho de Hola de hello **certificado** cuadro de texto. Cuando se abre el selector de archivos de hello, busque y seleccione el archivo de certificado de Hola que quiere tooupload tooyour integración cuenta.
7. Seleccione el certificado de hello y, a continuación, seleccione **Aceptar** en el selector de archivos de Hola. Esto se valida y carga Hola certificados tooyour integración cuentas.
8. Por último, encenderlo hello **agregar certificado** hoja, seleccione hello **Aceptar** botón.  
![Seleccione el botón Aceptar Hola](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Seleccione hello **certificados** icono. Debería ver Hola recién agregado el certificado.  
![Vea el nuevo certificado de Hola](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Carga de un certificado privado

toouse una *certificado privado* en las aplicaciones lógicas con capacidades de B2B, se puede cargar una cuenta de integración de certificado privado tooyour Hola realizar pasos

1. [Cargar su tooKey clave privada almacén](../key-vault/key-vault-get-started.md "Obtenga más información sobre el almacén de claves") y proporcionar un **nombre de clave** 
   
   > [!TIP]
   > Debe autorizar las operaciones de tooperform de las aplicaciones lógicas en el almacén de claves. Puede conceder a entidad de servicio de aplicaciones de la lógica de acceso toohello mediante Hola siguiente comando de PowerShell:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Una vez que haya realizado paso anterior de hello, agregue una cuenta de toointegration certificado privado.

A continuación se Hola pasos detallados para cargar los certificados privados en su cuenta de integración después de iniciar sesión en toohello portal de Azure:  
 
1. Seleccionar cuenta de hello integración toowhich desea tooadd Hola certificado y seleccione hello **certificados** icono.  
![Icono de hello seleccione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. Hola **certificados** hoja que se abre, seleccione hello **agregar** botón.   
![Seleccione el botón de agregar Hola](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Escriba un **nombre** para su certificado y el tipo de certificado de hello seleccione como **privada** de lista desplegable de Hola.   
4. Seleccione icono de carpeta de hello en hello derecha de hello **certificado** cuadro de texto. Cuando se abre el selector de archivos de hello, Buscar certificado público correspondiente Hola que quiere tooupload tooyour integración cuenta.   
   
   > [!Note]
   > Al agregar un certificado privado es importante tooadd correspondiente pública certificados tooshow en [acuerdo AS2](logic-apps-enterprise-integration-as2.md) reciben y envían la configuración para firmar y cifrar los mensajes de saludo.
   > 
   >   

5. Seleccione hello **grupo de recursos**, **el almacén de claves**, **nombre de clave** y seleccione hello **Aceptar** botón.  
![Agregar certificado](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Seleccione hello **certificados** icono. Debería ver Hola recién agregado el certificado.
![Vea el nuevo certificado de Hola](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Creación de un contrato B2B](logic-apps-enterprise-integration-agreements.md)  
* [Más información sobre Key Vault](../key-vault/key-vault-get-started.md "Información sobre el Almacén de claves")  

