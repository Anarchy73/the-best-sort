# Contributing to The Best Sort

Thank you for your interest in contributing to The Best Sort! This document provides guidelines and instructions for contributing to the project.

## Code of Conduct

### Our Pledge

In the interest of fostering an open and welcoming environment, we as contributors and maintainers pledge to making participation in our project and our community a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, sex characteristics, gender identity and expression, level of experience, education, national origin, personal appearance, race, religion, or sexual orientation.

### Our Standards

Examples of behavior that contributes to creating a positive environment include:
- Using welcoming and inclusive language
- Being respectful of differing opinions, viewpoints, and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

Examples of unacceptable behavior include:
- The use of sexualized language or imagery
- Trolling, insulting/derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate in a professional setting

## Getting Started

### Prerequisites

- Node.js 18.0.0 or higher
- npm or yarn
- Git
- Basic knowledge of TypeScript
- Understanding of OOP design patterns

### Setting Up Your Development Environment

1. Fork the repository on GitHub

2. Clone your fork locally:
```sh
git clone https://github.com/USERNAME/the-best-sort.git
cd the-best-sort
```
3. Add upstream remote to keep your fork updated:
```sh
git remote add upstream https://github.com/danilasar/the-best-sort.git
```
4. Install dependencies:
```sh
npm install -D typescript @types/node
```
5. Create a new branch for your work:
```sh
git checkout -b feature/your-feature-name
```

## Development Workflow

### Building

```sh
npx tsc src/index.ts --experimentalDecorators --emitDecoratorMetadata
```


### Running

```sh
npx tsx src/index.ts
```


### Testing Your Changes

Before submitting a pull request, ensure:

1. Your code compiles without errors
2. All functionality works as expected
3. New code follows the existing patterns
4. Documentation is updated accordingly

### Code Style

The Best Sort follows these style conventions:

#### TypeScript/JavaScript

- Use TypeScript strict mode
- Use arrow functions for callbacks
- Use const/let, avoid var
- Use meaningful variable names
- Use single quotes for strings (unless HTML content)
- Use 2-space indentation
- Add type annotations to function parameters

Example:

```typescript
class MyClass {
  private value: number;
  
  constructor(initialValue: number) {
    this.value = initialValue;
  }
  
  getValue(): number {
    return this.value;
  }
  
  setValue(newValue: number): void {
    this.value = newValue;
  }
}
```


#### Comments and Documentation

- Use JSDoc comments for public methods
- Add explanatory comments for complex logic
- Include type information in comments when not obvious
- Document all parameters and return types

Example:

```typescript
/*
 * Creates a new visualizer with the specified configuration
 *
 * @param array - The array of visualizable elements
 *
 * @param strategy - The visualization strategy to use
 *
 * @returns A configured ArrayVisualizer instance
 */
function createVisualizer<T>(
  array: T[],
  strategy: IVisualizationStrategy<T>
): ArrayVisualizer<T> {
  // Implementation
}
```


#### Naming Conventions

- Classes: PascalCase (e.g., ConfigurationManager)
- Interfaces: PascalCase with I prefix (e.g., IObserver)
- Functions/methods: camelCase (e.g., emitStarted)
- Constants: UPPER_SNAKE_CASE (e.g., MAX_ITERATIONS)
- Private members: camelCase with underscore prefix (e.g., _internalValue)


### Submitting Changes

1. Keep commits atomic and logical
2. Write clear commit messages:
   - Use present tense ("Add feature" not "Added feature")
   - Be descriptive but concise
   - Reference issues if applicable

3. Push to your fork:

```sh
git push origin feature/your-feature-name
```


4. Create a Pull Request with:
   - Clear title describing the changes
   - Description of what changed and why
   - Reference to related issues
   - Screenshots or examples if applicable

### Pull Request Process

1. Update documentation and CHANGELOG.md
2. Follow the existing code style
3. Test your changes thoroughly
4. Request review from maintainers
5. Address review comments
6. Ensure CI/CD checks pass

Checklist for PR:
- [ ] Code compiles without errors
- [ ] TypeScript strict mode passes
- [ ] Follows code style guidelines
- [ ] Documentation updated
- [ ] CHANGELOG.md updated
- [ ] No console.error or console.warn left in code
- [ ] New code includes JSDoc comments
- [ ] Examples work correctly

## Types of Contributions

### Bug Reports

Report bugs by opening an GitHub issue with:
- Clear title
- Detailed description
- Steps to reproduce
- Expected vs actual behavior
- Environment information (Node version, OS, etc.)

### Feature Requests

Request features by opening an issue with:
- Clear title
- Detailed description of the feature
- Use cases and benefits
- Possible implementation approach (optional)

### Documentation Improvements

Improvements to documentation are always welcome:
- Fix typos or clarify existing docs
- Add examples
- Improve organization
- Translate documentation

### Code Contributions

Code improvements including:
- New visualization strategies
- New observer implementations
- Performance improvements
- Bug fixes
- Test coverage

## Documentation

### README.md
Main project documentation and quick start guide

### Inline Comments
Complex logic should be explained with comments

### API Documentation
All public APIs should be documented with JSDoc

## Performance Considerations

When adding new features, consider:
- Event loop impact
- Memory usage with large arrays
- setTimeout precision limitations
- Observer notification overhead

## Questions?

- Check existing issues on GitHub
- Review the README and documentation
- Open a discussion issue if unsure
- Ask in comments on related issues

## Recognition

Contributors will be recognized in:
- CHANGELOG.md for releases
- GitHub contributors graph
- Project acknowledgments section

## License

By contributing to The Best Sort, you agree that your contributions will be licensed under the same license as the project.

---

Thank you for contributing to The Best Sort!

