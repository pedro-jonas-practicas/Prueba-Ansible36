# Actividad Clase 36

## Primero debemos configurar nuestro controllador como angente de Jenkins.

Que es un agente en Jenkins?

Un agente de Jenkins es un proceso que se ejecuta en un nodo y que realiza tareas en nombre de un controlador de Jenkins. Los agentes permiten a Jenkins ejecutar tareas en paralelo, lo que puede mejorar el rendimiento y la escalabilidad de Jenkins.

Como por ejemplo, podemos configurar un agente en un servidor remoto que ejecute tareas de compilación y pruebas en nombre de un controlador de Jenkins. El agente se conecta al controlador de Jenkins a través de una conexión segura y ejecuta las tareas asignadas por el controlador de Jenkins.

### Esta practica nos va a requerir que nuestro vm controller tenga mas espacio de disco disponible

1. Aumentar el tamaño del disco de la vm controller
   ```bash
    multipass set local.controller.disk=20G
    ```
2. Verificar el tamaño del disco
   ```bash
    multipass info controller
    ```
3. Comprobar el espacio en disco desde el OS.
   ```bash
    df -h
    ```

### Ahora convirtamos nuestro controlador de Ansible en un agente de Jenkins.

1. Instalar Java en el controlador de Ansible
   ```bash
    sudo apt update
    sudo apt install default-jre
    ```
2. Agregar el usuario de Jenkins
   ```bash
    sudo adduser jenkins
    ```
3. Crear directrio de trabajo para Jenkins
   ```bash
    sudo mkdir /var/lib/jenkins
    sudo chown jenkins:jenkins /var/lib/jenkins
    ```
4. Crear ssh key publica y privdada
   ```bash
    sudo su - jenkins
    ssh-keygen
    ```
5. Configurar la clave publica en el controlador de Ansible
   ```bash
    cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
    ```
6. Crear una nueva credencial en el controlador de Jenkins, con el usuario jenkins y la clave privada.
7. Crear un nuevo nodo en Jenkins, con el nombre de nuestro controlador de Ansible.
8. Testear la conexion controlador Jenkins con el Agente.

### Configuremos un Job de Jenkins para que ejecute un playbook de Ansible.

1. Crear un nuevo Job en Jenkins llamado ansible-test
2. Idicar el respositorio de nuestro playbook e indicar el Jenkinsfile-validate
3. Ejecutar el Job y verificar que se ejecute correctamente.

**Importante: recuerda cargar tus credenciales**

Volvamos a la clase y veamos algo un poco mas avanzado.
