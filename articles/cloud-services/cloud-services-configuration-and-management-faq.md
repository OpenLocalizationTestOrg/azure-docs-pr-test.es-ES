---
title: "problemas aaaConfiguration y la administración de preguntas más frecuentes sobre servicios de nube de Microsoft Azure | Documentos de Microsoft"
description: "Este artículo enumeran Hola preguntas más frecuentes sobre la configuración y la administración de servicios de nube de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Configuración y problemas de administración de Microsoft Azure Cloud Services: preguntas más frecuentes (P+F)

En este artículo se incluyen las preguntas frecuentes sobre la configuración y los problemas de administración de [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). También puede consultar hello [página de tamaño de máquina virtual de servicios de nube](cloud-services-sizes-specs.md) para obtener información de tamaño.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>¿Cómo se puede agregar sitio Web de toomy "nosniff"?
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

## <a name="how-do-i-customize-iis-for-a-web-role"></a>¿Cómo se personaliza IIS para un rol web?
Usar script de inicio IIS de Hola de hello [tareas comunes de inicio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artículo.

## <a name="i-cannot-scale-beyond-x-instances"></a>No puedo escalar más allá de X instancias
La suscripción de Azure tiene un límite en número de Hola de núcleos que se puede usar. Ajuste de escala no funcionará si ha utilizado todos los núcleos de hello disponibles. Por ejemplo, si tiene un límite de 100 núcleos, esto significa que podría tener 100 instancias de máquina virtual de tamaño A1 para su servicio en la nube o 50 instancias de máquina virtual de tamaño A2.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>¿Cómo se puede implementar el acceso basado en roles para Cloud Services?
Servicios en la nube no admite el modelo de Control de acceso basado en roles (RBAC) hello, ya que no es un servicio en función de administrador de recursos de Azure.

Consulte [RBAC de Azure frente a administradores de la suscripción clásica](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>¿Cómo configuro tiempo de espera de inactividad de hello para el equilibrador de carga de Azure?
Puede especificar el tiempo de espera de hello en el archivo de definición (csdef) de servicio similar al siguiente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Para más información consulte ///[New: Configurable Idle Timeout for Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) (Nuevo: Tiempo de espera de inactividad configurable para Azure Load Balancer).

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>¿Puede ingenieros de Microsoft internas a instancias de servicio RDP toocloud sin permiso?
Sigue Microsoft tooRDP los ingenieros de un proceso estricto que no le permitirá interno en su servicio en la nube sin permiso (correo electrónico u otra comunicación escrito) por escrito del propietario de Hola o su persona designada tal fin.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>¿Por qué está incompleta cadena de certificados de Hola de mi certificado SSL de servicio de nube?
Se recomienda que los clientes instalen la cadena de certificados completa hello (certificado de hoja, los certificados intermedios y certificado raíz) en lugar de simplemente el certificado de hoja Hola. Cuando se instala solo el certificado de hoja hello, que basarse en la cadena de certificados de Windows toobuild Hola recorriendo Hola CTL. Si intermitente de la red o problemas de DNS se producen en Azure o Windows Update cuando Windows está tratando de certificado de hello toovalidate, certificado Hola puede considerarse válido. Al instalar la cadena de certificados completa de hello, se puede evitar este problema. Hola blog en [cómo tooinstall un certificado SSL encadenado](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) muestra cómo toodo esto.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>¿Cómo se puede asociar un servicio de nube de toomy de direcciones IP estático?
tooset de una dirección IP estática, debe toocreate una dirección IP reservada. Esta dirección IP reservada puede ser asociado tooa nuevo servicio o tooan existente implementación en la nube. Vea Hola después de documentos para obtener más información:
* [¿Cómo toocreate una dirección IP reservada](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Reservar la dirección IP de Hola de un servicio de nube existente](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Asociar un reservada IP tooa nuevo servicio de nube](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Asociar un tooa IP reservada ejecutando implementación](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Asociar un servicio de nube de tooa IP reservado mediante un archivo de configuración de servicio](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>¿Cuál es el límite de cuota de Hola para mi servicio en la nube?
Consulte los [Límites específicos del servicio](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>¿Por qué aparece unidad hello en mi máquina virtual del servicio de nube muy poco espacio libre en disco?
Este comportamiento es normal y no debe hacer que cualquier aplicación de tooyour del problema. Registro en diario está activado para Hola % uproot % unidad en máquinas virtuales de PaaS de Azure, que básicamente consume double Hola cantidad de espacio que ocupan normalmente archivos. Sin embargo, hay varios aspectos toobe en cuenta que esto convertir básicamente en un no supone ningún problema.

tamaño de la unidad de % approot % Hello se calcula una como < tamaño de cspkg + tamaño del diario max > + un margen de espacio disponible, o 1,5 GB, lo que sea mayor. tamaño de saludo de la máquina virtual no influye en este cálculo. (Hola tamaño de máquina virtual solo afecta a tamaño Hola de temporal de la unidad C: Hola.) 

Es no compatible toowrite toohello % approot % unidad. Si está escribiendo toohello máquina virtual de Azure, debe hacerlo en un recurso de LocalStorage temporal (u otras opciones, como almacenamiento de blobs, archivos de Azure, etcetera.). Por lo que la cantidad de Hola de espacio libre en la carpeta de Hola % approot % no es significativo. Si no está seguro de si la aplicación escribe toohello % approot % unidad, siempre puede dejar que el servicio se ejecutan durante unos días y, a continuación, comparar Hola "antes" y "después" tamaños. 

Azure no escribirá nada toohello % approot % unidad. Una vez hello VHD es creado a partir de su .cspkg y montar en hello Azure VM, lo único Hola que podría escribir toothis unidad es la aplicación. 

configuración del diario de Hola es no configurable, por lo que no puede desactivar.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>¿Qué características de Hola y capacidades que proporciona identificadores de IP básicas Azure y DDOS?
Azure tiene direcciones IP/identificadores en toodefend de servidores físicos del centro de datos frente a amenazas. Además, los clientes pueden implementar soluciones de seguridad de terceros, como firewalls de aplicación web, firewalls de red, antimalware, detección de intrusiones, sistemas de prevención (IDS/IPS) y mucho más. Para más información, consulte ///[Protect your data and assets and comply with global security standards](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity) (Protección de datos y recursos y cumplimiento de los estándares de seguridad global).

Microsoft supervisa continuamente las amenazas de toodetect de servidores, redes y aplicaciones. Enfoque de administración de amenaza múltiple de Azure usa la detección de intrusiones, ataques de prevención, las pruebas de penetración, análisis de comportamiento, detección de anomalías distribuida por denegación de servicio (DDoS) y aprendizaje automático tooconstantly reforzar su defensa y reducir los riesgos. Microsoft Antimalware para Azure protege los servicios en la nube y las máquinas virtuales de Azure. Tener soluciones de seguridad de terceros de hello opción toodeploy por otra parte, como paredes de incendio de aplicación web, firewalls de red, antimalware, sistemas de detección y prevención de intrusiones (IDS/IPS) y mucho más.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>¿Por qué detener IIS escribir toohello directorio de registro?
Agotados cuota de almacenamiento local de Hola para escribir el directorio de registro de toohello. Para corregir este problema, puede elegir entre tres cosas:
* Habilitar los diagnósticos para IIS y disponer de almacenamiento de tooblob de diagnóstico mueven periódicamente de Hola.
* Quite manualmente los archivos de registro de hello directorio de registro.
* Aumentar el límite de cuota para los recursos locales.

Para obtener más información, vea Hola siguientes documentos:
* [Almacenamiento y visualización de los datos de diagnóstico en Azure Storage](cloud-services-dotnet-diagnostics-storage.md)
* [IIS Logs stops writing in cloud service](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/) (El registro IIS deja de escribir en el servicio en la nube)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>¿Cuál es el propósito de Hola Hola "Windows Azure Tools cifrado para las extensiones de certificado"?
Estos certificados se crean automáticamente cada vez que se agrega una extensión toohello servicio en la nube. Normalmente, se trata de hello extensión WAD o hello extensión RDP, pero podría deberse a otros usuarios, como Hola extensión Antimalware o compilador de registros. Estos certificados sólo se utilizan para cifrar y descifrar la configuración privada de hello para la extensión de Hola. nunca se comprueba la fecha de expiración de Hello, por lo que no importa si Hola certificado ha expirado. 

Puede omitir estos certificados. Si desea limpiar los certificados de hello, puede intentar eliminar todas ellas. Azure producirá un error si intenta toodelete un certificado que está en uso.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>¿Cómo puedo generar una firma de solicitud certificado (CSR) sin "RDP-ing" en la instancia de toohello?
Vea Hola siguiente documento de orientación:

>///[Obtaining a certificate for use with Windows Azure Web Sites (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/) (Obtención de un certificado para su uso con los sitios web de Windows Azure)

Tenga en cuenta que un CSR es simplemente un archivo de texto. No tiene toobe creado desde la máquina de Hola donde se utilizará en última instancia certificado Hola. Aunque este documento está dirigido a un servicio de aplicaciones, Hola creación CSR es genérica y se aplica también a los servicios en la nube.
