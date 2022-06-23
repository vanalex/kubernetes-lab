### Running Containers for Troubleshooting

Sometimes it’s handy
to be able to run commands like wget or nslookup in the cluster, to see the results
that your application would get. You’ve already learned how to run containers in the
cluster with kubectl run, but here are a few useful examples of running one-off
container commands for debugging purposes.

First, let’s run an instance of the demo application to test against:

`kubectl run demo --image cloudnatived/demo:hello --expose --port 8888`

The demo service should have been allocated an IP address and a DNS name of
demo that is accessible from inside the cluster. Let’s check that, using the nslookup
command running inside a container:

`kubectl run nslookup --image=busybox:1.28 --rm -it --restart=Never --command -- nslookup demo`

Good news: the DNS name works, so we should be able to make an HTTP request to
it using wget and see the result:

`kubectl run wget --image=busybox:1.28 --rm -it --restart=Never --command -- wget -qO- http://demo:8888`