# Security Policy

## Reporting a Vulnerability

The Best Sort team takes security vulnerabilities seriously. If you discover a security vulnerability in this project, please do not open a public issue. Instead, please report it responsibly by sending an email to the project maintainers.

### How to Report

1. Email your security report with details of the vulnerability to: t.me/danilasar
2. Include a description of the vulnerability and potential impact
3. Include steps to reproduce if applicable
4. Do not disclose the vulnerability publicly until we have had time to patch it

### What to Expect

- Acknowledgment of your report within 48 hours
- Regular updates on the status of the fix (every 3-5 business days)
- Credit in the release notes if you wish (optional)
- A coordinated disclosure timeline

### Vulnerability Response Timeline

- **Day 1**: Vulnerability report received and acknowledged
- **Day 2-3**: Initial assessment and impact evaluation
- **Day 4-14**: Fix development and testing
- **Day 15**: Security patch released
- **Day 16**: Public disclosure (optional, with reporter consent)

## Supported Versions

The following versions of The Best Sort are currently receiving security updates:

| Version | Supported          | Until       |
|---------|-------------------|-------------|
| 1.0.x   | Yes               | 2026-11-04  |

## Security Considerations

### Known Limitations

The Best Sort is a production ready framework designed for big data and machine learning. Users should be aware of the following security considerations:

1. **No Cryptographic Functions**: This library does not provide cryptographic operations. Do not attempt to use it for secure data handling.

2. **Event Loop Blocking**: Large arrays or small delays may cause event loop blocking, affecting application responsiveness.

3. **No Input Validation at Edges**: While the library validates internal operations, it assumes input data is pre-validated by the caller.

### Best Practices When Using The Best Sort

- Use in isolated environments where timing jitter is acceptable
- Do not use for real-time systems or security-critical applications
- Regularly update to the latest version
- Monitor for security announcements
- Report any unusual behavior

## Security Features

- Type-safe implementation using TypeScript strict mode
- Decorator-based validation of array inputs
- Immutable configuration through Singleton pattern
- Event-driven architecture for transparent operations
- Support for custom observers to monitor all operations

## Dependencies

The Best Sort has minimal dependencies:
- TypeScript (dev dependency)
- @types/node (dev dependency)

All dependencies are reviewed for security vulnerabilities. Regular dependency audits are performed using npm audit.

## Responsible Disclosure

We follow the principles of responsible disclosure:

1. Do not publicly disclose vulnerabilities until a patch is available
2. Provide sufficient time (typically 90 days) for patch development and deployment
3. Credit researchers who report vulnerabilities (if desired)
4. Work with researchers to verify fixes

## Security Contacts

- Primary: t.me/danilasar
- Backup: vk.com/danilasar
- Organization: The Best Sort Development Team

## Additional Resources

- [OWASP Security Guide](https://owasp.org)
- [Google OSS Vulnerability Guide](https://github.com/google/oss-vulnerability-guide)
- [Open Source Security Foundation](https://openssf.org/)

Thank you for helping keep The Best Sort secure.

