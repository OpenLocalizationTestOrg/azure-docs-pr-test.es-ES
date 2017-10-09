



Según el entorno y las opciones, script de Hola puede crear todos los infraestructura de clúster de hello, incluidas las Hola red virtual de Azure, las cuentas de almacenamiento, servicios en la nube, controlador de dominio, las bases de datos SQL locales o remotos, nodo principal y clúster adicionales nodos. Como alternativa, el script de Hola puede usar infraestructura preexistente de Azure y crear solo Hola nodos de clúster HPC.

Para obtener información general acerca de cómo diseñar un clúster de HPC Pack, vea hello [Product Evaluation and Planning](https://technet.microsoft.com/library/jj899596.aspx) y [Introducción](https://technet.microsoft.com/library/jj899590.aspx) contenido en la biblioteca de TechNet de HPC Pack 2012 R2 Hola.

## <a name="prerequisites"></a>Requisitos previos
* **Suscripción de Azure**: puede usar una suscripción en cualquier servicio Global de Azure o Azure China Hola. Afecta a los límites de su suscripción Hola número y tipo de nodos del clúster que puede implementar. Para obtener información, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../articles/azure-subscription-service-limits.md).
* **Equipo de cliente de Windows con PowerShell de Azure 0.8.10 o posterior instalado y configurado**: vea [empezar a trabajar con Azure PowerShell](/powershell/azureps-cmdlets-docs) para instalación pasos e instrucciones tooconnect tooyour suscripción de Azure.
* **Script de implementación de IaaS de HPC Pack**: Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Comprobar la versión de Hola de script de Hola ejecutando `New-HPCIaaSCluster.ps1 –Version`. En este artículo se basa en la versión 4.5.2 de script de Hola.
* **Archivo de configuración de la secuencia de comandos**: crear un archivo XML que el script de Hola usa clúster de HPC tooconfigure Hola. Para obtener información y ejemplos, vea las secciones más adelante en este artículo y Hola archivo Manual.rtf que se incluye en script de implementación de Hola.

## <a name="syntax"></a>Sintaxis
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Ejecutar script de Hola como administrador.
> 
> 

### <a name="parameters"></a>parameters
* **ConfigFile**: especifica la ruta de acceso de archivo de Hola Hola configuración archivo toodescribe Hola del clúster de HPC. Obtenga más información sobre el archivo de configuración de hello en este tema, o en el archivo hello Manual.rtf en carpeta de Hola que contiene el script de Hola.
* **AdminUserName**: especifica el nombre de usuario de Hola. Si el bosque de dominio de hello creado por el script de Hola, se convierte en nombre de usuario de administrador local de Hola para todas las máquinas virtuales y el nombre de administrador de dominio de Hola. Si ya existe un bosque de dominio de hello, esto especifica el usuario del dominio de Hola Hola tooinstall de nombre de usuario de administrador local HPC Pack.
* **AdminPassword**: especifica la contraseña del Administrador de Hola. Si no se especifica en la línea de comandos de hello, Hola script le indicará que contraseña de hello tooinput.
* **HPCImageName** (opcional): especifica el nombre de imagen de máquina virtual de HPC Pack hello usa el clúster de HPC de hello toodeploy. Debe ser una imagen proporcionada por Microsoft HPC Pack desde hello Azure Marketplace. Si hello (se recomienda normalmente), no se especificó script elige hello más reciente publicada [imagen de HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). imagen más reciente de Hola se basa en Windows Server 2012 R2 Datacenter con HPC Pack 2012 R2 Update 3 instalado.
  
  > [!NOTE]
  > Se producirá un error en la implementación si no se indica una imagen de HPC Pack válida.
  > 
  > 
* **Archivo de registro** (opcional): especifica la ruta de acceso de archivo de registro de hello implementación. Si no se especifica, el script de Hola crea un archivo de registro en el directorio temporal de hello del equipo de hello ejecutar script de Hola.
* **Force** (opcional): suprime todos los mensajes de confirmación de Hola.
* **NoCleanOnFailure** (opcional): Especifica que Hola máquinas virtuales de Azure que no se han implementado correctamente no se quitan. Quite manualmente estas máquinas virtuales antes de volver a ejecutar Hola script toocontinue hello, u Hola implementación puede producir un error.
* **PSSessionSkipCACheck** (opcional): para cada servicio de nube con máquinas virtuales implementadas por este script, Azure genera automáticamente un certificado autofirmado y Hola todas las máquinas virtuales en el servicio de nube de hello usan este certificado Hola predeterminado de Windows Certificado de administración (WinRM) remoto. toodeploy características de HPC en estas máquinas virtuales de Azure, script de Hola predeterminada temporalmente instala estos certificados en hello ordenador\\almacén de entidades de certificación raíz de confianza de toosuppress de equipo del cliente de Hola Hola seguridad "entidad emisora de certificados de confianza no" Error durante la ejecución del script. Hola certificados se eliminan cuando finaliza la secuencia de comandos de Hola. Si se especifica este parámetro, certificados de hello no están instalados en el equipo cliente de Hola y se suprime la advertencia de seguridad de Hola.
  
  > [!IMPORTANT]
  > No se recomienda el uso de este parámetro para implementaciones de producción.
  > 
  > 

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se crea un clúster de HPC Pack mediante el archivo de configuración *MyConfigFile.xml*y especifica las credenciales de administrador para la instalación de clúster de Hola.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Consideraciones adicionales
* script de Hola, opcionalmente, puede habilitar el envío de trabajos a través del portal web de HPC Pack de Hola o hello API de REST de HPC Pack.
* script de Hola, opcionalmente, puede ejecutar secuencias de comandos previas y posteriores a la configuración personalizadas en el nodo principal de hello si desea que un software adicional tooinstall o configurar otras opciones.

## <a name="configuration-file"></a>Archivo de configuración
archivo de configuración de Hello para el script de implementación de hello es un archivo XML. archivo de esquema de Hello HPCIaaSClusterConfig.xsd está en la carpeta de script de implementación de IaaS de HPC Pack de Hola. **IaaSClusterConfig** es elemento raíz de Hola Hola del archivo de configuración, que contiene elementos secundarios de Hola se describe detalladamente en el archivo hello Manual.rtf en la carpeta de script de implementación de Hola.

