---
title: "Introducción al Shell de nube (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Información general de hello Shell en la nube de Azure."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Introducción a Azure Cloud Shell (versión preliminar)
Azure Cloud Shell es un shell interactivo, accesible desde el explorador, para administrar recursos de Azure.

![](media/overview-pic.png)

## <a name="features"></a>Características
### <a name="browser-based-shell-experience"></a>Experiencia de shell basada en explorador
La nube Shell permite acceso tooa basadas en el Explorador de línea de comandos experiencia compilada con tareas de administración de Azure en mente. Aprovechar toowork de Shell en la nube sin restricción de un equipo local de forma que se puede proporcionar solo en la nube Hola.

### <a name="pre-configured-azure-workstation"></a>Estación de trabajo de Azure configurada previamente
Cloud Shell viene preinstalado con conocidas populares herramientas de línea de comandos y compatibilidad de idiomas para que pueda trabajar con mayor rapidez.

[Vista Hola herramientas completa lista para el Shell de nube de Azure aquí.](features.md#tools)

### <a name="automatic-authentication"></a>Autenticación automática
Shell de la nube segura autentica automáticamente en cada sesión en recursos de tooyour de acceso instantáneo a través de hello 2.0 de CLI de Azure.

### <a name="connect-your-azure-file-storage"></a>Conexión a Azure File Storage
Máquinas de Shell en la nube son temporales y ello requiere un toobe del recurso compartido de archivos de Azure montado como `clouddrive` toopersist el directorio $Home.
Primer inicio Shell de nube le pedirá toocreate que compartan un grupo de recursos, la cuenta de almacenamiento y el archivo en su nombre. Esto es un paso único y se adjuntará automáticamente en todas las sesiones. 

#### <a name="create-new-storage"></a>creación de nuevo almacenamiento
![](media/basic-storage.png)

Se crea una cuenta de almacenamiento con redundancia local (LRS) en su nombre con un recurso compartido de archivos de Azure que, de forma predeterminada, contiene una imagen de disco de 5 GB. recurso compartido de archivos de Hello monta como `clouddrive` archivo compartir interacción con la imagen de disco de Hola que se usa toosync y conservar el directorio $Home. Se aplican costos por almacenamiento normal.

Se crearán tres recursos en su nombre:
1. Grupo de recursos llamado: `cloud-shell-storage-<region>`
2. Cuenta de almacenamiento llamada: `cs<uniqueGuid>`
3. Recurso compartido de archivos llamado: `cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Todos los archivos en el directorio $Home, como las claves de SSH, se conservan en la imagen de disco de usuario almacenada en el recurso compartido de archivos montado. Ponga en práctica los procedimientos recomendados para guardar archivos en el directorio $Home y en el recurso compartido de archivos montado.

#### <a name="use-existing-resources"></a>Uso de recursos existentes
![](media/advanced-storage.png)

Una opción avanzada también se proporciona lo que permite tooassociate existente recursos tooCloud Shell. Cuando aparezca el símbolo del sistema de hello almacenamiento el programa de instalación, haga clic en Opciones adicionales de tooselect "Show advanced settings". Las listas desplegables se filtran para las cuentas de almacenamiento redundante local o globalmente y para la región asignada de Cloud Shell.

[Obtenga más información sobre el almacenamiento de Cloud Shell, la actualización de recursos compartidos de archivos y la carga y descarga de archivos]. (persisting-shell-storage.md)

## <a name="concepts"></a>Conceptos
* Cloud Shell se ejecuta en un equipo temporal proporcionado en cada sesión y por usuario
* Cloud Shell agota el tiempo de espera tras 20 minutos sin actividad interactiva.
* Solo se puede acceder a Cloud Shell mediante un recurso compartido de archivo adjuntado.
* Se asigna a Cloud Shell una máquina por cuenta de usuario.
* Los permisos se establecen como un usuario de Linux regular

[Más información sobre todas las características de Cloud Shell.](features.md)

## <a name="examples"></a>Ejemplos
* Crear o editar scripts tooautomate administración de Azure
* Administración simultánea los recursos a través de Azure Portal y la CLI de Azure 2.0
* Prueba de la CLI de Azure 2.0

[Pruebe todos estos ejemplos en Inicio rápido de nube Shell Hola.](quickstart.md)

## <a name="pricing"></a>Precios
máquina de Hello Shell en la nube de hospedaje es gratuito, con un requisito previo de un archivo de Azure montado compartir toopersist el directorio $Home. Se aplican costos por almacenamiento normal.

## <a name="supported-browsers"></a>Exploradores compatibles
Se recomienda Cloud Shell para Chrome, Edge y Safari. Aunque se admite el Shell de nube para Chrome, Firefox, Safari, Internet Explorer y borde, Shell en la nube es la configuración del explorador de toospecific de asunto.

## <a name="troubleshooting"></a>Solución de problemas
1. Cuando se utiliza una suscripción de Azure Active Directory, no se puede crear almacenamiento due tooError: 400 DisallowedOperation. tooresolve esto, use una suscripción de Azure capaz de crear los recursos de almacenamiento. Las suscripciones de AD es toocreate imposibilidad de recursos de Azure.

Para conocer las limitaciones conocidas específicas, consulte las [limitaciones de Cloud Shell](limitations.md).
