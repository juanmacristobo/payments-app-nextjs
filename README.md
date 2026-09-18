# Payments App — Groovy Music Store

Módulo de pagos de un marketplace de música física. Esta aplicación gestiona el ciclo de vida de los pagos: inicia el checkout con Mercado Pago, registra transacciones, administra la acreditación de fondos a vendedores y permite gestionar reembolsos y reclamos.

Forma parte de un ecosistema compuesto por cuatro aplicaciones independientes que se comunican mediante APIs.

**Deploy:** **[Payments App - Groovy Music Store](https://proyecto-c-payments-groovy-music-st.vercel.app/)**

## Mi Rol y Desarrollo

Fui responsable del diseño, implementación y despliegue de extremo a extremo de esta **Payments App**. Mi objetivo fue desarrollar el módulo encargado de gestionar el dominio de pagos y su integración con el resto de las aplicaciones del sistema:

* **Procesamiento de Pagos:** integración con **Mercado Pago Checkout Pro** para iniciar y gestionar el flujo de pagos mediante el entorno Sandbox.
* **Gestión de Transacciones:** implementación de la lógica para registrar pagos, consultar su estado y administrar el ciclo de vida de las transacciones.
* **Acreditación de Fondos:** gestión de los fondos correspondientes a los vendedores, incluyendo la liberación posterior a la confirmación de entrega.
* **Reembolsos y Reclamos:** implementación de funcionalidades para gestionar reembolsos y administrar información relacionada con reclamos.
* **Integración entre Servicios:** comunicación mediante APIs REST con las aplicaciones **Buyer, Seller, Shipping, Control Plane y Analytics**.
* **Webhook de Mercado Pago:** recepción y procesamiento de notificaciones relacionadas con los pagos.
* **Panel de Administración:** desarrollo de un panel propio para la gestión y consulta de información del módulo de pagos.

## Stack Tecnológico

* **Framework:** Next.js (App Router)
* **Lenguaje:** TypeScript
* **Estilos:** Tailwind CSS
* **Base de Datos:** PostgreSQL (Neon)
* **ORM:** Prisma 6
* **Autenticación:** Clerk
* **Pagos:** Mercado Pago Checkout Pro (Sandbox)
* **Despliegue:** Vercel

## Cómo probar

El flujo de pago se inicia desde la **Buyer App** y continúa en el checkout de Mercado Pago utilizando el entorno Sandbox.

**Buyer App:** **[Buyer App - Groovy Music Store](https://proyecto-c-buyer2-groovy-music-store.vercel.app/)**

### Acceso al panel de administración

<details>
  
<summary>Credenciales de prueba</summary>

Usuario: `adminpayments`
Contraseña: `adminpayments`

</details>

### Datos de prueba de Mercado Pago

<details>
  
<summary>Credenciales del comprador y tarjeta de prueba</summary>

**Comprador de test**

`TESTUSER7971489035181850335`

Código: `965242`

**Tarjeta**

* Número: `4002 7686 9439 5619`
* Nombre: `APRO`
* CVV: `123`
* Vencimiento: `11/30`
* DNI: `12345678`

</details>

## Endpoints

<details>
  
<summary>Endpoints de la aplicación</summary>

La aplicación expone endpoints REST consumidos por las distintas aplicaciones del ecosistema y endpoints internos utilizados para la integración con Mercado Pago.

</details>

## Configuración local

El repositorio incluye un `.env.example` con las variables necesarias para configurar Clerk, PostgreSQL, Mercado Pago y la URL de la aplicación.
