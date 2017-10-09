Cada equipo cliente que se conecta tooa red virtual con punto a sitio debe tener instalado un certificado de cliente. certificado de cliente de Hola se genera a partir de certificado de raíz de Hola e instalado en cada equipo cliente. Si no está instalado un certificado de cliente válido y cliente de hello intenta tooconnect toohello red virtual, se produce un error en la autenticación.

Puede generar un certificado único para cada cliente, o puede usar Hola mismo certificado para varios clientes. certificados de cliente único de Hello ventaja toogenerating es Hola capacidad toorevoke un certificado único. En caso contrario, si varios clientes están utilizando Hola el mismo certificado de cliente y necesita toorevoke, también tiene toogenerate e instalar nuevos certificados para todos los clientes que usan ese certificado tooauthenticate de Hola.

Puede generar certificados de cliente mediante Hola siguientes métodos:

- **Certificado de empresa:**

  - Si está utilizando una solución de certificado de empresa, generar un certificado de cliente con formato del valor de nombre común de hello 'name@yourdomain.com', en lugar de formato de hello 'dominio ombre de usuario'.
  - Asegúrese de que el certificado de cliente de Hola se basa en la plantilla de certificado de hello 'User' que tiene 'Autenticación de cliente' como primer elemento en la lista de uso de Hola de hello, en lugar de inicio de sesión de tarjeta, etcetera de Smart. Puede comprobar el certificado de hello si hace doble clic en el certificado de cliente de Hola y se visualiza **detalles > uso mejorado de clave**.

- **Certificado raíz autofirmado:** es importante que siga los pasos de hello en uno de los siguientes artículos de certificado de hello P2S. En caso contrario, los certificados de cliente hello que crea no son compatibles con conexiones de P2S y los clientes reciben un error al tratar de tooconnect. pasos de Hello en cualquiera de los siguientes artículos de hello generan un certificado de cliente compatible con: 

  * [Windows PowerShell de 10 instrucciones](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): estas instrucciones requieren certificados toogenerate PowerShell y Windows 10. certificados de Hello generados pueden instalarse en cualquier cliente P2S compatible.
  * [Instrucciones de MakeCert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): Use MakeCert si no tienes acceso tooa Windows 10 equipo toouse toogenerate certificados. MakeCert en desuso, pero todavía puede usar MakeCert toogenerate certificados. certificados de Hello generados pueden instalarse en cualquier cliente P2S compatible.

  Cuando genere un certificado de cliente de un certificado raíz autofirmado mediante Hola anteriores instrucciones, instala automáticamente en hello equipo que usa toogenerate se. Si desea tooinstall un certificado de cliente en otro equipo cliente, necesita tooexport como un .pfx, junto con la cadena de certificados completa de Hola. Esto crea un archivo .pfx que contiene la información del certificado de raíz de Hola que se necesita para autenticar Hola cliente toosuccessfully. Para pasos tooexport un certificado, consulte [certificados: exportar un certificado de cliente](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
