# Notes App

A modern, responsive notes application built with Svelte and TailwindCSS that allows users to create, read, update, and delete notes.

## Features

- Create, read, update, and delete notes
- Responsive design that works on all devices
- Dark mode support
- Modern UI with smooth animations
- Real-time updates

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn

## Getting Started

1. Clone the repository:
bash
git clone <repository-url>
cd notes-app


2. Install dependencies:
bash
npm install
# or
yarn install


3. Start the development server:
bash
npm run dev
# or
yarn dev


4. Open your browser and navigate to http://localhost:5173

## Trade-offs and Assumptions

1. *API Integration*:
   - Using a mock API (mockapi.io) for demonstration
   - In a production environment, you'd want to implement proper error handling and loading states
   - Assumed the API would return consistent data structure

2. *State Management*:
   - Used simple component-level state management
   - For a larger application, you might want to use a state management solution like Svelte stores

3. *Styling*:
   - Used TailwindCSS for rapid development and consistent styling
   - Trade-off between bundle size and development speed
   - Assumed modern browser support for CSS features

4. *Performance*:
   - Implemented basic optimizations like line clamping
   - Trade-off between feature richness and performance
   - Assumed reasonable note content length

## Future Improvements

Given more time, I would:

1. *Features*:
   - Add note categories/tags
   - Implement search functionality
   - Add rich text editing
   - Add note sharing capabilities
   - Implement note archiving

2. *Technical*:
   - Add proper authentication
   - Implement proper backend integration
   - Add unit and integration tests
   - Implement proper error boundaries
   - Add loading skeletons
   - Implement proper data persistence

3. *UX Improvements*:
   - Add keyboard shortcuts
   - Implement drag-and-drop reordering
   - Add note preview mode
   - Implement undo/redo functionality
   - Add note export/import features

4. *Performance*:
   - Implement virtual scrolling for large lists
   - Add proper caching strategies
   - Optimize bundle size
   - Implement proper lazy loading

5. *Accessibility*:
   - Add proper ARIA labels
   - Implement keyboard navigation
   - Add screen reader support
   - Improve color contrast
   - Add proper focus management

## Contributing

Feel free to submit issues and enhancement requests!
