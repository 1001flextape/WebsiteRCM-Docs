# What is an RCM?

A **Content Management System (CMS)** typically operates with a separate layer for JSON data and another separate layer for the React component. This separation means that the JSON data is used to populate the React component, but the component's structure remains relatively fixed.

An **RCM (React Component Management)** system, on the other hand, works differently. In an RCM, a JSON file not only populates the component but also changes the props of the React component dynamically. This effectively turns the React component into a "madlib" (a word game where you fill in the blanks). The component's behavior and presentation can change entirely based on the JSON input, allowing for a more flexible and dynamic system.
