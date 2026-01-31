# DevSecOps-Snyk-Security-Scanning

# Snyk DevSecOps Integration Guide



## Table of Contents
1. [Executive Summary](#executive-summary)
2. [What is Snyk?](#what-is-snyk)
3. [Core Capabilities](#core-capabilities)
4. [Supported Languages and Technologies](#supported-languages-and-technologies)
5. [Integration Methods](#integration-methods)
6. [DevSecOps Implementation Guide](#devsecops-implementation-guide)
7. [CI/CD Pipeline Integration](#cicd-pipeline-integration)
8. [Security Policy Configuration](#security-policy-configuration)
9. [Advanced Features](#advanced-features)
10. [Best Practices](#best-practices)
11. [Troubleshooting](#troubleshooting)

---

## Executive Summary

Snyk is an AI-powered developer security platform that enables organizations to find, prioritize, and fix security vulnerabilities across their entire software development lifecycle (SDLC). It integrates seamlessly into development workflows, providing real-time security feedback without disrupting developer productivity. It can be used to identify scan security vulnerability in third party libraries.

<img width="1600" height="779" alt="image" src="https://github.com/user-attachments/assets/a97d0bbb-12de-4c23-8d02-71f6359d1212" />

<img width="1600" height="739" alt="image" src="https://github.com/user-attachments/assets/fbbd548b-981d-4d35-84ec-9767b003527b" />

<img width="1600" height="453" alt="image" src="https://github.com/user-attachments/assets/418ab1e3-bc83-48f3-8b12-2ee046c81ffc" />


**Key Benefits:**
- **Shift-Left Security**: Identify vulnerabilities early in the development cycle
- **Developer-First Approach**: Native integration with IDEs, SCMs, and CI/CD tools
- **Comprehensive Coverage**: Scan code, dependencies, containers, and Infrastructure as Code
- **AI-Powered Remediation**: Automated fix suggestions and pull requests
- **Compliance Support**: Meet regulatory requirements (SOC 2, GDPR, PCI DSS)

---

## What is Snyk?

Snyk is a developer security platform that provides:

- **Vulnerability Detection**: Identifies security issues in real-time across multiple attack surfaces
- **Risk Prioritization**: Uses AI to prioritize vulnerabilities based on exploitability, reachability, and business context
- **Automated Remediation**: Generates pull requests with fixes for dependencies and code issues
- **Security Gates**: Enforces policies in CI/CD pipelines to prevent vulnerable code from reaching production
- **Developer Education**: Provides contextual security guidance and learning resources

### Snyk Product Suite

1. **Snyk Open Source**: Scans open source dependencies for known vulnerabilities
2. **Snyk Code**: Static Application Security Testing (SAST) for proprietary source code
3. **Snyk Container**: Scans container images and Kubernetes configurations
4. **Snyk Infrastructure as Code (IaC)**: Scans Terraform, CloudFormation, Kubernetes, ARM, and more

---

## Core Capabilities

### 1. Vulnerability Scanning

**Snyk Open Source:**
- Scans package manifests (package.json, requirements.txt, pom.xml, etc.)
- Identifies vulnerabilities in direct and transitive dependencies
- Provides detailed vulnerability information (CVE, CVSS scores, exploit maturity)
- Monitors projects continuously for new vulnerabilities

**Snyk Code:**
- Semantic analysis of source code (not just pattern matching)
- Detects security issues like SQL injection, XSS, path traversal, and more
- AI-powered analysis trained on millions of open-source repositories
- Low false-positive rate with context-aware analysis

**Snyk Container:**
- Scans base images and application layers
- Identifies OS package vulnerabilities
- Recommends more secure base images
- Detects configuration issues in Dockerfiles and Kubernetes manifests

**Snyk IaC:**
- Scans infrastructure code for misconfigurations
- Supports Terraform, CloudFormation, Kubernetes YAML, ARM templates, Helm charts
- Identifies security issues like open S3 buckets, overly permissive IAM policies
- Provides remediation guidance aligned with security frameworks (CIS, PCI DSS)

### 2. Risk Prioritization

Snyk uses multiple factors to prioritize vulnerabilities:

- **Exploit Maturity**: Whether exploits are available in the wild
- **Reachability Analysis**: Whether vulnerable code paths are actually executed
- **CVSS Score**: Industry-standard severity scoring
- **Social Trends**: Monitoring security community discussions
- **Business Context**: Custom priority based on project criticality

### 3. Automated Remediation

- **Automatic Fix PRs**: Snyk can automatically create pull requests with fixes
- **Upgrade Suggestions**: Recommends safe version upgrades
- **Patch Application**: Applies patches when upgrades aren't available
- **Code Fixes**: Suggests code changes for Snyk Code findings

---

## Supported Languages and Technologies

### Programming Languages

| Language | Package Managers | Snyk Open Source | Snyk Code |
|----------|-----------------|------------------|-----------|
| **JavaScript/TypeScript** | npm, Yarn, pnpm | ✓ | ✓ |
| **Java** | Maven, Gradle | ✓ | ✓ |
| **Python** | pip, Poetry, Pipenv | ✓ | ✓ |
| **.NET (C#, VB.NET)** | NuGet | ✓ | ✓ |
| **Go** | Go modules | ✓ | ✓ |
| **Ruby** | Bundler | ✓ | ✓ |
| **PHP** | Composer | ✓ | ✓ |
| **Swift/Objective-C** | CocoaPods, Carthage | ✓ | ✓ |
| **Scala** | sbt | ✓ | ✓ |
| **Kotlin** | Maven, Gradle | ✓ | ✓ |
| **Rust** | Cargo | ✓ | Limited |
| **C/C++** | Various | ✓ | ✓ |
| **Dart/Flutter** | pub | ✓ | Limited |

### Frameworks

**Python Frameworks:**
- Django, Flask, FastAPI, CherryPy, Pyramid, Tornado, Bottle, Falcon, Sanic

**JavaScript Frameworks:**
- React, Angular, Vue.js, Express.js, Next.js, Nest.js, Koa

**Java Frameworks:**
- Spring, Spring Boot, Hibernate, Struts, Play Framework

**.NET Frameworks:**
- ASP.NET Core, ASP.NET MVC, Entity Framework

### Container Platforms

- Docker
- Kubernetes
- Red Hat OpenShift
- Amazon ECS/EKS
- Azure AKS
- Google GKE

### Infrastructure as Code

- Terraform (.tf files)
- AWS CloudFormation (JSON/YAML)
- Azure Resource Manager (ARM) templates
- Kubernetes manifests (YAML)
- Helm charts
- Google Cloud Deployment Manager

---

## Integration Methods

### 1. Command Line Interface (CLI)

The Snyk CLI is the foundation for local development and CI/CD integration.

#### Installation

**Using npm (recommended):**
```bash
npm install -g snyk
```

**Using Homebrew (macOS):**
```bash
brew tap snyk/tap
brew install snyk
```

**Using Scoop (Windows):**
```bash
scoop bucket add snyk https://github.com/snyk/scoop-snyk
scoop install snyk
```

**Using binary download:**
```bash
# Linux
curl --compressed https://static.snyk.io/cli/latest/snyk-linux -o snyk
chmod +x ./snyk
mv ./snyk /usr/local/bin/


# macOS
curl --compressed https://static.snyk.io/cli/latest/snyk-macos -o snyk
chmod +x ./snyk
mv ./snyk /usr/local/bin/

# Windows (PowerShell)
Invoke-WebRequest -Uri https://static.snyk.io/cli/latest/snyk-win.exe -OutFile snyk.exe
```
<img width="1600" height="775" alt="image" src="https://github.com/user-attachments/assets/c3f8171a-d97f-4bf3-9bfd-5f5cc40999d6" />

#### Authentication

```bash
# Interactive authentication (opens browser)
snyk auth

# Token-based authentication (for CI/CD)
snyk auth <YOUR_API_TOKEN>

# Environment variable
export SNYK_TOKEN=<YOUR_API_TOKEN>
```

#### Basic Commands

**Test for vulnerabilities:**
```bash
# Test current project
snyk test

# Test specific package manager
snyk test --package-manager=npm
snyk test --package-manager=maven


# Test and show all dependency paths
snyk test --all-projects --print-deps

# Test with severity threshold
snyk test --severity-threshold=high

# JSON output for automation
snyk test --json > results.json
```
<img width="1697" height="768" alt="image" src="https://github.com/user-attachments/assets/163e33a4-2b1a-4e13-921e-af1a6cd5c77c" />

<img width="1661" height="798" alt="image" src="https://github.com/user-attachments/assets/99686907-d435-45f1-a1f8-3bce3f42a476" />

**Monitor projects:**
```bash
# Take snapshot and upload to Snyk for continuous monitoring
snyk monitor




# Monitor specific project
snyk monitor --project-name="My-App-Production"

# Monitor with custom organization
snyk monitor --org=my-org-name
```

<img width="1679" height="212" alt="image" src="https://github.com/user-attachments/assets/8645c9ed-df12-4d70-a6f8-eae5ba9b5b30" />

<img width="1919" height="879" alt="image" src="https://github.com/user-attachments/assets/6a07746e-9beb-4b0b-8264-6c3172660d30" />

<img width="1919" height="939" alt="image" src="https://github.com/user-attachments/assets/bad5ea84-dad0-4919-8169-d58468489b3d" />

**Scan source code:**
```bash
# SAST scan
snyk code test

# Scan specific path
snyk code test /path/to/source

# JSON output
snyk code test --json > code-results.json
```

**Scan container images:**
```bash
# Scan Docker image
snyk container test node:14-alpine
snyk container test
snyk container test snykcontainertest:v1

snyk container monitor snykcontainertest:v1

# Scan with Dockerfile for better recommendations
snyk container test node:14-alpine --file=Dockerfile

# Monitor container in Snyk platform
snyk container monitor node:14-alpine
```
<img width="1677" height="758" alt="image" src="https://github.com/user-attachments/assets/075d0d73-7b0e-4f71-bf52-615f98d1ca7f" />

 snyk container monitor snykcontainertest:v1

<img width="1919" height="943" alt="image" src="https://github.com/user-attachments/assets/322f8265-1703-4935-a788-18b79a1bf442" />
**Scan Infrastructure as Code:**
```bash
# Scan Terraform files
snyk iac test terraform/

# Scan Kubernetes manifests
snyk iac test k8s/deployment.yaml

# Scan CloudFormation templates
snyk iac test cloudformation.yaml

# Generate HTML report
snyk iac test --report --report-path=iac-report.html
```

#### Advanced CLI Usage

**Filtering and ignoring:**
```bash
# Ignore specific vulnerability
snyk ignore --id=SNYK-JS-LODASH-590103

# Ignore for specific duration
snyk ignore --id=SNYK-JS-LODASH-590103 --expiry=2026-12-31

# Exclude development dependencies
snyk test --dev=false
```

**Policy files (.snyk):**
```yaml
# .snyk file example
version: v1.25.0
ignore:
  SNYK-JS-LODASH-590103:
    - '*':
        reason: 'Not exploitable in our use case'
        expires: '2026-12-31T00:00:00.000Z'
patch: {}
```

### 2. GitHub Integration

Snyk provides multiple GitHub integration options depending on your plan and requirements.

#### GitHub Cloud App (Recommended)

**Setup:**

1. Navigate to Snyk Web UI → Integrations → GitHub
2. Click "Configure GitHub Cloud App"
3. Authorize Snyk GitHub App
4. Select repositories to monitor
5. Configure import settings

**Features:**
- Fine-grained permissions
- Higher API rate limits
- Repository-level access control
- Automatic PR checks
- Automated fix PRs
- Dependency upgrade PRs

**Configuration Options:**
```json
{
  "pullRequestTestEnabled": true,
  "pullRequestFailOnAnyVulns": false,
  "pullRequestFailOnlySevereVulns": true,
  "autoDependencyUpgradeEnabled": true,
  "autoDependencyUpgradeIgnoredDependencies": ["package-1"],
  "autoRemediationOpenedLimitPerDay": 4
}
```

#### GitHub Actions

**Basic workflow (.github/workflows/snyk.yml):**
```yaml
name: Snyk Security Scan
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run Snyk to check for vulnerabilities
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          args: --severity-threshold=high --fail-on=upgradable

      - name: Upload Snyk results to GitHub Code Scanning
        uses: github/codeql-action/upload-sarif@v3
        if: always()
        with:
          sarif_file: snyk.sarif
```

**Multi-product scan:**
```yaml
name: Snyk Multi-Product Scan
on: [push, pull_request]

jobs:
  snyk:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        scan-type: [open-source, code, container, iac]
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm ci
        if: matrix.scan-type == 'open-source'
      
      - name: Snyk Open Source
        if: matrix.scan-type == 'open-source'
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          command: test
          args: --severity-threshold=high
      
      - name: Snyk Code
        if: matrix.scan-type == 'code'
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          command: code test
      
      - name: Build Docker image
        if: matrix.scan-type == 'container'
        run: docker build -t myapp:latest .
      
      - name: Snyk Container
        if: matrix.scan-type == 'container'
        uses: snyk/actions/docker@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          image: myapp:latest
          args: --file=Dockerfile
      
      - name: Snyk IaC
        if: matrix.scan-type == 'iac'
        uses: snyk/actions/iac@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          file: terraform/
```

#### GitHub Enterprise Integration

**Setup:**

1. In Snyk: Settings → Integrations → GitHub Enterprise
2. Enter GitHub Enterprise URL
3. Create Personal Access Token with `repo` scope
4. Configure integration
5. Import repositories

**Required Permissions:**
- `repo` (full control of private repositories)
- `admin:read:org` (read-only access to organization data)

### 3. GitLab Integration

**Setup via GitLab CI/CD:**

**.gitlab-ci.yml:**
```yaml
include:
  - template: Security/SAST.gitlab-ci.yml
  - template: Security/Dependency-Scanning.gitlab-ci.yml

variables:
  SNYK_TOKEN: $SNYK_TOKEN

stages:
  - test
  - security

snyk_open_source:
  stage: security
  image: snyk/snyk:node
  script:
    - npm ci
    - snyk test --severity-threshold=high --json > snyk-results.json
    - snyk monitor --project-name=$CI_PROJECT_NAME
  artifacts:
    reports:
      dependency_scanning: snyk-results.json
    when: always
  allow_failure: true
  only:
    - merge_requests
    - main

snyk_code:
  stage: security
  image: snyk/snyk:node
  script:
    - snyk code test --sarif-file-output=snyk-code.sarif
  artifacts:
    reports:
      sast: snyk-code.sarif
    when: always
  allow_failure: true

snyk_container:
  stage: security
  image: snyk/snyk:docker
  services:
    - docker:dind
  script:
    - docker build -t $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA .
    - snyk container test $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA --file=Dockerfile
  allow_failure: true

snyk_iac:
  stage: security
  image: snyk/snyk:linux
  script:
    - snyk iac test terraform/ --report
  artifacts:
    paths:
      - snyk-iac-report.html
    when: always
  allow_failure: true
```

### 4. Bitbucket Integration

**Bitbucket Pipelines (bitbucket-pipelines.yml):**
```yaml
pipelines:
  default:
    - step:
        name: Snyk Security Scan
        image: snyk/snyk:node
        script:
          - npm ci
          - snyk auth $SNYK_TOKEN
          - snyk test --severity-threshold=high
          - snyk monitor --project-name=$BITBUCKET_REPO_SLUG
        artifacts:
          - snyk-report.json

  pull-requests:
    '**':
      - step:
          name: Snyk PR Check
          image: snyk/snyk:node
          script:
            - npm ci
            - snyk test --severity-threshold=medium --fail-on=upgradable

  branches:
    main:
      - step:
          name: Snyk Full Scan
          image: snyk/snyk:node
          script:
            - npm ci
            - snyk test --all-projects
            - snyk code test
            - snyk monitor
```

### 5. Azure DevOps Integration

**Azure Pipelines (azure-pipelines.yml):**
```yaml
trigger:
  branches:
    include:
      - main
      - develop

pool:
  vmImage: 'ubuntu-latest'

stages:
  - stage: Security
    jobs:
      - job: SnykScan
        steps:
          - task: NodeTool@0
            inputs:
              versionSpec: '18.x'
            displayName: 'Install Node.js'

          - script: |
              npm ci
            displayName: 'Install dependencies'

          - task: SnykSecurityScan@1
            inputs:
              serviceConnectionEndpoint: 'Snyk'
              testType: 'app'
              severityThreshold: 'high'
              monitorWhen: 'always'
              failOnIssues: true
              projectName: '$(Build.Repository.Name)'
              organization: 'my-org'
            displayName: 'Snyk Open Source Scan'

          - task: SnykSecurityScan@1
            inputs:
              serviceConnectionEndpoint: 'Snyk'
              testType: 'code'
              severityThreshold: 'high'
              failOnIssues: false
            displayName: 'Snyk Code Scan'

          - task: Docker@2
            inputs:
              command: 'build'
              Dockerfile: '**/Dockerfile'
              tags: '$(Build.BuildId)'
            displayName: 'Build Docker image'

          - script: |
              snyk container test myapp:$(Build.BuildId) --file=Dockerfile
            env:
              SNYK_TOKEN: $(SNYK_TOKEN)
            displayName: 'Snyk Container Scan'
```

### 6. IDE Integrations

Snyk provides plugins for major IDEs to catch vulnerabilities during development.

#### Visual Studio Code

**Installation:**
1. Open VS Code Extensions
2. Search for "Snyk Security"
3. Install and authenticate

**Features:**
- Real-time vulnerability scanning as you type
- Inline fix suggestions
- Hover tooltips with vulnerability details
- Code quality and security analysis

**Configuration (settings.json):**
```json
{
  "snyk.enabled": true,
  "snyk.severity": "low",
  "snyk.autoScanOpenSourceSecurity": true,
  "snyk.autoScanCodeSecurity": true,
  "snyk.autoScanCodeQuality": true,
  "snyk.features": {
    "openSourceSecurity": true,
    "codeSecurity": true,
    "codeQuality": true,
    "infrastructureAsCode": true
  }
}
```

#### IntelliJ IDEA / WebStorm / PyCharm

**Installation:**
1. File → Settings → Plugins
2. Search for "Snyk Security"
3. Install and restart
4. Configure with API token

**Features:**
- Vulnerability detection in dependencies
- Code security analysis
- Quick fixes and refactoring suggestions
- Integration with IntelliJ's problem viewer

#### Eclipse

**Installation:**
1. Help → Eclipse Marketplace
2. Search for "Snyk Security"
3. Install and authenticate

### 7. Container Registry Integration

**Docker Hub:**
```yaml
# Snyk monitors your Docker Hub repositories
# Configure in Snyk Web UI:
# Settings → Integrations → Container Registries → Docker Hub
```

**Amazon ECR:**
```bash
# Authenticate Snyk with ECR
snyk container monitor <AWS_ACCOUNT_ID>.dkr.ecr.<region>.amazonaws.com/myapp:latest

# Automated scanning via ECR integration
# Configure in Snyk: Settings → Integrations → Amazon ECR
```

**Google Container Registry:**
```bash
snyk container monitor gcr.io/my-project/myapp:latest
```

**Azure Container Registry:**
```bash
snyk container monitor myregistry.azurecr.io/myapp:latest
```

---

## DevSecOps Implementation Guide

### Phase 1: Planning and Setup

#### 1.1 Define Security Requirements

**Establish security policies:**
```yaml
# snyk-policy.yml
security_policies:
  vulnerability_thresholds:
    critical: 0
    high: 0
    medium: 5
    low: 10
  
  license_policies:
    allowed:
      - MIT
      - Apache-2.0
      - BSD-3-Clause
    disallowed:
      - GPL-3.0
      - AGPL-3.0
  
  compliance_frameworks:
    - OWASP Top 10
    - CIS Benchmarks
    - PCI DSS
```

#### 1.2 Organization Structure

**Create Snyk organization hierarchy:**
```
Company
├── Development
│   ├── Team-Frontend
│   ├── Team-Backend
│   └── Team-Mobile
├── Production
└── Security-Testing
```

**Benefits:**
- Separate development and production monitoring
- Team-specific policies and reporting
- Role-based access control

#### 1.3 Baseline Security Scan

**Initial assessment:**
```bash
#!/bin/bash
# baseline-scan.sh

echo "Running baseline security assessment..."

# Scan all projects
for dir in */; do
  echo "Scanning $dir..."
  cd "$dir"
  
  # Open Source scan
  snyk test --json > "../reports/${dir%/}-opensource.json"
  
  # Code scan
  snyk code test --json > "../reports/${dir%/}-code.json"
  
  # IaC scan if applicable
  if [ -d "terraform" ] || [ -d "k8s" ]; then
    snyk iac test --json > "../reports/${dir%/}-iac.json"
  fi
  
  cd ..
done

echo "Baseline scan complete. Review reports in ./reports/"
```

### Phase 2: Developer Workflow Integration

#### 2.1 Pre-Commit Hooks

**Using Husky and Snyk:**

```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "snyk test --severity-threshold=high"
    }
  }
}
```

**Git hooks:**
```bash
#!/bin/bash
# .git/hooks/pre-commit

echo "Running Snyk security check..."

# Check for high severity vulnerabilities
snyk test --severity-threshold=high --fail-on=upgradable

if [ $? -ne 0 ]; then
  echo "❌ Security vulnerabilities found. Commit rejected."
  echo "Run 'snyk test' for details or 'snyk wizard' for guided remediation."
  exit 1
fi

echo "✅ No critical vulnerabilities found."
exit 0
```

#### 2.2 Local Development Workflow

**Developer checklist:**

1. **Install Snyk CLI and IDE plugin**
   ```bash
   npm install -g snyk
   snyk auth
   ```

2. **Daily security checks**
   ```bash
   # Morning routine
   snyk test
   snyk code test
   ```

3. **Before creating PR**
   ```bash
   # Full scan
   snyk test --all-projects
   snyk code test --severity-threshold=medium
   ```

4. **Monitor dependencies**
   ```bash
   # After adding new packages
   npm install new-package
   snyk test
   ```

#### 2.3 Code Review Process

**PR template with security checklist:**
```markdown
## Security Checklist
- [ ] Snyk scan passed
- [ ] No new high/critical vulnerabilities introduced
- [ ] Dependencies are up to date
- [ ] Secrets scanning passed
- [ ] Code follows secure coding guidelines

## Snyk Results
<!-- Paste Snyk scan summary here -->
```

### Phase 3: CI/CD Pipeline Integration

#### 3.1 Jenkins Integration

**Jenkinsfile:**
```groovy
pipeline {
    agent any
    
    environment {
        SNYK_TOKEN = credentials('snyk-api-token')
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }
        
        stage('Snyk Security Gate') {
            parallel {
                stage('Open Source Scan') {
                    steps {
                        script {
                            sh '''
                                snyk test \
                                  --severity-threshold=high \
                                  --fail-on=upgradable \
                                  --json > snyk-opensource-results.json
                            '''
                        }
                    }
                }
                
                stage('Code Scan') {
                    steps {
                        sh '''
                            snyk code test \
                              --severity-threshold=high \
                              --json > snyk-code-results.json
                        '''
                    }
                }
                
                stage('IaC Scan') {
                    when {
                        expression {
                            fileExists('terraform') || fileExists('k8s')
                        }
                    }
                    steps {
                        sh 'snyk iac test --severity-threshold=high'
                    }
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:${BUILD_NUMBER} .'
            }
        }
        
        stage('Container Scan') {
            steps {
                sh '''
                    snyk container test myapp:${BUILD_NUMBER} \
                      --file=Dockerfile \
                      --severity-threshold=high
                '''
            }
        }
        
        stage('Monitor in Snyk') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                    snyk monitor \
                      --project-name=myapp-${BRANCH_NAME} \
                      --org=my-org
                    
                    snyk container monitor myapp:${BUILD_NUMBER} \
                      --project-name=myapp-container-${BRANCH_NAME}
                '''
            }
        }
        
        stage('Publish Results') {
            steps {
                publishHTML([
                    reportDir: '.',
                    reportFiles: 'snyk-*.json',
                    reportName: 'Snyk Security Report'
                ])
            }
        }
    }
    
    post {
        failure {
            emailext(
                subject: "Security Scan Failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}",
                body: "Security vulnerabilities detected. Check console output for details.",
                to: "security-team@company.com"
            )
        }
    }
}
```

#### 3.2 CircleCI Integration

**.circleci/config.yml:**
```yaml
version: 2.1

orbs:
  snyk: snyk/snyk@1.5.0

workflows:
  security-scan:
    jobs:
      - checkout-and-test
      - snyk-security-gate:
          requires:
            - checkout-and-test
      - build-and-deploy:
          requires:
            - snyk-security-gate

jobs:
  checkout-and-test:
    docker:
      - image: cimg/node:18.0
    steps:
      - checkout
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "package-lock.json" }}
      - run:
          name: Install dependencies
          command: npm ci
      - save_cache:
          paths:
            - node_modules
          key: v1-dependencies-{{ checksum "package-lock.json" }}
      - run:
          name: Run tests
          command: npm test

  snyk-security-gate:
    docker:
      - image: cimg/node:18.0
    steps:
      - checkout
      - restore_cache:
          keys:
            - v1-dependencies-{{ checksum "package-lock.json" }}
      - snyk/scan:
          severity-threshold: high
          fail-on-issues: true
          monitor-on-build: true
          project: ${CIRCLE_PROJECT_REPONAME}
          organization: my-org
      - run:
          name: Snyk Code Scan
          command: |
            npm install -g snyk
            snyk auth $SNYK_TOKEN
            snyk code test --severity-threshold=high
      - store_artifacts:
          path: snyk-results
          destination: security-reports

  build-and-deploy:
    docker:
      - image: cimg/base:stable
    steps:
      - checkout
      - setup_remote_docker
      - run:
          name: Build Docker image
          command: docker build -t myapp:${CIRCLE_SHA1} .
      - run:
          name: Scan container
          command: |
            npm install -g snyk
            snyk auth $SNYK_TOKEN
            snyk container test myapp:${CIRCLE_SHA1} --file=Dockerfile
      - run:
          name: Deploy
          command: ./deploy.sh
```

#### 3.3 Travis CI Integration

**.travis.yml:**
```yaml
language: node_js
node_js:
  - '18'

services:
  - docker

cache:
  directories:
    - node_modules

before_install:
  - npm install -g snyk

install:
  - npm ci

before_script:
  - snyk auth $SNYK_TOKEN

script:
  # Run tests
  - npm test
  
  # Snyk Open Source scan
  - snyk test --severity-threshold=high --fail-on=upgradable
  
  # Snyk Code scan
  - snyk code test --severity-threshold=high
  
  # Build Docker image
  - docker build -t myapp:$TRAVIS_COMMIT .
  
  # Snyk Container scan
  - snyk container test myapp:$TRAVIS_COMMIT --file=Dockerfile

after_success:
  # Monitor in Snyk (only on main branch)
  - |
    if [ "$TRAVIS_BRANCH" == "main" ]; then
      snyk monitor --project-name=myapp-production
      snyk container monitor myapp:$TRAVIS_COMMIT
    fi

notifications:
  slack:
    rooms:
      - secure: "encrypted-slack-webhook"
    on_failure: always
    on_success: change
```

#### 3.4 Security Gate Configuration

**Implement quality gates:**

```yaml
# snyk-gate-config.yml
gates:
  development:
    severity_threshold: medium
    fail_on: all
    allow_failure: false
  
  staging:
    severity_threshold: high
    fail_on: upgradable
    allow_failure: false
  
  production:
    severity_threshold: critical
    fail_on: all
    allow_failure: false
    require_manual_approval: true

policies:
  block_on:
    - critical_vulnerabilities: true
    - high_vulnerabilities: true
    - gpl_licenses: true
    - known_malware: true
  
  warn_on:
    - medium_vulnerabilities: true
    - outdated_dependencies: true
```

**Implementation example:**
```bash
#!/bin/bash
# security-gate.sh

ENVIRONMENT=${1:-development}
CONFIG_FILE="snyk-gate-config.yml"

# Parse configuration (requires yq)
SEVERITY=$(yq e ".gates.$ENVIRONMENT.severity_threshold" $CONFIG_FILE)
FAIL_ON=$(yq e ".gates.$ENVIRONMENT.fail_on" $CONFIG_FILE)

echo "Running security gate for $ENVIRONMENT environment"
echo "Severity threshold: $SEVERITY"

# Run Snyk scan
snyk test \
  --severity-threshold=$SEVERITY \
  --fail-on=$FAIL_ON \
  --json > snyk-results.json

EXIT_CODE=$?

# Parse results
CRITICAL=$(jq '.vulnerabilities | map(select(.severity=="critical")) | length' snyk-results.json)
HIGH=$(jq '.vulnerabilities | map(select(.severity=="high")) | length' snyk-results.json)

echo "Found $CRITICAL critical and $HIGH high severity vulnerabilities"

# Apply policies
if [ $CRITICAL -gt 0 ] || [ $HIGH -gt 0 ]; then
  echo "❌ Security gate failed. Blocking deployment."
  exit 1
fi

echo "✅ Security gate passed"
exit 0
```

### Phase 4: Continuous Monitoring

#### 4.1 Project Monitoring Setup

**Automated monitoring:**
```bash
#!/bin/bash
# setup-monitoring.sh

PROJECTS=(
  "frontend"
  "backend-api"
  "mobile-app"
  "infrastructure"
)

for project in "${PROJECTS[@]}"; do
  echo "Setting up monitoring for $project..."
  
  cd $project
  
  # Monitor open source dependencies
  snyk monitor \
    --project-name="$project-${ENVIRONMENT}" \
    --org=my-org \
    --remote-repo-url=https://github.com/myorg/$project
  
  # Monitor container if Dockerfile exists
  if [ -f "Dockerfile" ]; then
    docker build -t $project:latest .
    snyk container monitor $project:latest \
      --project-name="$project-container-${ENVIRONMENT}"
  fi
  
  cd ..
done

echo "Monitoring setup complete"
```



### 4. Reachability Analysis

**Enable reachable vulnerabilities analysis:**

```bash
# Test with reachability analysis (Java/JavaScript)
snyk test --reachable

# Filter to show only reachable vulnerabilities
snyk test --reachable --reachable-vulns
```

### 5. Container Base Image Recommendations

**Get base image recommendations:**

```bash
# Get recommendations for better base images
snyk container test node:14-alpine --file=Dockerfile --json | \
  jq '.baseImageRemediation.advice[]'
```

**Example output:**
```json
{
  "message": "Base image 'node:14-alpine' has 23 vulnerabilities",
  "bold": [
    "Base image 'node:18-alpine' has 3 vulnerabilities"
  ],
  "color": "green"
}
```

---

## Best Practices

### 1. Shift-Left Security

**Implement security at every stage:**

```
Developer Workstation → Pre-commit → PR Check → CI/CD → Runtime Monitoring
        ↓                   ↓          ↓          ↓              ↓
   IDE Plugin        Git Hooks    PR Gates   Security    Container Registry
   Snyk CLI                                   Gates       Scanning
```

### 2. Vulnerability Management

**Prioritization framework:**

1. **Critical + Exploitable**: Fix immediately (< 1 day)
2. **High + Exploitable**: Fix within 1 week
3. **High + No Exploit**: Fix within 1 month
4. **Medium**: Fix within 3 months
5. **Low**: Review quarterly

### 3. Developer Education

**Security champions program:**

```markdown
## Security Champion Responsibilities

1. **Weekly Security Reviews**
   - Review Snyk findings
   - Triage new vulnerabilities
   - Assign remediation tasks

2. **Developer Training**
   - Monthly security workshops
   - Secure coding guidelines
   - Snyk tool training

3. **Policy Enforcement**
   - Ensure policy compliance
   - Review security exceptions
   - Update security policies

4. **Metrics Reporting**
   - Track security metrics
   - Report to management
   - Identify trends
```

### 4. False Positive Management

**Handle false positives effectively:**

```bash
# Mark as false positive with detailed reason
snyk ignore --id=SNYK-JS-EXAMPLE-123456 \
  --reason="False positive: Function not used in production code path" \
  --path="dev-dependency > nested-package" \
  --expiry=2027-01-01
```


## Troubleshooting

### Common Issues and Solutions

#### 1. Authentication Issues

**Problem:** `Unauthorized` error

**Solution:**
```bash
# Verify token
snyk auth

# Check token validity
snyk whoami

# Use environment variable
export SNYK_TOKEN="your-token-here"
snyk test
```

#### 2. CLI Not Finding Manifest Files

**Problem:** CLI doesn't detect package manager

**Solution:**
```bash
# Explicitly specify package manager
snyk test --package-manager=npm

# Scan all subprojects
snyk test --all-projects

# Specify manifest file location
snyk test --file=backend/package.json
```

#### 3. False Positives

**Problem:** Vulnerabilities in non-production code

**Solution:**
```bash
# Exclude development dependencies
snyk test --dev=false

# Use .snyk file for permanent exclusions
# See Project-Level Policies section
```

#### 4. Rate Limiting

**Problem:** API rate limit exceeded

**Solution:**
```bash
# Use test command instead of monitor for CI
snyk test

# Reduce frequency of scans
# Use caching in CI/CD

# Contact Snyk for rate limit increase
```

#### 5. Container Scan Failures

**Problem:** Cannot scan private registry images

**Solution:**
```bash
# Authenticate with registry first
docker login myregistry.com

# Use --username and --password flags
snyk container test myregistry.com/myapp:latest \
  --username=$REGISTRY_USER \
  --password=$REGISTRY_PASS

# Or use docker credential helper
snyk container test myregistry.com/myapp:latest
```

#### 6. Large Monorepo Performance

**Problem:** Scanning takes too long

**Solution:**
```bash
# Scan specific directories
snyk test --file=backend/package.json
snyk test --file=frontend/package.json

# Use parallel scanning in CI
parallel snyk test --file={} ::: */package.json

# Enable gradle scan optimization
snyk test --gradle-sub-project=specific-module
```

#### 7. Proxy Configuration

**Problem:** CLI cannot reach Snyk API behind corporate proxy

**Solution:**
```bash
# Set HTTP proxy
export HTTP_PROXY=http://proxy.company.com:8080
export HTTPS_PROXY=http://proxy.company.com:8080

# For authenticated proxy
export HTTP_PROXY=http://user:pass@proxy.company.com:8080

# No proxy for certain domains
export NO_PROXY=localhost,127.0.0.1,.company.com
```

### Debug Mode

**Enable verbose logging:**

```bash
# Maximum debug output
snyk test --debug

# Save debug logs to file
snyk test --debug > debug.log 2>&1

# Print JSON for parsing
snyk test --json | jq .
```

### Getting Help

**Resources:**

1. **Snyk Documentation**: https://docs.snyk.io
2. **Support Portal**: https://support.snyk.io
3. **Community Forum**: https://community.snyk.io
4. **GitHub Issues**: https://github.com/snyk/cli/issues
5. **Status Page**: https://status.snyk.io

**Contact Support:**
yakubiliyas12@gmail.com

## Conclusion

Implementing Snyk in your DevSecOps pipeline provides comprehensive security coverage across the entire SDLC. This guide has covered:

- **Core Snyk capabilities** across Open Source, Code, Container, and IaC
- **Multiple integration methods** for SCM, CI/CD, and developer tools
- **DevSecOps implementation** from planning to incident response
- **Advanced features** like custom rules and SBOM generation
- **Best practices** for vulnerability management and developer education

### Next Steps

1. **Start Small**: Begin with CLI and IDE integration
2. **Expand Coverage**: Add CI/CD integration
3. **Implement Monitoring**: Set up continuous monitoring
4. **Refine Policies**: Customize security policies for your organization
5. **Measure Progress**: Track security metrics and improvement over time

### Additional Resources

- **Snyk Learn**: Free security education platform (https://learn.snyk.io)
- **Snyk Advisor**: Package health scores (https://snyk.io/advisor)
- **Vulnerability Database**: https://security.snyk.io
- **API Documentation**: https://snyk.docs.apiary.io

---

**Document Version**: 1.0  
**Last Updated**: January 31, 2026  
**Author**: DevSecOps Engineer (Yakub Ilyas)  
