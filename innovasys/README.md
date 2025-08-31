# Actividad 12 Configuración Automática de Servidores con Ansible
Este proyecto de Ansible es para automatizar la configuración de servidores Ubuntu 24.04.

## Roles y Funcionalidades
   El playbook configurara dos tipos de servicios:
   
   ### 1. Apache2: Despliega un servidor web de intranet con una página de bienvenida personalizada.
   
   1.1. El rol de Apache2 se encarga de instalar y configurar el servidor web.
   
   1.2. Instalación: El playbook utiliza el módulo apt para asegurar que el paquete apache2 esté instalado y actualizado en el sistema.
   
   1.3. Despliegue de la página: Un archivo de plantilla (templates/index.html.j2) se copiara a la ruta /var/www/html/index.html del ubuntu server.
   
   1.4. Estado del servicio: El playbook verifica que el servicio de Apache esté activo.

   1.5. Un handler (handlers/main.yml) se encarga de reiniciar el servicio de Apache si el archivo de configuración cambia.
   
   ### 2. Samba: Crea una carpeta compartida (/srv/samba/proyectos) con acceso restringido para el usuario devuser1.

   2.1. El rol de Samba automatiza la creación de un punto de acceso compartido para un equipo de desarrollo.
   
   2.2. Instala el paquete samba y crea un nuevo grupo (desarrolladores).
   
   2.3. Crea un usuario del sistema (devuser1) y lo añade al grupo desarrolladores para la autenticación de Samba.
   
   2.4. Crea el directorio /srv/samba/proyectos para los archivos del proyecto.
   
   2.5. Establece los permisos para que el grupo desarrolladores tenga acceso.
   
   2.6. Configura la contraseña de Samba para el usuario devuser1 (innova.2025).
   
   2.7. Utiliza la plantilla smb.conf.j2 para configurar el archivo principal de Samba (/etc/samba/smb.conf). Esto define la carpeta compartida [Proyectos], permitiendo el acceso solo a los usuarios del grupo desarrolladores.
   
   2.8. Se asegura de que el servicio de Samba (smbd) esté corriendo.
   
   2.9. Un handler (handlers/main.yml) se encarga de reiniciar el servicio de Samba si el archivo de configuración cambia.

## Ajustes del proyecto

   1. Modificar el archivo servidores con la ip y usuario para realizar el ssh:
      ```bash
      [innovasys]
      servidor-innovasys ansible_host=192.168.10.100 ansible_user=operador
   
   2. Clona el repositorio:
      ```bash
      git clone https://github.com/1Guardian10/Actividad-Nro-12.git
      cd Actividad-Nro-12
   
   3. Ejecuta el playbook:
      ```bash
      ansible-playbook -i servidores playbook.yml
