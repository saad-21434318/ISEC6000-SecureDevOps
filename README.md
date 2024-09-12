<h1>ISEC6000-SecureDevOps</h1>

<p>This repository is part of the ISEC6000 course project, focusing on deploying the Saleor e-commerce platform in a secure and scalable DevOps environment. It leverages Kubernetes, Docker, and cloud-native tools, adhering to best practices for container security, and vulnerability scanning.</p>
<h2>Table of Contents</h2>
<ul>
  <li><a href="#project-overview">Project Overview</a></li>
  <li><a href="#project-structure">Project Structure</a></li>
  <li><a href="#setup-instructions">Setup Instructions</a></li>
  <ul>
    <li><a href="#kubernetes-cluster-setup">Kubernetes Cluster Setup</a></li>
    <li><a href="#saleor-deployment">Saleor Deployment</a></li>
  </ul>
  <li><a href="#security-implementations">Security Implementations</a></li>
  <li><a href="#vulnerability-scanning">Vulnerability Scanning</a></li>
</ul>

<h2 id="project-overview">Project Overview</h2>
<p>The ISEC6000-SecureDevOps project focuses on building a secure and scalable architecture for deploying the Saleor e-commerce platform. The project includes multiple services (Saleor API, Dashboard, PostgreSQL, Redis) configured in a Dockerized and Kubernetes-managed environment. It follows DevOps practices to ensure a seamless and secure deployment process.</p>

<h2 id="project-structure">Project Structure</h2>
<ul>
  <li><strong>docker-compose.yml</strong>: Defines the configuration for deploying Saleor platform services using Docker Compose.</li>
  <li><strong>bin/trivy</strong>: Trivy vulnerability scanner binary for scanning container images.</li>
  <li>Kubernetes Configurations: Files related to managing Saleor services in a Kubernetes cluster.</li>
</ul>

<h2 id="setup-instructions">Setup Instructions</h2>

<h3 id="kubernetes-cluster-setup">Kubernetes Cluster Setup</h3>
<p>This project uses <strong>kind</strong> (Kubernetes in Docker) to manage a local Kubernetes cluster.</p>

<ol>
  <li><strong>Install <code>kind</code> and <code>kubectl</code>:</strong>
    <ul>
      <li><a href="https://kind.sigs.k8s.io/docs/user/quick-start/">Kind Installation Guide</a></li>
      <li><a href="https://kubernetes.io/docs/tasks/tools/install-kubectl/">Kubectl Installation Guide</a></li>
    </ul>
  </li>
  <li><strong>Create a Kubernetes Cluster:</strong>
    <pre><code>kind create cluster --name saleor-cluster</code></pre>
  </li>
  <li><strong>Configure kubectl to use the <code>kind</code> cluster:</strong>
    <pre><code>kubectl cluster-info --context kind-saleor-cluster</code></pre>
  </li>
  <li><strong>Deploy Saleor Services:</strong>
    Follow the <a href="https://github.com/saleor/saleor-platform">Saleor platform deployment guide</a> or use the forked version for deployment.
  </li>
</ol>

<h3 id="saleor-deployment">Saleor Deployment</h3>
<ol>
  <li>Clone the <a href="https://github.com/saleor/saleor-platform">Saleor platform repository</a> or use your forked version.</li>
  <li>Modify the <code>docker-compose.yml</code>:
    <ul>
      <li>Specify port mappings (e.g., Dashboard on port 9002).</li>
      <li>Define dependencies between services (e.g., PostgreSQL, Redis).</li>
    </ul>
  </li>
  <li>Deploy Saleor:
    <pre><code>docker-compose up -d</code></pre>
  </li>
</ol>

<h2 id="security-implementations">Security Implementations</h2>

<h3>Non-Root Containers</h3>
<p>All containers are configured to run as non-root users. This is specified by assigning user IDs in the <code>docker-compose.yml</code> file.</p>

<h3>Secure Base Images</h3>
<p>The images used (Saleor, Redis, PostgreSQL) are official and verified, ensuring a secure base for deployments.</p>

<h3>Resource Limits</h3>
<p>Each service is configured with CPU and memory limits to prevent resource exhaustion and mitigate potential denial-of-service attacks.</p>

<h2 id="vulnerability-scanning">Vulnerability Scanning</h2>
<p>Trivy is employed to scan Docker images for vulnerabilities.</p>

<ol>
  <li><strong>Install Trivy:</strong>
    <pre><code>sudo snap install trivy</code></pre>
  </li>
  <li><strong>Run a Vulnerability Scan:</strong>
    <pre><code>trivy image ghcr.io/saleor/saleor:3.20</code></pre>
  </li>
  <li>Document any vulnerabilities found and remedial actions taken to address them.</li>
</ol>
