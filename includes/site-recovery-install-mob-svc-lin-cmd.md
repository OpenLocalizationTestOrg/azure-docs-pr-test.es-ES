1. Copie Hola instalador tooa carpeta local (por ejemplo, / tmp) en servidores de Hola que desee que tooprotect. En un terminal, ejecute hello siguientes comandos:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall servicio de movilidad, ejecute el siguiente comando de hello:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Una vez completada la instalación, Hola Mobility Service debe servidor de configuración de tooget toohello registrados. Siguiente ejecución Hola comando tooregister Hola Mobility Service con el servidor de configuración.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Línea de comandos del instalador de Mobility Service

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parámetro|Tipo|Descripción|Valores posibles|
|-|-|-|-|
|-r |Obligatorio|Especifica si se debe instalar Mobility Service (MS) o debe instalarse MasterTarget(MT)|MS </br> MT|
|-d |Opcional|Ubicación en que se instalará Mobility Service|/usr/local/ASR|
|-v|Obligatorio|Especifica la plataforma de hello en qué Hola se instala el servicio de movilidad </br> </br>- **VMware**: utilice este valor si va a instalar Mobility Service en una máquina virtual que se ejecuta en *ESXi Hosts de VMware vSphere*, *Hosts de Hyper-V* y *servidores físicos* </br> - **Azure**: utilice este valor si va a instalar el agente en una máquina virtual de IaaS de Azure| VMware </br> Las tablas de Azure|
|-q|Opcional|Especifica el instalador de toorun en modo silencioso| N/D|


#### <a name="mobility-service-configuration-command-line"></a>Línea de comandos de configuración de Mobility Service

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parámetro|Tipo|Descripción|Valores posibles|
|-|-|-|-|
|-i |Obligatorio|Dirección IP del servidor de configuración de Hola|Cualquier dirección IP válida|
|-P |Obligatorio|Archivo de hello de ruta de acceso completa al archivo donde se guarda la frase de contraseña de conexión de Hola|Cualquier carpeta válida|
