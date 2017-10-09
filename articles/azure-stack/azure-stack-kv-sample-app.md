---
title: "secretos de almacén de claves de Azure pila de aaaAllow aplicación tooretrieve | Documentos de Microsoft"
description: "Usar un toowork de la aplicación de ejemplo con el almacén de claves de pila de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a>Ejecutar la aplicación de ejemplo de Hola para el almacén de claves

En esta guía, usará un tooretrieve de la aplicación de ejemplo secretos y las contraseñas desde el almacén de claves.

## <a name="download-hello-samples-and-prepare"></a>Descargar ejemplos de hello y preparar
Descargar los ejemplos de cliente del almacén de claves de Azure de Hola de hello [página de ejemplos de cliente de almacén de claves de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Extraiga el contenido de hello del equipo local del tooyour de archivo .zip Hola.

Hola de lectura **README.md** archivo (es decir, un archivo de texto) y, a continuación, siga las instrucciones de Hola.

## <a name="run-sample-1--hellokeyvault"></a>Ejecutar el ejemplo #1: HelloKeyVault
HelloKeyVault es una aplicación de consola que le guía a través de los escenarios clave de Hola que son compatibles con el almacén de claves:

1. Crear o importar una clave (clave HSM o software)
2. Cifrar un secreto con una clave de contenido
3. Incluir clave de contenido de hello mediante una clave de almacén de claves
4. Unwrap clave de contenido de Hola
5. Descifrar el secreto de Hola
6. Establecer un secreto

Debe ejecutar esa aplicación de consola sin realizar ningún cambio, salvo que los valores de configuración adecuados de hello en el archivo App.Config se actualizará según toohello pasos:

1. Actualizar valores de configuración de aplicación hello en HelloKeyVault\App.config con su URL del almacén, el Id. de aplicación principal y el secreto. información de Hello, opcionalmente, se pueden generar mediante **scripts\GetAppConfigSettings.ps1**.
2. Actualizar valores de hello de variables obligatoria de hello en GetAppConfigSettings.ps1.
3. Inicie la ventana de Windows PowerShell de Hola.
4. Ejecutar script de Hola GetAppConfigSettings.ps1 dentro de la ventana de PowerShell de hello.
5. Copiar resultados de Hola Hola toohello HelloKeyVault\App.config del archivo de script.

## <a name="next-steps"></a>Pasos siguientes
[Implementación de una máquina virtual con una contraseña de Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Implementación de una máquina virtual con un certificado de Key Vault](azure-stack-kv-push-secret-into-vm.md)

