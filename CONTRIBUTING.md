# 🤝 Contributing to MyNotes

Thank you for your interest in contributing to **MyNotes**! This repository is maintained by [ZenYukti](https://zenyukti.in) community, and we welcome contributions from students, educators, and anyone passionate about sharing knowledge.

Our mission: **Learn. Build. Share.** 💙

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Contribution Workflow](#contribution-workflow)
- [Repository Structure Guidelines](#repository-structure-guidelines)
- [Content Guidelines](#content-guidelines)
- [Updating the README](#updating-the-readme)
- [Creating Interactive HTML Notes](#creating-interactive-html-notes)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Pull Request Process](#pull-request-process)
- [Review Process](#review-process)
- [Questions?](#questions)

---

## 📜 Code of Conduct

By participating in this project, you agree to:
- Be respectful and inclusive
- Provide constructive feedback
- Focus on what's best for the community
- Show empathy towards other contributors
- Maintain academic integrity (no plagiarism)

---

## 💡 How Can I Contribute?

You can contribute in several ways:

1. **📝 Add New Notes**: Create study materials for new subjects or units
2. **✨ Improve Existing Notes**: Fix errors, add examples, enhance explanations
3. **🎨 Create Interactive HTML**: Build LastMinuteRevision HTML guides
4. **🐛 Report Issues**: Found an error? Let us know!
5. **💡 Suggest Improvements**: Share ideas for better organization or features
6. **📚 Add Practice Problems**: Include solved examples and practice questions

---

## 🚀 Getting Started

### Prerequisites

- Git installed on your machine
- GitHub account
- Text editor (VS Code recommended)
- Basic understanding of Markdown (for notes)
- Basic HTML/React knowledge (for interactive notes, optional)

### Fork & Clone

1. **Fork the repository** by clicking the "Fork" button at the top right of the [MyNotes repository](https://github.com/zenyukti/MyNotes)

2. **Clone your fork** to your local machine:
   ```bash
   git clone https://github.com/YOUR_USERNAME/MyNotes.git
   cd MyNotes
   ```

3. **Add upstream remote** to keep your fork synced:
   ```bash
   git remote add upstream https://github.com/zenyukti/MyNotes.git
   ```

4. **Verify remotes**:
   ```bash
   git remote -v
   # origin    https://github.com/YOUR_USERNAME/MyNotes.git (fetch)
   # origin    https://github.com/YOUR_USERNAME/MyNotes.git (push)
   # upstream  https://github.com/zenyukti/MyNotes.git (fetch)
   # upstream  https://github.com/zenyukti/MyNotes.git (push)
   ```

---

## 🔄 Contribution Workflow

### Step 1: Sync Your Fork

Before starting work, ensure your fork is up-to-date:

```bash
# Fetch latest changes from upstream
git fetch upstream

# Switch to main branch
git checkout main

# Merge upstream changes
git merge upstream/main

# Push to your fork
git push origin main
```

### Step 2: Create a Feature Branch

**Always create a new branch** for your contributions. Never work directly on `main`.

```bash
# Create and switch to a new feature branch
git checkout -b feature/add-data-structures-unit1

# OR for fixes
git checkout -b fix/typo-in-python-unit2

# OR for improvements
git checkout -b improve/dstl-unit3-examples
```

**Branch Naming Convention:**
- `feature/subject-description` - for new content
- `fix/issue-description` - for bug fixes
- `improve/area-description` - for enhancements
- `docs/description` - for documentation updates

### Step 3: Make Your Changes

Follow the guidelines below based on what you're adding.

### Step 4: Commit Your Changes

```bash
# Stage your changes
git add .

# Commit with a descriptive message
git commit -m "feat: Add Data Structures Unit-1 notes on Arrays and Stacks"
```

See [Commit Message Guidelines](#commit-message-guidelines) for details.

### Step 5: Push to Your Fork

```bash
git push origin feature/add-data-structures-unit1
```

### Step 6: Create a Pull Request

1. Go to your fork on GitHub
2. Click **"Compare & pull request"**
3. Fill in the PR template (see below)
4. Submit the pull request

---

## 📁 Repository Structure Guidelines

### Directory Structure

When adding content, follow this exact structure:

```
MyNotes/
├── 📁 [Subject Name]/
│   ├── 📁 LastMinuteRevision/        # Optional: Quick revision HTML guides
│   │   ├── Unit-1.html
│   │   ├── Unit-2.html
│   │   └── ...
│   │
│   ├── Unit-1.md                     # Required: Detailed markdown notes
│   ├── Unit-2.md
│   ├── Unit-3.md
│   ├── Unit-4.md
│   └── Unit-5.md
```

### Adding a New Subject

If you're adding a **completely new subject**:

1. **Create the subject folder** (use proper capitalization and spacing):
   ```bash
   mkdir "Subject Name"
   cd "Subject Name"
   ```

2. **Create Unit files** (markdown is required):
   ```bash
   # Create all unit files
   New-Item Unit-1.md, Unit-2.md, Unit-3.md, Unit-4.md, Unit-5.md
   ```

3. **Optional: Create LastMinuteRevision folder** (if you're adding HTML notes):
   ```bash
   mkdir LastMinuteRevision
   cd LastMinuteRevision
   New-Item Unit-1.html, Unit-2.html, Unit-3.html, Unit-4.html, Unit-5.html
   ```

### Adding to Existing Subject

If the subject folder already exists:

1. **Navigate to the subject folder**:
   ```bash
   cd "Subject Name"
   ```

2. **Add or edit the appropriate unit file**:
   - For markdown notes: `Unit-X.md`
   - For HTML notes: `LastMinuteRevision/Unit-X.html`

---

## ✍️ Content Guidelines

### Markdown Notes (`.md` files)

#### File Structure

Each markdown file should follow this structure:

```markdown
# Subject Name - Unit X: Topic Name

## Table of Contents
- [Topic 1](#topic-1)
- [Topic 2](#topic-2)
- [Summary](#summary)

---

## Topic 1

### Concept 1.1

**Definition**: Clear definition here

**Example**:
```language
code example if applicable
```

**Key Points**:
- Point 1
- Point 2
- Point 3

---

## Topic 2

...

---

## Summary

Quick recap of all important points

---

## Practice Questions

1. Question 1
2. Question 2

---

**References**: List any sources used
```

#### Content Standards

- ✅ **Clear and Concise**: Use simple language, avoid unnecessary jargon
- ✅ **Well-Structured**: Use proper headings hierarchy (H1 > H2 > H3)
- ✅ **Include Examples**: Provide code examples, diagrams (ASCII art), or real-world applications
- ✅ **Add Formulas**: Use proper markdown math notation when needed: `$E = mc^2$`
- ✅ **Use Lists**: Break down complex concepts into bullet points
- ✅ **Code Blocks**: Use proper syntax highlighting: \`\`\`python, \`\`\`javascript, etc.
- ✅ **Tables**: Use markdown tables for comparisons
- ✅ **Visual Elements**: Add diagrams using ASCII art or link to images
- ❌ **No Plagiarism**: Always credit sources, write in your own words
- ❌ **No Incomplete Content**: Don't commit half-finished notes

#### Example Structure

```markdown
# Data Structures - Unit 1: Arrays and Stacks

## Arrays

### What is an Array?

**Definition**: An array is a linear data structure that stores elements of the same type in contiguous memory locations.

**Syntax** (Python):
```python
# Declaration and initialization
arr = [1, 2, 3, 4, 5]
```

**Key Properties**:
- Fixed size (in most languages)
- Random access: O(1)
- Insertion/Deletion: O(n)

**Example**:
```python
# Accessing elements
print(arr[0])  # Output: 1

# Modifying elements
arr[2] = 10
print(arr)  # Output: [1, 2, 10, 4, 5]
```

...
```

---

## 📝 Updating the README

**IMPORTANT**: Every time you add new content, you **MUST** update the `README.md` file.

### What to Update

#### 1. Repository Structure Section

If you added a **new subject**, add it to the directory tree:

```markdown
├── 📁 [Your New Subject]/        # Brief Description
│   ├── 📁 LastMinuteRevision/    # (if applicable)
│   │   ├── Unit-1.html
│   │   └── ...
│   │
│   ├── Unit-1.md
│   ├── Unit-2.md
│   └── ...
```

#### 2. Subject Content Section

Add or update the subject's section in the README. Follow this template:

**For subjects WITH interactive HTML notes:**

```markdown
### 📌 [Subject Name]

#### ⚡ LastMinuteRevision (Interactive HTML)

| Unit | Topic | 🌐 Live Preview | Quick Revision | Detailed Notes |
|------|-------|----------------|----------------|----------------|
| **Unit 1** | [Topic Name] | [🔗 Live](https://zenyukti.github.io/MyNotes/[Subject]/LastMinuteRevision/Unit-1.html) | [📱 HTML]([Subject]/LastMinuteRevision/Unit-1.html) | [📄 Markdown]([Subject]/Unit-1.md) |
| **Unit 2** | [Topic Name] | 🔜 Coming Soon | 🔜 Coming Soon | [📄 Markdown]([Subject]/Unit-2.md) |
...
```

**For subjects WITHOUT interactive HTML notes:**

```markdown
### 📌 [Subject Name]

| Unit | Topic | Detailed Notes |
|------|-------|----------------|
| **Unit 1** | [Topic Name] | [📄 Markdown]([Subject]/Unit-1.md) |
| **Unit 2** | [Topic Name] | [📄 Markdown]([Subject]/Unit-2.md) |
...
```

#### 3. Status Tracking Section

Update the status table with your contribution:

```markdown
| Subject | Units | LastMinute HTML | Detailed MD | Status |
|---------|-------|-----------------|-------------|---------|
| **[Your Subject]** | 5 | ✅ X/5 | ✅ Y/5 | 🟡 In Progress |
```

#### 4. Key Features Section

If you added significant new features or content types, mention them in the "Key Features by Subject" section.

---

## 🎨 Creating Interactive HTML Notes

If you're creating **LastMinuteRevision** HTML files, follow these guidelines:

### Technology Stack

- **React 18** (via CDN)
- **ReactDOM 18** (via CDN)
- **Babel Standalone** (for JSX transformation)
- **Tailwind CSS** (via CDN)

### HTML Template Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Subject] Unit-X: [Topic] - Last Minute Revision</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        const YourComponent = () => {
            // Your React code here
            return (
                <div className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 p-4">
                    {/* Your content */}
                    
                    {/* ZenYukti Branding - REQUIRED */}
                    <div className="text-center mt-6 pt-4 border-t border-gray-300">
                        <p className="text-sm text-gray-700 mb-2">
                            Crafted with 💙 by <a href="https://zenyukti.in" target="_blank" rel="noopener noreferrer" className="font-semibold text-blue-600 hover:text-blue-800 underline">ZenYukti</a>
                        </p>
                        <p className="text-xs text-gray-500 italic">Learn. Build. Share.</p>
                    </div>
                </div>
            );
        };

        ReactDOM.render(<YourComponent />, document.getElementById('root'));
    </script>
</body>
</html>
```

### Design Guidelines

1. **Color Scheme**:
   - 🟨 Yellow: Definitions (`bg-yellow-50`, `border-yellow-400`)
   - 🔵 Blue: Examples (`bg-blue-50`, `border-blue-400`)
   - 🟢 Green: Formulas (`bg-green-50`, `border-green-400`)
   - 🟣 Purple: Properties (`bg-purple-50`, `border-purple-400`)
   - 🔴 Red: Quick Tips (`bg-red-50`, `border-red-400`)

2. **Collapsible Sections**: Use `useState` to create expandable sections

3. **Code Blocks**: Use `<pre>` or styled `<div>` with dark background

4. **Responsive**: Must work on mobile, tablet, and desktop

5. **ZenYukti Branding**: **ALWAYS** include the footer branding (shown above)

### Testing Your HTML

Before committing, test your HTML file:

```bash
# Open in browser
start LastMinuteRevision/Unit-1.html  # Windows
open LastMinuteRevision/Unit-1.html   # Mac
xdg-open LastMinuteRevision/Unit-1.html  # Linux
```

Verify:
- ✅ All sections expand/collapse properly
- ✅ Content is readable and well-formatted
- ✅ Colors match the scheme
- ✅ Responsive on different screen sizes
- ✅ ZenYukti branding footer is present

---

## 📝 Commit Message Guidelines

We follow **Conventional Commits** specification for clear and consistent commit history.

### Format

```
<type>(<scope>): <subject>

<body (optional)>

<footer (optional)>
```

### Types

- `feat`: New feature or content addition
- `fix`: Bug fix or error correction
- `improve`: Enhancement to existing content
- `docs`: Documentation changes
- `style`: Formatting changes (no content change)
- `refactor`: Code/content restructuring
- `test`: Adding tests or examples
- `chore`: Maintenance tasks

### Examples

```bash
# Adding new notes
git commit -m "feat(DataStructures): Add Unit-1 notes on Arrays and Stacks"

# Fixing errors
git commit -m "fix(Python/Unit-2): Correct loop syntax in examples"

# Improving content
git commit -m "improve(DSTL/Unit-3): Add more examples for predicate logic"

# Updating documentation
git commit -m "docs(README): Update Python section with Unit-3 completion"

# Adding interactive HTML
git commit -m "feat(COA): Add LastMinuteRevision HTML for Unit-1"
```

### Best Practices

- ✅ Use present tense: "Add feature" not "Added feature"
- ✅ Be specific and descriptive
- ✅ Reference issue numbers if applicable: `fix(Python): Resolve #42`
- ✅ Keep subject line under 72 characters
- ❌ Don't use vague messages like "Update files" or "Fix stuff"

---

## 🔀 Pull Request Process

### Before Submitting

- [ ] Your fork is synced with upstream/main
- [ ] All changes are in a feature branch (not main)
- [ ] Content follows the guidelines above
- [ ] README.md is updated appropriately
- [ ] Files are in correct folders with proper naming
- [ ] No sensitive/personal information included
- [ ] HTML files (if any) are tested and working
- [ ] Commit messages follow the convention
- [ ] No merge conflicts with main branch

### PR Title Format

Use the same format as commit messages:

```
feat(Subject): Brief description of changes
```

### PR Description Template

```markdown
## Description
Brief description of what you've added/changed.

## Type of Change
- [ ] New subject/unit notes
- [ ] Bug fix (typo, error correction)
- [ ] Enhancement (improved existing content)
- [ ] Interactive HTML notes
- [ ] Documentation update

## Checklist
- [ ] I have followed the contribution guidelines
- [ ] My content is original or properly credited
- [ ] I have updated the README.md
- [ ] Files are in the correct directory structure
- [ ] I have tested HTML files (if applicable)
- [ ] My commit messages follow the convention
- [ ] I have synced my fork with upstream

## Related Issues
Closes #(issue number) (if applicable)

## Screenshots (if applicable)
Add screenshots of HTML notes or visual changes

## Additional Context
Any other information that reviewers should know
```

### PR Labels

Maintainers will add appropriate labels:
- `new-content`: New notes or subjects
- `enhancement`: Improvements to existing content
- `bug`: Error corrections
- `documentation`: README or docs updates
- `html-notes`: Interactive HTML additions
- `good-first-issue`: Great for newcomers
- `help-wanted`: Community input needed

---

## 👀 Review Process

### What Happens Next?

1. **Automated Checks**: GitHub Actions will run (if configured)
2. **Review by Maintainers**: ZenYukti team will review your PR
3. **Feedback**: You may receive comments or change requests
4. **Iteration**: Make requested changes and push to same branch
5. **Approval**: Once approved, your PR will be merged
6. **Celebration**: You're now a contributor! 🎉

### Review Timeline

- Simple fixes: 1-2 days
- New content: 3-5 days
- Major additions: 1 week

### Addressing Feedback

If changes are requested:

```bash
# Make the requested changes

# Stage and commit
git add .
git commit -m "fix: Address review comments"

# Push to the same branch
git push origin feature/your-branch-name
```

The PR will automatically update.

---

## ❓ Questions?

### Need Help?

- **GitHub Issues**: [Create an issue](https://github.com/zenyukti/MyNotes/issues)
- **Email**: [hello@zenyukti.in](mailto:hello@zenyukti.in)
- **Community**: Join us on [Commudle](https://commudle.com/communities/zenyukti)

### Connect With ZenYukti

- 🌐 Website: [zenyukti.in](https://zenyukti.in)
- 💼 LinkedIn: [linkedin.com/company/zenyukti](https://linkedin.com/company/zenyukti)
- 📸 Instagram: [@zenyukti](https://instagram.com/zenyukti)
- 🐦 Twitter: [@zenyukti](https://twitter.com/zenyukti)

---

## 🎉 Recognition

All contributors will be:
- Listed in the repository's contributors section
- Mentioned in release notes for major contributions
- Part of the ZenYukti community

Your contributions help thousands of students learn better. Thank you! 🙏

---

<div align="center">

**Learn. Build. Share.** 💙

*Contributing to MyNotes is contributing to education for all*

</div>
