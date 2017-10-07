---
title: "aaaAzure servicio de metadatos de instancia para las máquinas virtuales de Linux | Documentos de Microsoft"
description: "Interfaz rESTful tooget saber de Linux VM proceso, red y eventos de mantenimiento próximo."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a>Servicio de metadatos de instancia de Azure para máquinas virtuales Linux


Hola servicio de metadatos de instancia de Azure proporciona información sobre instancias de máquina virtual que pueden ser usado toomanage y configurar las máquinas virtuales en ejecución.
Esto incluye información como SKU, configuración de red y eventos de mantenimiento próximos. Para más información sobre el tipo de información está disponible, vea las [categorías de metadatos](#instance-metadata-data-categories).

Servicio de metadatos de instancia de Azure es un extremo de REST accesible tooall las máquinas virtuales IaaS creada a través de hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Hola extremo está disponible en una dirección IP no enrutables conocida (`169.254.169.254`) que puede tener acceso sólo desde dentro de hello máquina virtual.

> [!IMPORTANT]
> Este servicio está **disponible con carácter general** en regiones de Azure globales. Azure Cloud se encuentra en versión preliminar pública para Azure Government, Azure en China y Azure Alemania. Periódicamente recibe actualizaciones tooexpose nueva información acerca de las instancias de máquina virtual. Esta página refleja Hola actualizada [categorías de datos](#instance-metadata-data-categories) disponibles.

## <a name="service-availability"></a>Disponibilidad del servicio
servicio de Hello está disponible en todas las regiones de Azure Global disponibles con carácter general. servicio de Hello está en vista previa pública en regiones de hello gubernamentales, China o Alemania.

Regiones                                        | ¿Disponibilidad?
-----------------------------------------------|-----------------------------------------------
[Todas las regiones globales de Azure disponibles con carácter general](https://azure.microsoft.com/regions/)     | Disponibilidad general 
[Azure Government](https://azure.microsoft.com/overview/clouds/government/)              | En versión preliminar 
[Azure en China](https://www.azure.cn/)                                                           | En versión preliminar
[Azure Alemania](https://azure.microsoft.com/overview/clouds/germany/)                    | En versión preliminar

Esta tabla se actualiza cuando Hola servicio deja de estar disponible en otras nubes de Azure.

tootry out Hola servicio de metadatos de instancia, cree una máquina virtual desde [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o hello [portal de Azure](http://portal.azure.com) Hola por encima de las regiones y seguimiento Hola ejemplos siguientes.

## <a name="usage"></a>Uso

### <a name="versioning"></a>Control de versiones
Hola servicio de metadatos de instancia tiene una versión. Versiones son obligatorias y la versión actual de hello es `2017-04-02`.

> [!NOTE] 
> Versiones anteriores de vista previa de los eventos programados formando Hola api-version {más reciente}. Este formato ya no se admite y dejará de utilizarse en hello futuras.

A medida que agreguemos versiones más recientes, todavía se podrá acceder a las versiones anteriores por motivos de compatibilidad si los scripts tienen dependencias en formatos de datos específicos. Sin embargo, tenga en cuenta que version(2017-03-01) de vista previa actual de hello puede no estar disponible una vez que el servicio Hola está generalmente disponible.

### <a name="using-headers"></a>Uso de encabezados
Al consultar Hola servicio de metadatos de instancia, debe proporcionar encabezado de hello `Metadata: true` solicitud de hello tooensure no se ha redirigido involuntariamente.

### <a name="retrieving-metadata"></a>Recuperar metadatos

Los metadatos de instancia están disponibles para ejecutar máquinas virtuales creadas o administradas mediante [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Tener acceso a todas las categorías de datos de una instancia de máquina virtual utilizando Hola después de solicitud:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Todas las consultas de metadatos de instancia distinguen mayúsculas de minúsculas.

### <a name="data-output"></a>Salida de datos
De forma predeterminada, Hola servicio de metadatos de la instancia devuelve datos en formato JSON (`Content-Type: application/json`). Pero las distintas API pueden devolver los datos en formatos diferentes si se solicita.
Hello tabla siguiente es una referencia de API pueden admitir otros formatos de datos.

API | Formato predeterminado de datos | Otros formatos
--------|---------------------|--------------
/instance | json | text
/scheduledevents | json | Ninguna

tooaccess un formato de respuesta no predeterminado, especificar formato solicitado Hola como un parámetro de cadena de consulta de solicitud de Hola. Por ejemplo:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Seguridad
extremo de servicio de metadatos de instancia de Hello es accesible únicamente desde dentro de hello ejecutando la instancia de máquina virtual en una dirección IP no es enrutable. Además, cualquier solicitud con un `X-Forwarded-For` encabezado es rechazado por el servicio de Hola.
También se requiere solicitudes toocontain una `Metadata: true` tooensure de encabezado que Hola solicitud real directamente era deseada y no forma parte de la redirección involuntaria. 

### <a name="error"></a>Error
Si hay un elemento de datos no encontrado o una solicitud con formato incorrecto, Hola servicio de metadatos de la instancia devuelve errores HTTP estándares. Por ejemplo:

Código de estado HTTP | Motivo
----------------|-------
200 OK |
400 - Solicitud incorrecta | Falta el encabezado `Metadata: true`
404 No encontrado | Existen Hello does't elemento solicitado 
405 Método no permitido | Solo se admiten solicitudes `GET` y `POST`
429 Demasiadas solicitudes | API de Hello actualmente admite un máximo de 5 consultas por segundo
500 Error de servicio     | Vuelva a intentarlo más tarde

### <a name="examples"></a>Ejemplos

> [!NOTE] 
> Todas las respuestas de las API son cadenas JSON. Todas las respuestas de ejemplo siguientes se han impreso correctamente para mejorar la legibilidad.

#### <a name="retrieving-network-information"></a>Recuperación de información de red

**Solicitud**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Respuesta**

> [!NOTE] 
> respuesta de Hello es una cadena JSON. Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Recuperación de dirección IP pública

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Recuperación de todos los metadatos para una instancia

**Solicitud**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Respuesta**

> [!NOTE] 
> respuesta de Hello es una cadena JSON. Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Recuperación de metadatos en una máquina virtual con Windows

**Solicitud**

Se pueden recuperar los metadatos de instancia de Windows a través de la utilidad de PowerShell de Hola `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

O a través de hello `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Respuesta**

> [!NOTE] 
> respuesta de Hello es una cadena JSON. Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Categorías de datos de metadatos de instancia
Hola siguientes categorías de datos está disponible a través de hello servicio de metadatos de instancia:

Datos | Descripción
-----|------------
location | Hola de región de Azure VM se esté ejecutando
name | Nombre del programa Hola a máquinas virtuales 
offer | Ofrece información para la imagen de máquina virtual de Hola. Este valor solo está presente para las imágenes que se implementan desde la galería de imágenes de Azure.
publisher | Publicador de la imagen de máquina virtual de Hola
sku | SKU específica para la imagen de máquina virtual de Hola  
versión | Versión de imagen de máquina virtual de Hola 
osType | Linux o Windows 
platformUpdateDomain |  [Dominio de actualización](manage-availability.md) Hola máquina virtual se está ejecutando en
platformFaultDomain | [Dominio de error](manage-availability.md) Hola máquina virtual se está ejecutando en
vmId | [Identificador único](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para hello VM
vmSize | [Tamaño de VM](sizes.md)
ipv4/privateIpAddress | Dirección IPv4 local de hello VM 
ipv4/publicIpAddress | Dirección IPv4 pública de hello VM
subnet/address | Dirección de subred de VM de hello
subnet/prefix | Prefijo de la subred, ejemplo, 24
ipv6/ipAddress | Dirección IPv6 local de hello VM
macAddress | Dirección de MAC de la VM 
scheduledevents | Actualmente en Versión preliminar pública Vea [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Escenarios de ejemplo de uso  

### <a name="tracking-vm-running-on-azure"></a>Seguimiento de una máquina virtual que se ejecuta en Azure

Como proveedor de servicios, puede requerir número de hello tootrack de máquinas virtuales que ejecutan el software o con agentes que necesitan tootrack unicidad del programa Hola a máquina virtual. toobe tooget capaz de un identificador único para una máquina virtual, use hello `vmId` arrastrándolo desde el servicio de metadatos de la instancia.

**Solicitud**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Respuesta**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Ubicación de los contenedores y el dominio de error/actualización basado en particiones de datos 

Para ciertos escenarios, la ubicación de las distintas réplicas de datos es de máxima importancia. Por ejemplo, [selección de ubicación de réplica HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la ubicación del contenedor a través de un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) puede requerir hello tooknow `platformFaultDomain` y `platformUpdateDomain` Hola VM se ejecuta en.
Puede consultar estos datos directamente a través de hello servicio de metadatos de la instancia.

**Solicitud**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Respuesta**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Obtener más información acerca de hello VM durante el caso de soporte técnico 

Como proveedor de servicios, puede obtener una llamada de soporte técnico que desee que tooknow obtener más información acerca de hello VM. Pedir Hola cliente tooshare Hola proceso metadatos pueden proporcionar información básica para tooknow profesional de soporte técnico de hello sobre tipo de saludo de la máquina virtual en Azure. 

**Solicitud**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Respuesta**

> [!NOTE] 
> respuesta de Hello es una cadena JSON. Después de respuesta de ejemplo de Hola es impreso correctamente para mejorar la legibilidad.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Ejemplos de llamar al servicio de metadatos mediante distintos lenguajes dentro de hello VM 

language | Ejemplo 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Go Lan   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
Python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
Javascript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>P+F
1. Recibo mensajes de error de hello `400 Bad Request, Required metadata header not specified`. ¿Qué significa?
   * Hola servicio de metadatos de instancia requiere el encabezado de hello `Metadata: true` toobe transmiten durante una solicitud de saludo. Pasar este encabezado en llamada REST de hello permite acceso toohello servicio de metadatos de la instancia. 
2. ¿Por qué no recibo información de proceso de mi máquina virtual?
   * Hola servicio de metadatos de instancia sólo admite actualmente instancias creadas con el Administrador de recursos de Azure. Hola futuras, podemos agreguemos compatibilidad para las VM del servicio de nube.
3. Creé mi máquina virtual mediante Azure Resource Manager hace un tiempo. ¿Por qué no veo la información de metadatos de proceso?
   * Para las máquinas virtuales creadas después de septiembre de 2016, agregue un [etiqueta](../../azure-resource-manager/resource-group-using-tags.md) toostart ver metadatos de proceso. Para máquinas virtuales anteriores (creadas antes de septiembre de 2016), agregar o quitar extensiones de metadatos o con datos discos toohello VM toorefresh.
4. ¿Por qué recibo errores hello `500 Internal Server Error`?
   * Vuelva a intentar la solicitud en función del sistema de interrupción exponencial. Si no se soluciona el problema de hello póngase en contacto con el soporte técnico de Azure.
5. ¿Dónde puedo compartir preguntas o comentarios adicionales?
   * Envíe los comentarios en http://feedback.azure.com.
7. ¿Esto funciona para la instancia del conjunto de escala de máquinas virtuales?
   * Sí, el servicio de metadatos está disponible para las instancias del conjunto de escala. 
6. ¿Cómo se puede obtener soporte técnico para servicio de hello?
   * tooget soporte para el servicio de hello, crear un problema de compatibilidad en el portal de Azure para hello VM donde no es capaz de tooget metadatos respuesta después de varios reintentos largos 

   ![Soporte técnico de metadatos de instancia](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Pasos siguientes

- Obtener más información sobre hello [eventos programados](scheduled-events.md) API **en vista previa pública** proporcionada por hello servicio de metadatos de la instancia.
