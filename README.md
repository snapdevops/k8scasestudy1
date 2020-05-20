# k8scasestudy1
-	Deploy nginx web service


kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml

-	Should be able to handle the zero downtime (or nearly) when upgrade nginx docker image to newer tag
[node2 ~]$ kubectl set image deployment/my-nginx nginx=nginx:1.16.1 --record
deployment.extensions/my-nginx image updated
[node2 ~]$ kubectl get pods --watch

-	If the pod tries to get more than 200Mb of memory, should be restarted by OOM
-	Content of index page will be passed in as a configmap, you define the content
-	Generate a self-signed cert, passed it to nginx for SSL configuration
-	Setup auto-scaling for nginx pods if CPU tries to reach a threshold (you define it), min pod is 1, max is 2
