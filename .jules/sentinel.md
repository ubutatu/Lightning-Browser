## 2025-05-15 - Insecure SSL Certificate Handling
**Vulnerability:** The `onReceivedSslError` method in `Barebones.java` was explicitly calling `handler.proceed()`, which instructed the WebView to ignore all SSL certificate errors (expired, mismatched hostname, untrusted CA).
**Learning:** This is a common but extremely dangerous pattern in Android WebView development, often used during development to bypass local certificate issues but frequently left in production code. It completely disables the security benefits of SSL/TLS and enables Man-in-the-Middle (MITM) attacks.
**Prevention:** Always default to `handler.cancel()` in `onReceivedSslError`. If a user bypass is desired, it must be implemented with an explicit warning dialog that explains the risks, rather than silently proceeding.

## 2025-05-15 - Insecure Default Protocol
**Vulnerability:** The application was using `http://` as the default protocol for Google searches, the default homepage, and for prefixing user-entered URLs that lacked a scheme.
**Learning:** Using `http://` by default exposes search queries and browsing activity to eavesdropping and tampering. Modern applications should always default to `https://` to ensure encrypted communication.
**Prevention:** All default URLs and automatic protocol prefixing logic should prioritize `https://` over `http://`.
