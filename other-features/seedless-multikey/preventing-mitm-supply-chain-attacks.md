# 🕵️‍♂️ Preventing MitM/Supply Chain Attacks

Obi SDK allows for appless, extensionless functionality by providing easy components which can be embedded in end applications or websites.

However, this opens the possibility of an attack by the end application, modifying the JavaScript and thus tricking the user into signing a message other than the one displayed to them.

Obi avoids this problem by using iFrames to include code which cannot be modified by the application. The relevant code itself can then also be verified by the user.
