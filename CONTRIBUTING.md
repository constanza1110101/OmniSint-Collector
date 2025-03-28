Contributing to OmniSINT Collector
Thank you for your interest in contributing to OmniSINT Collector! This document provides guidelines and instructions to help you contribute effectively to this project.

Table of Contents
Code of Conduct
Getting Started
Development Environment
Contribution Workflow
Coding Standards
Adding New Platforms
Testing
Documentation
Review Process
Community
Code of Conduct
Our project adheres to a Code of Conduct that establishes expected behavior in our community. Please read the CODE_OF_CONDUCT.md file before contributing.

Getting Started
Fork the repository on GitHub
Clone your fork locally:
bash

Hide
git clone https://github.com/YOUR-USERNAME/omnisint-collector.git
cd omnisint-collector
Add the upstream remote:
bash

Hide
git remote add upstream https://github.com/original-owner/omnisint-collector.git
Create a branch for your work:
bash

Hide
git checkout -b feature/your-feature-name
Development Environment
Prerequisites
Rust 1.60 or higher
OpenSSL development libraries
pkg-config (for Unix-like systems)
Docker (optional, for containerized testing)
Setup
Install dependencies:

bash

Hide
# Ubuntu/Debian
sudo apt-get install libssl-dev pkg-config

# macOS
brew install openssl pkg-config

# Windows
# Install OpenSSL using vcpkg or similar
Build the project:

bash

Hide
cargo build
Run tests:

bash

Hide
cargo test
Contribution Workflow
Update your fork with the latest changes from upstream:

bash

Hide
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
Create a new branch for your work:

bash

Hide
git checkout -b feature/your-feature-name
Make your changes and commit them:

bash

Hide
git add .
git commit -m "Add feature: brief description of changes"
Push your changes to your fork:

bash

Hide
git push origin feature/your-feature-name
Create a Pull Request from your branch to the upstream repository

Coding Standards
We follow Rust's official style guidelines. Please ensure your code:

Is formatted with rustfmt (run cargo fmt before committing)
Passes clippy checks (run cargo clippy before committing)
Includes appropriate error handling
Uses meaningful variable and function names
Has comments for complex logic
Includes docstrings for public functions and types
Adding New Platforms
To add support for a new platform to the username discovery or social media modules:

Update the appropriate module in src/modules/
Add the platform to the default configuration
Implement the platform-specific logic following the existing patterns
Add tests for the new platform
Update documentation to reflect the new platform
Example for adding a new social media platform:

rust

Hide
// In src/modules/social_media.rs

async fn get_social_profile_from_new_platform(client: &Client, username: &str) -> Result<Option<SocialProfile>, Box<dyn Error>> {
    let url = format!("https://newplatform.com/{}", username);
    
    // Implementation details...
    
    Ok(Some(profile))
}
Testing
Unit Tests
Write unit tests for all new functionality
Place tests in the same file as the code being tested
Use Rust's built-in testing framework
Example:

rust

Hide
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_platform_detection() {
        // Test implementation
    }
}
Integration Tests
Create integration tests in the tests/ directory
Mock external services where appropriate
Test full workflows
Running Tests
bash

Hide
# Run all tests
cargo test

# Run a specific test
cargo test test_name

# Run tests with output
cargo test -- --nocapture
Documentation
Update the README.md when adding new features
Document all public functions and types with docstrings
Keep API documentation up to date
Add examples for new functionality
Review Process
Initial review: A maintainer will review your PR for basic compliance
Technical review: Code will be reviewed for quality, style, and functionality
Testing: All tests must pass before merging
Changes: You may be asked to make changes before your PR is accepted
Approval and merge: Once approved, a maintainer will merge your PR
Community
Join our Discord server for discussions
Ask questions in the GitHub Discussions section
Report bugs and request features using GitHub Issues
Thank you for contributing to OmniSINT Collector! Your efforts help make this tool more powerful and useful for the security community.
