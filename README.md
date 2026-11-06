# FamRuta - Navegación Familiar en Tiempo Real (Android Nativo)

FamRuta es una aplicación Android nativa desarrollada en **Kotlin** con **Jetpack Compose**, **Google Sign-In** y **Firebase Firestore**.

---

## 🚀 ¿Por qué falló Codemagic y cómo solucionarlo?

En la captura de pantalla de Codemagic, el error fue:
```text
Get Flutter packages: Found no 'pubspec.yaml' file
Step 2 script 'Get Flutter packages' exited with status code 66
```

### La Razón:
FamRuta **NO es Flutter**, es una aplicación **Android Nativa (Kotlin + Gradle)**.
Por defecto, al conectar un repositorio a Codemagic, este intenta compilarlo como Flutter si no se le indica lo contrario.

### Solución en Codemagic (2 Opciones):

#### Opción A: Usar `codemagic.yaml` (Recomendada)
1. En tu panel de Codemagic en el proyecto `Fam`:
2. Haz clic en el engranaje de configuración (**Settings**) o en **"Switch to configuration from codemagic.yaml"**.
3. Codemagic detectará automáticamente el archivo `codemagic.yaml` que ya está en la raíz del proyecto.
4. Presiona **Start new build**. Compilará directamente `./gradlew assembleDebug` y generará el archivo `.apk` para descargar.

#### Opción B: Cambiar el tipo de proyecto en el Workflow Editor
1. En Codemagic, entra a la configuración del proyecto.
2. Si usas el editor visual, cambia el tipo de proyecto de **Flutter App** a **Android App**.
3. En la sección de Build, selecciona **Gradle wrapper** (`./gradlew assembleDebug`).

---

## ⚡ Alternativa directa: GitHub Actions (Automático y Gratis)

Ya incluimos el flujo automático en `.github/workflows/build-apk.yml`.
1. Cada vez que hagas `git push` a tu repositorio en GitHub:
2. Ve a la pestaña **Actions** en tu repositorio de GitHub (`github.com/daniellugoxd/Fam/actions`).
3. Verás la compilación ejecutándose automáticamente.
4. Al terminar (tarda ~2 minutos), haz clic en la ejecución y en la sección **Artifacts** descarga directamente `FamRuta-app-debug.apk` e instálalo en tu Android.

---

## 📂 Estructura del Proyecto Android

La estructura del proyecto sigue la arquitectura oficial de Google para Android:
- `/app`: Módulo principal de la aplicación (`src/main/java`, `res`, `AndroidManifest.xml`).
- `/gradle/wrapper`: Binarios y propiedades del Gradle Wrapper (`gradle-wrapper.jar`, `gradlew`).
- `build.gradle.kts` & `settings.gradle.kts`: Configuración de compilación Gradle Kotlin DSL.
- `codemagic.yaml`: Pipeline de CI/CD para compilación en Codemagic.
- `.github/workflows/build-apk.yml`: Pipeline de CI/CD para GitHub Actions.

---

## 📱 Compilación Local

Para compilar el APK en tu computadora o terminal:
```bash
./gradlew assembleDebug
```
El APK generado estará en:
`app/build/outputs/apk/debug/app-debug.apk`
