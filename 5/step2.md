Let’s check that the Service is load-balancing the traffic. To find out the exposed IP and Port we can use the describe service as we learned in the previously Module:

`kubectl describe services/kubernetes-bootcamp`{{execute}}

Create an environment variable called NODE_PORT that has as value the Node port:

`export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
echo NODE_PORT=$NODE_PORT`{{execute}}

Next, we’ll do a `curl` to the the exposed IP and port. Execute the command multiple times:

`curl host01:$NODE_PORT`{{execute}}

We hit a different Pod with every request. This demonstrates that the load-balancing is working.