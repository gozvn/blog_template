# Blog Template - Coding Guidelines

## Project Overview

This is a comprehensive blog template application featuring both a public frontend and an admin dashboard. The project is built using modern web technologies with a focus on responsive design, user experience, and maintainability.

## Technology Stack

### Frontend Technologies
- **Bootstrap 5.3.2**: Primary CSS framework for responsive design and components
- **Font Awesome 6.5.0**: Icon library for UI elements
- **Bootstrap Icons**: Additional icon set for specific UI components
- **Vanilla JavaScript**: Core JavaScript functionality
- **CSS3**: Custom styling and animations
- **HTML5**: Semantic markup structure

### Admin Dashboard Technologies
- **Start Bootstrap SB Admin v7.0.7**: Admin template framework
- **Simple DataTables 7.1.2**: Table management and pagination
- **Bootstrap 5.2.3**: CSS framework for dashboard components
- **Custom JavaScript**: Enhanced functionality and interactivity

### Development Tools
- **CSS Custom Properties**: For theming and consistent styling
- **ES6+ JavaScript**: Modern JavaScript features
- **Local Storage**: Client-side data persistence
- **CDN Dependencies**: External library delivery

## Project Structure

```
blog_template/
├── css/
│   └── custom.css                 # Main custom styles
├── img/                           # Public images and assets
├── dashboard/                     # Admin panel directory
│   ├── assets/
│   │   ├── demo/                  # Demo charts and data
│   │   └── img/                   # Dashboard images
│   ├── css/
│   │   ├── custom.css             # Dashboard custom styles
│   │   └── styles.css             # SB Admin styles
│   ├── js/
│   │   ├── admin-common.js        # Common dashboard functions
│   │   ├── datatables-simple-demo.js
│   │   └── scripts.js             # Main dashboard scripts
│   ├── *.html                     # Dashboard pages
├── *.html                         # Public pages
└── CODING_GUIDELINES.md           # This file
```

## Frontend Architecture

### 1. Public Pages Structure

#### Core Pages:
- `index.html` - Homepage with featured and latest posts
- `categories.html` - Category listing page
- `post_category.html` - Posts by category
- `detail_blog.html` - Individual post view
- `login.html` - User authentication
- `signup.html` - User registration
- `my-posts.html` - User's personal posts

#### Common Components:
- **Header**: Navigation with responsive offcanvas menu
- **Footer**: Site information and social links
- **Cards**: Post previews with hover effects
- **Modals**: Interactive dialogs
- **Toast Notifications**: User feedback system

### 2. Dashboard Structure

#### Admin Pages:
- `dashboard/index.html` - Admin dashboard homepage
- `dashboard/posts.html` - Post management
- `dashboard/post-add.html` - Create/edit posts
- `dashboard/users.html` - User management
- `dashboard/categories.html` - Category management
- `dashboard/comments.html` - Comment moderation

#### Dashboard Features:
- **Sidebar Navigation**: Collapsible menu system
- **Data Tables**: Sortable, searchable, paginated tables
- **CRUD Operations**: Create, Read, Update, Delete functionality
- **Bulk Actions**: Multi-select operations
- **Real-time Validation**: Form validation with feedback

## CSS Guidelines

### 1. Custom CSS Organization

```css
/* Organize CSS in this order: */
/* 1. Common/Global styles */
/* 2. Component-specific styles */
/* 3. Layout styles */
/* 4. Utility classes */
/* 5. Responsive modifications */
/* 6. Animations and transitions */
```

### 2. Bootstrap Customization

- Use Bootstrap utility classes first
- Create custom classes for reusable components
- Maintain consistent spacing using Bootstrap's spacing system
- Use Bootstrap's color system and extend when necessary

### 3. Component Styling Patterns

```css
/* Card hover effects */
.card-component {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card-component:hover {
    transform: translateY(-5px);
    box-shadow: 0 .5rem 1rem rgba(0,0,0,.15)!important;
}

/* Button enhancements */
.btn {
    transition: all 0.3s ease;
}

.btn:hover {
    transform: translateY(-1px);
}
```

### 4. Responsive Design Principles

- Mobile-first approach
- Use Bootstrap's grid system
- Test on multiple screen sizes
- Ensure touch-friendly interface elements
- Optimize images for different devices

## JavaScript Guidelines

### 1. Code Organization

#### Public Pages JavaScript:
```javascript
// 1. Event listeners setup
document.addEventListener('DOMContentLoaded', function() {
    initializeFeatures();
});

// 2. Feature initialization
function initializeFeatures() {
    setupToasts();
    setupValidation();
    setupInteractivity();
}

// 3. Utility functions
function showToast(message, type) {
    // Implementation
}
```

#### Dashboard JavaScript:
```javascript
// admin-common.js structure
// 1. Global variables
// 2. Common initialization
// 3. Utility functions
// 4. Page-specific functions
```

### 2. JavaScript Patterns

#### Toast Notifications:
```javascript
function showToast(message, type = 'success', duration = 3000) {
    // Create toast element
    const toastHtml = `
        <div class="toast align-items-center text-white bg-${type} border-0" role="alert">
            <div class="d-flex">
                <div class="toast-body">${message}</div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
            </div>
        </div>
    `;
    
    // Show toast using Bootstrap
    document.body.insertAdjacentHTML('beforeend', toastHtml);
    const toastElement = document.querySelector('.toast:last-child');
    const toast = new bootstrap.Toast(toastElement, { delay: duration });
    toast.show();
}
```

#### Form Validation:
```javascript
function validateForm(form) {
    let isValid = true;
    const inputs = form.querySelectorAll('input[required], select[required], textarea[required]');
    
    inputs.forEach(input => {
        if (!input.value.trim()) {
            input.classList.add('is-invalid');
            isValid = false;
        } else {
            input.classList.remove('is-invalid');
            input.classList.add('is-valid');
        }
    });
    
    return isValid;
}
```

#### Modal Management:
```javascript
function showModal(modalId, data = {}) {
    const modal = document.getElementById(modalId);
    if (modal && data) {
        // Populate modal with data
        Object.keys(data).forEach(key => {
            const element = modal.querySelector(`[data-field="${key}"]`);
            if (element) element.textContent = data[key];
        });
    }
    new bootstrap.Modal(modal).show();
}
```

### 3. Data Management

#### Local Storage Usage:
```javascript
// Save form data
function saveFormData(formId, data) {
    localStorage.setItem(`autosave-${formId}`, JSON.stringify(data));
}

// Load form data
function loadFormData(formId) {
    const saved = localStorage.getItem(`autosave-${formId}`);
    return saved ? JSON.parse(saved) : null;
}
```

#### AJAX Requests:
```javascript
function makeRequest(url, options = {}) {
    const defaultOptions = {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'X-Requested-With': 'XMLHttpRequest'
        }
    };
    
    return fetch(url, { ...defaultOptions, ...options })
        .then(response => {
            if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
            return response.json();
        })
        .catch(error => {
            showToast('Request failed!', 'danger');
            throw error;
        });
}
```

## Component Guidelines

### 1. Modal Components

#### Structure:
```html
<div class="modal fade" id="modalId" tabindex="-1">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Title</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
            </div>
            <div class="modal-body">
                <!-- Content -->
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button type="button" class="btn btn-primary">Action</button>
            </div>
        </div>
    </div>
</div>
```

### 2. Data Tables

#### Implementation:
```javascript
// Initialize DataTable
new simpleDatatables.DataTable(table, {
    perPageSelect: [5, 10, 15, 25, 50, ["All", -1]],
    perPage: 10,
    searchable: true,
    sortable: true,
    fixedHeight: false,
    labels: {
        placeholder: "Search...",
        perPage: "items per page",
        noRows: "No data found",
        info: "Showing {start} to {end} of {rows} items"
    }
});
```

### 3. Form Components

#### Validation Structure:
```html
<form id="formId" novalidate>
    <div class="mb-3">
        <label for="field" class="form-label">Label</label>
        <input type="text" class="form-control" id="field" required>
        <div class="invalid-feedback">Error message</div>
        <div class="valid-feedback">Success message</div>
    </div>
</form>
```

## AI Agent Guidelines

### 1. Code Generation Principles

#### Always Include:
- Bootstrap classes for styling
- Responsive design considerations
- Accessibility attributes (aria-labels, roles)
- JavaScript validation and feedback
- Error handling and user feedback
- Consistent naming conventions

#### Follow These Patterns:
```javascript
// Function naming: camelCase
function handleUserAction() {}

// Constants: UPPER_SNAKE_CASE
const MAX_UPLOAD_SIZE = 1024 * 1024;

// Variables: camelCase
const userInput = document.getElementById('input');

// CSS classes: kebab-case for custom, Bootstrap utilities as-is
.custom-component-name {}
.btn.btn-primary {}
```

### 2. Component Creation Guidelines

#### When Creating New Components:
1. **Start with Bootstrap base classes**
2. **Add custom styling in CSS files**
3. **Include hover effects and transitions**
4. **Ensure mobile responsiveness**
5. **Add JavaScript interactivity**
6. **Include proper validation**
7. **Provide user feedback**

#### Example Component Creation:
```html
<!-- HTML Structure -->
<div class="card custom-post-card">
    <img src="image.jpg" class="card-img-top" alt="Description">
    <div class="card-body">
        <span class="badge bg-primary mb-2">Category</span>
        <h5 class="card-title">Title</h5>
        <p class="card-text">Description</p>
        <div class="d-flex justify-content-between align-items-center">
            <small class="text-muted">Date</small>
            <button class="btn btn-primary btn-sm">Action</button>
        </div>
    </div>
</div>
```

```css
/* CSS Styling */
.custom-post-card {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.custom-post-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 .5rem 1rem rgba(0,0,0,.15)!important;
}
```

```javascript
// JavaScript Functionality
function initializePostCards() {
    const cards = document.querySelectorAll('.custom-post-card');
    cards.forEach(card => {
        card.addEventListener('click', function(e) {
            if (!e.target.closest('.btn')) {
                // Handle card click
                const postId = this.dataset.postId;
                navigateToPost(postId);
            }
        });
    });
}
```

### 3. Maintenance Guidelines

#### Code Quality:
- Use consistent indentation (2 or 4 spaces)
- Comment complex logic
- Use semantic HTML elements
- Optimize images and assets
- Minimize JavaScript and CSS where possible

#### Testing Considerations:
- Test all interactive elements
- Verify responsive behavior
- Check accessibility compliance
- Validate form submissions
- Test error scenarios

#### Performance Guidelines:
- Lazy load images when possible
- Use efficient CSS selectors
- Minimize DOM manipulation
- Debounce search inputs
- Cache frequently used elements

### 4. Integration Patterns

#### Adding New Features:
1. **Identify the target page/component**
2. **Follow existing patterns and conventions**
3. **Use established utility functions**
4. **Maintain consistent styling**
5. **Add appropriate validation and feedback**
6. **Test across different screen sizes**

#### Modifying Existing Features:
1. **Understand the current implementation**
2. **Maintain backward compatibility**
3. **Update related documentation**
4. **Test thoroughly after changes**

## Best Practices Summary

### Development Workflow:
1. **Plan the feature/component**
2. **Create HTML structure using Bootstrap**
3. **Add custom CSS for specific styling**
4. **Implement JavaScript functionality**
5. **Add validation and error handling**
6. **Test responsiveness and accessibility**
7. **Document any new patterns or utilities**

### Code Standards:
- **Consistent naming conventions**
- **Proper indentation and formatting**
- **Meaningful comments for complex logic**
- **Semantic HTML structure**
- **Accessible design patterns**
- **Mobile-first responsive design**

### User Experience:
- **Clear visual feedback for all actions**
- **Consistent interaction patterns**
- **Fast and responsive interfaces**
- **Accessible to all users**
- **Graceful error handling**

This guide serves as the foundation for maintaining and extending the blog template project. Always refer to these guidelines when implementing new features or modifying existing functionality.