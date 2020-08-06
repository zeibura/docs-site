# Configuring Zowe certificates 

To encrypt data across secure sockets and to establish client server trust relationships, Zowe uses certificates.  Zowe is able to work with existing certificates, create a new certificate based on an existing certificate authority (CA), or create its own CA and use that to create self-signed Zowe certificate.  Zowe is able to work with certificates held in a USS keystore directory or else a SAF keyring.

## Keystore versus keyring

If you are creating a personal or sandbox z/OS installation of Zowe then the advantage of a USS keystore is that you can create one in any directory for which you have write permissions, such as your TSO user ID home directory.  The disadvantage of a USS keystore is that any user who has a TSO user with read access to the keystore directory is able to retrieve the private key.  When the USS keystore directory is created its permissions are changed to lockdown access, however for some z/OS environments USS keystores are not permitted.  

- [Configuring Zowe certificates in UNIX files](./configure-certificates-keystore.md)

If you are deploying Zowe for production then a SAF keyring provides a greater level of security for protecting the Zowe certificate's private key.  The disadvantage of using a keyring is that for many z/OS environments the TSO user ID configuring the keyring needs to have elevated privileges so it will need to be performed by a specialized z/OS system programmer.  This makes it more difficult to use for sandbox and ad-hoc Zowe test installation scenarios where USS keystores may be preferable.  

- [Configuring Zowe certificates in a key ring](./configure-certificates-keyring.md)

