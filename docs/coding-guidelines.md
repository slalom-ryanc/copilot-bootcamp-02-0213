# Coding Guidelines - TODO App

## Overview

This document establishes the coding standards and quality principles for the TODO app project. These guidelines ensure consistency, maintainability, and quality across both frontend and backend codebases. All contributors are expected to follow these standards to create clean, readable, and maintainable code.

## Core Principles

### Code Quality Philosophy

Our approach to code quality is built on several foundational principles that guide all development decisions. Quality code is not just about making things work—it's about creating software that is easy to understand, modify, and extend. We believe that code is written once but read many times, so clarity and maintainability are paramount.

Every line of code should serve a clear purpose and be written with the next developer in mind. Whether that next developer is a teammate or your future self, the code should communicate its intent without requiring extensive documentation or mental gymnastics to understand.

## Formatting and Style Standards

### General Formatting Rules

Consistent formatting is essential for code readability and team collaboration. We use automated formatters to enforce these standards, ensuring that all code follows the same visual structure regardless of who writes it.

**Indentation**: Use 2 spaces for indentation in JavaScript, TypeScript, JSON, and CSS files. Never use tabs. This ensures consistent rendering across different editors and tools. Proper indentation reveals the logical structure of code at a glance and makes nested structures easier to follow.

**Line Length**: Limit lines to a maximum of 100 characters. This constraint encourages concise expressions and ensures code is readable on various screen sizes, in split-screen views, and in code review tools. When a line exceeds this limit, break it logically at natural boundaries such as after commas, operators, or method chains.

**Semicolons**: Always use semicolons to terminate statements in JavaScript. While ASI (Automatic Semicolon Insertion) can sometimes handle missing semicolons, explicit semicolons prevent subtle bugs and make code intentions clear.

**Quotes**: Use single quotes (`'`) for strings in JavaScript unless the string contains a single quote, in which case use double quotes to avoid escaping. For template literals requiring interpolation, use backticks. Consistency in quote usage reduces visual noise and makes the codebase feel cohesive.

**Trailing Commas**: Use trailing commas in multi-line arrays, objects, and function parameters. This practice simplifies version control diffs by isolating changes to a single line when adding new elements, and it prevents errors when reordering items.

```javascript
// Good
const task = {
  id: 1,
  title: 'Buy Christmas gifts',
  priority: 'high',
  tags: ['shopping', 'holiday'],
};

// Bad
const task = {
  id: 1,
  title: 'Buy Christmas gifts',
  priority: 'high',
  tags: ['shopping', 'holiday']
}
```

### Whitespace and Blank Lines

Strategic use of whitespace significantly improves code readability. Use blank lines to separate logical sections of code, creating visual breathing room that helps readers parse the code structure. Group related statements together and separate distinct operations with a blank line.

Add spaces around operators (`=`, `+`, `-`, `===`, etc.) and after keywords (`if`, `for`, `return`). Place spaces after commas in argument lists and array elements. These small touches create rhythm and flow in the code.

Avoid excessive blank lines—one or two blank lines between logical sections is sufficient. Multiple consecutive blank lines waste screen space without adding clarity.

```javascript
// Good - clear logical grouping
function calculateTaskPriority(task) {
  const dueDateScore = calculateDueDateScore(task.dueDate);
  const importanceScore = getImportanceScore(task.priority);
  
  const totalScore = dueDateScore + importanceScore;
  
  return Math.min(totalScore, 100);
}

// Bad - no structure
function calculateTaskPriority(task) {
  const dueDateScore = calculateDueDateScore(task.dueDate);
  const importanceScore = getImportanceScore(task.priority);
  const totalScore = dueDateScore + importanceScore;
  return Math.min(totalScore, 100);
}
```

## Import Organization

Organized imports make dependencies clear and prevent naming conflicts. Structure imports in a consistent order to help developers quickly locate where components and utilities come from.

### Import Order

Follow this order when organizing imports, with a blank line between each group:

1. **External dependencies** (third-party libraries from node_modules)
2. **Internal modules** (application modules using absolute paths)
3. **Relative imports** (local files using relative paths)
4. **Type imports** (TypeScript types/interfaces, when applicable)
5. **Styles** (CSS/SCSS imports)

Within each group, sort imports alphabetically for consistency and easy scanning.

```javascript
// Good - clear organization
// External dependencies
import React, { useState, useEffect } from 'react';
import { Box, Card, Typography } from '@mui/material';
import { format } from 'date-fns';

// Internal modules
import { TaskService } from 'services/TaskService';
import { useAuth } from 'hooks/useAuth';

// Relative imports
import TaskItem from './TaskItem';
import TaskForm from './TaskForm';

// Styles
import './TaskList.css';
```

### Named vs Default Imports

Prefer named imports over default imports when possible. Named imports provide better IDE support, make refactoring easier, and prevent naming inconsistencies across files. When a module exports a single primary entity, default exports are acceptable, but ensure the import name matches the module's purpose.

```javascript
// Good - named imports
import { TaskService, TaskValidator } from './services/taskService';

// Acceptable - default import with clear name
import TaskList from './components/TaskList';

// Bad - ambiguous default import name
import MyList from './components/TaskList'; // confusing name
```

### Import Destructuring

When importing multiple items from a module, use destructuring for clarity. Destructured imports immediately show what functionality is being used from each module.

```javascript
// Good
import { useState, useEffect, useCallback } from 'react';

// Avoid
import React from 'react';
const { useState, useEffect } = React;
```

## Linting and Code Quality Tools

### ESLint Configuration

We use ESLint to enforce code quality standards and catch potential errors before they reach production. ESLint runs automatically during development and in the CI/CD pipeline, providing immediate feedback on code quality issues.

The project's ESLint configuration extends recommended rulesets and includes custom rules tailored to our needs. All ESLint warnings and errors must be resolved before code can be merged. Disabling ESLint rules is discouraged and should only be done with clear justification documented in code comments.

**Key ESLint Rules We Enforce:**
- No unused variables (prevents dead code)
- No console statements in production code (use proper logging)
- Consistent return statements (all code paths must return)
- Proper dependency arrays in React hooks (prevents stale closures)
- No duplicate imports (keeps imports clean)

### Prettier Configuration

Prettier handles automatic code formatting, eliminating debates about styling preferences. When you save a file, Prettier automatically formats it according to the project's configuration. This ensures consistent formatting without manual effort.

Configure your IDE to run Prettier on save. This workflow means you never need to think about formatting—write code naturally, save, and let Prettier handle the rest.

### Running Linters

Linters run automatically in several contexts:
- **During development**: IDE integration provides real-time feedback
- **Pre-commit hooks**: Git hooks prevent committing code with linting errors
- **In CI/CD pipeline**: Automated checks ensure no linting errors reach main branch

Manually run linters using these commands:
```bash
# Run ESLint
npm run lint

# Auto-fix ESLint issues
npm run lint:fix

# Run Prettier
npm run format

# Check Prettier formatting
npm run format:check
```

## Naming Conventions

Clear, descriptive names make code self-documenting and reduce the need for comments. Names should reveal intent and follow consistent patterns throughout the codebase.

### Variables and Functions

Use `camelCase` for variables, functions, and methods. Names should be descriptive and communicate the purpose or content of the variable. Avoid abbreviations unless they're universally understood (like `id`, `url`, or `api`).

Boolean variables should start with verbs like `is`, `has`, `can`, or `should` to clearly indicate they represent yes/no states.

```javascript
// Good
const taskList = [];
const isCompleted = false;
const hasOverdueTasks = true;
const canEditTask = checkPermissions(user);

function calculatePriorityScore(task) {
  // implementation
}

// Bad
const tl = []; // unclear abbreviation
const completed = false; // unclear boolean
const x = true; // meaningless name

function calc(t) { // unclear abbreviation
  // implementation
}
```

### Constants

Use `UPPER_SNAKE_CASE` for constants that represent fixed configuration values or enums. This convention makes constants visually distinct and signals that values should never change.

```javascript
// Good
const MAX_TASK_TITLE_LENGTH = 200;
const API_BASE_URL = 'https://api.example.com';
const PRIORITY_LEVELS = {
  LOW: 'low',
  MEDIUM: 'medium',
  HIGH: 'high',
};

// Bad
const maxLength = 200; // looks like a variable
const apiUrl = 'https://api.example.com'; // not obviously constant
```

### React Components

Use `PascalCase` for React component names, with component files matching the component name. This convention distinguishes components from regular functions and aligns with JSX syntax.

```javascript
// Good
function TaskList() {
  return <div>...</div>;
}

function TaskItem({ task }) {
  return <Card>...</Card>;
}

// Bad
function taskList() { // should be PascalCase
  return <div>...</div>;
}
```

### Files and Directories

Use `camelCase` for utility files and `PascalCase` for component files. Directory names should be lowercase with hyphens for multiple words.

```
Good structure:
src/
  components/
    TaskList.js
    TaskItem.js
  utils/
    dateHelpers.js
    taskHelpers.js
  services/
    taskService.js
```

## Code Organization

### File Structure

Keep files focused and concise. Each file should have a single primary purpose. If a file exceeds 300 lines, consider whether it's doing too much and could be split into smaller, more focused modules.

Structure files from general to specific: imports at the top, constants next, then main code, followed by helper functions, and exports at the bottom.

```javascript
// File structure template

// 1. Imports
import React from 'react';
import { Box } from '@mui/material';

// 2. Constants
const MAX_TASKS = 100;

// 3. Main component/function
function TaskList() {
  // implementation
}

// 4. Helper functions (if needed)
function sortTasks(tasks) {
  // implementation
}

// 5. Exports
export default TaskList;
export { sortTasks };
```

### Function Length and Complexity

Keep functions short and focused on a single responsibility. A function should do one thing well. If a function exceeds 50 lines or has multiple levels of nested logic, it's likely doing too much and should be refactored.

Extract complex logic into well-named helper functions. This approach makes the main function read like a high-level procedure, with helper functions providing implementation details.

```javascript
// Good - single responsibility, readable
function createTask(taskData) {
  validateTaskData(taskData);
  const task = formatTask(taskData);
  return saveTask(task);
}

function validateTaskData(data) {
  if (!data.title) throw new Error('Title required');
  if (data.title.length > MAX_TITLE_LENGTH) throw new Error('Title too long');
}

// Bad - doing too much
function createTask(taskData) {
  if (!taskData.title) throw new Error('Title required');
  if (taskData.title.length > 200) throw new Error('Title too long');
  const task = {
    id: generateId(),
    title: taskData.title.trim(),
    completed: false,
    createdAt: new Date(),
    // ... many more lines
  };
  // ... database operations
  // ... error handling
  return task;
}
```

## Best Practices

### DRY Principle (Don't Repeat Yourself)

Duplication is one of the primary enemies of maintainable code. When the same logic appears in multiple places, it becomes difficult to update consistently. A bug fix or feature change requires modifying every instance, increasing the risk of inconsistency.

Identify repeated patterns and extract them into reusable functions, components, or utilities. However, be cautious of premature abstraction—wait until a pattern appears at least three times before creating an abstraction. Two instances might be coincidental; three instances indicate a true pattern.

```javascript
// Bad - repetition
function formatHighPriorityTask(task) {
  return {
    ...task,
    priorityLabel: 'High',
    color: '#C41E3A',
  };
}

function formatMediumPriorityTask(task) {
  return {
    ...task,
    priorityLabel: 'Medium',
    color: '#FFD700',
  };
}

// Good - DRY
const PRIORITY_CONFIG = {
  high: { label: 'High', color: '#C41E3A' },
  medium: { label: 'Medium', color: '#FFD700' },
  low: { label: 'Low', color: '#355E3B' },
};

function formatTaskWithPriority(task) {
  const config = PRIORITY_CONFIG[task.priority];
  return {
    ...task,
    priorityLabel: config.label,
    color: config.color,
  };
}
```

### SOLID Principles

While SOLID principles originated in object-oriented programming, their core concepts apply to JavaScript development:

**Single Responsibility**: Each function, component, or module should have one clear purpose. If you can't describe what a module does in a single sentence, it probably does too much.

**Open/Closed**: Code should be open for extension but closed for modification. Use composition and configuration over modification of existing code.

**Dependency Inversion**: Depend on abstractions (interfaces, contracts) rather than concrete implementations. This makes code more flexible and testable.

### Error Handling

Handle errors explicitly and gracefully. Every external operation (API calls, file operations, user input) can fail and should be handled appropriately.

Provide meaningful error messages that help users understand what went wrong and what they can do about it. In backend code, log errors with sufficient context for debugging.

```javascript
// Good - explicit error handling
async function fetchTasks() {
  try {
    const response = await api.get('/tasks');
    return response.data;
  } catch (error) {
    if (error.response?.status === 404) {
      return []; // no tasks found, return empty array
    }
    console.error('Failed to fetch tasks:', error.message);
    throw new Error('Unable to load tasks. Please try again.');
  }
}

// Bad - errors ignored
async function fetchTasks() {
  const response = await api.get('/tasks');
  return response.data; // what if this fails?
}
```

### Immutability

Prefer immutable data patterns. Avoid mutating objects and arrays directly; instead, create new versions with the desired changes. Immutability prevents unexpected side effects and makes code easier to reason about, especially in React applications where state changes trigger re-renders.

```javascript
// Good - immutable updates
const completedTask = { ...task, completed: true };
const updatedTasks = tasks.map(t => t.id === taskId ? completedTask : t);

// Bad - mutation
task.completed = true; // mutates original object
tasks[index] = task; // mutates original array
```

### Avoid Magic Numbers and Strings

Replace magic values with named constants. This practice makes code self-documenting and ensures consistency when the same value appears multiple times.

```javascript
// Bad - magic numbers
if (task.priority > 7) {
  // what does 7 mean?
}

setTimeout(fetchTasks, 5000); // why 5000?

// Good - named constants
const HIGH_PRIORITY_THRESHOLD = 7;
const FETCH_INTERVAL_MS = 5000;

if (task.priority > HIGH_PRIORITY_THRESHOLD) {
  // clear intent
}

setTimeout(fetchTasks, FETCH_INTERVAL_MS);
```

### Early Returns

Use early returns to reduce nesting and improve readability. Handle edge cases and error conditions first, then proceed with the main logic. This pattern keeps the "happy path" at the lowest indentation level, making it easier to follow.

```javascript
// Good - early returns
function processTask(task) {
  if (!task) return null;
  if (!task.title) throw new Error('Title required');
  if (task.completed) return task;
  
  // main logic at low indentation level
  const processed = validateAndFormat(task);
  return saveTask(processed);
}

// Bad - deeply nested
function processTask(task) {
  if (task) {
    if (task.title) {
      if (!task.completed) {
        const processed = validateAndFormat(task);
        return saveTask(processed);
      } else {
        return task;
      }
    } else {
      throw new Error('Title required');
    }
  }
  return null;
}
```

### Comment Guidelines

Write self-documenting code that explains itself through clear naming and structure. Use comments sparingly to explain *why* something is done, not *what* is being done. If you find yourself writing comments to explain what code does, consider whether better naming or refactoring would eliminate the need for the comment.

```javascript
// Good - comment explains why
// Using setTimeout to debounce rapid filter changes and improve performance
const debouncedFilter = debounce(filterTasks, 300);

// Bad - comment explains what (code already shows this)
// Set isLoading to true
setIsLoading(true);

// Good - no comment needed, code is clear
const isOverdue = task.dueDate < new Date();
```

## React-Specific Guidelines

### Component Structure

Structure React components consistently: state declarations at the top, event handlers next, effects after that, then render logic.

```javascript
function TaskItem({ task, onComplete, onDelete }) {
  // 1. State
  const [isEditing, setIsEditing] = useState(false);
  
  // 2. Hooks
  const { user } = useAuth();
  
  // 3. Event handlers
  const handleEdit = () => setIsEditing(true);
  const handleSave = (data) => {
    updateTask(data);
    setIsEditing(false);
  };
  
  // 4. Effects
  useEffect(() => {
    // effect logic
  }, [task]);
  
  // 5. Render
  return (
    <Card>
      {/* JSX */}
    </Card>
  );
}
```

### Prop Types and Validation

While the project may not use TypeScript initially, validate props using PropTypes or transition to TypeScript for compile-time type safety. Type validation catches errors early and documents component interfaces.

### Custom Hooks

Extract reusable stateful logic into custom hooks. Custom hooks provide powerful abstraction capabilities while following React's rules of hooks.

```javascript
// Good - reusable custom hook
function useTasks() {
  const [tasks, setTasks] = useState([]);
  const [loading, setLoading] = useState(false);
  
  useEffect(() => {
    setLoading(true);
    fetchTasks()
      .then(setTasks)
      .finally(() => setLoading(false));
  }, []);
  
  return { tasks, loading };
}
```

## Backend-Specific Guidelines

### RESTful API Design

Follow RESTful conventions for API endpoints. Use appropriate HTTP methods (GET, POST, PUT, DELETE) and meaningful URLs. Return appropriate status codes (200, 201, 400, 404, 500) and consistent response formats.

### Validation and Sanitization

Always validate and sanitize user input on the backend. Never trust client-side validation alone. Validate data types, formats, and constraints before processing.

### Environment Configuration

Use environment variables for configuration that changes between environments (development, staging, production). Never hardcode sensitive information like API keys or database credentials.

## Code Review Standards

All code must be reviewed before merging. Reviews should verify:
- Code follows these guidelines
- Tests are present and passing
- Code is clear and maintainable
- No obvious bugs or security issues
- Performance considerations are addressed

Be constructive in reviews. Focus on the code, not the person. Ask questions rather than make demands. Recognize good work.

## Continuous Improvement

These guidelines are living documents. As the project evolves and the team learns, update these standards to reflect new best practices and lessons learned. Propose changes through the same review process used for code changes.

## Tools and Resources

### Required Tools
- **ESLint**: Code quality and error detection
- **Prettier**: Code formatting
- **Git**: Version control with meaningful commit messages
- **VS Code Extensions**: ESLint, Prettier, GitLens (recommended)

### Recommended Reading
- Clean Code by Robert C. Martin
- The Pragmatic Programmer
- Refactoring by Martin Fowler
- React documentation and best practices

## Conclusion

Following these coding guidelines ensures our codebase remains clean, consistent, and maintainable. Quality code is an investment in the project's future—it pays dividends in reduced bugs, easier onboarding, faster feature development, and improved team morale. Every developer has a responsibility to uphold these standards and contribute to a codebase we can all be proud of.
