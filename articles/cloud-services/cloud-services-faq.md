---
title: "roles de servicios en la nube aaaAzure preguntas más frecuentes | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre Azure Cloud Services. Responde a algunas preguntas comunes sobre certificados, roles web y roles de trabajo."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>P+F de Servicios en la nube
En este artículo se responden algunas preguntas frecuentes sobre Servicios en la nube de Microsoft Azure. También puede visitar hello [preguntas frecuentes de soporte de Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para información general de precios y soporte técnico de Azure. También puede consultar hello [página de tamaño de máquina virtual de servicios de nube](cloud-services-sizes-specs.md) para obtener información de tamaño.

## <a name="certificates"></a>Certificados
### <a name="where-should-i-install-my-certificate"></a>¿Dónde debo instalar mi certificado?
* **My**  
  Certificado de aplicación con clave privada (\*.pfx, \*.p12).
* **CA**  
  Todos los certificados intermedios van a este almacén (entidades de certificación de directivas y secundarias).
* **ROOT**  
  almacén de CA raíz de Hola, por lo que el certificado de CA raíz principal aquí debe ir.

### <a name="i-cant-remove-expired-certificate"></a>No se puede quitar el certificado expirado
Azure impide quitar un certificado mientras está en uso. Se necesita tooeither eliminación hello de la implementación que utiliza certificados de Hola o parche Hola con un certificado diferente o renovado.

### <a name="delete-an-expired-certificate"></a>Eliminar un certificado expirado
Como certificado de hello no está en uso, puede usar hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove de cmdlet de PowerShell un certificado.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Tengo certificados expirados denominados Administración de servicios de Microsoft Azure para Extensiones
Estos certificados se crean cada vez que se agrega una extensión toohello servicio en la nube como Hola extensión de escritorio remoto. Estos certificados sólo se utilizan para cifrar y descifrar la configuración privada de Hola de extensión de Hola. No importa si estos certificados expiran. no se comprueba la fecha de expiración de Hola.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Siguen apareciendo certificados que he eliminado
Estos siguen reapareciendo muy probablemente a causa de una herramienta que esté utilizando, como Visual Studio. Cada vez que se vuelve a conectar con una herramienta que está utilizando un certificado, nuevo será tooAzure cargado.

### <a name="my-certificates-keep-disappearing"></a>Mis certificados siguen desapareciendo
Cuando se recicla la instancia de la máquina virtual de hello, se pierden todos los cambios locales. Use un [tarea de inicio](cloud-services-startup-tasks.md) tooinstall certificados toohello virtual machine se inicia cada rol de Hola de tiempo.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>No encuentro mi certificados de administración en el portal de Hola
[Certificados de administración](../azure-api-management-certs.md) sólo están disponibles en hello Portal clásico de Azure. portal de Azure actual Hello no utiliza certificados de administración. 

### <a name="how-can-i-disable-a-management-certificate"></a>¿Cómo puedo deshabilitar un certificado de administración?
[certificados de administración](../azure-api-management-certs.md) . Eliminarlas a través de hello Portal clásico de Azure si no quiere toobe usar más.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>¿Cómo puedo crear un certificado SSL para una dirección IP específica?
Siga las instrucciones de Hola Hola [crear un tutorial de certificado](cloud-services-certs-create.md). Usar dirección IP de hello como Hola nombre DNS.

## <a name="security"></a>Seguridad
### <a name="disable-ssl-30"></a>Deshabilitar SSL 3.0
toodisable SSL 3.0 y utilizar la seguridad TLS, cree una tarea de inicio que se describe en esta entrada de blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Agregar **nosniff** sitio Web de tooyour
los clientes de tooprevent de examen de los tipos MIME hello, agregar una configuración en su *web.config* archivo.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

También puede agregarlo como un ajuste en IIS. Comando siguiente de Hola de uso con hello [tareas comunes de inicio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artículo.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>Personalización de IIS para un rol web
Usar script de inicio IIS de Hola de hello [tareas comunes de inicio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artículo.

## <a name="scaling"></a>Escalado
### <a name="i-cannot-scale-beyond-x-instances"></a>No puedo escalar más allá de X instancias
La suscripción de Azure tiene un límite en número de Hola de núcleos que se puede usar. Ajuste de escala no funcionará si ha utilizado todos los núcleos de hello disponibles. Por ejemplo, si tiene un límite de 100 núcleos, esto significa que podría tener 100 instancias de máquina virtual de tamaño A1 para su servicio en la nube o 50 instancias de máquina virtual de tamaño A2.

## <a name="networking"></a>Redes
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>No se puede reservar una dirección IP en un servicio en la nube con varias direcciones IP virtuales
En primer lugar, asegúrese de que esa instancia de máquina virtual de Hola que intentas tooreserve Hola IP para está activada. En segundo lugar, asegúrese de que está usando direcciones IP reservadas para implementaciones de ensayo y producción de hello molestarse en. **No** cambiar la configuración de hello mientras se actualiza la implementación de Hola.

## <a name="remote-desktop"></a>Escritorio remoto
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>¿Cómo se usa el escritorio remoto con un NSG?
Agregar reglas toohello NSG que permitan el tráfico en puertos **3389** y **20000**.  Escritorio remoto usa el puerto **3389**.  Instancias de servicio en la nube son carga equilibrada, por lo que directamente no se puede controlar qué tooconnect de instancia a.  Hola *RemoteForwarder* y *RemoteAccess* agentes administrar el tráfico RDP y permitir Hola cliente toosend una cookie RDP y especificar un tooconnect de una instancia individual a.  Hola *RemoteForwarder* y *RemoteAccess* agentes requieren ese puerto **20000*** abrirse, que pueden bloquearse si tienes un NSG.
