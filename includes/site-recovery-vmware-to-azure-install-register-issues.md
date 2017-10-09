
### <a name="installation-failures"></a>Errores de instalación
| **Ejemplo de mensaje de error** | **Acción recomendada** |
|--------------------------|------------------------|
|ERROR no se pudo tooload cuentas. Error: System.IO.IOException: conexión de transporte de datos de no se puede tooread de hello al instalar y registrar Hola servidor CS.| Asegúrese de que TLS 1.0 está habilitado en el equipo de Hola. |

### <a name="registration-failures"></a>Errores de registro
Se pueden depurar errores de registro si examina los registros de Hola Hola **%ProgramData%\ASRLogs** carpeta.

| **Ejemplo de mensaje de error** | **Acción recomendada** |
|--------------------------|------------------------|
|**09:20:06**:InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>Mensaje: ACS50008: SAML token is invalid (el token SAML no es válido).<br>Id. de seguimiento: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>Id. de correlación: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>Marca de tiempo: **2016-12-12 14:50:08Z<br>** | Asegúrese de que hello en el reloj del sistema no es más de 15 minutos Hola local tiempo de inactividad. Vuelva a ejecutar el registro de hello instalador toocomplete Hola.|
|**09:35:27** : DRRegistrationException al intentar tooget todos los almacén de recuperación ante desastres para el certificado seleccionado hello:: Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException produjo, Exception.Message: ACS50008: Token SAML no es válido.<br>Id. de seguimiento: e5ad1af1-2d39-4970-8eef-096e325c9950<br>Id. de correlación: abe9deb8-3e64-464d-8375-36db9816427a<br>Marca de tiempo: **2016-05-19 01:35:39Z**<br> | Asegúrese de que hello en el reloj del sistema no es más de 15 minutos Hola local tiempo de inactividad. Vuelva a ejecutar el registro de hello instalador toocomplete Hola.|
|06:28:45: error toocreate certificado<br>06:28:45:Setup cannot proceed (el programa de instalación no puede proseguir). TooSite tooauthenticate que no se puede crear la recuperación requiere un certificado. Vuelva a ejecutar el programa de instalación | Asegúrese de que ejecuta el programa de instalación como un administrador local. |
