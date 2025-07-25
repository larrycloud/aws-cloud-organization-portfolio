# 🌩️ AWS Cloud Organization

Este repositorio documenta la creación de una **organización real en AWS**, implementada completamente desde la consola. El objetivo es demostrar conocimientos en buenas prácticas de gobernanza cloud, separación de entornos y administración de múltiples cuentas en un entorno corporativo simulado.

---

## 🎯 Objetivo

Diseñar una arquitectura organizacional en AWS que refleje una estructura empresarial escalable con:

- Separación de entornos (`DEV`, `TEST`, `PROD`, `SECURITY`)
- Control centralizado de facturación
- Jerarquía clara basada en cuentas
- Roles delegados entre cuentas (`OrganizationAccountAccessRole`)
- Documentación visual completa y real
- Preparación para evolucionar hacia **Terraform (IaC)**

---

## 🧰 Tecnologías y herramientas utilizadas

- **Consola de AWS**
- **AWS Organizations**
- **AWS Billing & Cost Explorer**
- **Cambio de rol IAM entre cuentas (`OrganizationAccountAccessRole`)**
- **Draw.io** (para el diagrama de arquitectura)
- **Capturas de pantalla reales** desde la consola AWS

---

## 🧱 Estructura de la organización

```text
Root
├── DEV
│   └── AWS-DEVELOPMENT
├── PROD
│   └── AWS-PROD
├── TEST
│   └── AWS-TEST
├── SECURITY
│   └── AWS-SECURITY
└── AWS-GENERAL (Cuenta de administración)
```

📅 **Fechas de creación:**

- Cuentas DEV y PROD: 19/10/2024  
- Cuenta TEST: 19/04/2025  
- Cuenta SECURITY: 23/07/2025 (agregada desde cuenta existente)

---

## 🖼️ Diagrama de arquitectura

📂 Ver imagen:  
![Diagrama](architecture/aws-org-diagram.png)

Representa gráficamente la jerarquía OU y las cuentas asociadas a cada entorno, creada en Draw.io.

---

## 📸 Capturas y documentación visual

Capturas reales tomadas desde la consola AWS:  

📁 Ubicación: `docs/screenshots/`

Algunas incluyen:

- Jerarquía en AWS Organizations  
  ![Jerarquía](docs/screenshots/general/Jerarquía-en-AWS-Organizations.png)

- Configuración de facturación centralizada  
  ![Facturación](docs/screenshots/general/Facturacion-unificada.png)

- Consola Cost Explorer mostrando consolidación  
  ![Cost Explorer](docs/screenshots/general/cost-explorer.png)
  
- Proceso visual para agregar cuenta existente a la organización  
- Cambio de rol IAM entre cuentas

---

### ✅ Integración de cuenta SECURITY (paso a paso visual)

Se muestra el proceso completo y real de integración de una cuenta AWS existente (`AWS-SECURITY`) dentro de una Organización.

📁 Carpeta: `docs/screenshots/aws-security-account-onboarding/`

---

### 🔖 Pasos documentados:

1. **Enviar invitación desde AWS-GENERAL**  
   ![Enviar invitación](docs/screenshots/aws-security-account-onboarding/01-Enviar-invitacion-IAM-larry-(security).png)

2. **Revisar invitación**  
   ![Revisar invitación](docs/screenshots/aws-security-account-onboarding/02-Revisar-invitacion-IAM-Larry-security.png)

3. **Aceptar invitación desde SECURITY**  
   ![Aceptar invitación](docs/screenshots/aws-security-account-onboarding/03-aceptar-invitacion-iam-larry-security.png)

4. **Invitación aceptada**  
   ![Invitación aceptada](docs/screenshots/aws-security-account-onboarding/04-Invitacion-aceptada-IAM-Larry-security.png)

5. **Crear rol de confianza para la cuenta general desde security**  
   ![Rol](docs/screenshots/aws-security-account-onboarding/05-Generar-rol-desde-security-para-general.png)

6. **Crear rol `OrganizationAccountAccessRole`**  
   ![Cambiar rol](docs/screenshots/aws-security-account-onboarding/06-OrganizationAccountAccessRole-Asignacion-de-rol.png)

7. **Visualización del rol disponible**  
   ![Acceso demostrado](docs/screenshots/aws-security-account-onboarding/07-Acceso-a-cambiar-rol.png)

8. **Cambio de rol entre cuentas**  
   ![Cambio de rol](docs/screenshots/aws-security-account-onboarding/08-Cambio-de-rol-desde-general-a-security.png)

9. **Acceso confirmado desde cuenta SECURITY**  
   ![Acceso confirmado](docs/screenshots/aws-security-account-onboarding/09-Rol-accedido-a-security-desde-general.png)

10. **Crear OU SECURITY**  
   ![Crear OU](docs/screenshots/aws-security-account-onboarding/10-Crear-OU-SECURITY.png)

11. **Nombrar la OU SECURITY**  
   ![Nombre OU](docs/screenshots/aws-security-account-onboarding/11-Crear-OU-SECURITY-colocar-nombre.png)

12. **Agregar cuenta SECURITY a la OU**  
   ![Agregar cuenta](docs/screenshots/aws-security-account-onboarding/12-Agregar-cuenta-SECURITY-A-OU.png)

13. **Trasladar cuenta SECURITY a OU SECURITY**  
   ![Traslado cuenta](docs/screenshots/aws-security-account-onboarding/13-Traslado-cuenta-SECURITY-A-OU-SECURITY.png)

14. **Finalizar traslado de la cuenta SECURITY**  
   ![Traslado final](docs/screenshots/aws-security-account-onboarding/14-Traslado-finalizado-cuenta-SECURITY-A-OU-SECURITY.png)

---

## 🔐 Ejemplo visual de política SCP aplicada

Se documenta visualmente cómo aplicar una **política de control de servicios (SCP)** para **denegar el uso de IAM** a la cuenta `AWS-SECURITY`.

📂 Carpeta: `docs/screenshots/SCP/`

### 🔎 Pasos documentados:

1. **Crear política IAMDeny**  
   Política SCP personalizada que deniega el uso de IAM a nivel organizativo.  
   ![Política creada](docs/screenshots/SCP/01-politica-denegacion-uso-IAM.png)

2. **Asociar política IAMDeny**  
   Desde el panel de SCP, se asocia la política a la OU `SECURITY`.  
   ![Asociar política](docs/screenshots/SCP/02-asociar-politica-denegacion-uso-IAM.png)

3. **Política asociada correctamente**  
   Confirmación visual de que la SCP fue aplicada correctamente a la OU `SECURITY`.  
   ![Confirmación asociación](docs/screenshots/SCP/03-asociar-politica-denegacion-uso-IAM-realizada.png)

4. **Verificación de denegación efectiva**  
   Desde la cuenta `AWS-SECURITY`, se intenta acceder a IAM y el acceso es denegado explícitamente.  
   ![Acceso denegado](docs/screenshots/SCP/04-denegacion-efectiva-uso-iam-a-cuenta-security.png)

---

## 💳 Configuración de facturación

Todas las cuentas están vinculadas a la cuenta raíz `AWS-GENERAL`, la cual:

- Administra y paga todos los servicios de la organización
- Permite visualización unificada de costos desde Cost Explorer
- Aplica políticas presupuestarias y restricciones en un solo lugar

📸 Captura:  
![Facturación](docs/screenshots/general/Facturacion-unificada.png)

---

## 💰 Visualización de costos con Cost Explorer

Se utilizó la herramienta **AWS Cost Explorer** desde la cuenta principal `AWS-GENERAL` para analizar el consumo mensual consolidado de la organización. Esta vista permite monitorear los servicios utilizados, sus costos asociados y los patrones de consumo durante los últimos meses.

📊 **Resumen del reporte generado:**

- Costo total: **$10.48 USD**
- Promedio mensual: **$1.75 USD**
- Servicios activos: **24**
- Intervalo visualizado: **Enero 2025 - Junio 2025**
- Agrupado por: **Servicio**

📸 Captura real del informe:  
![Cost Explorer](docs/screenshots/general/cost-explorer.png)

> 💡 Nota: Las cuentas vinculadas aparecen correctamente configuradas, sin embargo, no figuran individualmente en el reporte porque **aún no han generado consumo directo**.

## 🛠 Futuras mejoras

- ✨ Agregar documentación en Terraform (`main.tf`, `outputs.tf`, `variables.tf`)
- 📊 Configurar alertas y monitoreo inter-cuenta
- 🔄 Automatizar provisión de cuentas sandbox para pruebas

---

## 🙋 Autor

**Larry Andrés Rondan Manrique**  
📬 Email: larrycloudaws@gmail.com  
🐙 GitHub: [@larrycloud](https://github.com/larrycloud)

🛡️ *Nota: Las IDs de cuenta en el diagrama han sido modificadas por motivos de seguridad.*
