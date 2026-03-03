**Yes, HTML + JavaScript can absolutely handle this!** All the logic (user input, seconds calculation, URL encoding, link generation) runs in the browser. No server needed.

Let me draft the SRS for the web version:

---

# JobPulse Web Tool - Software Requirements Specification (SRS)

## 1. Introduction

**Product Name**: JobPulse  
**Version**: 1.0  
**Purpose**: A single-page web application that generates filtered LinkedIn job search URLs using the f_TPR (time posted range) parameter to find recently posted jobs.

**Deployment**: GitHub Pages (static hosting, zero cost)

---

## 2. System Overview

A client-side web tool that accepts user inputs, constructs a LinkedIn search URL with time-based filtering, and provides one-click access to fresh job listings.

---

## 3. Functional Requirements

### FR1: User Input Collection
- **FR1.1**: Provide text input field for "Job Title" (e.g., "Software Engineer", "Product Manager")
- **FR1.2**: Provide text input field for "Location" (e.g., "New York, NY", "Remote", "United Kingdom")
- **FR1.3**: Provide dropdown/radio buttons for "Time Range" with options:
  - Last 1 Hour
  - Last 3 Hours
  - Last 6 Hours
  - Last 12 Hours
  - Last 24 Hours
- **FR1.4**: All fields should have placeholder text for guidance
- **FR1.5**: Form should validate that Job Title is not empty before generating URL

### FR2: URL Generation Logic
- **FR2.1**: Convert time range to seconds using formula: `Seconds = Hours × 3600`
  - 1 Hour = r3600
  - 3 Hours = r10800
  - 6 Hours = r21600
  - 12 Hours = r43200
  - 24 Hours = r86400
- **FR2.2**: URL-encode Job Title and Location using `encodeURIComponent()`
- **FR2.3**: Construct final URL in format:
  ```
  https://www.linkedin.com/jobs/search/?keywords={ENCODED_TITLE}&location={ENCODED_LOCATION}&f_TPR=r{SECONDS}
  ```
- **FR2.4**: Handle empty location field (omit location parameter if blank)

### FR3: Output Display
- **FR3.1**: Display generated URL in a read-only text field or copyable area
- **FR3.2**: Provide "Copy URL" button to copy link to clipboard
- **FR3.3**: Provide "Go to LinkedIn" button that opens URL in new tab
- **FR3.4**: Show success feedback when URL is copied

### FR4: User Experience
- **FR4.1**: Single-page interface (no navigation required)
- **FR4.2**: Mobile-responsive design (works on phones/tablets)
- **FR4.3**: Clean, professional UI suitable for LinkedIn sharing
- **FR4.4**: No page refresh required (dynamic URL generation)

---

## 4. Non-Functional Requirements

### NFR1: Performance
- Page load time < 1 second
- URL generation instantaneous (< 100ms)

### NFR2: Compatibility
- Works on Chrome, Firefox, Safari, Edge (last 2 versions)
- Mobile browsers (iOS Safari, Chrome Mobile)
- No external dependencies or API calls

### NFR3: Accessibility
- Keyboard navigation support
- Proper form labels for screen readers
- Sufficient color contrast (WCAG 2.1 AA)

### NFR4: Deployment
- Single HTML file (embedded CSS and JS)
- Deployable to GitHub Pages
- No build process required

---

## 5. Technical Specifications

### 5.1 Technology Stack
- **HTML5**: Structure and form elements
- **CSS3**: Styling (embedded in `<style>` tag or inline)
- **Vanilla JavaScript**: Logic (embedded in `<script>` tag)

### 5.2 Key Functions
```javascript
// Time conversion
function hoursToSeconds(hours) {
  return hours * 3600;
}

// URL encoding
encodeURIComponent(userInput)

// Clipboard API
navigator.clipboard.writeText(url)

// Open in new tab
window.open(url, '_blank')
```

### 5.3 File Structure
```
index.html (single file containing all HTML, CSS, JS)
```

---

## 6. User Interface Mockup (Text Description)

**Layout**:
1. Header: "JobPulse" with tagline
2. Form section with three inputs (Job Title, Location, Time Range)
3. "Generate Link" button
4. Output section (initially hidden):
   - Generated URL display
   - "Copy URL" button
   - "Go to LinkedIn" button
5. Footer with creator credit/GitHub link

**Design Notes**:
- Clean, minimalist design
- Use LinkedIn brand colors (optional accent)
- Center-aligned, max-width container for readability

---

## 7. Testing Requirements

### Test Cases:
- **TC1**: Generate URL with all fields filled
- **TC2**: Generate URL with empty location (should work)
- **TC3**: Special characters in job title (e.g., "C++ Developer")
- **TC4**: Copy to clipboard functionality
- **TC5**: Open in new tab functionality
- **TC6**: Mobile responsiveness (test on phone)

---

## 8. Deployment Instructions

1. Create GitHub repository named `JobPulse`
2. Upload `index.html` to repository root
3. Enable GitHub Pages in repository settings
4. Access at: `https://yourusername.github.io/JobPulse`

---

## 9. Future Enhancements (Optional)

- Add "Share on LinkedIn" button to post about the tool
- Save recent searches in localStorage
- Add "Custom Hours" input for advanced users
- Dark mode toggle
- Analytics to track usage (privacy-respecting)
