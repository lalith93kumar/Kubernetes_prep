# Kubernetes_prep

interview queston rough

How do you handle a node failure in Kubernetes?
- make sure we have topologySpreadConstraints configured in podaffinity. so that the service is not stuck with one node. like if Node A has 15 pod B. It should be like one node should contain one pod b. so that user won't face tracfic ditrupotion.
- configure pod distruption budget so that node drain It caps what percentage of pods can go down at the same time during a voluntary drain, so you can drain multiple nodes in parallel during patching without wrecking your traffic.

How do you plan for Black Friday-level traffic?
- auto scalling will away handle it. But we should predict it future. like we should run a load test against the service with 1.5X load that might happen on blackfriday traffic. They add the desied kaprpenter max capacity with 1.5x resources. configure auto scaling based on traffic, cpu, memory capacity reached 50 % to 80 % based on new pod start time.

What is your approach to real-time troubleshooting for microservices running on Kubernetes?
- acknowlege the alert in pagerduty or teams channel,
- check grafana based on time frame. check the pod cpu & memory insights,
- check k8 event if the pod 
- check the application logs & spikes on DB query with read & write.
- Most production incidents trace back to a change somewhere, so this check often narrows things down faster than logs alone.
- updating stakeholders
- once fixed start full postmortem.

What measures do you take to reduce latency for microservices running on Kubernetes?
- trafficDistribution, set to PreferClose. It tells Kubernetes to prefer sending traffic to a pod in the same availability zone before going cross-zone.
- Pod-to-pod communication is the first layer I use pod affinity rules to group frequently communicating services on the same node, so that traffic stays local and fast.

How do you approach capacity planning for a multi-region EKS setup?
- AWS Global Accelerator, which uses a fixed anycast IP and routes each user to the nearest healthy region over the AWS backbone using BGP. If i have one load balancer per region & eks cluster per region.
- Database planning is the harder part, because a database has one writer at a time. Within a region, you typically run one writer and multiple readers across zones, with automatic failover if the writer goes down.

StatefulSet
- If database-1 is restarted, Kubernetes brings it back as database-1, rather than creating an arbitrary new identity. Pods have stable, predictable names & Pods have stable network identities & Can provide persistent storage through PersistentVolumeClaims.

DaemonSet
- it is windows node exportor. When a new node joins the cluster, Kubernetes automatically schedules the DaemonSet Pod there.
ConfigMap vs Secret
- A ConfigMap stores non-sensitive configuration data as key-value pairs.
- A Secret stores sensitive information. encrypted in based 64
ClusterIP
- It makes an application accessible only inside the Kubernetes cluster. http://backend:80

