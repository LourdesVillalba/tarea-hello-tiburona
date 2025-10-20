# Hello Tiburona - Smart Contract 

> Implementación de un contrato inteligente en Soroban (Stellar) con manejo de errores, storage organizado, validaciones y control de acceso.

* Desarrollado como parte de la **Clase 4**.

##  Descripción

**Hello Tiburona** es un contrato inteligente desarrollado en Rust para la blockchain de Stellar usando Soroban SDK. Este proyecto implementa un sistema de saludos con las siguientes características profesionales:

- ✅ Manejo de errores personalizado
- ✅ Storage organizado (Instance y Persistent)
- ✅ Validaciones de entrada
- ✅ Control de acceso con roles de administrador
- ✅ Gestión de TTL (Time To Live)
- ✅ Suite completa de tests

## Características

## Tecnologías

- **Lenguaje**: Rust
- **Blockchain**: Stellar
- **SDK**: Soroban SDK v23.0.3
- **Target**: WebAssembly (wasm32-unknown-unknown / wasm32v1-none)

## Requisitos previos

- Rust (versión estable)
- Soroban CLI / Stellar CLI
- Cargo
- Target WebAssembly instalado

    ```bash
    rustup target add wasm32-unknown-unknown
    rustup target add wasm32v1-none
    ```

##  Instalación

### 1. Clonar o crear el proyecto

```bash
cd ~/proyectos-soroban
stellar contract init hello-tiburona
cd hello-tiburona
```

### 2. Compilar el contrato

```bash
# Usando Soroban CLI
soroban contract build

# O usando Cargo directamente
cargo build --target wasm32-unknown-unknown --release
```

### 3. Ejecutar tests


```
cargo test
```

### 4. Optimizar el WASM (Opcional)

```bash
soroban contract optimize --wasm target/wasm32-unknown-unknown/release/hello_world.wasm
```


##  Estructura del proyecto

```
hello-tiburona/
├── contracts/
│   └── hello-world/
│       ├── src/
│       │   └── lib.rs          # Código principal del contrato
│       └── Cargo.toml
├── Cargo.toml
└── README.md
```

## Tests implementados

| Test                       | Descripción                        |
|----------------------------|------------------------------------|
| `test_initialize`          | Verifica inicialización correcta   |
| `test_no_reinicializar`    | Previene doble inicialización      |
| `test_hello_exitoso`       | Verifica funcionamiento del saludo |
| `test_nombre_vacio`        | Valida que el nombre no esté vacío |
| `test_reset_solo_admin`    | Admin puede resetear contador      |
| `test_reset_no_autorizado` | Usuario normal no puede resetear   |

## Captura de test
<img width="942" height="291" alt="captura_test" src="https://github.com/user-attachments/assets/9b3aaa07-2101-46f8-b625-ac79808ffb56" />


## Reflexion
* **¿Qué fue lo más retador?**

Lo más retador fue entender las diferencias entre versiones del SDK de Soroban. Al principio seguí la guía tal cual, pero me encontré con errores de compilación porque Address::generate() no funcionaba y los tests fallaban. Tuve que adaptar el código, cambiando:

register_contract() por register()

Ajustando los should_panic para buscar "Error(Contract, #N)" en lugar del nombre del error

También fue desafiante entender por qué usar String en lugar de Symbol para el parámetro nombre.

* **¿Qué aprendiste que no esperabas?**

 Los tests son MUY importantes en blockchain. No son opcionales. Cuando estás manejando dinero real o datos críticos, cada función debe tener tests que verifiquen tanto casos exitosos como casos de error.
 
* **¿Qué aplicarías en tus propios proyectos?**

Definitivamente voy a aplicar:

El patrón de validaciones tempranas (early returns): Validar inputs antes de tocar el storage es más eficiente y previene estados inconsistentes.

Storage organizado con enums: Usar DataKey enum en lugar de strings hardcodeados hace el código mucho más mantenible y previene bugs de typos.

Control de acceso desde el inicio: Implementar roles y permisos desde el día uno, no como "lo agregamos después". La seguridad debe ser parte del diseño, no un parche.

Tests comprehensivos: Para cada función pública, escribir al menos 2 tests: uno de caso exitoso y uno de caso de error. Es la única forma de estar seguro de que el contrato funciona como debe.





