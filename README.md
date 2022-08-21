# sonarqube-kubernetes

-----
Create sonarqube namescpace
-----
    kubectl create namespace sonarqube
-----

Encode USERNAME and PASSWORD of Postgres using following commands:
--------
    echo -n "this_is_a_fake_user_dev" | base64
    echo -n "this_is_a_fake_password_dev" | base64
Create the Secret using kubectl apply:
-------
    kubectl apply -f postgres-secrets.yml -n sonarqube

Create PV and PVC for Postgres using yaml file:
-----
    kubectl apply -f postgres-storage.yaml -n sonarqube

Deploying Postgres with kubectl apply:
-----------
    kubectl apply -f postgres-deployment.yaml -n sonarqube
    kubectl apply -f postgres-service.yaml -n sonarqube

Create PV and PVC for Sonarqube:
-------------
    kubectl apply -f sonar-pv-data.yml -n sonarqube
    kubectl apply -f sonar-pv-extensions.yml -n sonarqube
    kubectl apply -f sonar-pvc-data.yml -n sonarqube
    kubectl apply -f sonar-pvc-extentions.yml -n sonarqube
Create configmaps for URL which we use in Sonarqube:
-------
    kubectl apply -f sonar-configmap.yaml -n sonarqube
Deploy Sonarqube:
-------------
    kubectl apply -f sonar-deployment.yml -n sonarqube
    kubectl apply -f sonar-service.yml -n sonarqube
Check secrets:
-------
    kubectl get secrets -n sonarqube
    kubectl get configmaps -n sonarqube
    kubectl get pv -n sonarqube
    kubectl get pvc -n sonarqube
    kubectl get deploy -n sonarqube
    kubectl get pods -n sonarqube
    kubectl get svc -n sonarqube
    
Now Goto Loadbalancer and check whether service comes Inservice or not, If it comes Inservice copy DNS Name of Loadbalancer and check in web UI

Default Credentials for Sonarqube:
-------
    UserName: admin
    PassWord: admin
    
Now we can cleanup by using below commands:
--------
    kubectl delete deploy postgres sonarqube -n sonarqube
    kubectl delete svc postgres sonarqube -n sonarqube
    kubectl delete pvc postgres-pv-claim sonar-data sonar-extensions -n sonarqube
    kubectl delete pv postgres-pv-volume sonar-pv-data sonar-pv-extensions -n sonarqube
    kubectl delete configmaps sonar-config -n sonarqube
    kubectl delete secrets postgres-secrets -n sonarqube
