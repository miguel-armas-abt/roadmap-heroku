# CONTENEDORES CON HEROKU

[← Regresar a notas](../../README.md) <br>

----

> 💵 Heroku eliminó los dynos gratuitos en 2022, por lo que cualquier despliegue (ya sea via contenedores o via git push) genera un coste.

### Instrucciones:

- Crear una cuenta en Heroku.

- Ir al perfil y seleccionar `Account Settings`.

- Seleccionar el tab `Billing` y añadir una tarjeta como método de pago. (Tener almenos 2$).

- Ubicar la sección `Api Key`, dar clic en el botón `Reveal` y resguardar la credencial.

> ⚙️ Instalar Heroku CLI
> ```shell
> choco install heroku-cli
> ```

> 🔓 Abrir una sesión de GitBash y exportar las siguientes variables
> ```shell
> export HEROKU_API_KEY="HEROKU_API_KEY"
> export HEROKU_EMAIL="<EMAIL>"
> ```

> 🔎 Verificar sesión
> ```shell
> heroku whoami
> ```

> ⚙️ Crear app
> ```shell
> heroku create repository-finder
> ```

> 🔎 Consultar apps
> ```shell
> heroku apps
> heroku apps:info
> ```

> 🗑️ Eliminar app *(Detiene el consumo)*
> ```shell
> heroku apps:destroy --app repository-finder --confirm repository-finder
> ```

> 🔑 Login al Container Registry de Heroku *(Requiere Docker iniciado)*
> ```shell
> heroku container:login
> ```

> 🏷️ Etiquetar imagen para heroku *(El tag de destino será `web`)*
> ```shell
> docker tag miguelarmasabt/repository-finder:v1.0.1 registry.heroku.com/repository-finder/web
> ```

> ⬆️ Empujar imagen a Heroku
> ```shell
> docker push registry.heroku.com/repository-finder/web
> ```

> 🔧 Mover la app al stack de contenedores
> ```shell
> heroku stack:set container --app repository-finder
> ```

> 📦 Generar release para producción (deploy)
> ```shell
> heroku container:release web --app repository-finder
> ```

> 🔎 Ver logs del contenedor
> ```shell
> heroku logs --tail --app repository-finder
> ```

> 📋 Establecer variables de entorno:
> ```shell
> heroku config:set PASSWORD='fake_password'
> ```
> Si el valor tiene caracteres extraños, mejor añadir las variables desde el [dashboard de Heroku](https://dashboard.heroku.com/apps)<br> 
> `Settings` → `Config Vars` → `Reveal Config Vars`

> 🔎 Ver variables de entorno
> ```shell
> heroku config --app repository-finder
> ```

> 📦 Escalar réplicas
> - Escalar a 0 detiene el consumo
> ```shell
> heroku ps:scale web=1 --app repository-finder
> ```

📌 Si necesitas realizar cambios, repite `push`/`release`
