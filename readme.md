# IBM Multicloud Manager

## Overview 

IBM Multicloud Manager is the enterprise-grade multicloud management solution for Kubernetes. Multicloud Manager improves visibility, security and governance, and automation across all Kubernetes environments.

Below diagram represents a generic reference architecture for multi cloud management for k8s cluster.
![Alt Text](\images\multicluster-k8s-mgmt.jpg)

The **IBM Cloud Pak for Multicloud Management**, running on Red Hat Red Hat® OpenShift®, provides consistent visibility across  multiple clusters, governance, event management, application management, infrastructure management and automation from on premises to the edge. The IBM Cloud Pak for Multicloud Management includes IBM Multicloud Manager, IBM Cloud App Management, IBM Cloud Automation Manager, and IBM Cloud Event Management. IBM Multicloud Manager provides application and cluster visibility across the enterprise to any public or private cloud.
* IBM Multicloud Manager - Provides user visibility, application-centric management (governance, deployments, health, operations), and policy-based compliance across clouds and kubernetes clusters.
* IBM Cloud App Management - Monitors cloud and on-premises application environments
* Cloud Event Management - Consolidates information from monitoring systems and corelates all events associated with a single application or single cluster to an incident. Event Management can receive events from various monitoring sources, either on-premises or in the cloud. Event Management is installed along with IBM Cloud App Management.
* Cloud Automation Manager - Cloud management solution in IBM Cloud Private that automates provisioning of infrastructure and virtual machine applications across multiple cloud environments with optional workflow orchestration.

**IBM Multicloud Manager usage:**
* Cluster inventory
* Multicluster operations and visibility
* Deployment of application resources
* Governance and risk

## Architecture

Main conponents of Multicloud Manager:
* Multicloud Manager Controller (MCM Controller aka **Hub Cluster**) - It asynchronously aggregates multiple clusters of information and maintains the state of managed clusters and applications. The Multicloud Manager Controller stores information in etcd, typically by using the host Kubernetes etcd. Interaction with the Multicloud Manager Controller occurs through a set of REST APIs.

* Multicloud Manager Klusterlet aka **Managed Cluster** - This agent runs on a managed Kubernetes cluster. It creates a connection with the Multicloud Manager Controller by using a unidirectional communication pattern. The cluster inventory, application management, and policy enforcement operations are communicated through Klusterlet in a Multicloud Manager environment.

The below reference diagram shows IBM MCM managing multiple clusters. In the Datacenter, it is hosted on top of Openshift container platform and manages the local cluster. It also manages VMware PKS in the branch office and Azure AKS in the public cloud. The MCM controller (Hub cluster) communicates with the klusterlet (Managed cluster) using port 443. The managed cluster communicates with Kubernetes API server port on the hub cluster over port 8001 and with image resistry server over port 8500.

![Alt Text](\images\ibm-mcm-k8s-ra.jpg)