---
layout: post
title:  "Scaling & Optimization: T-Shirt Method"
date:   2021-03-03
desc: "Recommendations on scaling and cluster sizing that will increase utilization and decrease costs."
keywords: "kubernetes,gke,docker,scaling,cost,cloud,compute,ml,terraform"
categories: [Kubernetes]
tags: [kubernetes,optimization,scaling]
icon: fa-cloud
---

I've had the opportunity work for many diverse companies in sectors ranging from sustainability, fintech, marketing, and e-commerce. One objective they all have in common is to reduce opperating costs where possible without sacrificing the end product.  One easy way to bring costs down without affecting the end product is by applying different scaling techniques to various Kubernetes workloads. I'm not just talking about enabling autoscaling. That's one component, but autoscaling itself can also be inefficient causing resources to idle. 

Companies like Airbnb follow a t-shirt sizing technique where they size all their workloads and label them as small, medium, or large.  By following this technique they're able to compact multiple workloads into a node, increasing their utilization to 85 - 90 percent. 

For example, the following diagram has four nodes. If we look closely at Node A, we notice that it does not follow the t-shirt method. So, whenever a new workload is added, if it can't fit into an existing node, Kubernetes will scale up the node-pool adding another node so this workload can run.  By doing so, this actually decreases our utilization, because the new node that was added only has 1 workload running and the remaining resources in that node are not being used.

<p align="center">
  <img width="460" src="https://royerramirez.com/static/assets/img/blog/kubernetes/scaling-and-optimization/2020-03-03-tshirt-method.png">
</p>

If we look at Node B, Node C, and Node D, we notice that in fact most of the resources in that node are being used. This gives us the flexibility to build actual node-pools targeting those specific workloads ensuring our environment is always scaling up and down efficiently. 

When managing the infrastructure for my team, I like to take this method into consideration. However, I don't let it become a blocker. There are use cases, where knowing the exact resources required to run an application are unknown. In general, my recommendation is to build multiple node-pools that give your cluster the opportunity to scale up and down smarter. Take advantage of taints, labels, and node-affinities. They will help with segregating workloads into different node-pools.
