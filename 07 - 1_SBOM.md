#### SBOM - Software Bill of Materials

- `SBOM` documents everything that goes inside the software.
  - For example:
    - Licenses
    - version
    - Patches
    - Software Components
    - etc

- Formats:
  - CycloneDX
  - SPDX

- SBOMs enable:
  - Better management of software dependencies,
  - Improved compliance with licensing requirements,
  - Quick responses to security threats.

- Tools:
  - For the test focus on BOM <https://github.com/kubernetes-sigs/bom>:
    ```
    bom generate --output=nginx.spdx --image registry.k8s.io/kube-apiserver:v1.21.0
    ```
  - Syft <https://github.com/anchore/syft>
    - `curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin`
    - `syft --version`
    - spdx output:
      - `syft scan docker.io/library/nginx:latest -o spdx-json`
    - cyclonedx output:
      - `syft scan docker.io/library/nginx:latest -o cyclonedx-json`
  - Grype <https://github.com/anchore/grype>
    - `curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sh -s -- -b /usr/local/bin`
    - Analize and generate a vulnerability report(json output):
      - `grype sbom:/path/sbom-file.json -o json`
    - Looking at the one vulnerability
      - `cat grype-report.json | jq -e '.matches[] | select(.vulnerability.id == "CVE-2018-x")'`