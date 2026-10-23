# Part 0 Exercises

## Exercise 0.4: New note diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: The user writes a note and clicks the Save button

    browser->>server: POST https://helsinki.fi
    activate server
    Note left of server: The server extracts the data, saves the new note to the array, and prepares a redirect
    server-->>browser: HTTP status code 302 (URL Redirect to /exampleapp/notes)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser executes the JS code to fetch the updated JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "Your new note", "date": "2026-10-23" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function to render the updated notes list
```

## Exercise 0.5: Single page app diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://helsinki.fi
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing JS code which requests the JSON data

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "spa note", "date": "2026-10-23" }, ... ]
    deactivate server

    Note right of browser: The browser renders the initial notes dynamically using JavaScript
```

## Exercise 0.6: New note in Single page app diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: The user types a note and clicks Save

    Note right of browser: The JS code intercepts the form submit, appends the note locally, and redraws the DOM instantly

    browser->>server: POST https://helsinki.fi_spa
    activate server
    Note over browser, server: Sends JSON data: { content: "single page note", date: "2026-10-23" }
    server-->>browser: HTTP status code 201 (Created)
    deactivate server
    
    Note right of browser: No further data or page reload is requested; the UI is already updated
```
