# k8scasestudy1
-	Deploy nginx web service


kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml

-	Should be able to handle the zero downtime (or nearly) when upgrade nginx docker image to newer tag

kubectl set image deployment/my-nginx nginx=nginx:1.16 --record

Here when image upgrade is happening all the exisitng replicas still be available, and extra 10% of total replicas will be created with new image and keep rolling till all the pods are migrated to new images.
      rollingUpdate:
        maxSurge: 10%
        maxUnavailable: 0%

-	If the pod tries to get more than 200Mb of memory, should be restarted by OOM
        resources:
          requests:
            memory: "128Mi"
          limits:
            memory: "200Mi"
       
-	Content of index page will be passed in as a configmap, you define the content

 kubectl create cm webcodecm --from-file=nginx-web.html

-	Generate a self-signed cert, passed it to nginx for SSL configuration
-	Setup auto-scaling for nginx pods if CPU tries to reach a threshold (you define it), min pod is 1, max is 2
