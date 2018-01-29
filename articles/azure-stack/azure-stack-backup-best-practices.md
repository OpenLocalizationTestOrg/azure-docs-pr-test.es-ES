---
title: Procedimientos recomendados del servicio Infrastructure Backup para Azure Stack | Microsoft Docs
description: "Puede seguir el conjunto de procedimientos recomendados al implementar y administrar Azure Stack en su centro de datos para ayudar a mitigar la pérdida de datos si se produce un error grave."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 221FDE40-3EF8-4F54-A075-0C4D66EECE1A
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/27/2017
ms.author: mabrigg
ms.openlocfilehash: b9438f3bab92f40a5c79ce7b7a572195c182be45
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="infrastructure-backup-service-best-practices"></a>Procedimientos recomendados del servicio Infrastructure Backup

*Se aplica a: sistemas integrados de Azure Stack y kit de desarrollo de Azure Stack*

Puede seguir procedimientos recomendados al implementar y administrar Azure Stack en su centro de datos para ayudar a mitigar la pérdida de datos si se produce un error grave.

Debe revisar los procedimientos recomendados periódicamente para comprobar que la instalación cumple aún las normas cuando se realicen cambios en el flujo de la operación. Si surgieran problemas al implementar estos procedimientos recomendados, póngase en contacto con el soporte técnico de Microsoft para obtener ayuda.

## <a name="configuration-best-practices"></a>Procedimientos recomendados de configuración

### <a name="deployment"></a>Implementación

Habilite Infrastructure Backup después de la implementación en cada nube de Azure Stack. Con las herramientas AzureStack-Tools puede programar copias de seguridad desde cualquier cliente o servidor con acceso al punto de conexión de la API de administración del operador.

### <a name="networking"></a>Redes

La cadena de convención de nomenclatura universal (UNC) para la ruta de acceso debe utilizar un nombre de dominio completo. Es posible usar una dirección IP si la resolución de nombres no es posible. Una cadena UNC especifica la ubicación de recursos como archivos compartidos o dispositivos.

### <a name="encryption"></a>Cifrado

La clave de cifrado se utiliza para cifrar los datos de copia de seguridad que se exportan a un almacenamiento externo. La clave se puede generar mediante AzureStack-Tools. 

![AzureStack-Tools](media\azure-stack-backup\azure-stack-backup-encryption1.png)

La clave debe almacenarse en una ubicación segura (por ejemplo, un secreto de Azure Key Vault público). Esta clave se debe utilizar durante la reimplementación de Azure Stack. 

![Almacenamiento de la clave en una ubicación segura.](media\azure-stack-backup\azure-stack-backup-encryption2.png)

## <a name="operational-best-practices"></a>Procedimientos recomendados operativos

### <a name="backups"></a>Copias de seguridad

 - Infrastructure Backup Controller debe activarse a demanda. Se recomienda hacer una copia de seguridad al menos dos veces al día.
 - Los trabajos de copia de seguridad se ejecutan mientras se está ejecutando el sistema, de modo que no hay ningún tiempo de inactividad en las aplicaciones de usuario o las experiencias de administración. Los trabajos de copia de seguridad tardan entre 20 y 40 minutos para una solución que está bajo una carga razonable.
 - Utilizando las instrucciones proporcionadas por el OEM,el host de ciclo de vida de hardware y los conmutadores de red de copia de seguridad manuales deben almacenarse en el recurso compartido de copia de seguridad en el que Backup Controller almacena los datos de copia de seguridad del plano de control. Considere la posibilidad de almacenar las configuraciones del host de ciclo de vida de hardware y el conmutador en la carpeta de la región. Si tiene varias instancias de la Azure Stack en la misma región, puede usar un identificador para cada configuración que pertenezca a una unidad de escala.

### <a name="folder-names"></a>Nombres de carpetas

 - La infraestructura crea la carpeta MASBACKUP automáticamente. Se trata de un recurso compartido administrado por Microsoft. Puede crear recursos compartidos en el mismo nivel que MASBACKUP. No se recomienda la creación de carpetas o datos de almacenamiento dentro de MASBACKUP que no cree Azure Stack. 
 -  Use el nombre de dominio completo y la región en el nombre de la carpeta para diferenciar los datos de copia de seguridad de nubes diferentes. El nombre de dominio completo (FQDN) de su implementación y puntos de conexión de Azure Stack es la combinación de los parámetros de región y de nombre de dominio externo. Para obtener más información, vea [Integración del centro de datos de Azure Stack: DNS](azure-stack-integrate-dns.md).

Por ejemplo, el recurso compartido de copia de seguridad es AzSBackups, hospedado en fileserver01.contoso.com. En ese recurso compartido de archivos puede haber una carpeta para cada implementación de Azure Stack que use el nombre de dominio externo y una subcarpeta que use el nombre de región. 

FQDN: contoso.com  
Región: nyc


    \\fileserver01.contoso.com\AzSBackups
    \\fileserver01.contoso.com\AzSBackups\contoso.com
    \\fileserver01.contoso.com\AzSBackups\contoso.com\nyc
    \\fileserver01.contoso.com\AzSBackups\contoso.com\nyc\MASBackup

La carpeta MASBackup es donde Azure Stack almacena sus datos de copia de seguridad. No debe usar esta carpeta para almacenar sus propios datos. Los OEM no deben usar tampoco esta carpeta para almacenar los datos de copia de seguridad. 

Se recomienda a los OEM que almacenen los datos de copia de seguridad de sus componentes en la carpeta de la región. Cada conmutador de red, host de ciclo de vida de hardware, etc. puede almacenarse en su propia subcarpeta. Por ejemplo: 

    \\fileserver01.contoso.com\AzSBackups\contoso.com\nyc\HLH
    \\fileserver01.contoso.com\AzSBackups\contoso.com\nyc\Switches
    \\fileserver01.contoso.com\AzSBackups\contoso.com\nyc\DeploymentData
    \\fileserver01.contoso.com\AzSBackups\contoso.com\nyc\Registration

### <a name="monitoring"></a>Supervisión

El sistema prevé las siguientes alertas:

| Alerta                                                   | DESCRIPCIÓN                                                                                     | Corrección                                                                                                                                |
|---------------------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Error de copia de seguridad porque el recurso compartido de archivos ha llegado al límite de su capacidad | Recurso compartido de archivos ha llegado al límite de su capacidad y el controlador de copia de seguridad no puede exportar archivos de copia de seguridad a la ubicación. | Agregue más capacidad de almacenamiento e intente realizar la copia de seguridad de nuevo. Elimine copias de seguridad existentes (de la más antigua a la primera) para liberar espacio.                    |
| Error de copia de seguridad debido a problemas de conectividad.             | La red entre Azure Stack y el recurso compartido de archivos está experimentando problemas.                          | Solucione el problema de red e intente realizar la copia de seguridad de nuevo.                                                                                            |
| Error de copia de seguridad debido a un error en la ruta de acceso                | No se puede resolver la ruta de acceso del recurso compartido de archivos                                                          | Asigne el recurso compartido desde otro equipo para asegurarse de que es posible acceder a él. Es posible que tenga que actualizar la ruta de acceso si ya no es válida.       |
| Error de copia de seguridad debido a un problema de autenticación               | Puede haber un problema con las credenciales o un problema de red que afecta a la autenticación.    | Asigne el recurso compartido desde otro equipo para asegurarse de que es posible acceder a él. Es posible que tenga que actualizar las credenciales si ya no son válidas. |
| Error de copia de seguridad debido a un error general                    | La solicitud con error podría deberse a un problema intermitente. Intente realizar la copia de seguridad de nuevo.                    | Llame al soporte técnico.                                                                                                                               |

## <a name="next-steps"></a>pasos siguientes

 - Revise el material de referencia para [el servicio Infrastructure Backup](azure-stack-backup-reference.md).  
 - Habilite el [servicio Infrastructure Backup](azure-stack-backup-enable-backup-console.md).