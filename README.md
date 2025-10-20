# Hello Tiburona - Smart Contract 

> Implementación de un contrato inteligente en Soroban (Stellar) con manejo de errores, storage organizado, validaciones y control de acceso.

Desarrollado como parte de la **Clase 4**.

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

## 📦 Requisitos previos

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
```


