## 📦 Library Publishing Workflow
This repository contains a shared collection of Spring Boot-based libraries, including:

string-lib – Utilities and helpers for string manipulation

integer-lib – Utilities for integer operations

open-api-spec – Centralized OpenAPI specifications for integration with services

To streamline versioning and publishing, this repository includes a GitHub Actions workflow to automate publishing packages to GitHub Packages.

### 🚀 What the Workflow Does
The Publish package to GitHub Packages workflow performs the following tasks:

1. Manual Trigger via GitHub UI – You can manually trigger the pipeline using workflow_dispatch with a version_type input (either MAJOR or MINOR).

2. Checkout Code – Uses the GitHub token to securely checkout the code.

3. Set Up JDK 17 – Ensures Java 17 (Corretto) is used for the build.

4. Publish to GitHub Packages – Runs mvn deploy to publish your library modules to GitHub's package registry.

5. Determine Current Version – Extracts the current version from pom.xml.

6. Increment Version – Based on input:

        MAJOR: Increments major version (e.g., 1.2.3 → 2.0.0)

        MINOR: Increments minor version (e.g., 1.2.3 → 1.3.0)

7. Create Pull Request – A pull request is automatically opened to reflect the version bump with:

8. Updated pom.xml files A commit message like: "CI Increment Version from '1.0.0' to '1.1.0'"

9. PR labeled as merge-lib

### ✅ How to Publish a New Version
1. Go to the Actions tab in GitHub.

2. Select the workflow titled “Publish package to GitHub Packages”.

3. Click “Run workflow”.

Choose either:

        MAJOR – For breaking changes or significant updates.

        MINOR – For backward-compatible changes or feature additions.

#### The pipeline will:

  * Deploy the updated libraries.

  * Increment the version.

  * Create a new pull request with version changes.

Once the PR is merged, the new version will be available on GitHub Packages.

<img width="1723" alt="image" src="https://github.com/user-attachments/assets/c3b75388-8fe9-4287-b2f1-902fc8e0ef44" />


### 🧪 Notes
1. This workflow uses the Maven build-helper and versions plugins to parse and update project versions.

2. All published packages will be available under the GitHub Packages section of this repository.

3. You must have a valid GH_PAT and GITHUB_TOKEN configured in the repository secrets for this workflow to function correctly.


## How to add the library in your application
1. Goto github packages page,
<img width="1651" alt="image" src="https://github.com/user-attachments/assets/c30a9e71-3919-4f7a-b3cc-789ba0b6f867" />

2. Select the lib which you want to add. You will find the dependencies tag,
<img width="1644" alt="image" src="https://github.com/user-attachments/assets/618dfed9-0304-4129-9221-f4b459889214" />

3. Add the dependency in your application.

4. Configure the repository element in your .m2 file to downlaod the libaries published.
```
<repositories>
                <repository>
                    <id>github</id>
                    <url>https://maven.pkg.github.com/SanthoshKumar-Ravi/spring-boot-library</url>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                  </releases>
                </repository>
            </repositories>
```
   
