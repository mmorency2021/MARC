# Telco Hub Reference Design System (RDS)

This directory contains the **Telco Hub** component of the [OpenShift KNI Telco Reference](https://github.com/openshift-kni/telco-reference/tree/main/telco-hub) architecture, which provides a comprehensive reference design for telecommunications hub sites in cloud-native telecommunications deployments.

## Overview

The **Telco Hub RDS** is designed for telecommunications hub sites that serve as centralized management and aggregation points in telco networks. Hub sites typically provide:

- **Centralized Management**: Management of multiple edge/RAN sites
- **Network Function Virtualization (NFV)**: Hosting virtualized network functions
- **Service Orchestration**: Coordinating services across multiple edge locations
- **Data Aggregation**: Collecting and processing data from edge sites
- **Regional Connectivity**: Providing connectivity between edge sites and core networks

## Architecture Components

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

## Key Features

### 1. **Multi-Site Management Capabilities**
- Advanced Cluster Management (ACM) integration
- GitOps-based configuration management
- Centralized policy enforcement across edge sites

### 2. **Storage and Data Management**
- OpenShift Data Foundation (ODF) configurations
- Local Storage Operator (LSO) setup
- Container registry services for edge sites

### 3. **Networking and Connectivity**
- Hub-to-edge networking configurations
- Service mesh integration capabilities
- Load balancing and traffic management

### 4. **Observability and Monitoring**
- Centralized logging infrastructure
- Monitoring and alerting for hub and edge sites
- Performance metrics collection and analysis

### 5. **Security and Compliance**
- Security policies for telecommunications environments
- Compliance configurations for telecom standards
- Certificate management for secure communications

## Configuration Categories

### Required Configurations (`reference-crs/required/`)
Essential configurations that must be applied for a functional hub site:
- Core networking components
- Security policies and configurations
- Basic monitoring and logging
- Storage class definitions
- Performance tuning for telecommunications workloads

### Optional Configurations (`reference-crs/optional/`)
Additional features and enhancements:
- Advanced networking features
- Enhanced security configurations
- Additional monitoring and observability tools
- Performance optimization configurations
- Integration with external systems

### Example Overlays (`example-overlays-config/`)
Pre-configured examples for common scenarios:
- **ACM**: Advanced Cluster Management for multi-cluster scenarios
- **GitOps**: ArgoCD and Flux configurations for continuous deployment
- **Logging**: ELK stack and OpenShift Logging configurations
- **LSO**: Local Storage Operator for persistent storage
- **ODF**: OpenShift Data Foundation for software-defined storage
- **Registry**: Container registry configurations for edge distribution

## Deployment Scenarios

### Hub Site Characteristics
Telco Hub sites are typically characterized by:
- **Medium to High Resource Availability**: More compute and storage than edge sites
- **Stable Network Connectivity**: Reliable, high-bandwidth connections
- **Centralized Services**: Hosting services for multiple edge locations
- **Management Functions**: Orchestration and management of edge deployments
- **Regional Scope**: Serving a geographic region with multiple edge sites

### Use Cases
1. **5G Core Network Functions**: Hosting 5G core network components
2. **Edge Orchestration**: Managing and orchestrating edge site deployments
3. **Data Processing**: Regional data processing and analytics
4. **Service Assurance**: Monitoring and managing service quality across the region
5. **Content Distribution**: Caching and distributing content to edge sites

## Container Build and Deployment

### Building the Container

The telco-hub container is built using the provided Dockerfile:

```dockerfile
FROM registry.redhat.io/ubi9/ubi-minimal:${RHEL_VERSION}
COPY ./telco-hub /usr/share/telco-hub-rds
# ... container configuration
```

### Container Labels

The container includes comprehensive metadata:

```yaml
com.redhat.component: "openshift-telco-hub-rds-container"
name: "openshift4/openshift-telco-hub-rds-rhel9"
summary: "Telco Hub RDS manifests"
description: "Telco Hub RDS manifests"
io.k8s.display-name: "openshift-telco-hub-rds"
io.k8s.description: "Telco Hub RDS manifests"
io.openshift.maintainer.component: "Telco Hub RDS"
io.openshift.maintainer.product: "OpenShift Container Platform"
maintainer: "cnf-devel@redhat.com"
vendor: "Red Hat, Inc."
url: "https://github.com/openshift-kni/telco-reference"
```

## Integration with Konflux CI/CD

The telco-hub component integrates with Red Hat's Konflux CI/CD platform for automated building and deployment. See the pipeline configurations in the `.tekton/` directory for:

- **Dedicated Pipeline**: `telco-hub-rds-build-pipeline.yaml` - Specific pipeline for hub container
- **Parameterized Pipeline**: `single-build-pipeline.yaml` - Shared pipeline with container-type parameter

### Pipeline Parameters

Key parameters for hub container builds:
```yaml
path-context: "telco-hub"                    # Build context
dockerfile: "Dockerfile.telco-hub"           # Dockerfile location
output-image: "quay.io/your-org/telco-hub-rds:tag"
container-type: "hub"                       # For parameterized pipeline
```

## Installation and Usage

### Prerequisites
- OpenShift Container Platform 4.12+
- Adequate resources for hub site workloads
- Network connectivity to edge sites (if managing edge deployments)

### Basic Installation

1. **Extract Container Manifests**:
   ```bash
   # Pull and extract the telco-hub-rds container
   podman pull quay.io/openshift-kni/telco-hub-rds:latest
   podman run --rm quay.io/openshift-kni/telco-hub-rds:latest | base64 -d | tar -xf -
   ```

2. **Apply Required Configurations**:
   ```bash
   # Apply required configurations
   oc apply -k telco-hub-rds/configuration/reference-crs/required/
   ```

3. **Apply Optional Configurations** (as needed):
   ```bash
   # Example: Apply ACM configuration
   oc apply -k telco-hub-rds/configuration/example-overlays-config/acm/
   ```

### Customization

Use Kustomize to customize configurations for your environment:

```yaml
# kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - telco-hub-rds/configuration/reference-crs/required/
  - telco-hub-rds/configuration/reference-crs/optional/

patchesStrategicMerge:
  - custom-patches.yaml
```

## Version Management

The telco-hub RDS follows semantic versioning aligned with OpenShift releases:
- **Major.Minor**: Aligned with OpenShift versions (e.g., 4.20)
- **Patch**: Bug fixes and minor updates
- **Build Date**: Included in container labels for traceability

### Version Checking

Use the included script to check current versions:
```bash
./scripts/check_current_versions.sh
```

## Support and Maintenance

### Documentation
- [OpenShift KNI Documentation](https://openshift-kni.github.io/)
- [Telco Reference Architecture Guide](https://github.com/openshift-kni/telco-reference)
- [Red Hat OpenShift Documentation](https://docs.openshift.com/)

### Community and Support
- **GitHub Issues**: [telco-reference issues](https://github.com/openshift-kni/telco-reference/issues)
- **Maintainers**: cnf-devel@redhat.com
- **Community**: OpenShift KNI community

### Contributing

Contributions to the telco-hub reference design are welcome:

1. Fork the [telco-reference repository](https://github.com/openshift-kni/telco-reference)
2. Create a feature branch
3. Submit a pull request with detailed description
4. Ensure all tests pass and follow coding standards

## Related Components

- **[Telco Core RDS](../telco-core/)**: Core network configurations for telecommunications
- **[Telco RAN RDS](../telco-ran/)**: Radio Access Network configurations
- **Lifecycle Agent**: Operator for managing cluster lifecycle operations

## License

This project is licensed under the Apache License 2.0. See the [LICENSE](../LICENSE) file for details.

---

For the latest updates and detailed technical documentation, visit the [telco-reference repository](https://github.com/openshift-kni/telco-reference/tree/main/telco-hub) on GitHub.
