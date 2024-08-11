ArgoCD installation
------------------

kubectl create ns argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

watch kubectl get pods -n argocd

kubectl edit svc argocd-server -n argocd

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

kubectl edit svc argocd-server -n argocd



Jenkins Execute shell I
---------------------

git clone https://github.com/mdhugol/gitops-demo.git devopsconfig

cd devopsconfig/helm

ls -lrt

echo $BUILD_NUMBER

sed -i "s/{tagversion}/$BUILD_NUMBER/g" gittemplate.yaml

cp -f gittemplate.yaml ../gitops.yaml

sed -i "s/$BUILD_NUMBER/{tagversion}/g" gittemplate.yaml



Jenkins Execute shell II
---------------------
cd ${WORKSPACE}/devopsconfig

ls -lrt

git config user.email "mdhugol@gmail.com"

git config user.name "mdhugol"

git add .

git commit -m "Modofied the template file and pushed to gitops-demo.git for build $BUILD_NUMBER"

git push https://{username}:{token}@github.com/mdhugol/gitops-demo.git

