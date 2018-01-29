---
title: Referencia del servicio Infrastructure Backup de Azure Stack | Microsoft Docs
description: "Este artículo contiene material de referencia para el servicio Infrastructure Backup de Azure Stack."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: D6EC0224-97EA-446C-BC95-A3D32F668E2C
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: mabrigg
ms.openlocfilehash: 4e6e0a52b2c55239e38757223f54e5e94dc98c42
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="infrastructure-backup-service-reference"></a>Referencia del servicio Infrastructure Backup

## <a name="azure-backup-infrastructure"></a>Infraestructura de copia de seguridad de Azure

*Se aplica a: sistemas integrados de Azure Stack y kit de desarrollo de Azure Stack*

Azure Stack consta de muchos servicios entre los que figuran el portal, Azure Resource Manager y la experiencia de administración de la infraestructura. La experiencia de administración de Azure Stack, similar a la de un dispositivo, se centra en reducir la complejidad expuesta al operador de la solución.

Infrastructure Backup está diseñado para internalizar la complejidad de la copia de seguridad y la restauración de datos para los servicios de infraestructura, asegurándose de que los operadores puede centrarse en la administración de la solución y el mantenimiento del Acuerdo de Nivel de Servicio de los usuarios.

Se requiere la exportación de los datos de copia de seguridad a un recurso compartido externo para evitar el almacenamiento de copias de seguridad en el mismo sistema. La necesidad de un recurso compartido externo proporciona al administrador flexibilidad para determinar dónde se almacenarán los datos en función de las directivas existentes sobre continuidad del negocio y recuperación ante desastres de la empresa. 

### <a name="infrastructure-backup-components"></a>Componentes de Infrastructure Backup

Infrastructure Backup incluye los siguientes componentes:

 - **Infrastructure Backup Controller**  
 En cada nube de Azure Stack se genera una instancia del controlador Infrastructure Backup Controller, que además reside en ellas.
 - **Backup Resource Provider**  
 El proveedor Backup Resource Provider (Backup RP) consta de la interfaz de usuario y de las interfaces de programación de aplicaciones (API) que exponen la funcionalidad básica de copia de seguridad para la infraestructura de Azure Stack.

#### <a name="infrastructure-backup-controller"></a>Infrastructure Backup Controller

Infrastructure Backup Controller es un servicio de Service Fabric del cual se generan instancias para una nube de Azure Stack. Los recursos de copia de seguridad se crean a nivel regional y capturan datos de servicio específicos de la región de AD, CA, Azure Resource Manager, CRP, SRP, NRP, KeyVault, RBAC. 

### <a name="backup-resource-provider"></a>Backup Resource Provider

Backup Resource Provider presenta la interfaz de usuario en el portal de Azure Stack para la configuración básica y la lista de recursos de copia de seguridad. El operador puede realizar las operaciones siguientes en la interfaz de usuario:

 - Habilitar la copia de seguridad por primera vez al proporcionar la ubicación de almacenamiento externa, las credenciales y la clave de cifrado
 - Ver los recursos de copia de seguridad creados y completados y los recursos de estado en creación
 - Modificar la ubicación de almacenamiento en la que Backup Controller coloca los datos de copia de seguridad
 - Modificar las credenciales que utiliza Backup Controller para tener acceso a la ubicación de almacenamiento externa
 - Modificar la clave de cifrado que utiliza Backup Controller para cifrar las copias de seguridad 


## <a name="backup-controller-requirements"></a>Requisitos de Backup Controller

En esta sección se describen los requisitos importantes para Infrastructure Backup. Es recomendable que revise cuidadosamente la siguiente información antes de habilitar la copia de seguridad para su instancia de Azure Stack y que luego la consulte según sea necesario durante la implementación y el funcionamiento posterior.

Estos requisitos son:

  - **Requisitos de software**: describe las ubicaciones de almacenamiento admitidas y las orientaciones sobre el ajuste de tamaño. 
  - **Requisitos de red**: describe los requisitos de red para las diferentes ubicaciones de almacenamiento.  

### <a name="software-requirements"></a>Requisitos de software

#### <a name="supported-storage-locations"></a>Ubicaciones de almacenamiento admitidas

| Ubicación de almacenamiento                                                                 | Detalles                                                                                                                                                  |
|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Recurso compartido de archivos SMB hospedado en un dispositivo de almacenamiento dentro del entorno de red de confianza | Recurso compartido SMB en el mismo centro de datos en el que está implementado Azure Stack u otro centro de datos. Varias instancias de Azure Stack pueden usar el mismo recurso compartido de archivos. |
| Recurso compartido de archivos SMB en Azure                                                          | No se admite actualmente.                                                                                                                                 |
| Blob Storage en Azure                                                            | No se admite actualmente.                                                                                                                                 |

#### <a name="supported-smb-versions"></a>Versiones de SMB admitidas

| SMB | Versión |
|-----|---------|
| SMB | 3.x     |

#### <a name="storage-location-sizing"></a>Ajuste del tamaño de la ubicación de almacenamiento 

Infrastructure Backup Controller realizará una copia de datos a petición. La recomendación es realizar una copia de seguridad por lo menos dos veces al día y guardar como máximo siete días de copias de seguridad. 

| Escala del entorno | Tamaño previsto de copia de seguridad | Cantidad total de espacio necesario |
|-------------------|--------------------------|--------------------------------|
| 4-12 nodos        | 10 GB                     | 140 GB                          |

### <a name="network-requirements"></a>Requisitos de red
| Ubicación de almacenamiento                                                                 | Detalles                                                                                                                                                                                 |
|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Recurso compartido de archivos SMB hospedado en un dispositivo de almacenamiento dentro del entorno de red de confianza | El puerto 445 es necesario si la instancia de Azure Stack reside en un entorno protegido por firewall. Infrastructure Backup Controller iniciará una conexión con el servidor de archivos SMB en el puerto 445. |
| Para usar el FQDN en el servidor de archivos, el nombre debe poder resolverse desde el PEP.             |                                                                                                                                                                                         |

> [!Note]  
> Ningún puerto de entrada debe estar abierto.


## <a name="infrastructure-backup-limits"></a>Límites de Infrastructure Backup

Tenga en cuenta estos límites a medida que planee, implemente y maneje las instancias de Microsoft Azure Stack. En la siguiente tabla se describen estos límites.

### <a name="infrastructure-backup-limits"></a>Límites de Infrastructure Backup
| Identificador de límites                                                 | Límite        | Comentarios                                                                                                                                    |
|------------------------------------------------------------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de copia de seguridad                                                      | Solo completa    | Infrastructure Backup Controller solo admite copias de seguridad completas. Las copias de seguridad incrementales no se admiten.                                          |
| Copias de seguridad programadas                                                | Solo manual  | Backup Controller actualmente solo admite copias de seguridad a petición                                                                                 |
| Número máximo de trabajos de copia de seguridad simultáneos                                   | 1            | Se admite solo un trabajo de copia de seguridad activo por instancia de Backup Controller.                                                                  |
| Configuración del conmutador de red                                     | Fuera del ámbito | El administrador debe hacer una copia de seguridad de la configuración del conmutador de red con herramientas de OEM. Consulte la documentación para Azure Stack proporcionada por cada proveedor de OEM. |
| Host de ciclo de vida de hardware                                          | Fuera del ámbito | El administrador debe hacer una copia del host de ciclo de vida de hardware mediante herramientas de OEM. Consulte la documentación para Azure Stack proporcionada por cada proveedor de OEM.      |
| Número máximo de recursos compartidos de archivos                                    | 1            | Solo se puede usar un recurso compartido de archivo para almacenar los datos de copia de seguridad                                                                                        |
| Backup App Services, Function, SQL, mysql, datos de proveedores de recursos | Fuera del ámbito | Consulte las orientaciones publicadas para implementar y administrar los proveedores de recursos de valor añadido creados por Microsoft.                                                  |
| Copia de seguridad de proveedores de recursos de terceros                              | Fuera del ámbito | Consulte las orientaciones publicadas para implementar y administrar los proveedores de recursos de valor agregado creados por otros proveedores.                                          |

## <a name="next-steps"></a>pasos siguientes

 - Para obtener más información sobre Infrastructure Backup Service, consulte [Copia de seguridad y recuperación de datos para Azure Stack con el servicio Infrastructure Backup](azure-stack-backup-infrastructure-backup.md).