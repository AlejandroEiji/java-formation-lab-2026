# Enunciado — Week 07: DI/IoC (Profiles/Wiring)

## Contexto del reto

**Indra Notifications** envía alertas por email. En entorno `dev` se usa un `FakeEmailSender` que solo loguea (sin enviar nada real). En `prod` se usa `SmtpEmailSender` que conecta al servidor real. Actualmente hay un `if` en el código que revisa una variable de entorno para decidir cuál usar. Esto hace los tests impredecibles.

## Lo que debes implementar

1. Define la interfaz `EmailSender` con el método `send(String to, String subject, String body)`.
2. Implementa `FakeEmailSender` anotada con `@Profile("dev")` — solo loguea en consola.
3. Implementa `SmtpEmailSender` anotada con `@Profile("prod")` — simula el envío (no conectar SMTP real).
4. Refactoriza `NotificationService` para recibir `EmailSender` por **constructor** (sin `@Autowired` en campo).
5. Crea `application-dev.properties` y `application-prod.properties` con configuraciones distintas (ej. `notification.retry-attempts`).
6. Escribe tests con `@ActiveProfiles("dev")` que verifiquen que `FakeEmailSender` es el bean activo.

## Restricciones técnicas (para todos)

- **Sin `@Autowired` en campos** — inyección solo por constructor.
- El `if` de entorno debe desaparecer del código de negocio.
- Los beans de `EmailSender` no deben coexistir en el mismo perfil.
- **Criterio no funcional (operación)**: en `dev` no debe salir ninguna conexión real — verificable ejecutando los tests sin red.

## Criterio de aceptación del PR

- [ ] `FakeEmailSender` activo en `dev`, `SmtpEmailSender` en `prod`
- [ ] `NotificationService` con inyección por constructor
- [ ] Sin `@Autowired` en campos en ninguna clase nueva
- [ ] Test con `@ActiveProfiles("dev")` que verifica el bean correcto
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Usar `@ConditionalOnProperty` para habilitar un `EmailSender` adicional basado en una property.
- Configurar un `@TestConfiguration` que registre un bean de test sin contaminar los perfiles.
