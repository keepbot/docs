### Certificate for password encryption

How to rencrypt of RDCMan credentials with a custom certificate?
Here the steps.

* **Generate** certificate

```bash
# makecert -sky exchange -r -pe -e <expiration_date> -a sha1 -len <key_lenght> -ss my -n "CN=RDCManCertCustomName"
# Example:
makecert -sky exchange -r -pe -e 01/01/2220 -a sha1 -len 2048 -ss my -n "CN=RDCManCertCustomName"
```

* Go to RDCman and open RDG file you want to reencrypt with the **Custom** certificate insetead of **Logged User** certificate
* Open file properties and go to **Encription Settings**
* Choose the newly created certificate
* _And don't forget to create a backup!_
