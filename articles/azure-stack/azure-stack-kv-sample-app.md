---
title: "Permitir a la aplicación recuperar los secretos del almacén de claves de Azure Stack | Microsoft Docs"
description: "Usar una aplicación de ejemplo para trabajar con el almacén de claves de Azure Stack"
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
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a>Ejecutar la aplicación de ejemplo para el almacén de claves

En esta guía, deberá usar una aplicación de ejemplo para recuperar los secretos y las contraseñas desde el almacén de claves.

## <a name="download-the-samples-and-prepare"></a>Descargue las muestras y preparar
Descargar los ejemplos de cliente del almacén de claves de Azure desde el [página de ejemplos de cliente de almacén de claves de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Extraiga el contenido del archivo .zip en el equipo local.

Leer la **README.md** archivo (es decir, un archivo de texto) y, a continuación, siga las instrucciones.

## <a name="run-sample-1--hellokeyvault"></a>Ejecutar el ejemplo #1: HelloKeyVault
HelloKeyVault es una aplicación de consola que le guía a través de los escenarios clave que son compatibles con el almacén de claves:

1. Crear o importar una clave (clave HSM o software)
2. Cifrar un secreto con una clave de contenido
3. Ajustar la clave de contenido utilizando una clave de almacén de claves
4. Desempaquetar la clave de contenido
5. Descifrar el secreto
6. Establecer un secreto

Esa aplicación de consola debe ejecutar sin cambios, excepto en que los valores de configuración adecuado en el archivo App.Config se actualizarán según los pasos siguientes:

1. Actualice los valores de configuración de aplicación en HelloKeyVault\App.config con su URL del almacén, el Id. de aplicación principal y el secreto. Opcionalmente, se pueden generar la información mediante **scripts\GetAppConfigSettings.ps1**.
2. Actualice los valores de las variables en GetAppConfigSettings.ps1 obligatorios.
3. Inicie la ventana de Windows PowerShell.
4. Ejecute el script GetAppConfigSettings.ps1 dentro de la ventana de PowerShell.
5. Copiar los resultados de la secuencia de comandos en el archivo HelloKeyVault\App.config.

## <a name="next-steps"></a>Pasos siguientes
[Implementación de una máquina virtual con una contraseña de Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Implementación de una máquina virtual con un certificado de Key Vault](azure-stack-kv-push-secret-into-vm.md)

