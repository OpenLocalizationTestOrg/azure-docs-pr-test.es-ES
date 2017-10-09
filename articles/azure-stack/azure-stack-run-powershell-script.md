---
title: Hola aaaDeploy Kit de desarrollo de pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprepare Hola Kit de desarrollo de pila de Azure y ejecución Hola PowerShell script toodeploy."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 0ad02941-ed14-4888-8695-b82ad6e43c66
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/17/2017
ms.author: erikje
ms.openlocfilehash: a96879fb91000f6b3d3aac3089861e8a573ebead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-azure-stack-development-kit"></a>Implementar Hola Kit de desarrollo de pila de Azure
kit de desarrollo de hello toodeploy, debe completar Hola pasos:

1. [Descargar el paquete de implementación de hello](https://azure.microsoft.com/overview/azure-stack/try/?v=try) tooget hello Cloudbuilder.vhdx.
2. [Preparar hello cloudbuilder.vhdx](#prepare-the-development-kit-host) por equipo en ejecución hello asdk installer.ps1 script tooconfigure Hola (host de kit de desarrollo de Hola) en el que desea que el kit de desarrollo de tooinstall. Después de este paso, el host de kit de desarrollo de hello arrancará toohello Cloudbuilder.vhdx.
3. [Implementar el kit de desarrollo de hello](#deploy-the-development-kit) en host de kit de desarrollo de Hola.

> [!NOTE]
> Para obtener mejores resultados, incluso si desea que toouse un entorno desconectado de la pila de Azure, es mejor toodeploy al toohello conectado internet. De este modo, se puede activar versión de evaluación de Windows Server 2016 de Hola durante la implementación. Si no está activada la versión de evaluación de Windows Server 2016 Hola dentro de 10 días, se apaga.
> 
> 

## <a name="download-and-extract-hello-development-kit"></a>Descargue y extraiga el kit de desarrollo de Hola
1. Antes de iniciar la descarga de hello, asegúrese de que el equipo cumple Hola siguiendo los requisitos previos:

   * equipo de Hello debe tener al menos 60 GB de espacio libre en disco.
   * [.NET framework 4.6 (o una versión posterior)](https://aka.ms/r6mkiy) debe estar instalado.

2. [Página de introducción de vaya toohello](https://azure.microsoft.com/overview/azure-stack/try/?v=try), proporcione los detalles y haga clic en **enviar**.
3. En **descargar el software de hello**, haga clic en **Kit de desarrollo de Azure pila**.
4. Ejecute el archivo de AzureStackDownloader.exe de hello descargado.
5. Hola **descargador del Kit de desarrollo de Azure pila** ventana, siga los pasos 1 a 5.
6. Una vez finalizada la descarga de hello, haga clic en **ejecutar** toolaunch hello MicrosoftAzureStackPOC.exe.
7. Revise la pantalla Contrato de licencia de bienvenida y la información de hello Self-Extractor asistente y, a continuación, haga clic en **siguiente**.
8. Revise la pantalla de la declaración de privacidad de bienvenida y la información de hello Self-Extractor asistente y, a continuación, haga clic en **siguiente**.
9. Hola seleccione toobe extraído de los archivos de destino para hello, haga clic en **siguiente**.
   * valor predeterminado de Hello es: <drive letter>:\<carpeta actual > \Microsoft pila de Azure
10. Revise la pantalla de ubicación de destino de bienvenida y la información de hello Self-Extractor asistente y, a continuación, haga clic en **extraer** tooextract Hola CloudBuilder.vhdx (~ 25 GB) y archivos de ThirdPartyLicenses.rtf. Este proceso tardará algún tiempo toocomplete.

> [!NOTE]
> Después de extraer los archivos de hello, puede eliminar Hola exe y bin archivos toorecover espacio en hello máquina. O bien, puede mover estas ubicación tooanother de archivos, así que si necesita tooredeploy no deberá archivos de hello toodownload nuevo.
> 
> 

## <a name="prepare-hello-development-kit-host"></a>Preparar el host de kit de desarrollo de Hola
1. Asegúrese de que puede físicamente conectar el host de kit de desarrollo de toohello, o que tenga acceso a la consola física (por ejemplo, KVM). Debe tener acceso después de reiniciar el host de kit de desarrollo de hello en el paso 13 siguiente.
2. Asegúrese de que cumple de host de kit de desarrollo de Hola Hola [requisitos mínimos](azure-stack-deploy.md). Puede usar hello [Comprobador de implementación para la pila de Azure](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm sus requisitos.
3. Inicie sesión como Hola host de kit de desarrollo de tooyour de administrador Local.
4. Copiar o mover hello CloudBuilder.vhdx archivo toohello raíz Hola unidad C:\ (C:\CloudBuilder.vhdx).
5. Siguiente ejecución hello toodownload Hola development kit instalador (asdk-installer.ps1) toohello c:\AzureStack_Installer carpeta de archivos en el host del kit de desarrollo de la secuencia de comandos.
    ```powershell
    # Variables
    $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
    $LocalPath = 'c:\AzureStack_Installer'

    # Create folder
    New-Item $LocalPath -Type directory

    # Download file
    Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
    ```
6. Abra una consola de PowerShell con privilegios elevados > Ejecutar script de Hola C:\AzureStack_Installer\asdk-installer.ps1 > haga clic en **preparar vhdx**.
7. En hello **vhdx Cloudbuilder seleccione** página del instalador de hello, examinar tooand Hola seleccione cloudbuilder.vhdx archivo descargado en pasos anteriores Hola.
8. Opcional: Comprobación de hello **agregar controladores** cuadro toospecify una carpeta que contenga los controladores adicionales que desee en el host de Hola.
9. En hello **configuración opcional** , proporcione la cuenta de administrador local de hello para el host de kit de desarrollo de Hola. Si no proporciona estas credenciales, necesitará acceso toohello host de KVM durante el proceso de instalación de Hola a continuación.
10. También en hello **configuración opcional** página, tienes Hola Hola de tooset opción siguientes:
    - **NombreDeEquipo**: esta opción establece el nombre de Hola para host de kit de desarrollo de Hola. nombre de Hello debe cumplir los requisitos de FQDN y debe tener una longitud máxima de 15 caracteres. valor predeterminado de Hello es un nombre de equipo aleatorio generado por Windows.
    - **Zona horaria**: Hola de conjuntos de zona horaria para el host de kit de desarrollo de Hola. valor predeterminado de Hello es (UTC-8:00) hora del Pacífico (Estados Unidos y Canadá).
    - **Configuración de IP estática**: establece una dirección IP estática de su toouse de implementación. En caso contrario, cuando se reinicia el instalador de hello en hello cloudbuilder.vhx, interfaces de red de Hola se configuran con DHCP.
11. Haga clic en **Siguiente**.
12. Si elige una configuración de IP estática en el paso anterior de hello, ahora debe:
    - Seleccionar un adaptador de red. Asegúrese de que puede conectar el adaptador de toohello antes de hacer clic **siguiente**.
    - Asegúrese de que ese hello **dirección IP**, **puerta de enlace**, y **DNS** valores son correctos y, a continuación, haga clic en **siguiente**.
13. Haga clic en **siguiente** toostart proceso de preparación de Hola.
14. Cuando se indique preparación hello **completado**, haga clic en **siguiente**.
15. Haga clic en **reiniciar ahora** tooboot en cloudbuilder.vhdx de Hola y continuar el proceso de implementación de Hola.

## <a name="deploy-hello-development-kit"></a>Implementar el kit de desarrollo de Hola
1. Inicie sesión como Hola host de kit de desarrollo de toohello de administrador Local. Usar credenciales de hello especificadas en los pasos anteriores de Hola.

    > [!IMPORTANT]
    > Para las implementaciones de Azure Active Directory, pila de Azure requiere toohello de acceso a Internet, ya sea directamente o a través de un proxy transparente. implementación de Hello es compatible con exactamente una NIC de redes. Si tiene varios NIC, asegúrese de que sólo uno está habilitado (y todos los demás están deshabilitadas) antes de ejecutar el script de implementación de hello en la sección siguiente de Hola.
    
2. Abra una consola de PowerShell con privilegios elevados > Ejecutar script de \AzureStack_Installer\asdk-installer.ps1 hello (que puede estar en una unidad diferente en hello Cloudbuilder.vhdx) > haga clic en **instalar**.
3. Hola **tipo** cuadro, seleccione **en la nube Azure** o **ADFS**.
    - **Nube de Azure**: Azure Active Directory es el proveedor de identidades de Hola. Utilice este toospecify parámetro un directorio específico que hello AAD cuenta no tiene permisos de administrador global. Nombre completo de un inquilino de directorio de AAD en formato de Hola de. onmicrosoft.com. 
    - **ADFS**: marca predeterminada de hello servicio de directorio es el proveedor de identidades de hello, Hola predeterminado cuenta toosign con es azurestackadmin@azurestack.local, y toouse de contraseña de hello es hello una proporcionada como parte del programa de instalación de Hola.
4. En **contraseña de administrador Local**, Hola **contraseña** cuadro, escribir contraseña de administrador local de hello (que debe coincidir con la contraseña de administrador local de hello actual configurado) y, a continuación, haga clic en  **Siguiente**.
5. Seleccione un toouse de adaptador de red para el kit de desarrollo de hello y, a continuación, haga clic en **siguiente**.
6. Seleccione configuración de red estático para la máquina virtual de hello BGPNAT01 o DHCP.
    - **DHCP** (valor predeterminado): Hola virtual machine Obtiene la configuración de red IP de Hola de servidor DHCP de Hola.
    - **Estática**: use esta opción solo si DHCP no puede asignar una dirección IP válida para Azure pila tooaccess Hola Internet. Debe especificarse una dirección IP estática con longitud de máscara de subred de hello (por ejemplo, 10.0.0.5/24).
7. Además, puede establecer Hola siguientes valores:
    - **Id. de VLAN**: conjuntos de Hola ID de VLAN. Use esta opción solo si hello host y AzS BGPNAT01 deben configurar red física de Hola de tooaccess de Id. de VLAN (e Internet). 
    - **Reenviador DNS**: un servidor DNS se crea como parte del programa Hola a implementación de la pila de Azure. tooallow equipos dentro de hello solución tooresolve nombres fuera de la marca de hello, proporcione el servidor DNS de infraestructura existente. servidor DNS de Hello en marca reenvía el servidor de toothis de las solicitudes de resolución de nombres desconocido.
    - **Servidor horario**: permite establecer un servidor horario específico. 
8. Haga clic en **Siguiente**. 
9. En hello **comprobar propiedades de tarjeta de interfaz de red** página, verá una barra de progreso. 
    - Si dice **no se puede descargar una actualización**, siga las instrucciones de hello en página de Hola.
    - Cuando diga **Completado**, haga clic en **Siguiente**.
10. En la página de **resumen**, haga clic en **Implementar**.
11. Si usa una implementación de Active Directory de Azure, estará más frecuentes tooenter sus credenciales de cuenta de administrador global de Azure Active Directory.
12. proceso de implementación de Hello puede tardar unas horas, durante el cual Hola sistema se reinicia automáticamente una vez.
   
   > [!IMPORTANT]
   > Si desea que el progreso de la implementación de toomonitor hello, inicie sesión como azurestack\AzureStackAdmin. Si inicias sesión en como un administrador local una vez máquina Hola Unidos a un dominio de toohello, no podrá ver progreso de la implementación de Hola. No vuelva a ejecutar la implementación, en su lugar de inicio de sesión como toovalidate azurestack\AzureStackAdmin que se está ejecutando.
   > 
   > 
   
    Cuando se realiza correctamente la implementación de hello, consola de PowerShell de hello muestra: **COMPLETE: acción 'Implementación'**.
   
Si se produce un error en la implementación de hello, puede usar Hola siguientes PowerShell vuelva a ejecutar el script de Hola misma ventana de PowerShell con privilegios elevados:

```powershell
cd c:\CloudDeployment\Setup
.\InstallAzureStackPOC.ps1 -Rerun
```

Este script reiniciará implementación Hola del paso última de Hola que se realizó correctamente.

O bien, puede [volver a implementar](azure-stack-redeploy.md) desde el principio.


## <a name="reset-hello-password-expiration-too180-days"></a>Restablecer días para expiración too180 de hello contraseña

toomake seguro de que esa contraseña Hola de host de kit de desarrollo de hello no expire demasiado pronto, siga estos pasos después de implementar:

1. En el host del kit de desarrollo de hello, abra **Group Policy Management** y navegue demasiado**Group Policy Management** : **bosque: azurestack.local** – **dominios**  : **azurestack.local**.
2. Haga clic con el botón derecho en **MemberServer** y haga clic en **Editar**.
3. Hola Editor de administración de directivas de grupo, navegue demasiado**configuración del equipo** : **directivas** : **configuración de Windows** : **laconfiguracióndeseguridad**: **Directivas de cuenta** : **directiva de contraseñas**.
4. En el panel derecho de hello, haga doble clic en **vigencia máxima de la contraseña**.
5. Hola **vigencia máxima de la contraseña propiedades** cuadro de diálogo, cambio hello **contraseña expirará en** valor too180, a continuación, haga clic en **Aceptar**.


## <a name="next-steps"></a>Pasos siguientes
[Registro de Azure Stack con una suscripción de Azure](azure-stack-register.md)

[Conectar tooAzure pila](azure-stack-connect-azure-stack.md)

