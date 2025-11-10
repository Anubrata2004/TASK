1. Refactor Blocking I/O

Replaced all synchronous file operations (fs.readFileSync) in src/routes/items.js with asynchronous, non-blocking methods (fs.promises.readFile, fs.promises.writeFile).

Improved server responsiveness and scalability.

2. Performance Optimization (Caching)

Optimized /api/stats route to cache computed statistics instead of recalculating them on every request.

Implemented cache invalidation when data files change.

Result: faster response times and lower CPU usage on repeated requests.

3. API Enhancements – Pagination & Search

Added server-side pagination (page, pageSize) and search (q query parameter) for /api/items.

API now returns paginated data and total count metadata for frontend integration:

{
  "items": [...],
  "meta": { "page": 1, "pageSize": 10, "total": 200 }
}

🧪 Testing
4. Added Comprehensive Jest Tests

Added unit tests for items routes covering:

✅ Happy paths (GET, POST, search, single item)

⚠️ Error cases (invalid ID, invalid payload, invalid JSON)

File: test/items.test.js

All tests passing:

Test Suites: 1 passed, 1 total
Tests:       9 passed, 9 total

💻 Frontend (React)
5. Fixed Memory Leak

Fixed memory leak in Items.js where fetch requests were not aborted when the component unmounted.

Added AbortController cleanup to cancel in-flight requests.

6. Added Paginated + Searchable Items List

Implemented a new React component:
frontend/src/components/ItemsPaginated.js

Features:

Real-time search with debounce

Server-side pagination

Clean loading/error states

Accessible keyboard navigation

Uses query parameters dynamically

7. Improved UI/UX

Replaced inline styles with a dedicated stylesheet:
frontend/src/components/ItemsPaginated.css

Added:

Modern, minimal UI design

Responsive layout

Hover and focus states for accessibility

Skeleton shimmer loading placeholders

Clean typography using Inter/system font stack

Subtle shadows and rounded corners for better readability

8. Enhanced Performance via Virtualization

Integrated list virtualization (with @tanstack/react-virtual) for smooth rendering even with large lists.

Only visible items are rendered into the DOM, improving scrolling performance.
