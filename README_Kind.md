### Kind
Kind è uno strumento con cui possiamo creare facilmente un Cluster in locale, sfruttando Docker.  
**Ovviamente serve che Docker sia già installato.**

Kind farà in modo di creare, per ogni nodo, un Container su Docker.  
Se non gli specificheremo nulla, creerà il solo Nodo-Master (Control Plane), quindi su Docker vedremo solo un Container.  
Ma come vedremo è possibile creare un cluster con ad esempio 2 Nodi-Master e 4 NodiWorker per un totale di 6 Container Docker.

### Perché Kind invece di MiniKube o K3S ?
- Kind riesce ad avviarsi in maniera estremamente rapida.
- Utilizza molte meno risorse
- Permette anche di creare dei Cluster in High Availability, quindi con più Nodi-Master e più Nodi-Worker

**[Documentazione Kind]: https://kind.sigs.k8s.io/docs/user/quick-start/**
**[Installazione di Kind]: https://kind.sigs.k8s.io/docs/user/quick-start/#installation**

### Configurare un Cluster Locale con Kind
- Il comando più classico per creare un cluster con Kind è:
        
        // crea un cluster con un solo nodo
        >> kind create cluster

- Ma possiamo anche specificare un nome in modo da avere più cluster locali:

        // crea un cluster dandogli un nome
        >> kind create cluster --name < NOME-CLUSTER >

- Possiamo creare configurazioni avanzate mediante file YAML

        // crea un cluster con configurazioni avanzate
        >> kind create cluster --config < NOME-FILE-YAML-DI-CONFIGURAZIONE > 

### Interrogazione dei Clusters
- Possiamo farci dire da Kind quali Clusters abbiamo creato

        // lista dei cluster
        >> kind get clusters

- Possiamo farci dire i Nodi presenti su un determinato cluster

        // lista dei nodi di un cluster
        >> kind get nodes --name < NOME-CLUSTER >

## Configurazioni avanzate del Cluster via file YAML
Abbiamo detto che mediante file yaml possiamo creare configurazioni avanzate per indicare magari più Nodi-Worker.  
Vediamo alcuni esempi.  
Per tutte le specifiche ulteriori vedi la documentazione: https://kind.sigs.k8s.io/docs/user/quick-start/#configuring-your-kind-cluster

1. Esempio di Cluster con 1 Nodo-Master e 3 Nodi-Worker

        # 4 nodes (3 workers and 1 master) cluster config
        kind: Cluster
        apiVersion: kind.x-k8s.io/v1alpha4
        nodes:
        - role: control-plane
        - role: worker
        - role: worker
        - role: worker

2. Esempio di Cluster in HA con 3 Nodi-Master e 5 Nodi-Worker

        # 8 nodes (5 workers and 3 masters) cluster config
        kind: Cluster
        apiVersion: kind.x-k8s.io/v1alpha4
        nodes:
        - role: control-plane
        - role: control-plane
        - role: control-plane
        - role: worker
        - role: worker
        - role: worker
        - role: worker
        - role: worker
