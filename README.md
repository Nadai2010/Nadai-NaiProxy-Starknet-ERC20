<div align="center">
    <img src="./Imagenes/Starknet.png" style="width: 300px">
    <h1>Nadai Token NaiProxy ERC20</h1>

[![StarkWare](https://img.shields.io/badge/powered_by-StarkWare-navy?style=for-the-badge&flat&logo=Starkware)](https://starkware.co/)
[![Cairo](https://img.shields.io/badge/-%F0%9F%90%AB%20%20Cairo-red?style=for-the-badge&flat&logo=Cairo)](https://www.cairo-lang.org/)
[![Protostar](https://img.shields.io/badge/-%E2%9C%A8PROTOSTAR-blue?style=for-the-badge&flat&logo=Protostar)](https://docs.swmansion.com/protostar/)
</div>

## Nadai Token ERC20 con Proxy en Starknet

En este tutorial aprenderemos a crear un token ERC20 con PROXY . El `NaiProxy` estará en `Cairo` y lanzado en Starknet Goerli. 

## Ajustes de entorno

Antes de empezar asegurese de tener instalado [Protostar](https://github.com/Nadai2010/Nadai-ERC721-Protostar-Cairo#instalaci%C3%B3n)

Debemos instalar las librerias de OpenZeppelin usando el comando

```bash
gh repo clone OpenZeppelin/cairo-contracts
```

## Creación de NaiProxy en Cairo

* Puedes usar esta implementación como base del Smart [NaiProxy](https://github.com/Nadai2010/Nadai-NaiProxy-Starknet-ERC20/blob/master/src/NaiProxy.cairo)

* Puede crear su propia implementación de ERC20 en Cairo herramienta de OpenZeppelin [Wizard](https://wizard.openzeppelin.com/cairo#erc20)

Empezaremos el proyecto con la herramienta Protostar, que creará directamente el archivo `protostar.toml` y ajustes necesarios usando el siguiente comando.

```bash
protostar init
```

Luego cambiaremos el nombre del contrato en el archivo `protostar.toml` en el que indicaremos el nombre y ruta para hacer el compile.

![Graph](/Imagenes/toml.png)

Ahora realizaremos el `build`. Esto nos creará dos archivos `.json` dentro de la carpeta `build`. Si da error revisar que la carpeta y ruta sea la correcta. Luego procedermos hacer el `deploy`, en el cual no se le deberá pasar ningun argumento. Tener en cuenta que si no tienen error, el `DEPLOY` puede tardar más de `1 HORA-PACIENCIA`.

```bash
protostar build
```

![Graph](/Imagenes/build.png)


```bash
protostar deploy ./build/NaiProxy.json --network alpha-goerli
```

![Graph](/Imagenes/deploy.png)

* [HASH](https://goerli.voyager.online/contract/0x04f1677490ac748f53e3972ab95a4dd61f54b079b57598bf6c108dabb42e6e9d)

---

### Mint de NaiProxy Token

Usaremos la herramienta [stark-utils](https://www.stark-utils.xyz/converter) para pasar `hex` a `felt`, que aunque en este caso no hace falta, aprenderemos a usarla.

Luego iremos al contract que hemos creado [NaiProxy](https://goerli.voyager.online/contract/0x04f1677490ac748f53e3972ab95a4dd61f54b079b57598bf6c108dabb42e6e9d#writeContract) en Voyaguer o Starkscan y en `write contract` pasaremos al `initializer` el felt que acabamos de conseguir. Aquí podremos decir quien será el `owner`, quien recibirá con `recipient` y quien será el `proxy_admin`, en este caso es el mismo para los 3.

* [HASH](https://goerli.voyager.online/tx/0x23b57abcfd2bf38ab1686d6a9babad52ce9377f572459759d65570b6d28a2b2)

![Graph](/Imagenes/ini.png)


Ahora que ya se ha realizado el `initializer` podremos ver el nombre del token, simbolo, supply, quien es el dueño y admin de contract...

![Graph](/Imagenes/nombre.png)
![Graph](/Imagenes/supply.png)
![Graph](/Imagenes/owner.png)



## Conclusión

Al tener proxy activado podremos actualizarlo con `CAIRO 1.0` llegado el momento, o esa es la idea de este tutorial.
