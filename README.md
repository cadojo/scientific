# ✏️ `scientific`

*Workflows for technical writing, editing, publishing, and hosting.*

## Envisioned Usage

Users write a document in a supported format, and use a GitHub Webhook (through an open-source bot) to *submit* the document to a document registry review.
The review occurs through a GitHub pull request, where the document source is automatically compiled into output formats, which are attached to the pull request as build artifacts.
Once the pull request merges, the final build artifacts are uploaded to the document server.

### Writing

Document writers can submit document source as a single Markdown file with additional resource files, or as a Quarto project, or as a LaTeX project.
Quarto projects are encouraged because they can automatically accommodate many document source formats.
Users should write their documents in their own repositories, and submit their document source with a GitHub comment on a commit.
For example: `@robot submit quarto /path/to/quarto/project`.

### Review

Once the document server bot receives the `submit` command, it will copy all project files and create a pull request on the document server GitHub project; there, CI will build the project (in accordance with the provided project type, in this case Quarto) and save the compiled artifacts for human review.

### Hosting

Once the document review passes, the pull request will be merged into the `source` branch of the document server repository.
The compiled artifacts will be committed to the `published` branch, which will automatically populate the document server website.

## Pipeline Components

The following software components will need to be developed to achieve the writing to hosting pipeline described above.

### Writing

-   LaTeX templates
-   Quarto templates

### Review

-   GitHub App (bot with webhook integration)
-   GitHub Actions
-   GitHub Workflows

### Hosting

-   GitHub repository
-   Quarto website