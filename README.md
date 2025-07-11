# Replicant fullstack Template

Este proyecto es un template para crear proyectos fullstack preparado para integrar en un pipeline CI/CD

Se cuenta con el siguiente Stack. En el backend:

1. Pathom
2. Ring
3. Next-JDBC
4. Donut-system

Y para el frontend:

1. Replicant
2. Tailwind
3. DaisyUI

## Uso

Para crear un template a partir de este proyecto debes instalar [deps-new](https://github.com/seancorfield/deps-new?tab=readme-ov-file) en tus herramientas de Clojure CLI. 

Luego, en la línea de comandos ejecuta:

```bash
clojure -Sdeps '{:deps {io.github.sanatoriocolegiales/deps-new-fullstack-replicant-template {:git/tag "v0.0.1" :git/sha "a28266"}}}' -Tnew create :template sanatoriocolegiales/deps-new-fullstack-replicant-template :name sanatoriocolegiales/<mi-proyecto>
```

O en su defecto utilizar el último sha tomado de los commits:

```bash
clojure -Sdeps '{:deps {io.github.sanatoriocolegiales/deps-new-fullstack-replicant-template {:git/sha "CODIGO-SHA"}}}' -Tnew create :template sanatoriocolegiales/deps-new-fullstack-replicant-template :name sanatoriocolegiales/<mi-proyecto>
```

## Desarrollo

Antes de iniciar revisa tu archivo config.edn y setea todo lo que sea necesario para que el backend arranque correctamente. En especial la variable de entorno CREDENTIALS tiene que apuntar a un archivo .edn con las llaves que se especifican más abajo. Igual todo se puede cambiar a conveniencia. También vas a necesitar el .jar de Relativity en la carpeta *resources* o puedes retirarlo del deps.edn si lo prefieres. 

Para iniciar tu entorno de desarrollo en el root del proyecto teclea:

```bash
bb dev
```
Esto instalará las dependencias de node, iniciará un proceso de vigilancia de tailwind y de shadow con los perfiles app-dev y portfolio. Adicionalmente se lanzará una ventana de [Portal](https://github.com/djblue/portal) que puedes configurar a voluntad en dev/user.clj 

En el archivo mise.toml se encuentran las dependencias necesarias para el entorno, por lo que es necesario tener (mise-en-place)[https://mise.jdx.dev/] instalado y activado. 

Una vez que el proceso indique que se han compilado los perfiles *app-dev* y *portfolio*, conectarse a VSCode eligiendo la opción "Connect to a running REPL in your project". Elegir el puerto 9500 y luego el perfil *app-dev*.

### Portfolio

Este proyecto cuenta con [Portfolio](https://github.com/cjohansen/portfolio?tab=readme-ov-file) para asistir en el desarrollo de la UI. Los archivos necesarios se levantan en un build aparte y se usa el http server de shadow-cljs. Revisar la documentación.

## Tests

Para ejecutar los tests correr:

```bash
bb tests
```

## Tests de aceptación

Existe un directorio aparte configurado para ejecutar los tests de aceptación apuntado al puerto 4500 (donde se espera que la aplicación de producción se ejecute). Para correr los tests de aceptación:

```bash
bb acc-tests
```

## Crear Release Candidate

Llegado el momento de desplegar ejecutar:

```bash
bb release
```

Este comando corre los tests unitarios, compila el jar, crea una imagen de Docker con el jar y corre el contenedor. Para realizar cualquier prueba estos comandos se pueden correr por separados. Ejecute lo siguiente para poder ver las opciones disponibles:

```bash
bb tasks
```