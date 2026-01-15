# Contributing to WindPulse

Thank you for your interest in contributing to WindPulse! This document provides guidelines for contributing to the project.

## How to Contribute

### Reporting Bugs

If you find a bug, please open an issue on GitHub with:
- A clear, descriptive title
- Detailed description of the issue
- Steps to reproduce the problem
- Expected vs. actual behavior
- Your environment (OS, Python version, etc.)
- Any relevant code snippets or error messages

### Suggesting Enhancements

We welcome suggestions for improvements! Please open an issue with:
- A clear description of the enhancement
- The motivation and use case
- Any implementation ideas you have
- Examples of how it would work

### Pull Requests

1. **Fork the repository** and create your branch from `main`
2. **Make your changes**:
   - Write clear, readable code
   - Follow existing code style and conventions
   - Add comments where necessary
   - Update documentation if needed
3. **Test your changes**:
   - Ensure existing tests pass
   - Add new tests for new functionality
   - Verify visualizations render correctly
4. **Commit your changes**:
   - Write clear, descriptive commit messages
   - Reference any related issues
5. **Push to your fork** and submit a pull request

### Code Style

- Follow PEP 8 style guide for Python code
- Use meaningful variable and function names
- Write docstrings for functions and classes
- Keep functions focused and modular
- Add type hints where appropriate

### Documentation

- Update README.md if you change functionality
- Add docstrings to new functions/classes
- Update methodology docs if you add new analysis methods
- Include comments for complex algorithms

### Testing

- Write unit tests for new functions
- Test with different input data sizes
- Verify visualizations look correct
- Check for edge cases and error handling

## Development Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/windpulse.git
cd windpulse

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install pytest black flake8 mypy
```

## Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=windpulse

# Run specific test file
pytest tests/test_analysis.py
```

## Code Review Process

1. All submissions require review
2. Reviewers will check:
   - Code quality and style
   - Test coverage
   - Documentation
   - Performance implications
3. Address reviewer feedback promptly
4. Once approved, maintainers will merge

## Community Guidelines

- Be respectful and inclusive
- Welcome newcomers and help them get started
- Focus on constructive feedback
- Assume good intentions
- Follow the code of conduct

## Questions?

If you have questions about contributing, feel free to:
- Open an issue for discussion
- Reach out to maintainers
- Check existing issues and pull requests

Thank you for contributing to WindPulse!
