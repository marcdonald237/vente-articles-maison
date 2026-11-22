# Déploiements

Même site, même base Firebase (les choix et paiements sont partagés entre toutes les versions).

## 1. Hébergeur gratuit avec nom au choix (Netlify)
1. Compte gratuit sur netlify.com, puis « Add new site » > « Deploy manually ».
2. Glisse le dossier du site (index.html + img/) ou le fichier .zip.
3. « Site configuration » > « Change site name » : choisis ex. `vente-marc` → https://vente-marc.netlify.app
4. Pour mettre à jour : re-glisse le dossier.
Alternative : Cloudflare Pages (nom `xxx.pages.dev`, choisi à la création du projet).

## 2. Kubernetes
Image Docker construite automatiquement par GitHub Actions (`.github/workflows/docker.yml`) → `ghcr.io/<repo>:latest`.
Rendre le paquet public : GitHub > Packages > vente-articles-maison > Package settings > Change visibility > Public.

    kubectl apply -k k8s/
    kubectl port-forward svc/vente-maison 8080:80   # test : http://localhost:8080

Test local sans cluster : `docker build -t vente-maison . && docker run -p 8080:8080 vente-maison`
