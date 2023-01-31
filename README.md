### **Describe your approach to set up a CD solution for a Kubernetes environment, where there is a need to serve five teams of developers that can’t have direct kubectl access to the cluster and maintain their autonomy to deploy and see the production environment for debugging purposes.** ###

*I think that the most suitable option for this problem is creating users on ArgoCD and giving each team of developers a user. If you just create the user, it'll only have read access to see all deployments and services that are deployed on the cluster. The would be able to see the state of pods and also clic on it to see why they're down. Of course they won't be able to recreate or redeploy it.
There's also a tool named Teleport which make it easier just by using RBAC to do it and, they won't be able to interact with the control plane. This is not a CD solution but it's worth to mention.*

### **How would you manage secrets inside?**  ###

*There are several ways to manage secrets, Kubernetes has its own by creating secrets and mount it using CLI, and they can be encoded with base64 or just like stringData with hardcoded secret (this is not recommended by anymeans). Cloud Providers has it too and also you got Hashicorp Vault to store secrets. I think that the best way of doing it is by creating secrets from files and then mount them as volumns. There's a pretty cool tool named stakater/Reloader that restart pods everytime that a secret changes its value so, you're not concerned anymore with restarting pods from your own.*

### **What tooling would you use?**  ###

*Well, it depends on where I'm running Kubernetes, if I'm running it on any Cloud Provider at first I'll look at the solution to manage secrets that they have. Nonetheless, I think Hashicorp Vault is the best, is open source and, like Terraform, is cloud agnostic. You can also use Vault at local solutions for k8s, for example Minikube which is very awesome (I didn't know until now).*

 ### **Describe your approach for deploying and managing “Addons” applications that enable, automate or facilitate setups on Kubernetes.**  ###

*Well, nowadays when you think about Kubernetes, you gotta think about CI/CD, so the first thing that I would do is find a CI/CD circuit that can be adapted to the way that we work. Mostly focusing on a GitOps approach to make things easier and be very flexible with how devs works on repositories. Forgetting about GitFlow and having branches for environments. Next thing, dashboard or a tool like k9s just to make sure that you don't have to go trought all commands that k8s has to make one simple task (Even though I love k8s and CLI). Of course, another tool for metrics and logging, Prometheus/Grafana and Loki or ELK stack are good enough. Use Helm to deploy apps that you may need to use, or even to creates custom charts in order to have a full declarative and more flexible approach (Kustomize can also do the work). Cert-manager of course.*
