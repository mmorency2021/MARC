# Telco Hub Reference Design System (RDS)

This directory contains the **Telco Hub** component of the [OpenShift KNI Telco Reference](https://github.com/openshift-kni/telco-reference/tree/main/telco-hub) architecture, which provides a comprehensive reference design for deploying hub cluster.

## Description

The **Telco Hub Reference Design Specification** defines a standardized OpenShift Container Platform deployment model specifically designed for telecommunications hub sites. This specification provides validated configurations, resource requirements, and architectural guidelines for deploying and managing hub clusters that serve as centralized management points for distributed telecommunications infrastructure.

The hub cluster serves as the management and orchestration layer for multiple edge and Radio Access Network (RAN) sites, providing centralized lifecycle management, policy enforcement, and observability across a geographically distributed telecommunications network.

## Overview

The **Telco Hub RDS** is designed for telecommunications hub sites that function as regional management centers in telecommunications network architectures. The hub cluster model is characterized by:

- **Multi-Cluster Management**: Centralized management and lifecycle operations for multiple managed clusters using Red Hat Advanced Cluster Management (RHACM)
- **GitOps-Based Automation**: Zero Touch Provisioning (ZTP) and automated cluster lifecycle management using GitOps workflows
- **Regional Orchestration**: Coordination of services and policies across multiple edge/RAN sites within a geographic region
- **Scalable Infrastructure**: Designed to manage hundreds to thousands of edge clusters with efficient resource utilization
- **Observability Hub**: Centralized monitoring, logging, and alerting for distributed telecommunications infrastructure
- **Policy Management**: Centralized policy creation, distribution, and compliance enforcement across managed clusters

### Hub Cluster Use Model

The telco management hub cluster is designed to:
- Manage the lifecycle of multiple edge and RAN clusters
- Provide GitOps-based configuration management and policy enforcement
- Serve as a centralized observability and monitoring hub
- Enable disaster recovery and backup operations for managed clusters
- Support disconnected or semi-connected deployment scenarios

### Container Image: `telco-hub-rds`

The telco-hub container packages OpenShift configuration manifests and reference architectures specifically tailored for hub site deployments.

**Container Details:**
- **Component**: `openshift-telco-hub-rds-container`
- **Image**: `openshift4/openshift-telco-hub-rds-rhel9`
- **Description**: Telco Hub RDS manifests
- **Maintainer**: cnf-devel@redhat.com

### Directory Structure

```
telco-hub/
├── Dockerfile.telco-hub          # Container build definition
├── configuration/                # OpenShift configuration manifests
│   ├── reference-crs/           # Reference Custom Resources
│   │   ├── required/            # Mandatory configurations for hub sites
│   │   └── optional/            # Optional enhancements and features
│   ├── example-overlays-config/ # Example overlay configurations
│   │   ├── acm/                 # Advanced Cluster Management
│   │   ├── gitops/              # GitOps configurations
│   │   ├── logging/             # Logging configurations
│   │   ├── lso/                 # Local Storage Operator
│   │   ├── odf/                 # OpenShift Data Foundation
│   │   └── registry/            # Container registry configurations
│   ├── reference-crs-kube-compare/ # Kubernetes comparison baselines
│   └── kustomization.yaml       # Kustomize configuration
├── install/                     # Installation configurations
│   ├── openshift/               # OpenShift installation configs
│   └── mirror-registry/         # Mirror registry configurations
└── scripts/                     # Utility scripts
    └── check_current_versions.sh
```


## Support and Documentation

### Official Documentation
- **[Telco Hub Reference Design Specification](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/scalability_and_performance/telco-hub-ref-design-specs)** - Official Red Hat documentation for OpenShift Container Platform 4.18 telco hub reference design
- [OpenShift KNI Documentation](https://openshift-kni.github.io/)
- [Telco Reference Architecture Guide](https://github.com/openshift-kni/telco-reference)
- [Red Hat OpenShift Documentation](https://docs.openshift.com/)

### Validated Software Components

The telco hub solution has been validated with the following Red Hat software components:

| Component | Version |
|-----------|---------|
| OpenShift Container Platform | 4.18 |
| Local Storage Operator | 4.18 |
| Red Hat OpenShift Data Foundation (ODF) | 4.18 |
| Red Hat Advanced Cluster Management (RHACM) | 2.13 |
| Red Hat OpenShift GitOps | 1.15 |
| GitOps Zero Touch Provisioning (ZTP) plugins | 4.18 |
| multicluster engine Operator PolicyGenerator plugin | 2.12 |
| Topology Aware Lifecycle Manager (TALM) | 4.18 |
| Cluster Logging Operator | 6.2 |
| OpenShift API for Data Protection (OADP) | Aligned with RHACM release |

### Community and Support
- **GitHub Issues**: [telco-reference issues](https://github.com/openshift-kni/telco-reference/issues)
- **Maintainers**: cnf-devel@redhat.com
- **Community**: OpenShift KNI community

## Related Components

- **[Telco Core RDS](../telco-core/)**: Core network configurations for telecommunications
- **[Telco RAN RDS](../telco-ran/)**: Radio Access Network configurations
- **Lifecycle Agent**: Operator for managing cluster lifecycle operations

## License

This project is licensed under the Apache License 2.0. See the [LICENSE](../LICENSE) file for details.

---

For the latest updates and detailed technical documentation, visit the [telco-reference repository](https://github.com/openshift-kni/telco-reference/tree/main/telco-hub) on GitHub.
