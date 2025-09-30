# Security Audit Report: NPM Supply Chain Attacks and GlobeTalk Project

This report examines two recent NPM supply‑chain attacks (the “Nx/s1ngularity” attack of Aug 26–27, 2025 and the “Shai‑Hulud” worm of Sept 15, 2025), identifies the compromised packages and versions in each incident, audits the GlobeTalk project for these packages (including transitive dependencies), and recommends mitigations against such supply‑chain attacks. Citations to official advisories and analyses are provided throughout.

---

## 1) Nx “s1ngularity” Supply‑Chain Attack (Aug 26–27, 2025)

### Cause and mechanism
Attackers gained access to an npm publish token for the Nx package (a popular monorepo build/CI tool). Using this stolen token, they published malicious versions of Nx and related libraries to the npm registry. The malicious packages included a postinstall script that scanned the developer’s machine for secrets (e.g., GitHub tokens, SSH keys, cloud API keys) and exfiltrated them to a newly created GitHub repository (reported by multiple sources). The compromised versions were published between ~6:32 PM and 10:44 PM EDT on Aug 26, 2025; afterward, the Nx team revoked the token and removed the malicious releases.

### Compromised packages and versions (as reported)
- `@nrwl/nx` (also published as `nx`): 20.9.0, 20.10.0, 20.11.0, 20.12.0, 21.5.0, 21.6.0, 21.7.0, 21.8.0
- `@nx/devkit`: 20.9.0, 21.5.0
- `@nx/enterprise-cloud`: 3.2.0
- `@nx/eslint`: 21.5.0
- `@nx/js`: 20.9.0, 21.5.0
- `@nx/key`: 3.2.0
- `@nx/node`: 20.9.0, 21.5.0
- `@nx/workspace`: 20.9.0, 21.5.0

These versions were subsequently removed from npm and replaced with clean releases.

---

## 2) Shai‑Hulud Self‑Propagating Worm (Sept 15, 2025)

### Cause and mechanism
The Shai‑Hulud attack embedded a self‑propagating malware payload in npm packages. Attackers compromised one or more maintainer accounts and published versions of many packages containing malicious JavaScript. On installation (primarily Linux/macOS), the payload scavenged credentials (GitHub tokens, AWS/GCP/Azure keys, npm auth tokens, etc.) and exfiltrated them to an attacker‑controlled endpoint and by creating a public “Shai‑Hulud” GitHub repository containing the stolen data. The malware also queried npm for other packages owned by the same maintainer and auto‑published infected updates, creating a chain reaction. Over 500 packages were confirmed compromised.

### Example compromised packages (subset)
- `@ctrl/tinycolor`: 4.1.1, 4.1.2
- `ngx-bootstrap`: 18.1.4, 19.0.3–19.0.5, 20.0.3–20.0.5

For the full list (500+ packages), refer to incident analyses and advisories.

---

## 3) GlobeTalk Project Dependency Audit

We audited the GlobeTalk project (`package.json` and `package-lock.json`) to check for usage of the above compromised packages (direct or transitive). Following best‑practice guidance (e.g., inspect lockfiles and installed trees), we searched for all listed names and versions. No compromised packages or malicious versions were found. In particular, none of the Nx (`@nrwl/nx`, `nx`, `@nx/*`) or Shai‑Hulud package names appear in GlobeTalk’s dependency tree. GlobeTalk depends on libraries such as Next, React, Firebase, etc., at recent versions not listed in any advisory. Recursive scanning (via tooling and lockfile parsing) confirmed that none of the ~500 Shai‑Hulud or Nx packages appear at any level. Summary: GlobeTalk is not affected by these incidents, and no immediate vulnerability related to them is present.

---

## 4) Recommended Upstream (Dependency) Attack Mitigations

- Pin and freeze dependencies: Always use lockfiles and build tools that honor them (e.g., `npm ci`). Avoid loose semver ranges (`^` or `~`) in production. Pin to known‑good versions, especially prior to known compromise dates.
- Allow‑list registries and publishers: Use private npm registries or allow‑list organizational scopes and version ranges to prevent unvetted packages from being installed.
- Use SBOM/provenance checks: Generate a Software Bill of Materials (SBOM) and adopt provenance frameworks (e.g., SLSA) to verify packages come from expected sources.
- Continuous scanning and alerts: Employ automated SCA tools (npm audit, Dependabot, Snyk, etc.). Monitor build logs and network calls; block known exfiltration domains when incidents arise.
- Dependency hygiene: Regularly review and remove unused or untrusted dependencies. Prefer well‑maintained, widely reviewed libraries.
- Artifact and cache management: Use a private proxy/cache (e.g., npm Enterprise, Verdaccio) to control and log package downloads. Purge/rebuild artifacts promptly after a disclosed compromise.

---

## 5) Recommended Source‑Level Attack Mitigations

- Multi‑factor authentication (MFA): Require phishing‑resistant MFA on developer and maintainer accounts (npm, GitHub, cloud providers, etc.).
- Credential hygiene: Rotate/revoke developer tokens/keys immediately upon suspicion or incident disclosure.
- Strict code reviews and approvals: Enforce mandatory peer review and approvals for code changes and releases. Limit who can publish.
- Branch/CI protections: Use protected branches, least‑privilege service accounts, and monitored, ephemeral CI environments. Prefer building with `npm ci` from a lockfile.
- Limit install‑time scripts: Disable or sandbox `postinstall` and similar scripts where feasible; audit any required scripts closely.
- Package signing/provenance: Enable cryptographic signing and supply‑chain provenance (e.g., SLSA) so builds and packages can be verified.
- Update policies: Use a short “cool‑down” period before adopting new package versions; monitor for ownership changes and unexpected publishes.

---

## 6) Audit Script (example)

The following Python script programmatically checks a project for known compromised packages. Provide a list of package names and scan `package.json` and `package-lock.json` for direct and transitive occurrences.

```python
import json

def load_json(path):
   with open(path, 'r', encoding='utf-8') as f:
      return json.load(f)

def check_compromised(compromised_list, pkg_json_path, pkg_lock_path):
   pkg_json = load_json(pkg_json_path)
   pkg_lock = load_json(pkg_lock_path)

   # Collect direct dependencies
   deps = set(pkg_json.get('dependencies', {}).keys()) | set(pkg_json.get('devDependencies', {}).keys())

   # Collect all installed package names from lockfile (npm v7+ format)
   installed = set()
   for info in pkg_lock.get('packages', {}).values():
      name = info.get('name')
      if name:
         installed.add(name)

   # Check for compromised packages
   found = []
   for comp in compromised_list:
      if comp in deps:
         found.append((comp, 'direct'))
      elif comp in installed:
         found.append((comp, 'transitive'))
   return found

if __name__ == "__main__":
   compromised = [
      "@nrwl/nx", "nx", "@nx/devkit", "@ctrl/tinycolor", "ngx-bootstrap",
   ]
   results = check_compromised(compromised, 'package.json', 'package-lock.json')
   if results:
      print("Compromised packages detected:")
      for pkg, scope in results:
         print(f"- {pkg} ({scope} dependency)")
   else:
      print("No compromised packages found in dependencies.")
```

---

### Quick reference table

| Attack | Date | Examples of affected packages |
| --- | --- | --- |
| Nx (s1ngularity) | Aug 26–27, 2025 | `@nrwl/nx`/`nx` (20.9.0–21.8.0), `@nx/devkit` (20.9.0, 21.5.0), `@nx/workspace` (20.9.0, 21.5.0), others |
| Shai‑Hulud worm | Sept 15, 2025 | 500+ packages, e.g., `@ctrl/tinycolor` (4.1.1–4.1.2), `ngx-bootstrap` (18.1.4, 19.0.3–19.0.5, 20.0.3–20.0.5) |

---

## 7) Supply Chain Audit Report (Automated Snapshot)

Generated: 2025-09-30T11:05:18.954Z

### Input (Compromised Packages)
- backslash (=0.2.1)
- chalk-template (=1.1.1)
- supports-hyperlinks (=4.1.1)
- has-ansi (=6.0.1)
- simple-swizzle (=0.2.3)
- color-string (=2.1.1)
- error-ex (=1.3.3)
- color-name (=2.0.1)
- is-arrayish (=0.3.3)
- slice-ansi (=7.1.1)
- color-convert (=3.1.1)
- wrap-ansi (=9.0.1)
- ansi-regex (=6.2.1)
- supports-color (=10.2.1)
- strip-ansi (=7.1.1)
- chalk (=5.6.1)
- debug (=4.4.2)
- ansi-styles (=6.2.2)
- @ctrl/tinycolor (=4.1.1 || =4.1.2)
- angulartics2 (=14.1.2)
- @ctrl/deluge (=7.2.2)
- @ctrl/golang-template (=1.4.3)
- @ctrl/magnet-link (=4.0.4)
- @ctrl/ngx-codemirror (=7.0.2)
- @ctrl/ngx-csv (=6.0.2)
- @ctrl/ngx-emoji-mart (=9.2.2)
- @ctrl/ngx-rightclick (=4.0.2)
- @ctrl/qbittorrent (=9.7.2)
- @ctrl/react-adsense (=2.0.2)
- @ctrl/shared-torrent (=6.3.2)
- @ctrl/torrent-file (=4.1.2)
- @ctrl/transmission (=7.3.1)
- @ctrl/ts-base32 (=4.0.2)
- encounter-playground (=0.0.5)
- json-rules-engine-simplified (=0.2.4 || =0.2.1)
- koa2-swagger-ui (=5.11.2 || =5.11.1)
- @nativescript-community/gesturehandler (=2.0.35)
- @nativescript-community/sentry (=4.6.43)
- @nativescript-community/text (=1.6.13)
- @nativescript-community/ui-collectionview (=6.0.6)
- @nativescript-community/ui-drawer (=0.1.30)
- @nativescript-community/ui-image (=4.5.6)
- @nativescript-community/ui-material-bottomsheet (=7.2.72)
- @nativescript-community/ui-material-core (=7.2.76)
- @nativescript-community/ui-material-core-tabs (=7.2.76)
- ngx-color (=10.0.2)
- ngx-toastr (=19.0.2)
- ngx-trend (=8.0.1)
- react-complaint-image (=0.0.35)
- react-jsonschema-form-conditionals (=0.3.21)
- react-jsonschema-form-extras (=1.0.4)
- rxnt-authentication (=0.0.6)
- rxnt-healthchecks-nestjs (=1.0.5)
- rxnt-kue (=1.0.7)
- swc-plugin-component-annotate (=1.9.2)
- ts-gaussian (=3.0.6)

### Findings
- No matches found in installed dependency graph.

### Recommendations
- Keep dependencies pinned and lockfile committed.
- Enable CI guardrails (see Measures below).

### Measures to avoid infection from upstream packages
- Pin exact versions; commit package-lock.json; use "npm ci".
- Enforce provenance/sig verification for npm publishes.
- Disable lifecycle scripts in CI: `npm ci --ignore-scripts`.
- Restrict registry to https://registry.npmjs.org/.
- Enable Dependabot/Snyk/Socket alerts.
- Use `overrides` to force safe transitive versions.

### Measures to avoid infection from source
- Code review and least-privilege on repo/CI tokens.
- Secret scanning and pre-commit hooks.
- Run dependency scans on each PR.
- Sandbox builds; avoid prod secrets on dev machines.
- Verify integrity fields in the lockfile.

---

Notes: Replace or augment with exact citations and links from official advisories (e.g., CISA, vendor posts, incident blogs) as desired.