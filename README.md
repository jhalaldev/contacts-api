# Contacts API

[![tests](https://github.com/USUARIO/taskflow-api/actions/workflows/tests.yml/badge.svg)](https://github.com/USUARIO/taskflow-api/actions/workflows/tests.yml)
![PHP](https://img.shields.io/badge/PHP-8.3-777BB4)
![Laravel](https://img.shields.io/badge/Laravel-13-FF2D20)
![Licencia](https://img.shields.io/badge/licencia-MIT-blue)

API REST para gestionar contactos, con autenticación mediante Laravel Sanctum.

## Contenido
- [Tecnologías](#tecnologías)
- [Instalación](#instalación)
- [Pruebas](#pruebas)
- [Endpoints](#endpoints)
- [Flujo de trabajo](#flujo-de-trabajo)
- [Licencia](#licencia)

## Tecnologías
PHP 8.3, Laravel 13, MySQL 8, Laravel Sanctum, Pest, Scramble.

## Requisitos
PHP 8.3+, Composer 2, MySQL 8, Git.

## Instalación
```bash
git clone https://github.com/jhalaldev/contacts-api.git
cd contacts-api
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
```
## Modelo de datos

Diagrama entidad-relación: [docs/er.md](docs/er.md)

## Datos de prueba

```bash
php artisan migrate:fresh --seed
```

Crea el usuario de prueba `test@example.com` (contraseña `password`), diez usuarios
aleatorios y tres contactos para cada uno de los primeros diez usuarios, para desarrollo local.

## Variables de entorno
| Variable    | Ejemplo        | Descripción             |
|-------------|----------------|-------------------------|
| DB_DATABASE | db_taskflow_api       | Base de datos MySQL     |
| DB_PREFIX   | a07_           | Prefijo de las tablas   |

## Pruebas
```bash
php artisan test
```

## Documentación de la API
Con el servidor local: http://127.0.0.1:8000/docs/api

## Endpoints

| Método | Ruta                 | Descripción                       | Auth   |
|--------|----------------------|-----------------------------------|--------|
| GET    | /api/v1/health       | Estado del servicio               | No     |
| POST   | /api/v1/auth/login   | Inicia sesión y entrega un token  | No     |
| GET    | /api/v1/auth/me      | Perfil del usuario autenticado    | Bearer |
| POST   | /api/v1/auth/logout  | Cierra sesión y revoca el token   | Bearer |
| GET    | /api/v1/contacts     | Lista los contactos del usuario   | Bearer |
| POST   | /api/v1/contacts     | Crea un contacto                  | Bearer |
| GET    | /api/v1/contacts/{id}| Consulta un contacto propio       | Bearer |
| PUT/PATCH | /api/v1/contacts/{id} | Actualiza un contacto propio   | Bearer |
| DELETE | /api/v1/contacts/{id}| Elimina un contacto propio        | Bearer |

## Autenticación

1. POST /api/v1/auth/login con email, password y device_name.
2. Guardar el token de la respuesta.
3. Enviar en cada petición protegida:
   Authorization: Bearer {token}
   Accept: application/json

El login admite 5 intentos por minuto por correo e IP.

## Flujo de trabajo
Git Flow (main, develop, feature/*, release/*, hotfix/*),
Conventional Commits y versionado semántico.
Los cambios se registran en CHANGELOG.md.

## Autor
Addu Nuñez

## Licencia
Distribuido bajo la licencia MIT. Ver LICENSE.md.
