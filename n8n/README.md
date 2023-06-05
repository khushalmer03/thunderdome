flux create source helm n8n-helm-source \
--namespace flux-system \
--interval 60m \
--url https://improwised.github.io/charts/ \
--export > n8n-helm-source.yaml

flux create helmrelease n8n-helmrelease \
--namespace n8n \
--source Helmrepository/n8n-helm-source.flux-system \
--chart polymorphic-app \
--values ~/deployn8n/values.yaml \
--interval 10m \
--export > n8n-helmrelease.yaml

flux create source helm bitnami-helm-source \
--namespace flux-system \
--interval 60m \
--url https://charts.bitnami.com/bitnami/ \

flux create helmrelease n8n-database-helmrelease \
--namespace n8n \
--source Helmrepository/bitnami-helm-source.flux-system \
--chart postgresql \
--values ~/deployn8n/post.yaml \
--interval 10m \
--export > n8n-database-helmrelease.yaml
