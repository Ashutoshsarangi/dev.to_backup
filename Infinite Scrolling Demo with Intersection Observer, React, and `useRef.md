## Introduction

This project demonstrates an infinite scrolling implementation using the Intersection Observer API, React, and the `useRef` hook. The primary focus is on preventing layout shifts and improving Cumulative Layout Shift (CLS) by ensuring that new elements are added without impacting the rest of the page.

## Features

-   **Optimized Layout**: The parent `div` is assigned a specific height, ensuring that the addition of new elements does not cause layout shifts, thereby enhancing CLS performance.
-   **Infinite Scrolling**: As you scroll, new elements are continuously added to the DOM, creating an infinite scrolling effect.


NOTE:-
- If you wanted to learn more about performance improvement I have an article on the same (https://dev.to/ashutoshsarangi/performance-improvement-for-web-applications-1plk)

## Installation and Usage

To use this project, follow these steps:

1.  **Clone the repository**:
    
    ```git clone https://github.com/Ashutoshsarangi/react-infinity-loading```
    
2.  **Install dependencies**:
    
    ```npm install``` 
    
3.  **Run the development server**
    
    ```npm run dev``` 
    

## Limitations

While this approach successfully creates an infinite scroll, there is a limitation: **It keeps adding elements to the DOM indefinitely.** After around 1,000 elements, you may notice browser performance issues, such as lagging, due to the increasing number of DOM nodes. This is not ideal for a true infinite scroll experience.



## Future Work

I am actively working on a more efficient solution that mitigates this issue by optimizing the handling of elements in the DOM. Once completed, I will update the repository with the new approach.

Stay tuned!

**Demo Video**
![infiniteLoading_v1-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/4b0f48b0-6523-443d-b267-d1c4da745c6c)
