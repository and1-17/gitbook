# 🥷 Metasploitable 2

Metasploitable 2 es un sistema Ubuntu diseñado con vulnerabilidades, de manera intencional, para que estas sean explotadas y aprender el uso de Metasploit como herramienta de trabajo y todas sus funcionalidades. El equipo de Rapid 7 tienen en su [web las guias de descarga](https://docs.rapid7.com/metasploit/metasploitable-2)  para el SO  . En esta web enseñan guias tanto de uso, instalación y explotación de Metasploitable 2, las cuales se recomiendan ser consultadas ante cualquier duda. Es recomendable instalar Metasploitable 2 en una Máquina Virtual, ya sea VMware, Virtual Box o cualquier software de virtualización, para no comprometer ningún equipo físico y facilitar el trabajo de estudio de Metasploit. Para descargar Metasploitable 2 puedes [usar este enlace](https://sourceforge.net/projects/metasploitable/).&#x20;

{% hint style="info" %}
Recuerda que puedes explotar estas vulnerabilidades con Metasploit o directamente con las herramientas y exploits de manera manual. La recomendación para comenzar a trabajar y entender "que estás haciendo" es ejecutar de manera sencilla con Metasploit y posteriormente estudiar el trabajo por detrás de la herramienta con reportes de otros compañeros o los informes de los CVEs. Pero realizar todo de manera automátizada sin entenderlo no te ayudará a avanzar.
{% endhint %}

### Instalación de Metasploitable2 en VMware

En este apartado vamos a generar una máquina virtual Metasploitable 2 en VMware para poder realizar pruebas con Metasploit dirigidas a esta máquina y así facilitarnos el estudio. Para ello vamos a acudir al recurso oficial en [SourceForge ](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/). Pulsaremos “Download Latest Version” en la página, esto hará esperar 5 segundos y se descargará un archivo .zip con Metasploitable 2.

<figure><img src="../../.gitbook/assets/10 (8).png" alt=""><figcaption></figcaption></figure>

Una vez lo descargamos debemos descomprimirlo. Y al descomprimirlo pulsaremos sobre “Open a Virtual Machine” y seleccionaremos el archivo Metasploitable.vmx para configurar la mágica.&#x20;

<figure><img src="../../.gitbook/assets/11 (7).png" alt=""><figcaption></figcaption></figure>

Al abrir el archivo nos cargará la máquina virtual en VMware con la configuración por defecto de la máquina virtual. Y podremos modificar los parámetros que creamos convenientes.

<figure><img src="../../.gitbook/assets/12 (6).png" alt=""><figcaption></figcaption></figure>

Al iniciar la máquina aparecerá una pantalla en la terminal en la que habrá que iniciar sesión. La contraseña por defecto y el usuario es msfadmin y viene descrito en el inicio del sistema.

<figure><img src="../../.gitbook/assets/13 (2).png" alt=""><figcaption></figcaption></figure>

Según iniciamos le sistema aparecerá la siguiente pantalla y ya podremos trabajar con la misma.

<figure><img src="../../.gitbook/assets/14 (4).png" alt=""><figcaption></figcaption></figure>



