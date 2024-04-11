**1. Introduction**
The Dark Pattern Detection Extension is a tool designed to identify and counteract dark patterns on websites. 
Dark patterns are user interface design choices crafted to trick users into making decisions they might not 
otherwise make. This extension helps users by providing insights into detected dark patterns on the websites 
they visit. 
**2. Installation**** 
The Dark Pattern Detection Extension is not limited to Chrome; it can also be installed on Opera, Edge, and 
Firefox. However, for Chrome users, follow these steps: 
1. Download the extension package. 
2. Open Google Chrome. 
3. Navigate to `chrome://extensions/`. 
4. Enable "Developer mode" in the top-right corner. 
5. Click on "Load unpacked" and select the extension directory. 
The extension icon will appear in the Chrome toolbar once installed.

**3. Usage -Icon Badge**: The extension icon displays a badge indicating the number of detected pattern elements on the 
active webpage. - Popup: Clicking the extension icon opens a popup with detailed information about the detected patterns.
-Content Script: The content script injected into web pages analyzes the page for potential dark patterns. 

**4.  Background Script** 
The `background.js` script manages the extension's behavior across tabs and ensures proper activation based on 
webpage URLs. 
1. API Access: - Utilizes the `chrome` API to access browser functionalities. - Defines `brw` constant as the API object for runtime, tabs, and actions. 
2. Activation State Storage: - Uses session storage for activation state or falls back to local storage if session storage is not supported (e.g., 
Firefox). 
3. Activation State Management: - `getActivation(tabId)`: Retrieves activation state for a tab.
4. - `setActivation(tabId, activation)`: Sets activation state for a tab.
   - `removeActivation(tabId)`: Removes activation state for a closed tab.
   - `getActivationOrSetDefault(tabId)`: Retrieves or sets the activation state for a tab, defaulting to 
active if not set. 
5. Message Handling:
   - Listens for messages from content or popup scripts. - Updates icon badge with detected pattern count.
   - Manages activation state changes and responds to activation queries. 
6. Tab Event Handling: - Handles tab replacements and closures, updating activation states accordingly.
   - Monitors tab updates, dynamically changing extension icons based on page URLs (HTTP(S) vs. non-HTTP(S)). 
7. Icon Management: - Retrieves icon paths from the manifest file.
   - Generates disabled (grayed out) icons for inactive extension state.
   - Sets icons based on the webpage's protocol (HTTP(S) or non-HTTP(S)). 
8. Pattern Count Display: - Displays the number of detected pattern elements on the extension's icon.
    - Adjusts badge text and background color based on the detected count (green for 0, red otherwise). 
9. Automatic URL-based Activation: - Automatically activates or deactivates for tabs based on the webpage's URL protocol (HTTP(S) or non
HTTP(S)). 
This script ensures the extension's seamless functionality, managing activation states, responding to messages, 
and dynamically adapting icons for optimal user experience.

**5. Content Script***
The `content.js` script is injected into web pages and handles:
-Dark Pattern Detection: Detects patterns on the webpage and sends counts to the background script. 
-Message Handling: Listens for messages from the background script to update pattern counts and 
enable/disable the extension. 

**6. Localization**
The extension supports localization for different languages. The `manifest.json` file uses placeholders like 
`__MSG_extName__` and `__MSG_extDescription__` for dynamic language substitution. 

**7. Web Accessible Resources**
The extension makes specific resources accessible to web pages, such as the `constants.js` file. This file may 
contain shared constants or configurations for both the background and content scripts. 
The constant.js file serves as a crucial component in the dark pattern detection  
1. Browser API Access: - The solution interacts with the browser API, providing essential functions like runtime and internationalization 
(i18n). 
2. Pattern Configuration: - A `patternConfig` object defines various patterns, each with attributes such as name, class name, detection 
functions, information URL, and a brief explanation. 
3. Detection Functions: - Detection functions are at the core of the solution, responsible for identifying specific dark patterns on 
webpages. 
- These functions take two parameters (`node` and `nodeOld`) representing the HTML node in the current and 
previous states. - Detection functions return `true` if the pattern is detected and `false` otherwise. 
4. Detection Logic: - Detection logic is implemented within each detection function, using regular expressions and specific criteria 
to identify patterns such as countdowns, scarcity, social proof, and forced continuity. 
5. Validation and Config: - The `validatePatternConfig` function ensures the correctness of the `patternConfig` object by checking for 
duplicate pattern names, valid data types, and overall structure. - A boolean variable (`patternConfigIsValid`) indicates whether the configuration is valid. 
6. CSS Classes and Blacklist: - Constants like `extensionClassPrefix` and `patternDetectedClassName` define CSS classes for styling elements 
related to the extension. - The `tagBlacklist` array contains HTML tags that should be ignored during pattern detection. 
7. Summary: - The solution employs a modular approach, allowing for the addition of new patterns and languages.
  - Detection functions inspect changes in HTML nodes, applying specific logic for each pattern.
  - The `patternConfig` object serves as a central configuration, and validation ensures its integrity.
  - CSS classes and tag blacklists contribute to the seamless functioning of the dark pattern detection extension.
