1. Copiar carpeta local de hello installer tooa (por ejemplo, C:\Temp) en servidores de Hola que desee que tooprotect. Ejecute hello después de comandos como administrador en un símbolo del sistema:

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall servicio de movilidad, ejecute el siguiente comando de hello:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Ahora, agente de hello debe toobe registrado con el servidor de configuración de Hola.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>Argumentos de la línea de comandos del instalador de Mobility Service

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| Parámetro|Tipo|Descripción|Valores posibles|
|-|-|-|-|
|/Role|Obligatorio|Especifica si se debe instalar Mobility Service (MS) o debe instalarse MasterTarget(MT)|MS </br> MT|
|/InstallLocation|Opcional|Ubicación en que se instala Mobility Service|Cualquier carpeta de equipo de Hola|
|/Platform|Obligatorio|Especifica la plataforma de hello en qué Hola se instala el servicio de movilidad </br> </br>- **VMware**: utilice este valor si va a instalar Mobility Service en una máquina virtual que se ejecuta en *ESXi Hosts de VMware vSphere*, *Hosts de Hyper-V* y *servidores físicos* </br> - **Azure**: utilice este valor si va a instalar el agente en una máquina virtual de IaaS de Azure| VMware </br> Las tablas de Azure|
|/Silent|Opcional|Especifica el instalador de hello toorun en modo silencioso| N/D|

>[!TIP]
> registros de instalación de Hello pueden encontrarse en %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Argumentos de la línea de comandos del registro de Mobility Service

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Parámetro|Tipo|Descripción|Valores posibles|
  |-|-|-|-|
  |/CSEndPoint |Obligatorio|Dirección IP del servidor de configuración de Hola| Cualquier dirección IP válida|
  |/PassphraseFilePath|Obligatorio|Ubicación de frase de contraseña de Hola |Cualquier ruta de acceso local o UNC válida|


>[!TIP]
> Hola AgentConfiguration registros pueden encontrarse en %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
