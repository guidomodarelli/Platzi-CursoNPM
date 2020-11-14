# Curso de Gestión de Dependencias y Paquetes con NPM

Iniciar un proyecto en npm con licencia MIT de forma automatica

```bash
  npm set init.license "MIT"
  npm <command> --dd # mostrar los comandos ejecutados internamente por npm
```

![image](./docs/notas.webp)

Puedes también especificar scripts con el prefijo "pre" que se ejecutarán automáticamente antes del comando que ejecutaste. Por ejemplo, si defines el comando build y prebuild, cuando corras npm run build el comando prebuild se ejecutará primero. Esto sirbe para poder ejecutar tareas que hagan algún tipo de preparación necesaria para correr el comando principal. Sin embargo, hay que hacer notar que si el comando pre falla (retorna un valor que no es 0) el comando principal no se ejecutará. Esto es algo bueno ya que si nuestro proceso de preparación no se realiza de forma exitosa, puede que tengamos problemas al querer ejecutar la tarea principal.

En algunas ocaciones, sin embargo, la tarea previa puede fallar sin que eso afecte la ejecución de la tarea principal. En esos casos puedes usar || exit 0 para retornar 0:

```json
  "presass-build": "(rm css/*.css; rm css/*.css.map) || exit 0"
```

Ese es un ejemplo de un comando que hice hace un tiempo. rm puede fallar si el directorio css está vacio, y en ese caso no hay problema, la tarea principal puede funcionar sin ningún problema ya que presass-build tiene el propósito de vaciar ese directorio.

**NOTA**: Puedes también especificar scripts con el prefijo "post" que se ejecutarán automáticamente antes del comando que ejecutaste

- En caso de que nuestros archivos de node_module no estén bien instalados o tengamos una versión anterior lo que podemos hacer es lo siguiente:

```bash
npm cache clear --force
#Para verificar que verdaderamente se borro podemos usar
npm cache verify
```

- Uno de los errores que podemos tener es tener algún valor corrupto en node_module, o tambien que la instalación no este completa de los paquetes que hemos instalado, para ello podemos eliminar el paquete con el siguiente comando:

```bash
rm -rf node_modules  #este comando eliminar la carpeta
```

- Otra alternativa para eliminar de forma segura una carpeta es instalando el siguiente paquete:

```bash
sudo npm install -g rimraf
```

- Ahora podemos ejecutar el siguiente comando para eliminar node_module

```bash
rimraf node_modules
#Ahora podemos volver a instalar nuestro paquetes
npm install
```

## Carpeta de configuración

Se crea la carpeta bin/, con el archivo global.js para incluir la configuracion de nuestro proyecto.

Para asegurarse de ejecutar archivos como javascript

```bash
#!/usr/bin/env node
```

En `packaje.json`, creamos el apartado

```jsonc
    "bin": {
    "random-msg": "./bin/global.js"
  },
  "preferGlobal": true
```
