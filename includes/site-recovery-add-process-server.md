1. Iniciar hello Azure sitio recuperación UnifiedSetup.exe
2. En **antes de comenzar**, seleccione **agregar tooscale de servidores de proceso adicionales horizontalmente la implementación**.

  ![Agregar servidores de procesos](./media/site-recovery-add-process-server/ps-page-1.png)

3. En **detalles del servidor de configuración**, especifique la dirección IP de Hola de servidor de configuración de hello y Hola frase de contraseña.

  ![Agregar servidores de procesos 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. En **configuración de Internet**, especifique cómo proveedor se ejecuta en el servidor de configuración de Hola conecta tooAzure Site Recovery a través de Hola Hola Internet.

  ![Agregar servidores de procesos 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Seleccione si desea tooconnect con proxy de Hola que actualmente está configurado en el equipo de hello, **conectar con la configuración de proxy existente**.
   * Si desea Hola proveedor tooconnect directamente, seleccione **conectar directamente sin proxy**.
   * Si Hola existente proxy requiere autenticación, o si desea toouse un proxy personalizado para la conexión del proveedor de hello, seleccione **conectar con la configuración de proxy personalizada**.

     * Si usa a un proxy personalizado, necesita las credenciales, el puerto y dirección de hello toospecify.
     * Si usa a un servidor proxy, debe haya permitido ya direcciones URL del servicio de acceso toohello.

5. En **comprobación de requisitos previos**, el programa de instalación ejecuta un toomake de comprobación confirma que puede ejecutar la instalación. Si aparece una advertencia acerca de hello **comprobación de la sincronización de hora Global**, comprobar esa hora Hola de reloj del sistema hello (**fecha y hora** configuración) Hola igual como zona de horaria Hola.

     ![Agregar servidores de procesos 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. En **detalles del entorno**, seleccione si se va a máquinas virtuales de VMware tooreplicate. Si realiza la configuración, compruebe si PowerCLI 6.0 está instalado.

     ![Agregar servidores de procesos 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. En **ubicación de instalación**, seleccione si desea que los archivos binarios de tooinstall hello y almacenar en memoria caché de Hola. unidad de Hola que seleccione debe tener al menos 5 GB de espacio en disco disponible, pero se recomienda una unidad de memoria caché con un mínimo de 600 GB de espacio libre.
     ![Agregar servidores de procesos 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. En **selección de red**, especifique el agente de escucha de hello (adaptador de red y el puerto SSL) en qué servidor de configuración, Hola envía y recibe datos de replicación. 9443 Hola puerto predeterminado es usado para enviar y recibir tráfico de replicación, pero puede modificar este toosuit de número de puerto de los requisitos de su entorno. En el puerto de suma toohello 9443, también se abra el puerto 443, que es utilizado por una operación de replicación de web server tooorchestrate. No use el puerto 443 para enviar o recibir tráfico de replicación.

     ![Agregar servidores de procesos 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. En **resumen**, revise la información de Hola y haga clic en **instalar**. Se genera una frase de contraseña cuando finaliza la instalación. La necesitará al habilitar la replicación, así que cópiela y manténgala en una ubicación segura.

     ![Agregar servidores de procesos 7](./media/site-recovery-add-process-server/ps-page-8.png)
