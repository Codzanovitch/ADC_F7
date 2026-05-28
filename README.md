# ADC_F7
Drivers for a dev board

## GitHub & Documentation Best Practices

This guide is intended for team members to ensure consistency and efficiency when working with this repository.

### 1. GitHub Best Practices

#### Branching
- **Main Branch:** The `main` branch should always be stable and deployable. Never commit directly to `main`.
- **Feature Branches:** Create a new branch for every task or bug fix.
  - Name your branch descriptively: `feature/adc-init`, `fix/interrupt-timing`.
- **Stay Updated:** Regularly pull the latest changes from `main` into your feature branch to resolve conflicts early.

#### Commits
- **Atomic Commits:** Make small, logical commits. Each commit should do one thing.
- **Commit Messages:** Write clear, concise messages.
  - Good: `feat: add ADC initialization function`
  - Bad: `fixed stuff` or `update`
- **Prefixes:** Use prefixes like `feat:`, `fix:`, `docs:`, or `refactor:` to categorize changes.

#### Pull Requests (PRs)
- **Review:** Always create a Pull Request to merge your feature branch into `main`.
- **Description:** Explain what changes were made and why. Link any relevant issues.
- **Feedback:** Be open to feedback and address comments before merging.

### 2. Repository Content & File Restrictions

To maintain a clean and legal repository, please adhere to the following rules:

- **What to Upload:** Source code (`.c`, `.h`), build scripts, and Markdown documentation (`.md`).
- **Reference Manuals & Datasheets:** Prefer providing **links** to official manufacturer websites (e.g., STMicroelectronics) in your documentation.
  - **No Direct Root Uploads:** Do not upload these PDFs to the root directory.
  - **Fallback:** If no stable link is available, you may upload the PDF as a static file to a dedicated `docs/external/` or `assets/` folder. Always prefer linking over uploading to respect copyright and keep the repository size manageable.
- **No Word Documents:** Documentation must be written in **Markdown (`.md`)**. Do **NOT** upload `.docx` or other binary document formats. Markdown is easier to track in version control and can be rendered directly by GitHub.
- **Static Files (Images/Assets):** If you need to include images or diagrams in your documentation, place them in an `assets/` or `docs/images/` folder. Use relative paths in your Markdown files to display them. Keep these files as small as possible.
- **Binary Files & Build Artifacts:** Do **NOT** upload compiled binaries (`.bin`, `.out`, `.elf`, `.exe`), object files (`.o`), or temporary build folders (e.g., `Debug/`, `Release/`). These should be managed by the `.gitignore` file. GitHub is for source code, not generated artifacts.

### 3. Documentation Best Practices

#### Markdown over Word
- **Text-Based Only:** Always use Markdown for documentation. This allows us to see exactly what changed during code reviews.
- **Keep it Updated:** If you change how something works, update the documentation.
- **Structure:** Use headers (`#`, `##`, `###`) to organize information.
- **Formatting:** Use code blocks (```) for snippets and bold/italics for emphasis.

#### Markdown Formatting Rules
To keep our documentation consistent and professional, follow these basic Markdown rules:
- **Headers:** Use `#` for the main title, `##` for sections, and `###` for subsections. Always put a space after the `#`.
- **Lists:** Use `-` or `*` for unordered lists and `1.` for ordered lists.
- **Code Blocks:** Use triple backticks (```) for code snippets. Specify the language for syntax highlighting (e.g., ```c for C code).
- **Inline Code:** Use single backticks (`) for variable names or short commands within a sentence.
- **Bold & Italic:** Use `**bold**` for emphasis and `*italic*` for subtle highlights.
- **Links:** Use `[Link Text](URL)` for external links or file paths.
- **Images:** Use `![Alt Text](path/to/image.png)`. Ensure images are stored in the `assets/` folder.
- **Horizontal Rules:** Use `---` to separate major sections visually.

#### Code Documentation
- **Comments:** Explain *why* something is done, not just *what* the code does. The code itself should be readable enough to show *what* is happening.
- **Function Headers:** Document functions with their purpose, parameters, and return values.
- **Consistency:** Follow the existing naming conventions and style in the codebase.

### 3. Workflow Summary
1. `git pull origin main` (Start with the latest code)
2. `git checkout -b feature/your-feature-name` (Create a branch)
3. *Make changes and commit*
4. `git push origin feature/your-feature-name` (Upload your branch)
5. Create a Pull Request on GitHub.
6. Merge after approval.
