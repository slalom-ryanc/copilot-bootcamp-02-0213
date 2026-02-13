# UI Guidelines - TODO App

## Theme Overview

The TODO app uses a **Christmas theme** to create a festive and delightful user experience. All UI components must follow Material Design principles using Material-UI (MUI) components.

## Color Palette

### Primary Colors
- **Christmas Red**: `#C41E3A` - Primary action buttons, important highlights
- **Forest Green**: `#0F5132` - Secondary elements, success states
- **Snow White**: `#FFFAFA` - Background, cards
- **Deep Red**: `#8B0000` - Hover states, emphasis

### Accent Colors
- **Gold**: `#FFD700` - Badges, priority indicators, decorative accents
- **Silver**: `#C0C0C0` - Secondary text, borders
- **Holly Green**: `#355E3B` - Active states, completed tasks
- **Candy Cane**: `#FF6B6B` - Error states, overdue tasks

### Neutral Colors
- **Charcoal**: `#2C2C2C` - Primary text
- **Warm Gray**: `#F5F5F5` - Backgrounds, dividers
- **Light Gray**: `#E8E8E8` - Disabled states

## Typography

### Font Family
- **Primary Font**: 'Roboto', sans-serif (Material-UI default)
- **Decorative Headers**: 'Mountains of Christmas', cursive (for app title and section headers)

### Font Sizes
- **H1**: 2.5rem (40px) - App title
- **H2**: 2rem (32px) - Section headers
- **H3**: 1.5rem (24px) - Card titles
- **Body**: 1rem (16px) - Regular text
- **Caption**: 0.875rem (14px) - Metadata, timestamps

### Font Weights
- **Regular**: 400 - Body text
- **Medium**: 500 - Task titles
- **Bold**: 700 - Headers, important labels

## Material-UI Components

### Required Components

#### 1. AppBar (MUI Component)
```jsx
import { AppBar, Toolbar, Typography } from '@mui/material';
```
- Use `AppBar` for the main navigation header
- Background color: Christmas Red (`#C41E3A`)
- Include snowflake icon (❄️) or Christmas tree icon (🎄) in the title
- Show task count badge with gold background

#### 2. Card (MUI Component)
```jsx
import { Card, CardContent, CardActions } from '@mui/material';
```
- Use `Card` components for each task item
- Background: Snow White with subtle shadow
- Border: Optional 1px gold accent on high-priority tasks
- Corner decoration: Small holly leaf or snowflake icon
- Hover effect: Slight elevation increase + gold border glow

#### 3. TextField (MUI Component)
```jsx
import { TextField } from '@mui/material';
```
- Use outlined variant for task input
- Label color: Forest Green
- Focus color: Christmas Red
- Include Christmas-themed placeholder text (e.g., "Add a new festive task...")

#### 4. Button (MUI Component)
```jsx
import { Button, IconButton, Fab } from '@mui/material';
```
- **Primary Button**: Christmas Red background, white text
- **Secondary Button**: Forest Green outlined variant
- **FAB (Floating Action Button)**: Gold background for "Add Task" with plus icon
- Icons: Use festive alternatives where possible (e.g., snowflake for delete, star for priority)

#### 5. Chip (MUI Component)
```jsx
import { Chip } from '@mui/material';
```
- Use for tags and priority indicators
- **High Priority**: Gold background with red text
- **Medium Priority**: Silver background
- **Low Priority**: Light green background
- Include small decorative icons (ornament, gift box, candy cane)

#### 6. Checkbox (MUI Component)
```jsx
import { Checkbox } from '@mui/material';
```
- Custom checkbox color: Forest Green when checked
- Large size (24px) for easy interaction
- Checked state shows a holly leaf or star icon if possible

#### 7. Select/Menu (MUI Component)
```jsx
import { Select, MenuItem } from '@mui/material';
```
- Use for filters and sort options
- Christmas Red focus indicator
- Dropdown icon: Use custom festive icon

#### 8. DatePicker (MUI X Component)
```jsx
import { DatePicker } from '@mui/x-date-pickers';
```
- Use Material-UI DatePicker for due date selection
- Custom calendar colors: Christmas theme
- Highlight today with gold circle
- Weekend dates in Forest Green

#### 9. Badge (MUI Component)
```jsx
import { Badge } from '@mui/material';
```
- Use gold badges for task counts
- Overdue tasks badge in Candy Cane red

#### 10. Snackbar (MUI Component)
```jsx
import { Snackbar, Alert } from '@mui/material';
```
- Success: Holly Green background with checkmark
- Error: Candy Cane background with warning icon
- Position: bottom-center with festive styling

## Layout Guidelines

### Spacing
- Use Material-UI spacing scale (`theme.spacing()`)
- Default padding: 16px (theme.spacing(2))
- Card margins: 8px vertical gap
- Section spacing: 24px (theme.spacing(3))

### Container
- Max width: 1200px for desktop
- Centered layout with festive border or background pattern
- Optional: Subtle falling snowflakes animation in the background

### Grid System
- Use Material-UI `Grid` component
- Responsive breakpoints:
  - Mobile: 1 column
  - Tablet: 2 columns
  - Desktop: 3 columns (for task cards)

## Decorative Elements

### Icons
- Use Material Icons library with Christmas alternatives:
  - Add: `AddCircle` with star accent
  - Delete: `DeleteOutline` with snowflake overlay
  - Edit: `EditOutlined` with candy cane accent
  - Complete: `CheckCircle` with holly leaf
  - Priority: `Star`, `StarHalf`, `StarBorder` in gold

### Ornamental Graphics
- Holly leaves and berries for corners and dividers
- Snowflakes for background patterns (subtle, low opacity)
- Christmas lights string at the top of the app (optional)
- Ornament bullets for lists
- Gift box icons for completed tasks milestone

### Animations
- Smooth transitions using Material-UI transitions
- Task completion: Confetti or sparkle effect
- Loading: Christmas ornament spinner
- Hover states: Gentle glow effect in gold

## Accessibility

### Color Contrast
- Ensure WCAG AA compliance for all text
- Primary text on Snow White: Minimum 4.5:1 ratio
- White text on Christmas Red: Verified contrast ratio

### Focus States
- Visible focus indicators: 2px gold outline
- Keyboard navigation fully supported
- Screen reader labels for all interactive elements

### Responsive Design
- Touch targets: Minimum 44x44px
- Mobile-friendly Material components
- Readable text sizes on all devices

## Dark Mode (Optional)

### Dark Theme Colors
- Background: Dark charcoal (`#1A1A1A`)
- Cards: Slightly lighter charcoal (`#2C2C2C`)
- Primary: Brighter Christmas Red (`#E63946`)
- Secondary: Lighter Forest Green (`#2D6A4F`)
- Accents: Brighter gold and silver for visibility

## Implementation Notes

### Material-UI Setup
```bash
npm install @mui/material @emotion/react @emotion/styled
npm install @mui/icons-material
npm install @mui/x-date-pickers
```

### Theme Configuration
```javascript
import { createTheme } from '@mui/material/styles';

const christmasTheme = createTheme({
  palette: {
    primary: {
      main: '#C41E3A', // Christmas Red
    },
    secondary: {
      main: '#0F5132', // Forest Green
    },
    success: {
      main: '#355E3B', // Holly Green
    },
    error: {
      main: '#FF6B6B', // Candy Cane
    },
    background: {
      default: '#FFFAFA', // Snow White
      paper: '#FFFFFF',
    },
  },
  typography: {
    fontFamily: 'Roboto, Arial, sans-serif',
    h1: {
      fontFamily: '"Mountains of Christmas", cursive',
    },
  },
});
```

## Design Principles

1. **Consistency**: Use Material-UI components consistently throughout the app
2. **Festivity**: Incorporate Christmas theme without overwhelming functionality
3. **Usability**: Maintain clarity and ease of use despite decorative elements
4. **Performance**: Keep animations smooth and lightweight
5. **Accessibility**: Ensure all users can enjoy the festive experience
6. **Responsiveness**: Beautiful experience on all devices

## Component States

### Task Card States
- **Default**: Snow White background, subtle shadow
- **Hover**: Elevated shadow, gold border glow
- **Active/Focus**: Gold border, increased elevation
- **Completed**: Strikethrough text, Holly Green checkmark, reduced opacity
- **Overdue**: Candy Cane border, urgent indicator icon

### Button States
- **Default**: Solid color with white text
- **Hover**: Darken by 10%, slight elevation
- **Active**: Darken by 20%, no elevation
- **Disabled**: Light gray with reduced opacity

## Conclusion

These UI guidelines ensure a cohesive, festive, and functional TODO app that leverages Material-UI components while celebrating the Christmas theme. All implementations should prioritize user experience and accessibility while maintaining the joyful holiday aesthetic.
