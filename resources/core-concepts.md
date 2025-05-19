# Terraform Enterprise: Core Concepts

## What is Terraform Enterprise?

Terraform Enterprise (TFE) is HashiCorp's self-hosted distribution of HCP Terraform (formerly Terraform Cloud). It provides organizations with a private instance of Terraform Cloud that can be deployed in their own infrastructure environment with enterprise-grade features like audit logging and SAML single sign-on.

## Infrastructure as Code Foundation

At its foundation, Terraform is an infrastructure as code tool that lets you define both cloud and on-premises resources in human-readable configuration files that you can version, reuse, and share. This enables you to use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle.

## Core Concepts

### 1. Workspaces

A workspace is a fundamental organizing principle in Terraform Enterprise. While Terraform CLI uses content from the directory it runs in, Terraform Enterprise manages infrastructure collections with workspaces instead of directories.

Each workspace contains:
- **Configuration**: The Terraform code that defines your infrastructure
- **Variables**: Input values that customize your configuration
- **State**: The record of what resources have been deployed
- **Run History**: Record of all past executions
- **Permissions**: Access controls defining who can manage the workspace

Workspaces are isolated environments with a 1:1 mapping between configuration and state file, providing a boundary for changes and helping to manage blast radius.

### 2. Runs

In Terraform Enterprise, operations are wrapped up in what's called a "run." TFE separates the plan and apply phases, allowing for serialization through these steps and adding additional phases.

A typical run process:
1. **Queue**: The run is queued until a worker is available
2. **Plan**: Terraform analyzes what changes need to be made
3. **Cost Estimation**: Shows estimated costs for resources (if enabled)
4. **Policy Check**: Sentinel policies are evaluated against the plan
5. **Apply**: Changes are applied to create/modify infrastructure
6. **State Update**: The resulting state file is updated

### 3. Modules

Modules are reusable packages of Terraform configurations that are managed as a group. They provide:
- **Encapsulation**: Grouping related resources together
- **Reusability**: Using the same infrastructure patterns across workspaces
- **Consistency**: Standardizing infrastructure patterns across teams
- **Abstraction**: Hiding complex implementation details behind a simpler interface

Modules can be:
- Published in the Terraform Registry
- Stored in private version control systems
- Referenced with Git URLs in your configuration

### 4. Projects

Projects let you organize your workspaces into logical groups. In Terraform Enterprise, you can assign project permissions to scope access to collections of workspaces based on business needs, such as:
- By application/service
- By environment (dev/staging/prod)
- By team ownership
- By business unit

### 5. Remote State Management

When remote operations are run, Terraform Enterprise automatically configures the workspace's state. TFE provides:
- **Versioning**: Maintaining history of state changes
- **Locking**: Preventing concurrent operations
- **Sharing**: Enabling outputs to be consumed by other workspaces
- **Access Controls**: Restricting who can view and modify state

### 6. Version Control Integration

As an infrastructure-as-code service, Terraform Enterprise supports Version Control System (VCS) integration with providers like:
- GitHub
- GitLab
- Azure DevOps
- Bitbucket

Benefits include:
- Triggering Terraform runs on code changes
- Functioning as a CI/CD pipeline for infrastructure
- Tracking history of infrastructure changes
- Supporting pull request workflows

### 7. Policy as Code (Sentinel)

Sentinel is HashiCorp's language and framework for embedding policy as code into Terraform Enterprise. It runs between the plan and apply phases to enforce governance rules.

Key aspects:
- **Policy Language**: A domain-specific language for writing policies
- **Policy Framework**: Tools for testing and applying policies
- **Enforcement Levels**:
  - Advisory: Warns but allows the operation to proceed
  - Soft-Mandatory: Requires override by authorized users
  - Hard-Mandatory: Cannot be overridden

Common policy use cases:
- Enforce security standards
- Control resource costs
- Ensure compliance requirements
- Standardize resource configurations

### 8. Teams and Access Control

Terraform Enterprise provides role-based access control that can be managed at various levels:
- **Organization Level**: Global policies and teams
- **Project Level**: Project-specific access
- **Workspace Level**: Fine-grained control over specific workspaces

Common permissions include:
- **Read**: View configurations and state
- **Plan**: Execute terraform plan
- **Apply**: Execute terraform apply
- **Variables**: Manage workspace variables
- **State**: View and manage state
- **Admin**: Full control over workspace settings

### 9. Run Triggers

Run triggers allow runs to queue automatically in your workspace when runs in other workspaces are successful, creating dependencies between workspaces.

This enables:
- Sequencing infrastructure deployments
- Building workflows across multiple workspaces
- Ensuring dependent components are updated together

### 10. Private Module Registry

Terraform Enterprise includes a private module registry that allows organizations to:
- Share internal modules securely
- Version modules using semantic versioning
- Document modules with standardized formatting
- Control access to proprietary infrastructure patterns

## Key Benefits of Terraform Enterprise

Terraform Enterprise helps organizations:
- Cut costs and minimize redundant work
- Improve team productivity with a unified workflow
- Provide full visibility across all environments
- Automatically enforce policies to limit unneeded and insecure infrastructure
- Reduce risk by standardizing how infrastructure is codified and reused
- Meet security and compliance requirements with a self-hosted solution

