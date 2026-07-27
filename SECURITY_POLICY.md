# Política de Seguridad — Corporación Favorita SGSI

## Revocación Inmediata de Accesos (Offboarding)

Cuando un integrante deja el equipo de desarrollo (renuncia, cambio de rol o
cese), el Proveedor de Identidad (IdP: Active Directory / IAM) DEBE suspender
todas sus cuentas en un plazo MENOR A 5 MINUTOS, mediante el siguiente
procedimiento:

1. RRHH/CISO dispara el evento de baja (webhook o ticket).
2. El IdP deshabilita la cuenta de dominio y expira la sesion.
3. Se revocan tokens OAuth, llaves SSH y Personal Access Tokens del
   repositorio asociados al usuario.
4. Se rota cualquier credencial o secreto compartido al que el usuario haya
   tenido acceso (bases de datos, buckets, API keys).
5. Se retira al usuario de todos los grupos y ramas protegidas.
6. Queda registro en los logs de auditoria (control 8.15).

Responsable: CISO. Verificacion: Auditor de Seguridad (trimestral).

## Estándar de almacenamiento de contraseñas (Control A.8.24)

- PROHIBIDO el uso de MD5 o SHA-1 para almacenar contraseñas.
- OBLIGATORIO usar funciones de hashing con sal y factor de costo: bcrypt
  (password_hash con PASSWORD_BCRYPT) o Argon2id.
- La verificación se realiza siempre con password_verify(), nunca comparando
  hashes manualmente.
- Toda contraseña heredada en MD5 debe migrarse (ver NC-2026-001).

## Escritorio y Pantalla Limpia

- Bloqueo automático de sesión por inactividad a los 2 minutos.
- Prohibido anotar credenciales en post-its, hojas físicas o archivos de
  texto sin cifrar.
- Uso obligatorio del gestor de contraseñas corporativo.
