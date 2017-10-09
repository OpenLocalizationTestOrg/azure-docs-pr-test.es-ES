---
title: problemas de almacenamiento de archivos de Azure aaaTroubleshoot en Windows | Documentos de Microsoft
description: "Solución de problemas de Azure File Storage en Windows"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Solución de problemas de Azure File Storage en Windows

Este artículo enumeran los problemas comunes que están relacionado tooMicrosoft almacenamiento de archivos de Azure cuando se conecta desde los clientes de Windows. También se proporcionan posibles causas de estos problemas y sus resoluciones. Además de solución de problemas de toohello los pasos en este artículo, también puede usar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para asegurarse de que Windows hello entorno de cliente tiene requisitos previos correcta. AzFileDiagnostics automatiza la detección de la mayoría de los síntomas de Hola que se mencionan en este artículo y le ayuda a configurar su entorno tooget un rendimiento óptimo. También puede encontrar esta información en hello [Solucionador de problemas de recursos compartidos de archivos de Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que proporciona pasos tooassist con problemas comparte archivos de Azure de conectarse, asignación/montaje.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Error 53, Error 67 o Error 87 al montar o desmontar un recurso compartido de archivos de Azure

Cuando intente toomount un archivo de recurso compartido desde el entorno local o desde otro centro de datos, podría recibir Hola siguientes errores:

- Error de sistema 53. no se encontró la ruta de acceso de red de Hola.
- Error de sistema 67. no se encuentra el nombre de red de Hola.
- Error de sistema 87. Hola parámetro es incorrecto.

### <a name="cause-1-unencrypted-communication-channel"></a>Causa 1: Canal de comunicación sin cifrar

Por motivos de seguridad, las conexiones se bloquean recursos compartidos de archivos de tooAzure si no se cifra canal de comunicación de Hola y si no está realizando el intento de conexión de Hola de Hola mismo centro de datos donde residen los recursos compartidos de archivos de Azure de Hola. Proporciona el cifrado de canal de comunicación únicamente si el sistema operativo de cliente del usuario de hello es compatible con el cifrado SMB.

Windows 8, Windows Server 2012 y versiones posteriores de cada sistema negocian solicitudes que incluyen SMB 3.0, que es compatible con el cifrado.

### <a name="solution-for-cause-1"></a>Solución para la causa 1

Conectarse desde un cliente que realiza una de las siguientes hello:

- Hola cumple los requisitos de Windows 8 y Windows Server 2012 o versiones posteriores
- Se conecta desde una máquina virtual en hello mismo centro de datos como Hola cuenta de almacenamiento de Azure que se usa para el recurso compartido de archivos de Azure de Hola

### <a name="cause-2-port-445-is-blocked"></a>Causa 2: Puerto 445 bloqueado

Error del sistema 53 o error del sistema 67 puede producirse si se ha bloqueado el puerto 445 comunicación saliente tooan archivos de Azure almacenamiento centro de datos. Resumen de hello toosee de ISP que permitir o denegar el acceso desde el puerto 445, vaya demasiado[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand si ésta es la razón de hello detrás de mensaje de bienvenida de "Error del sistema 53", puede utilizar el punto de conexión de Portqry tooquery hello TCP:445. Si el punto de conexión de hello TCP:445 se muestra como filtrados, Hola el puerto TCP está bloqueado. Aquí se muestra una consulta de ejemplo:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Si el puerto TCP 445 está bloqueado por una regla a lo largo de la ruta de acceso de red de hello, verá Hola después de salida:

  `TCP port 445 (microsoft-ds service): FILTERED`

Para obtener más información acerca de cómo toouse Portqry, consulte [descripción de la utilidad de línea de comandos Portqry.exe de hello](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Solución para la causa 2

Trabajar con el puerto de tooopen del departamento de TI 445 saliente demasiado[intervalos de direcciones IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Causa 3: NTLMv1 habilitado

Error del sistema 53 o error del sistema 87 puede producirse si se habilita la comunicación de NTLMv1 en cliente Hola. Azure File Storage solo admite la autenticación NTLMv2. Si se habilita NTLMv1, el cliente será menos seguro. Por lo tanto, se bloquea la comunicación con Azure File Storage. 

toodetermine si ésta es Hola causa del error de hello, compruebe que hello en la siguiente subclave del registro está establecido el valor de tooa de 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa &gt; LmCompatibilityLevel**

Para obtener más información, vea hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) tema en TechNet.

### <a name="solution-for-cause-3"></a>Solución para la causa 3

Revertir hello **LmCompatibilityLevel** valor toohello el valor de 3 en la siguiente subclave del registro de hello:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Error 1816 "no hay suficiente cuota está disponible tooprocess este comando" al copiar recurso compartido de archivos de Azure de tooan

### <a name="cause"></a>Causa

Error 1816 se produce cuando se alcanza el límite superior de Hola de identificadores abiertos simultáneas que se permiten en un archivo en el equipo de Hola donde se está montado el recurso compartido de archivos de Hola.

### <a name="solution"></a>Solución

Reduzca el número de Hola de simultáneos identificadores abiertos por cerrar algunos identificadores y, a continuación, vuelva a intentar. Para más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Archivo lento copiar tooand de almacenamiento de archivos de Azure en Windows

Puede que vea un rendimiento lento cuando intente tootransfer archivos toohello servicio archivo de Azure.

- Si no tiene un requisito específico de tamaño de E/S mínima, se recomienda que utilice 1 MB como Hola tamaño de E/S para un rendimiento óptimo.
-   Si conoce tamaño final de Hola de un archivo que está ampliando con escribe y el software no tiene problemas de compatibilidad al final no escrito en el archivo hello hello contiene ceros, a continuación, conjunto Hola tamaño del archivo de antemano en lugar de realizar una escritura de ampliación de cada escritura.
-   Utilice el método de copia derecho de hello:
    -   Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para todas las transferencias entre dos recursos compartidos de archivos.
    -   Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre recursos compartidos de archivos en un equipo local.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Consideraciones para Windows 8.1 o Windows Server 2012 R2

Para los clientes que ejecutan Windows 8.1 o Windows Server 2012 R2, asegúrese de que ese hello [KB3114025](https://support.microsoft.com/help/3114025) revisión esté instalada. Esta revisión mejora el rendimiento de Hola de crear y cerrar identificadores.

Puede ejecutar Hola después script toocheck si se ha instalado la revisión de hello:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Si está instalada la revisión, hello resultado siguiente se muestra:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Las imágenes de Windows Server 2012 R2 de Azure Marketplace tienen la revisión KB3114025 instalada de manera predeterminada desde diciembre de 2015.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>No hay ninguna carpeta con una letra de unidad en **Mi PC**

Si asigna un recurso compartido de archivos de Azure como administrador mediante el uso de net use, el recurso compartido de hello aparece toobe falta.

### <a name="cause"></a>Causa

De manera predeterminada, el Explorador de archivos de Windows no se ejecuta como administrador. Si ejecuta net use desde un símbolo del sistema administrativo, asignar unidad de red de hello como administrador. Dado que las unidades asignadas son centrado en el usuario, cuenta de usuario de Hola que se registra en no muestra las unidades de hello si se montan en una cuenta de usuario diferente.

### <a name="solution"></a>Solución
Monte el recurso compartido de Hola desde una línea de comandos sin privilegios de administrador. Como alternativa, puede seguir [en este tema de TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** valor del registro.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Se produce un error en el comando NET use si la cuenta de almacenamiento de hello contiene una barra diagonal

### <a name="cause"></a>Causa

comando de net use Hola interpreta una barra diagonal (/) como una opción de línea de comandos. Si el nombre de cuenta de usuario comienza con una barra diagonal, se produce un error en la asignación de unidades de Hola.

### <a name="solution"></a>Solución

Puede utilizar cualquiera de hello siguiendo los pasos toowork problema hello:

- Ejecute el siguiente comando de PowerShell de hello:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  Desde un archivo por lotes, puede ejecutar comandos de hello así:

  `Echo new-smbMapping ... | powershell -command –`

- Colocar comillas dobles alrededor de hello toowork clave alternativa para este problema, a menos que coincide con barra diagonal Hola Hola primer carácter. Si es así, use el modo interactivo de Hola y escriba la contraseña por separado o volver a generar el tooget claves una clave que no se inicia con una barra diagonal.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>La aplicación o el servicio no puede acceder a una unidad de Azure File Storage montada

### <a name="cause"></a>Causa

Las unidades se montan para usuarios individuales. Si su aplicación o servicio se ejecuta bajo una cuenta de usuario diferente de Hola que Hola unidad montada, aplicación hello no podrán ver la unidad de Hola.

### <a name="solution"></a>Solución

Use uno de hello siguientes soluciones:

-   Monte la unidad de Hola de hello misma cuenta de usuario que contiene la aplicación hello. Puede usar una herramienta como PsExec.
- Pasar el nombre de cuenta de almacenamiento de Hola y la clave en los parámetros de nombre y la contraseña de usuario Hola de comando de net use Hola.

Después de seguir estas instrucciones, es posible que reciba Hola mensaje de error siguiente cuando ejecute net use para la cuenta de servicio de red o sistema de hello: "1312 error del sistema. Una sesión de inicio especificada no existe. Es posible que haya finalizado." Si esto ocurre, asegúrese de que ese nombre de usuario de Hola que se pasa el uso de toonet incluye información de dominio (por ejemplo: "[nombre de cuenta de almacenamiento]. file.core.windows. NET").

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Error "Va a copiar un archivo de destino tooa que no admite el cifrado"

Cuando se copia un archivo a través de red de hello, archivo hello se descifra en equipo de origen de hello, transmiten en texto sin formato y vuelve a cifrar en el destino de Hola. Sin embargo, podría ver Hola tras error al que está tratando de toocopy un archivo cifrado: ", copia Hola archivo tooa destino que no admite el cifrado."

### <a name="cause"></a>Causa
Este problema puede producirse si está usando Sistema de cifrado de archivos (EFS). Archivos cifrados mediante BitLocker pueden ser almacenamiento de archivos copiados tooAzure. Sin embargo, Azure File Storage no admite NTFS EFS.

### <a name="workaround"></a>Solución alternativa
toocopy un archivo a través de red de hello, deberá descifrarlo. Utilice uno de los siguientes métodos de hello:

- Hola de uso **copiar /d** comando. Permite Hola cifrado archivos toobe guardado como archivos descifrados en el destino de Hola.
- Establecer Hola después de la clave del registro:
  - Ruta de acceso = HKLM\Software\Policies\Microsoft\Windows\System
  - Tipo de valor = DWORD
  - Nombre = CopyFileAllowDecryptedRemoteDestination
  - Valor = 1

Tenga en cuenta esa clave del registro de hello de configuración afecta a todas las operaciones de copia que se realizan acciones toonetwork.

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget resuelva el problema rápidamente.
