# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :**
**Groupe :**

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   > il en affiche 3 : 2 agents et 1 server
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   > docker ps montre les containers ID , l'historique de création, leur status, et leur ports si connecté.

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   > un Cluster IP sur le port 443.
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   > Kubernetes l'a recréé avec un nouveau nom : le Deployment veille à maintenir le nombre de réplicas demandé.

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   > Non, il n'a pas survécu. Car le pod à changé de nom lors de son redéployement.
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   > Le port-forward était lié à l'ancien pod. Sa suppression a interrompu le tunnel, il faut donc le relancer vers le nouveau pod.

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   > kubectl create crée une ressource et échoue si elle existe déjà. kubectl apply crée ou met à jour la ressource à partir d'un fichier déclaratif.
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   > Le selector repère les pods auxquels le Service envoie le trafic grâce à leurs labels. Sans pod correspondant, le Service n'a aucun endpoint et ne peut pas transmettre le trafic.

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`.
   > Kubernetes répartit les pods sur au moins deux nœuds workers ; la répartition exacte varie selon le cluster.
   > Sortie à coller depuis votre cluster : `kubectl get pods -l app=site -o wide`
10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    > Il passait en `ImagePullBackOff` (après `ErrImagePull`), car l'image/tag est introuvable. `kubectl describe pod <nom-du-pod>` indique la cause.
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    > Oui : pendant le rolling update, les anciens pods prêts continuent de servir le trafic tant que les nouveaux ne sont pas prêts.

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    > `https://<ATELIER_KUBERNETES_2026>-8585.app.github.dev/` .
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    > Oui. Les deux pilotent le même cluster via l'API Server de Kubernetes. On peut afficher le Deployment avec `kubectl get deploy mario -o yaml`.

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** ... / ...
