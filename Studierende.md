## Bereitstellung von Kubernetes Ressoucen

Die Netzlabore stellen den Studierenden im Rahmen von Projekten, Übungen und Abschlussarbeiten Ressourcen auf einem Kubernetes Cluster zur Verfügung. Jeder Studierende hat die Möglichkeit im Cluster Ressourcen in Form von einem Namespace zu beantragen. Auf dem Cluster betriebene Container sind bei Bedarf aus dem Internet erreichbar. Der Zugriff auf das Kubernetes Cluster efolgt über [Rancher](https://rancher.docklab.de/login).  

## Beantragung von einem Namespace auf dem Cluster

Füllen Sie bitte dieses [Formular]() aus und senden es an die E-Mail-Adresse [netlab@inf.h-brs.de](mailto:netlab@inf.h-brs.de). Alle weiteren Informationen senden wir Ihnen per E-Mail zu. 

---

## Nutzung vom Cluster

Nachdem Sie von uns eine Bestätigung per E-Mail erhalten haben, stehen Ihnen Ressourcen auf dem Cluster zur Verfügung. Melden sich dich mit Ihren Unix-Zugangsdaten (z.B. mmuster2s) bei [Rancher](https://rancher.docklab.de/login) an.

![login](res/rancher_start.png)

*Abbildung: Beispielhafter Login-Vorgang

Anschließend habe Sie Möglichkeit in Ihrem Projekt Namespaces anzulegen und Container zu betreiben. Der Projektname ist dabei Ihr Benutzerkürzel (z.B. mmuster2s).

---

## Let's Encypt Zertifikat erstellen

Über den Dienst `cert-manager` haben Sie die Möglichkeit eigene Let's Encypt Zertifikate für Ihre Webanwendungen zu erzeugen. Als Voraussetzung benötigen Sie eine Internetdomain. Als DNS Eintrag muss die lPv4-Adresse von einem Clusterknoten angegeben werden. 

### 1. Zertifikatsinformationen hinterlegen

Öffnen Sie im Cluster-Explorer die YAML Eingabe.

![login](res/LetsEncrypt_S1.png)

Anschließend kopieren Sie den Text aus der Codebox in den YAML Editor und ersetzen das Attribut<E-MAIL> durch Ihre eigene E-Mail-Adresse. Diese E-Mail-Adresse wird benutzt, um das Zertifikat bei Let's Encrypt zu erzeugen. Anschließend importieren Sie den YAML Text.

```
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: letsencrypt
spec:
  acme:
    email: <E-MAIL>
    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      name: example-issuer-account-key
    solvers:
    - http01:
        ingress:
          class: nginx
```

Bitte achten Sie darauf Ihren Namespace anzugeben.

![login](res/YAML_eingabe.png)

### 2. Zertifikat erzeugen

Anschließend kopieren Sie den Text aus der Codebox in den YAML Editor und ersetzen die Attribute `example.com` durch Ihre Domain oder Sub-Domain.

```
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: example.com
spec:
  secretName: tls-example.com
  dnsNames:
  - example.com
  issuerRef:
    name: letsencrypt
    kind: Issuer
```

Nachdem Sie den YAML Text importiert habe, wird ein Zertifikat erzeugt. Dies kann eine Minute dauern. Anschließen wird das Zertifikat als Secret im Namespace angelegt. Sollte kein Zertifikat erzeugt werden, suche sie nach den Ressourcen `certificaterequest`,`order` und `challenges` um Hinweise für den Grund zu bekommen.

### 3. Zertifikat auf Webdienst anwenden

Das Zertifikat müssen Sie nun in der Ingress Ressource hinterlegen. Wenn bei der Eingabemaske von der Ingress Ressouce nach einem Wert für das Zertifikat verlangt wird, nehmen Sie eine beliebige Zeichenfolge.
